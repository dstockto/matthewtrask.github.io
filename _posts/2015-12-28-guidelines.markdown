## 0. Preface
 
This document is maintained by TNG of Insight Global.  For feedback or questions, please write to developers@insightglobal.net.
 
### 0.1. References
 
This document references the following other documents:
 
* [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt)
* [PSR-0](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md)
* [PSR-1](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md)
* [PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md)
* [PSR-4](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md)
* [SemVer](http://semver.org/spec/v2.0.0.html)
 
### 0.2. Preamble
 
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt).
 
## 1. Environment
 
### 1.1. Language
 
The project language is English. Names, identifiers, comments, commit messages, documentation, documents such as this one, issue tracking etc. MUST use the English language.
 
### 1.2. PHP
 
The project MUST be compatible with all versions of PHP that are [actively supported](http://php.net/supported-versions.php) by the PHP project.
 
### 1.3. Version Control
 
Git MUST be used for version control.
 
## 2. Directory Structure
 
All object-oriented code MUST be placed in a directory named `src`. All test code MUST be placed in a directory named `tests`. The `src` and `tests` directories MUST be placed in the project's root directory. Third-party code MUST be placed in a directory named `vendors`. Refer to Section 8.1 of this document for details.
 
## 3. Formatting
 
Code MUST follow the [PSR-1](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md) "basic coding standard" and the [PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md) "coding style guide".
 
### 3.1. Grouping and Sorting of Methods
 
The following order for method declarations within the source code of a class MUST BE followed:
 
* __construct()
* abstract methods
* static methods
* non-static methods
*__toString() 
 
Interceptor methods other than the ones listed SHOULD NOT be used ( i.e. __call() ).
 
Semantically related methods SHOULD be grouped together, and SHOULD follow the order of operations where possible.
 
### 3.2. Arrays
 
The short array syntax `[]` MUST be used instead of `array()` to declare arrays.
 
### 3.3. Namespaces
 
#### 3.3.1. Syntax
 
The `namespace vendor\project;` syntax to declare namespaces MUST BE used. The alternative syntax `namespace vendor\project { /* ... */ }` MUST NOT be used.
 
#### 3.3.2. Use Statements
 
Unused `use` statements MUST NOT exist.
 
`use` statements that alias a name from the global namespace to the same basename in the current namespace MUST NOT be used. Use a fully qualified 
name prefixed with `\`.
 
## 4. PHP Subset
 
### 4.1. Prohibited Language Features
 
#### 4.1.1. Prohibited Built-In Functions
 
Without exception, the following built-in functions MUST NOT be used:
 
* `addslashes()`
* `addcslashes()`
* `create_function()`
* `dl()`
* `error_reporting()`
* `eval()`
* `forward_static_class()`
* `forward_static_class_array()`
* `get_called_class()`
* `import_request_variables()`
* `ini_set()`
* `set_include_path()`
* `set_magic_quotes_runtime()`
* `trigger_error()`
 
#### 4.1.2. Prohibited Language Constructs
 
Without exception, the following language constructs MUST NOT be used:
 
* `global`
* `goto`
* Coroutines
* regular expressions with the `e` switch
* Variable variable names such as `$$name`
 
#### 4.1.3. Prohibited Interceptor Methods
 
Without exception, the following interceptor methods MUST NOT be used:
 
* `__destruct()`
* `__callStatic()`
* `__get()`
* `__set()`
* `__isset()`
* `__unset()`
* `__sleep()`
* `__wakeup()`
* `__set_state()`
 
#### 4.1.4. Prohibited Operators
 
The error suppression operator (`@`) MUST NOT be used.
 
The reference operator (`&`) MUST NOT be used. A method (or function) MAY only have a single return value. Variables of the caller's scope MUST NOT be modified via references.
 
#### 4.1.5. Invoking Interceptor Methods
 
Interceptor methods such as `__toString()` MUST NOT be invoked directly. Unit tests are exempt from this rule.
 
#### 4.1.6. Declaring Interceptor Methods in Interfaces
 
Interceptor methods MUST NOT be declared in an interface.
 
#### 4.1.7. Static Attributes
 
Static attributes MUST NOT be used.
 
#### 4.1.8. Global Constants and Variables
 
Custom global constants MUST NOT be used. Custom class constants MAY be used but are considered bad practice.
 
Global variables MUST NOT be accessed outside of the bootstrap script.
 
Super-global variables MUST NOT be accessed outside of the bootstrap script or the factory method of a request object.
 
Without exception, `$GLOBALS` MUST NOT be used.
 
#### 4.1.9. HTML
 
PHP code MUST be separated from HTML code. The heredoc (`<<<EOT ... EOT;`) and nowdoc (`<<<'EOT' ... EOT;`) syntax MUST NOT be used.
 
### 4.2. Discouraged Language Features
 
The following language features SHOULD NOT be used:
 
* Reflection API
* `call_user_func()` and `call_user_func_array()`
* Usage of the `new` operator with variable class names
* Variable class names for static method calls such as `$class::method()`
* Variable function or method names such as `$function()` or `$object->$method()`
 
## 5. Error Handling
 
### 5.1. Exceptions
 
Exceptions MUST be used to communicate and handle errors. Alternatives such as `trigger_error()` MUST NOT be used.
 
#### 5.1.1. Exception Hierarchy
 
Each project MUST declare a marker interface that is used to identify the exceptions that are raised by it. This marker interface MUST then be implemented by all exception classes of the project.
 
A project MUST NOT raise exceptions that are not marked using the project's marker interface. Consequentially, a project MUST NOT raise an exception of the built-in class Exception.
 
#### 5.1.2. Guard Clauses
 
Guard clauses that raise an exception MUST be implemented in a separate method. The name of this method MUST be prefixed with `ensure`.
 
## 6. Object-Orientation
 
All code MUST be object-oriented. Functions MUST NOT be used. Anonymous functions MAY be used for autoloading or as comparison functions for sorting.
 
### 6.1. SOLID Principles
 
Object-oriented code MUST adhere to the [SOLID](http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod) principles of class design:
 
#### 6.1.1. Single Responsibility Principle
 
The Single Responsibility Principle MUST be followed. There MUST NOT be more than one reason to change a class.
 
#### 6.1.2. Open/Closed Principle
 
It SHOULD be possible to extend the behavior of a class without modifying it.
 
#### 6.1.3. Liskov Substitution Principle
 
Derived classes MUST be substitutable for their base classes.
 
#### 6.1.4. Interface Segregation Principle
 
Interfaces MUST be fine-grained and client-specific.
 
#### 6.1.5 Dependency Inversion Principle
 
Depend on abstractions, not on concretions.
 
### 6.2. Best Practices
 
Object-oriented code MUST adhere to the following best practices
 
#### 6.2.1. Minimal Visibility Principle
 
All attributes of a class MUST be private. All non-public methods SHOULD be declared private and MAY only be declared protected when they have to be visible in a subclass.
 
#### 6.2.2. Explicit APIs
 
APIs MUST be explicit, not implicit. For instance, an explicit method such as `$config->getKey()` MUST be used instead of an implicit method such as `$config->get('key')`. Objects that encapsulate an HTTP request MAY deviate from this rule.
 
#### 6.2.3. Favor Composition over Inheritance
 
Inheritance breaks encapsulation. Composition MUST be favored over inheritance. If inheritance cannot be avoided then the depth of the inheritance tree MUST NOT exceed three levels (classes that are built into PHP or provided by third-party code are not counted).
 
Exception classes are exempt from this rule.
 
#### 6.2.4. Favor Polymorphism over Conditionals
 
Polymorphism MUST be favored over conditionals. The possible execution branches SHOULD be encapsulated in separate objects, if feasible.
 
#### 6.2.5. Object Creation
 
All objects that have dependencies MUST be created in a Factory.
 
A Factory MUST NOT use static methods.
 
Only a Factory MAY depend on a global Configuration. Other object MUST NOT depend on a global Configuration.
 
Value objects and domain objects without technical dependencies (such as an Observer, for instance) MAY be created outside the Factory.
 
A class MUST NOT have a dependency on the Factory. Locators are exempt from this rule.
 
For objects that can only be created at runtime, ie. after the bootstrap, a Locator MUST be implemented that selects the implementation and then delegates to the Factory to create the object.
 
##### 6.2.5.1. Named Constructors
 
The `__construct()` method of a class that declares a named constructor method MUST NOT be public. A named constructor method MUST be `public static` and MAY be `final`. The name of a named constructor method MUST begin with `from`. 
 
#### 6.2.6. Accessor and Mutator Methods (Getters and Setters)
 
Getters MAY only be declared public when there is a concrete business requirement for the getter method.
 
By default, private attributes are accessed directly. A getter method MUST NOT be written unless it encapsulates business rules, or validation.
 
Subclasses MUST access attributes of their parent class via accessor methods provided by the parent class.
 
Setters MAY only be implemented when validation has to be performed or when a subclass requires write access to the respective attribute.
 
If a setter method exists for an attribute of a class then this setter method MUST be used by all methods of that class for mutating the attribute. The same holds true for getter methods.
 
## 7. Typing
 
Type declarations (commonly referred to as "type hints") MUST be used for method (and function) arguments when the type of the argument can be declared (class name, interface name, `array`, `callable`).
 
Interfaces MUST be used for the type declaration of infrastructure objects. Classes MAY be used for the type declaration of domain or value objects. Abstract classes SHOULD be favored over concrete classes for type declarations.
 
Multi-dimensional arrays MUST NOT be used for method (and function) arguments or return values. Objects MUST be used instead.
 
Associative arrays MUST NOT be used for method (and function) arguments. Objects MUST be used instead. Constructor arguments are exempt from this rule.
 
Arrays MUST NOT be used to pass configuration settings or options to a constructor.
 
The return value of a `__toString()` method MUST be explicitly cast to string using `(string)`.
 
## 8. Dependencies
 
### 8.1. Component-Level
 
[Composer](https://getcomposer.org/) SHOULD be used for dependency management.
 
Components that you do not own (third-party code) MUST NOT be used directly. Instead implement an adapter class that isolates the project code from the component.
 
### 8.2. Object-Level
 
All code MUST be loosely coupled.
 
Implicit dependencies such as global constants, static methods, or global and super-global variables MUST NOT be used.
 
Static methods MUST NOT be used. Static factory methods (named constructors) and validation methods in value objects are exempt from this rule.
 
Singletons, Multitons, and Static Registries MUST NOT be used. If no more than one instance of a class is to be created then it is the Factory's job to ensure this.
 
Dependencies MUST NOT be pulled into an object. Instead Dependency Injection MUST be used to push dependencies into an object.
 
## 9. Testing
 
### 9.1. Unit Tests
 
#### 9.1.1. General Guidelines
 
Each class MUST have a corresponding unit test class that yields 100% line coverage for the class.
 
#### 9.1.2. Namespace
 
Test case classes MUST use the same namespace as the production code that they test.
 
#### 9.1.3. Collaborators
 
Each collaborator of the unit of code under test MUST be replaced with a test double. Value objects are exempt from this rule.
 
#### 9.1.4. Naming
 
Test methods MUST have a concise yet speaking name that makes it clear what the test ensures. If PHPUnit is used then the test names SHOULD be chosen with PHPUnit's TestDox functionality in mind.
 
#### 9.1.6. Assertions
 
The most specific assertion possible MUST be used.
 
Each test method uses exactly one assertion to verify the aspect of the unit of code under test it is responsible for. Tests that verify that an expected exception is raised, use mock objects, or (also) need to verify the type of the return value are exempt from this rule.
 
All assertions of a test method are at the end of test method's body. There MUST NOT be additional code after the final assertion. Tests which are depended upon by other tests and need to return a value are exempt from this rule. The `return` statement MUST be the only code after the final assertion.
 
#### 9.1.7. Test Dependencies
 
Tests MUST NOT depend on each other or a specific order of execution. Test dependencies expressed using PHPUnit's `@depends` annotation are exempt from this rule.
 
#### 9.1.8. Code Duplication
 
Duplicate code MUST be avoided in unit tests. Common fixture, for instance, MUST be prepared in a setup method (`setUp()` in PHPUnit, for instance). Attributes that hold the fixture MUST be declared private.
 
#### 9.1.9. Test Results
 
Tests MUST NOT be incomplete or risky.
 
#### 9.1.10. Code Coverage
 
Each test case class MUST have a `@covers` annotation on the class-level. Additional `@covers` annotations on the method-level MAY be used but are not required.
 
The `@codeCoverageIgnore`, `@codeCoverageIgnoreStart`, and `@codeCoverageIgnoreEnd` annotations MUST NOT be used. The `@codeCoverageIgnore` annotation MAY be used on the method-level.
 
#### 9.1.11. PHPUnit Configuration
 
The following options MUST be set in PHPUnit's XML configuration file:
 
* `addUncoveredFilesFromWhitelist="true"` (on the `filter/whitelist` element)
* `beStrictAboutOutputDuringTests="true"` (on the `phpunit` element)
* `beStrictAboutTestsThatDoNotTestAnything="true"` (on the `phpunit` element)
* `beStrictAboutTodoAnnotatedTests="true"` (on the `phpunit` element)
* `checkForUnintentionallyCoveredCode="true"` (on the `phpunit` element)
* `forceCoversAnnotation="true"` (on the `phpunit` element)
 
A whitelist MUST be used to configure which files are to be included in a code coverage report. This whitelist usually only includes the `*.php` files of the directory named `src` that is mentioned in Section 2.
 
The following options SHOULD be set in PHPUnit's XML configuration file:
 
* `backupGlobals="false"` (on the `phpunit` element)
* `backupStaticAttributes="false"` (on the `phpunit` element)
* `processUncoveredFilesFromWhitelist="true"` (on the `filter/whitelist` element)
* `verbose="true"` (on the `phpunit` element)
 
## 10. Documentation
 
Each method MUST have a docblock that documents at least all arguments (`@param`) of the method and the return value (`@return`) returned by it as well as the exceptions (`@throws`) raised by it.
 
Constructors do not have a return value. A return value MUST NOT be documented in their docblock.
 
Methods that do not have a return value MUST be documented with `@return void`. Constructors are exempt from this rule.
 
Inline documentation that explains what the code is doing MUST NOT be used. Inline documentation MAY be used to explain why the code does something. Speaking names of identifiers MUST be favored over inline documentation.
 
Code MUST NOT be commented out.
 
## 11. Development Process
 
### 11.1. Version Control
 
Each commit MUST have a single purpose and SHOULD completely implement that purpose.
 
The commit message MUST concisely describe the commit's purpose.
 
Cosmetic changes to the code MUST NOT be made at the same time as non-cosmetic changes.
 
## 12. Release Management
 
### 12.1. Semantic Versioning
 
[Semantic Versioning](http://semver.org/spec/v2.0.0.html) MUST be used to assign version numbers for releases.
