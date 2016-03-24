---
layout: post
title: 'Head First Java Notes'
date: 2014-07-01 16:28:08
tags:
---


After a few days' reading, I have finally gone through this book. Here are some of my notes.

# polymorphism

With polymorphism, the reference and the object can be different. And the subclass methods can be called via a suuperclass type.

```
Animal[] animals = new Animal[2];
animals[0] = new Dog();
animals[1] = new Cat();

for (int i = 0; i < animals.length; i++) {
    // call dog's eat method when i == 0, call cat's eat method when i == 1
    animals[i].eat();
    animals[i].roam();
}

```

# polymorphic arguments

```java
class Vet {
    public void giveShot(Animal a) {
        a.makeNoise(); // call the animal's own makeNoise()
    }
}

class PetOwner {
    public void start() {
        Vet v = new Vet();
        Dog d = new Dog();
        Cat c = new Cat();
        v.giveShot(d); // it will work as long as Dog is a subclass of Animal
        v.giveShot(c);
    }
}
```

# Non-public class: 
It can be subclassed only by classes in the same package.
  Classes in a different package won't be able to subclass or even use the non-public class.

# Final class:
It's the end of the inheritance line. Nobody can extend a final class.

# Private constructor:
If a class has only private constructor, it can't be subclassed.

# abstract class and abstract method

An abstract class cannot be initialized. It can only be inherited.
If you declare an abstract method, you MUST mark the class abstract as well, but abstract class can have non-abstract methods.
All abstract methods must be implemented.

```java
abstract class Canine extends Animal {
    public void roam() {};

    // An abstract method means the method must be overridden
    public abstract void eat(); // no method body
}
```

# define and implement an interface
Methods in an interface must be all abstract.
```java
public interface Pet {
    // interface methods are implicitly public and abstract,
    // so typing 'public' and 'abstract' is optional
    void beFriendly();
    public abstract void play();
}

public class Dog exteds Canine implements Pet {
    public void beFriendly() {...}
    public void play() {...}

    public void roam() {...}
    public void eat() {...}
}

// implement multiple interfaces
public class Cat exteds Animal implements Pet, Paintable {...}
```

# superclass constructors with arguments
```
public class MakeHippo {
    public static void main(String [] args) {
        Hippo h = new Hippo("Buffy");
        System.out.println(h.getName());
    }
}

public abstract class Animal {
    private String name;

    public String getName() {
        return name;
    }

    public Animal(String theName) {
        name = theName;
    }
}

public class Hippo extends Animal {
    public Hippo(String name) {
        super(name);
    }
}

```

# this
Every constructor can have a call to super() or this(), but never both.

```java
class Mini extends Car {
    Color color;

    public Mini() {
        this(Color.Red);
    }

    public Mini(Color c) {
        super("Mini");
        color = c;
    }

    public Mini(int size) {
        this(Color.Red); 
        super(size); // won't work!
    }
}
```


# static method
The keyword static lets a method run without any instance of the class.
Static methods can't use non-static (instance) variables. Neither non-static methods.

```java
class Math {
    public static int min(int a, int b){...}
}
```

# static variables

```java
public class Duck {
    private int size;
    // initialized ONLY when the class is first loaded
    private static int duckCount = 0;

    public Duck() {
        duckCount++;
    }
}
```

# all about final
A final variable means you can't change its value.
A final method means you can't override the method.
A final class means you can't extend the class.

# private constructor

If you have a class with only static methods, and you do not want the class to be instantiated, you can mark the constructor private.

# autoboxing

```java
Integer i;
int j;
j = i; // good
i = j; // error
```

# about exception

## Risky, exception-throwing code

```java
public void takeRisk() throws BadException {
    if (abandonAllHope) {
        throw new BadException
    }
}
```

## Your code that calls the risky method

```
public void crossFingers() {
    try {
        anObject.takeRisk();
    } catch (BadException ex) {
        System.out.println("Aaarh!")
        ex.printStackTrace();
    }
}
```

## A finally block is where you put code that must run regardless of an exception.

```java
try {
    turnOvenOn();
    x.bake();
} catch (BakingException ex) {
    ex.printStackTrace();
} finally {
    turnOvenOff();
}
```

# serialization and deserialization

```
FileOutputStream fs = new FileOutputStream("Pond.ser")；
ObjectOutputStream os = new ObjectOutputStream(fs);

os.writeObject(myPond);
os.close();

//========

FileInputStream fs = new FileInputStream("MyGame.ser");
ObjectInputStream os = new ObjectInputStream(fs);

// read the objects
Object one = os.readObject();
Object two = os.readObject();

// cast the objects
GameCharacter elf = (GameCharacter) one;
GameCharacter troll = (GameCharacter) two;

os.close();
```

# read data from a Socket

```
Socket s = new Socket("127.0.0.1", 4242);
InputStreamReader streamReader = new InputStreamReader(s.getInputStream());
BufferedReader reader = new BufferedReader(streamReader);

String msg = reader.readLine();
```

# write data to a Socket

```
Socket chatSocket = new Socket("127.0.0.1", 5000);

PrintWriter writer = new PrintWriter(chatSocket.getOutputStream());

writer.println("message");
```

# hashcode() and equals()

If two objects are equal, they MUST have matching hashcodes. So, if you override equals(), you MUST override hashCode().

# compile code in package

```
% cd MyProject/source
% javac -d ../classes com/headfirstjava/PackageExercise.java
```

# running the code
```
% cd MyProject/classes
% java com.headfirstjava.PackageExercise
```

# public, protected, default and private

```
Modifier    | Class | Package | Subclass | World
————————————+———————+—————————+——————————+———————
public      |  y    |    y    |    y     |   y
————————————+———————+—————————+——————————+———————
protected   |  y    |    y    |    y     |   n
————————————+———————+—————————+——————————+———————
no modifier |  y    |    y    |    n     |   n
————————————+———————+—————————+——————————+———————
private     |  y    |    n    |    n     |   n

y: accessible
n: not accessible
```