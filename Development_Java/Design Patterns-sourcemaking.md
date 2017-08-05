From: https://sourcemaking.com/design_patterns



# Creational patterns



## Abstract Factory

> Creates an instance of several families of classes.

### Intent

- provide an interface for creating families of related or dependent objects without specifying their concrete classes.
- A hierarchy that encapsulates: many possible "platforms", and the construction of a suite of "products".
- The `new` operator considered harmful.



### Code examples

#### Java

```java
// class CPU 
abstract class CPU {}

// class EmberCPU
class EmberCPU extends CPU {}

// class EnginolaCPU
class EnginolaCPU extends CPU {}
```

  



 

