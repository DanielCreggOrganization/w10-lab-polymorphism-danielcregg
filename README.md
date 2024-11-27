# Java Polymorphism Lab

## Table of Contents
1. [Runtime Polymorphism: Understanding "Many Forms"](#1-runtime-polymorphism-understanding-many-forms)
2. [Compile-time Polymorphism (Method Overloading)](#2-compile-time-polymorphism-method-overloading)
3. [Reference Type Conversions](#3-reference-type-conversions)
4. [Heterogeneous Collections](#4-heterogeneous-collections)
5. [Benefits of Polymorphism](#5-benefits-of-polymorphism)

## Lab Setup
1. Create a package called `ie.atu.polymorphism`
2. Create a `Main` class inside this package
3. Place all the below classes from the DIY sections into this package

## 1. Runtime Polymorphism: Understanding "Many Forms"

### Learning Objective
Understand how polymorphism allows objects to take different forms at runtime, making programs more flexible and reusable.

### Explanation
The word "polymorphism" comes from Greek, meaning "many forms." In Java, this concept allows us to write code that can work with objects of different types as if they were the same type, as long as they share a common parent class. Think of it like a family - while everyone in a family is different, they all respond to their family name.

Consider a real-world example: When you press the "play" button on different devices (phone, TV, radio), they all understand the command "play" but respond differently. This is polymorphism in action - same command, different behaviors based on the type of object.

### Example: Animal Kingdom Hierarchy

```java
public class Animal {
    protected String name;
    protected int age;
    
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public void makeSound() {
        System.out.println(name + " makes a generic sound");
    }
    
    public void move() {
        System.out.println(name + " moves around");
    }
    
    public String getInfo() {
        return name + " (" + age + " years old)";
    }
}
```

```java
public class Dog extends Animal {
    private String breed;
    
    public Dog(String name, int age, String breed) {
        super(name, age);
        this.breed = breed;
    }
    
    @Override
    public void makeSound() {
        System.out.println(name + " barks: Woof! Woof!");
    }
    
    @Override
    public void move() {
        System.out.println(name + " runs on four legs");
    }
    
    // Dog-specific method
    public void fetch() {
        System.out.println(name + " fetches the ball");
    }
}
```

```java
public class Cat extends Animal {
    private boolean isIndoor;
    
    public Cat(String name, int age, boolean isIndoor) {
        super(name, age);
        this.isIndoor = isIndoor;
    }
    
    @Override
    public void makeSound() {
        System.out.println(name + " meows: Meow!");
    }
    
    @Override
    public void move() {
        System.out.println(name + " prowls gracefully");
    }
    
    // Cat-specific method
    public void climb() {
        System.out.println(name + " climbs up high");
    }
}
```

```java
public class Bird extends Animal {
    private double wingspan;
    
    public Bird(String name, int age, double wingspan) {
        super(name, age);
        this.wingspan = wingspan;
    }
    
    @Override
    public void makeSound() {
        System.out.println(name + " chirps: Tweet! Tweet!");
    }
    
    @Override
    public void move() {
        System.out.println(name + " flies through the air");
    }
    
    // Bird-specific method
    public void soar() {
        System.out.println(name + " soars with " + wingspan + "cm wingspan");
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        // Create an array of Animals (demonstrating polymorphism)
        Animal[] animals = new Animal[4];
        animals[0] = new Dog("Buddy", 5, "Golden Retriever");
        animals[1] = new Cat("Whiskers", 3, true);
        animals[2] = new Bird("Tweety", 1, 15.5);
        animals[3] = new Dog("Rex", 7, "German Shepherd");
        
        // Demonstrate polymorphic behavior
        System.out.println("Animals making sounds:");
        for (Animal animal : animals) {
            System.out.println(animal.getInfo());
            animal.makeSound();
            animal.move();
            System.out.println("---------------");
        }
        
        // Demonstrate type-specific behavior
        System.out.println("\nSpecial behaviors:");
        for (Animal animal : animals) {
            if (animal instanceof Dog) {
                ((Dog) animal).fetch();
            } else if (animal instanceof Cat) {
                ((Cat) animal).climb();
            } else if (animal instanceof Bird) {
                ((Bird) animal).soar();
            }
        }
    }
}
```

### Key Concepts Illustrated
1. Common Interface: All animals share basic behaviors (makeSound, move)
2. Different Implementations: Each animal type implements these behaviors differently
3. Type-Specific Methods: Each animal type can also have its own unique methods
4. Runtime Behavior: The actual method called depends on the object's type at runtime

### DIY Exercise: University Community
Create a hierarchy of university community members:

1. Create a base Person class with:
   - Properties: name, id
   - Methods: introduce(), getRole()

2. Create three subclasses:
   - Student (with major, year)
   - Professor (with department, researchArea)
   - Staff (with department, jobTitle)

3. Each subclass should:
   - Override introduce() to provide specific information
   - Override getRole() to return their role
   - Add at least one unique method

4. Create a main program that:
   - Creates an array of Person objects
   - Demonstrates polymorphic behavior
   - Shows how each type can be treated both uniformly and specifically

This exercise will help you understand how polymorphism enables both uniform treatment of different objects and specific behaviors when needed.

## 2. Compile-time Polymorphism (Method Overloading)

### Learning Objective
Understand method overloading as a form of compile-time polymorphism, including how method signatures work and how the compiler resolves method calls.

### Explanation
Method overloading occurs when we create multiple methods in the same class with the same name but different parameter lists. The compiler determines which version of the method to call based on the method signature. Think of it like having multiple doors to the same room - while the destination (method name) is the same, how you get there (parameters) can be different.

A method signature includes:
- Method name
- Number of parameters
- Type of parameters
- Order of parameters

Note: Return type and parameter names are NOT part of the method signature.

### Example

```java
public class Calculator {
    // Basic integer addition
    public int add(int x, int y) {
        System.out.println("Adding two integers");
        return x + y;
    }
    
    // Three parameter addition
    public int add(int x, int y, int z) {
        System.out.println("Adding three integers");
        return x + y + z;
    }
    
    // Double addition
    public double add(double x, double y) {
        System.out.println("Adding two doubles");
        return x + y;
    }
    
    // String concatenation
    public String add(String x, String y) {
        System.out.println("Concatenating strings");
        return x + y;
    }
    
    // Mixed parameter types
    public double add(int x, double y) {
        System.out.println("Adding integer and double");
        return x + y;
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        
        // The compiler chooses the correct method based on arguments
        int sum1 = calc.add(5, 3);                    // Calls first method
        int sum2 = calc.add(5, 3, 2);                 // Calls second method
        double sum3 = calc.add(5.5, 3.5);             // Calls third method
        String result = calc.add("Hello ", "World");   // Calls fourth method
        double sum4 = calc.add(5, 3.5);               // Calls fifth method
        
        // This won't compile - no matching signature
        // calc.add("Hello", 5);
    }
}
```

### Why This is Compile-time Polymorphism
The term "compile-time" comes from when the decision about which method to call is made. The compiler looks at:
1. The method name
2. The arguments provided in the call
3. The available method signatures

Based on this information, it determines at compile time (before the program runs) which method should be called. If no matching method is found, you'll get a compilation error.

### DIY Exercise: MessageFormatter
Create a class MessageFormatter that demonstrates method overloading:

1. Create methods that format messages in different ways:
   - format(String message) - returns message in uppercase
   - format(String message, boolean uppercase) - returns message in upper or lowercase
   - format(String message, String prefix) - returns message with prefix
   - format(String message, String prefix, String suffix) - returns message with prefix and suffix

2. In your main method, demonstrate calling each version of the format method with appropriate arguments.

This exercise will help you practice creating methods with different signatures and understand how the compiler chooses the correct method to call.

## 4. Reference Type Conversions

### Example

```java
public class Vehicle {
    protected String model;
    
    public Vehicle(String model) {
        this.model = model;
    }
    
    public void start() {
        System.out.println(model + " is starting");
    }
}
```

```java
public class Car extends Vehicle {
    public Car(String model) {
        super(model);
    }
    
    public void drive() {
        System.out.println(model + " is driving on the road");
    }
}
```

```java
public class Motorcycle extends Vehicle {
    public Motorcycle(String model) {
        super(model);
    }
    
    public void wheelie() {
        System.out.println(model + " is doing a wheelie!");
    }
}
```

```java
public class TypeConversionDemo {
    public static void main(String[] args) {
        // Upcasting - implicit and safe
        Car car = new Car("Tesla Model 3");
        Vehicle vehicle = car;  // Upcasting happens automatically
        
        vehicle.start();        // Works fine
        // vehicle.drive();     // Won't compile - drive() not in Vehicle
        
        // Safe downcasting
        if (vehicle instanceof Car) {
            Car downcastCar = (Car) vehicle;  // Explicit casting
            downcastCar.drive();              // Now works fine
        }
        
        // Demonstration of unsafe casting
        Vehicle genericVehicle = new Vehicle("Generic");
        // Car wrongCar = (Car) genericVehicle;  // Throws ClassCastException!
        
        // Array of vehicles containing different types
        Vehicle[] vehicles = new Vehicle[3];
        vehicles[0] = new Car("Toyota Camry");
        vehicles[1] = new Motorcycle("Harley Davidson");
        vehicles[2] = new Car("Honda Civic");
        
        // Process all vehicles, checking for specific types
        for (Vehicle v : vehicles) {
            v.start();  // Common method for all vehicles
            
            // Specific processing based on type
            if (v instanceof Car) {
                ((Car) v).drive();
            } else if (v instanceof Motorcycle) {
                ((Motorcycle) v).wheelie();
            }
        }
    }
}
```
## 5. Heterogeneous Collections

### Learning Objective
Understand how to use polymorphism to create and manage collections containing different types of objects that share a common parent class, a powerful real-world application of polymorphism.

### Example: Media Library System
Let's create a media library system that can handle different types of media items. This example shows how polymorphism allows us to manage diverse objects in a single collection.

```java
public class MediaItem {
    private String title;
    private int year;
    private double price;
    
    public MediaItem(String title, int year, double price) {
        this.title = title;
        this.year = year;
        this.price = price;
    }
    
    public void play() {
        System.out.println("Playing: " + title);
    }
    
    public String getInfo() {
        return title + " (" + year + ") - $" + price;
    }
    
    public double getPrice() {
        return price;
    }
}
```

```java
public class Book extends MediaItem {
    private int pages;
    private String author;
    
    public Book(String title, int year, double price, String author, int pages) {
        super(title, year, price);
        this.author = author;
        this.pages = pages;
    }
    
    @Override
    public void play() {
        System.out.println("Opening e-book reader for: " + getInfo());
        System.out.println("Written by: " + author);
    }
    
    public void readPage(int pageNumber) {
        if (pageNumber <= pages) {
            System.out.println("Reading page " + pageNumber);
        } else {
            System.out.println("Page number exceeds book length");
        }
    }
}
```

```java
public class Movie extends MediaItem {
    private String director;
    private int duration;  // in minutes
    
    public Movie(String title, int year, double price, String director, int duration) {
        super(title, year, price);
        this.director = director;
        this.duration = duration;
    }
    
    @Override
    public void play() {
        System.out.println("Starting movie player for: " + getInfo());
        System.out.println("Directed by: " + director);
        System.out.println("Duration: " + duration + " minutes");
    }
    
    public void showSubtitles(boolean enabled) {
        System.out.println("Subtitles " + (enabled ? "enabled" : "disabled"));
    }
}
```

```java
public class MusicAlbum extends MediaItem {
    private String artist;
    private int tracks;
    
    public MusicAlbum(String title, int year, double price, String artist, int tracks) {
        super(title, year, price);
        this.artist = artist;
        this.tracks = tracks;
    }
    
    @Override
    public void play() {
        System.out.println("Starting music player for: " + getInfo());
        System.out.println("Artist: " + artist);
        System.out.println("Number of tracks: " + tracks);
    }
    
    public void shuffle() {
        System.out.println("Shuffling tracks for " + getInfo());
    }
}
```

```java
public class Library {
    private List<MediaItem> mediaItems;
    
    public Library() {
        this.mediaItems = new ArrayList<>();
    }
    
    public void addItem(MediaItem item) {
        mediaItems.add(item);
    }
    
    public void playAll() {
        System.out.println("\nPlaying all media items:");
        for (MediaItem item : mediaItems) {
            item.play();
            System.out.println("------------------------");
        }
    }
    
    public void displayCatalog() {
        System.out.println("\nLibrary Catalog:");
        for (MediaItem item : mediaItems) {
            System.out.println(item.getInfo());
        }
    }
    
    public double calculateTotalValue() {
        double total = 0;
        for (MediaItem item : mediaItems) {
            total += item.getPrice();
        }
        return total;
    }
    
    // Method showing type-specific operations
    public void performSpecialActions() {
        System.out.println("\nPerforming special actions:");
        for (MediaItem item : mediaItems) {
            if (item instanceof Book) {
                Book book = (Book) item;
                book.readPage(1);
            } else if (item instanceof Movie) {
                Movie movie = (Movie) item;
                movie.showSubtitles(true);
            } else if (item instanceof MusicAlbum) {
                MusicAlbum album = (MusicAlbum) item;
                album.shuffle();
            }
        }
    }
}
```

```java
public class LibraryDemo {
    public static void main(String[] args) {
        Library library = new Library();
        
        // Adding different types of media items
        library.addItem(new Book("Clean Code", 2008, 49.99, "Robert Martin", 464));
        library.addItem(new Movie("The Matrix", 1999, 19.99, "Wachowski Sisters", 136));
        library.addItem(new MusicAlbum("Dark Side of the Moon", 1973, 29.99, "Pink Floyd", 10));
        library.addItem(new Book("Design Patterns", 1994, 54.99, "Gang of Four", 395));
        
        // Demonstrate various operations on the collection
        library.displayCatalog();
        library.playAll();
        library.performSpecialActions();
        
        System.out.printf("\nTotal value of library: $%.2f%n", 
                         library.calculateTotalValue());
    }
}
```

### Why This is Powerful
1. Single Collection for Multiple Types: The Library class can manage all media types using a single List<MediaItem>.
2. Common Interface: All items can be played and provide info through common methods.
3. Type-Specific Behavior: Each subclass can implement play() differently and add its own unique methods.
4. Easy Extension: New media types can be added by creating new subclasses of MediaItem.
5. Simplified Management: Common operations can be performed on all items regardless of their specific type.

### DIY Exercise: School Management System
Create a school management system that demonstrates heterogeneous collections:

1. Create a base Person class with:
   - Basic attributes (name, id)
   - Common methods (getInfo, introduce)

2. Create specific classes:
   - Student (with grade, major)
   - Teacher (with subject, yearsOfExperience)
   - Staff (with role, department)

3. Create a School class that:
   - Maintains a single list of all people
   - Can add any type of person
   - Can display all people's information
   - Can find people by role
   - Can perform role-specific operations
## 6. Benefits of Polymorphism

### Learning Objective
Understand the practical advantages of using polymorphism in real-world applications and how it improves code design, maintainability, and reusability.

### Example: Drawing Application
Let's create a simple drawing application that demonstrates the key benefits of polymorphism. This example will show how polymorphism helps create flexible, maintainable code.

```java
public class Point {
    private int x;
    private int y;
    
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
    
    public int getX() { return x; }
    public int getY() { return y; }
    
    @Override
    public String toString() {
        return "(" + x + "," + y + ")";
    }
}
```

```java
public class Shape {
    protected Point position;
    protected String color;
    
    public Shape(Point position, String color) {
        this.position = position;
        this.color = color;
    }
    
    public void draw() {
        System.out.println("Drawing a shape at " + position + " in " + color);
    }
    
    public void move(int newX, int newY) {
        position = new Point(newX, newY);
        System.out.println("Moving shape to " + position);
    }
    
    public Point getPosition() {
        return position;
    }
}
```

```java
public class Circle extends Shape {
    private int radius;
    
    public Circle(Point center, String color, int radius) {
        super(center, color);
        this.radius = radius;
    }
    
    @Override
    public void draw() {
        System.out.println("Drawing a " + color + " circle at " + position + 
                         " with radius " + radius);
    }
}
```

```java
public class Rectangle extends Shape {
    private int width;
    private int height;
    
    public Rectangle(Point topLeft, String color, int width, int height) {
        super(topLeft, color);
        this.width = width;
        this.height = height;
    }
    
    @Override
    public void draw() {
        System.out.println("Drawing a " + color + " rectangle at " + position + 
                         " with width " + width + " and height " + height);
    }
}
```

```java
public class Triangle extends Shape {
    private int base;
    private int height;
    
    public Triangle(Point apex, String color, int base, int height) {
        super(apex, color);
        this.base = base;
        this.height = height;
    }
    
    @Override
    public void draw() {
        System.out.println("Drawing a " + color + " triangle at " + position + 
                         " with base " + base + " and height " + height);
    }
}
```

```java
public class DrawingBoard {
    private List<Shape> shapes;
    
    public DrawingBoard() {
        this.shapes = new ArrayList<>();
    }
    
    // Demonstrates code reusability - works with any shape
    public void addShape(Shape shape) {
        shapes.add(shape);
    }
    
    // Demonstrates flexibility - treats all shapes uniformly
    public void drawAll() {
        System.out.println("\nDrawing all shapes:");
        for (Shape shape : shapes) {
            shape.draw();  // Each shape knows how to draw itself
        }
    }
    
    // Demonstrates maintainability - single point of modification
    public void moveAllShapes(int deltaX, int deltaY) {
        for (Shape shape : shapes) {
            Point currentPos = shape.getPosition();
            shape.move(currentPos.getX() + deltaX, currentPos.getY() + deltaY);
        }
    }
}
```

```java
public class DrawingDemo {
    public static void main(String[] args) {
        DrawingBoard board = new DrawingBoard();
        
        // Adding different shapes demonstrates polymorphism's flexibility
        board.addShape(new Circle(new Point(10, 10), "red", 5));
        board.addShape(new Rectangle(new Point(20, 20), "blue", 15, 10));
        board.addShape(new Triangle(new Point(15, 15), "green", 8, 12));
        
        // Drawing all shapes demonstrates uniform treatment
        board.drawAll();
        
        // Moving all shapes demonstrates code reuse
        System.out.println("\nMoving all shapes:");
        board.moveAllShapes(5, 5);
        
        // Redraw to show new positions
        board.drawAll();
    }
}
```

### Key Benefits Demonstrated

1. **Code Reusability**
   - The DrawingBoard class works with any shape through the common Shape interface
   - New shape types can be added without changing the DrawingBoard code
   - Common behaviors (like moving) are defined once in the parent class

2. **Flexibility**
   - Shapes can be treated uniformly when needed (drawing, moving)
   - Each shape maintains its specific behavior when drawing
   - New shapes can be added by extending the Shape class

3. **Improved Maintenance**
   - Changes to common behavior only need to be made in one place
   - Each shape class is responsible for its own specific implementation
   - The DrawingBoard doesn't need to know about specific shape types

4. **Better Organization**
   - Clear hierarchy of classes
   - Related code is grouped together
   - Common behaviors are centralized

5. **Runtime Flexibility**
   - Objects can be treated according to their common interface
   - Specific behaviors are determined at runtime
   - Collections can hold mixed types of shapes

### DIY Exercise: Simple Game System
Create a game system that demonstrates these benefits:

1. Create a base Character class with:
   - Basic attributes (name, health, position)
   - Common methods (move, attack, defend)

2. Create specific character types:
   - Warrior (strong attack, weak defense)
   - Archer (ranged attack, medium defense)
   - Mage (magical attack, very weak defense)

3. Create a Game class that:
   - Manages a list of characters
   - Can process all character actions in each turn
   - Demonstrates the benefits of polymorphism through:
     * Code reuse in movement and combat systems
     * Flexibility in character interactions
     * Easy addition of new character types
     * Centralized game logic
     * Runtime character behavior differences

## Summary
Through these examples and exercises, we've seen how polymorphism provides:
- A way to write more flexible and reusable code
- Simplified program structure and maintenance
- The ability to treat different objects uniformly when needed
- Easy extension of functionality through new subclasses
- Better organization of related code

These benefits make polymorphism a crucial concept in object-oriented programming, enabling the creation of more maintainable and scalable applications.

End of Lab
---
