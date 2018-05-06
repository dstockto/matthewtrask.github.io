---
layout: post
title:  "Two nifty things I learned about Doctrine over the past week"
date:   2018-02-05
comments: yes
description: I had a fun thing to work on at work and it let me dive into some cool Doctrine stuff.
tags: ORM, Doctrine, Work
---

This is now the 4th different database tool I've worked with in PHP. It helps that the original author is just 25 feet or so awat from me
at work, but as I grew as a PHP developer, the debate I always heard was: Eloquent vs Doctrine. Active Record ORM vs Data Mapper ORM. Personally
I never dove into what the difference was, I just went with what was being used and learned it to make sure I could leverage whichever tool Im using.

### A brief primer on ORM's

From Wikipedia[1]: 

> Object-relational mapping (ORM, O/RM, and O/R mapping tool) in computer science is a programming technique for converting data between incompatible type systems using object-oriented programming languages. This creates, in effect, a "virtual object database" that can be used from within the programming language.

So from this, we can infer that an ORM is a layer in between our application and the database itself. Wikipedia uses an example of a Person class with properties like 

* Name
* Address
* PhoneNumber

and more. But we can't store a phone number as is, if we follow the American format (111-867-5309) right? So we "let" the ORM transform it when it goes into the database to 
something easy for the database to deal with such as one big integer (1118675309), and when we pull it out of the database, we can then transform it back to 111-867-5309 or something else. 

But there are two types of ORM's out there, what is the main difference? Martin Fowler's [blog](https://www.martinfowler.com) has a definition of each:

#### Data Mapper

"The Data Mapper is a layer of software that separates the in-memory objects from the database. Its responsibility is to transfer data between the two and also to isolate them from each other. With Data Mapper the in-memory objects needn't know even that there's a database present; they need no SQL interface code, and certainly no knowledge of the database schema. (The database schema is always ignorant of the objects that use it.) Since it's a form of Mapper (473), Data Mapper itself is even unknown to the domain layer."

#### Active Record

"An object carries both data and behavior. Much of this data is persistent and needs to be stored in a database. Active Record uses the most obvious approach, putting data access logic in the domain object. This way all people know how to read and write their data to and from the database."

The main difference we can infer is that Active Record carries more then just data, it carries behavior and lets you do some cool and powerful things. Data mapper works in the background, almost hidden, doing its job and forgetting once the job is finished. I may also be super wrong. Meh. 

But so no that we clarified that, lets look at Doctrine and the cool things I figured out this week. 

### An event listener pattern in the ORM. 

The task at hand was this: create an audit log for certain parts of our admin system so when a change is made, we have a record of who did it, why and when. My boss mentioned the event system in Doctrine would be ideal for this. At first I had zero idea what he meant. 
In Eloquent, which I used previously, it never exposed events to userland. Things like 
```
preFlush(), onFlush(), postFlush()
```
were not things we had to deal with. It was all handled in the background through the Active Record pattern. So as I dove in, I noticed two things: there are events you can have on the model itself, or you can create whole class listeners that listen for what Doctrine calls ```php LifecycleEvents```. How does differ? Lets make an example of a class, a User model. It can look like this:

```
<?php

declare(strict_types=1);

namespace Crm\Models;

/**
 * @Entity(repositoryClass="UserRepository") @Table(name="users")
 * @HasLifecycleCallbacks
 */
 class User implements UserInteferace
 {
     /**
     * @Id @Column(type="integer") @GeneratedValue
     * @var int
     */
     private $id;
     
     /**
      * @Column(type="string")
      * @var string
      */
     private $name;
     
     /**
      * @Column(type="string")
      * @var string
      */
     private $address;
     
     /**
      * @Column(type="int")
      * @var int
      */
     private $phoneNumber;
     
     private $weeklyAccomplishment;

     public function getId() { // }
     
     public function setId($id) { // }
     
     ...
     
     public function getWeeklyAccomplishment() : ? string
     {
         return $this->weeklyAccomplishment;
     }
     
     public function setWeeklyAccomplishment(string $weeklyAccomplishment) 
     {
         $this->weeklyAccomplishment = $weeklyAccomplishment;
     }
 }
```

Alright! Our model is set. Now, lets look at what I did. The user model is pretty straightforward, and we use annotations cause that is how Doctrine works. If you want to read more about the annotations, you can go [here](https://www.doctrine-project.org/projects/doctrine-annotations/en/latest/index.html). The interesting thing here though is the first thing, I learned: Transient Properties. Notice when we set up our properties, I left off a docblock for the ```$weeklyAccomplishment```. That is for two reasons: one: on our users table, there is no column for the value there, and we are going to use this value elsewhere, two: this prevents the value from being persisted, so Doctrine just holds this value in memory and we can access it later. Pretty neat! So how will we use this new value that we can't store on our users model? We can make a simple model that will store the userId, the accomplishment and a timestamp. I don't think I need to write that out right now, but I can. But lets say we want to store it when we update the user in the admin system we are creating. Where would we call this ```$weeklyAccomplishment``` value? Well, it seems we can do it two places. Either on the model itself with a ```onFlush``` method or an event listener. 

The ```onFlush``` method would look this on our model about:

```
    public function onFlush() 
    {
        $accomplishments = new Accomplishments();
        $accomplishmnets->setUser($this->getId());
        $accomplishments->setWeeklyAccomplishments($this->getWeekylAccomplishment());
    }
```

And when we call ```$this->flush();```, Doctrine will go ahead and save all of our changes including the work done in the ```onFlush``` method there. You can also do work in the ```preFlush()``` or ```postFlush``` among other events. All the events available are [here](https://www.doctrine-project.org/projects/doctrine-orm/en/2.6/reference/events.html).

So this is great, but lets say we want a listener because we want to be more flexible and possibly decouple ourselves for testing or flexibility. Lets do it!

```
<?php

declare(strict_types=1);

namespace Crm\Events;

class AccomplishmentsEvent
{
    public function onFlush(OnFlushEventArgs $event)
    {
       $entity = $event->getObject();
       $em = $args->getObjectManager();
       $uow = $em->getUnitOfWork();

       
       if ($entity !instanceof UserInterface) {
           continue;
       }
       
       foreach ($uow->getScheduledEntityInsertions() as $entity) {
           $this->insertAccomplishments($entity);
       }

       foreach ($uow->getScheduledEntityUpdates() as $entity) {
           $this->insertAccomplishments($entity);
       }

       foreach ($uow->getScheduledEntityDeletions() as $entity) {
           $this->insertAccomplishments($entity); 
       }
    }
    
    private function insertAccomplishment($entity) 
    {
       $accomplishments = new Accomplishments();
       $accomplishmnets->setUser($entity->getId());
       $accomplishments->setWeeklyAccomplishments($entity->getWeekylAccomplishment()); 
    }
}
```

Lets look closely at one thing: 
```
if ($entity !instanceof UserInterface) {
    continue;
}
```
we do this because this event listener will be called on every entity we have ```@HasLifeCycleEvents``` on. How can we get around this? We can create an empty interface like we did above, namely ```UserInterface```, and if the entity in question does not implement this interface, we can just continue on like nothing happens. Its a nice little trick to keep in the back of your mind. 

The next part is that because there are different ways data can be inserted, we need to check all the possible versions. Are we creating a new record, or editing a record? Well we don't know in this class, so we get Doctrine's UnitOfWork class and check all possible methods to see which one contains the work we want to perform. 

### Wrap up

That was a lot! What did we cover?

* ORM: Active Record vs Data Mapper
* A basic model for Doctrine
* Tapping into the Event Architecture of Doctrine

Hopefully this will come in handy for you sometime soon!
