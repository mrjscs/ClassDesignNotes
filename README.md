## Class Design

***
### Java Classes

We have seen that Java uses a structure called a `class` to organize its code. We have also seen that these classes can contain multiple method definitions:

```java
public class Example {
    public static void main(String[] args) {
        int[] arr = {5, 2, 1, 0, -14, 12, 2, 9};
        
        System.out.println( max(arr) ); // prints 12
    }

    public static void max(int[] nums) {
        int m = nums[0];
        
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] > m) {
                m = nums[i];
            }
        }
        
        return m;
    }
}
```

These classes can also be used to create **reference types**. We have already been using some classes in our code, most notably the `String` class and the `Math` class.

When we declare and initialize `String` variables we just assign the variable to the value of a literal in double quotations. For example:

```java
String message = "Hello World"; 
```

There is another (less used) way to assign a value to a `String` variable:

```java
String message = new String("Hello World");
```

The `new` keyword is used to create an **instance** of a class.
Here are some more examples:

```java// Create an instance of the String class:
String name = new String("Jane Doe");

// Call methods of the String class:
String firstName = name.substring(0, name.indexOf(" "));
System.out.println("Welcome " + firstName);
```

A class **instance** is an **object** of that class that is referenced by a variable.

***
### Defining Classes

As well as containing methods, classes can also store data in variables. These variables are declared inside a class, but not within a method. They are called **instance variables**. For example, a class that represents a car might look something like this:

<table>
<thead>
<tr><th>Car.java</th><th>Example.java</th></tr>
</thead>
<tbody>
<tr>
<td style="vertical-align: top">

```java
public class Car {
    String make;
    String model;
    int year;
    int mpg;  // miles per gallon
}
```
</td>
<td style="vertical-align: top">

```java
public class Example {
    public static void main(String[] args) {
        // Instantiate a new Car object:
        Car myRide = new Car();
        
        // Initialize variables using dot notation:
        myRide.make = "Toyota";
        myRide.model = "Corolla";
        myRide.year = 2023;
        myRide.mpg = 33;
        
        System.out.print("I drive a ");
        System.out.print(myRide.make + " " + myRide.model);
    }
}
```
</td>
</tr>
</tbody></table>

The `Example` class creates an instance of the `Car` class and initializes its variables.

In this way a class can group all data about a car in a single variable called `myRide`. The **dot notation** can be used to access the variables defined inside the class.

***
### Encapsulation

Unfortunately, storing data in this way is considered a bad programming practice. This is because changing the values of the instance variables from a different class (e.g. `Example`) may cause the data to lose integrity or become corrupted. To prevent this, the variables inside a class can be declared using the `private` keyword, meaning they cannot be accessed from a different class.

<table>
<thead>
<tr><th>Car.java</th><th>Example.java</th></tr>
</thead>
<tbody>
<tr>
<td style="vertical-align: top">

```java
public class Car {
    private String make;
    private String model;
    private int year;
    private int mpg;  // miles per gallon
}
```
</td>
<td style="vertical-align: top">

```java
public class Example {
    public static void main(String[] args) {
        // Instantiate a new Car object:
        Car myRide = new Car();
        
        // Attempt to initialize variable:
        myRide.make = "Toyota"; // ERROR!!!!
        // There is no public access to "make"
    }
}
```
</td>
</tr>
</tbody></table>

Using the `private` modifier, hides the implementation of a class. This is a programming technique called **encapsulation** in which data and methods are wrapped together under a single unit (a class).

***
### Constructor Methods

So how can private instance variables be initialized? It is usually done by creating a special method called a **constructor**.

A constructor method is declared without a return type and must have the same name as the class itself. It uses **parameter variables** to initialize its **instance variables**.

<table>
<thead>
<tr><th>Car.java</th><th>Example.java</th></tr>
</thead>
<tbody>
<tr>
<td style="vertical-align: top">

```java
public class Car {
    private String make;
    private String model;
    private int year;
    private int mpg;  // miles per gallon
    
    // Constructor method:
    public Car(String mk, String mdl, int yr, int miles) {
        make = mk;
        model = mdl;
        year = yr;
        mpg = miles;
    }
}
```
</td>
<td style="vertical-align: top">

```java
public class Example {
    public static void main(String[] args) {
        // Instantiate a new Car object:
        Car myRide = new Car("Toyota", "Corrola", 2013, 33);

        System.out.print("I own a ");
        
        // Attempt to access variable:
        System.out.println(myRide.make); // ERROR!!!!
        // There is no public access to "make"
    }
}
```
</td>
</tr>
</tbody></table>

There is still a problem, the values from the instance variables cannot be accessed from the `Example` class because they have been declared as `private`. To make the values accessible, a method can be defined to return its value:

<table>
<thead>
<tr><th>Car.java</th><th>Example.java</th></tr>
</thead>
<tbody>
<tr>
<td style="vertical-align: top">

```java
public class Car {
    private String make;
    private String model;
    private int year;
    private int mpg;  // miles per gallon
    
    // Constructor method:
    public Car(String mk, String mdl, int yr, int miles) {
        make = mk;
        model = mdl;
        year = yr;
        mpg = miles;
    }
    
    // Getter methods:
    
    public String getMake() {
        return make;
    }

    public String getModel() {
        return model;
    }
}
```
</td>
<td style="vertical-align: top">

```java
public class Example {
    public static void main(String[] args) {

        // Instantiate a new Car object:
        Car myRide = new Car("Toyota", "Corrola", 2013, 33);

        System.out.print("I own a ");
        
        // Access instance variables:
        System.out.print(myRide.getMake() + " ");
        System.out.println(myRide.getModel());
    }
}
```
</td>
</tr>
</tbody></table>

Methods that return the value of an instance variable are called **getter methods** and traditionally named to start with thw word `get` followed by the name of the variable (e.g. `getMake()`, `getModel()`)

You might be wondering why go to the trouble of having private instance variables and getter methods to access them. This is because you can guarantee data integrity by checking the assigned values:

```java
public class Car {
    private String make;
    private String model;
    private int year;
    private int mpg;  // miles per gallon
    
    // Constructor method:
    public Car(String mk, String mdl, int yr, int miles) {
        make = mk;
        model = mdl;
        
        // Check for a valid year:
        if (yr > 1970 && yr < 2025) { 
            year = yr;
        }
        
        // Check for a valid mpg:
        if (miles  > 0) {
            mpg = miles;
        }
    }
    
    // Getter methods:
    
    public String getMake() {
        return make;
    }

    public String getModel() {
        return model;
    }
}
```

As well as getter methods, setter methods can be added that can change the value of instance fields. These methods should have a `void` return type.

<table>
<thead>
<tr><th>Car.java</th><th>Example.java</th></tr>
</thead>
<tbody>
<tr>
<td style="vertical-align: top">

```java
public class Car {
    private String make;
    private String model;
    private int year;
    private int mpg; 
    
    // Constructor method:
    public Car(String mk, String mdl, int yr, int miles) {
        make = mk;
        model = mdl;
        if (yr > 1970 && yr < 2025) year = yr;
        if (miles > 0) mpg = miles;
    }
    
    // Getter methods:
    public String getMake() { return make; }
    public String getModel() { return model; }
    public int getYear() { return year; }
    public int getMpg() { return mpg; }
    
    // Setter methods:
    
    public void setYear(int yr) {
        if (yr > 1970 && yr < 2025) 
            year = yr;
    }

    public void setMpg(int miles) {
        if (miles > 0) 
            mpg = miles;
    }
}
```
</td>
<td style="vertical-align: top">

```java
public class Example {
    public static void main(String[] args) {

        // Instantiate a new Car object:
        Car myRide = new Car("Toyota", "Corrola", 2013, 33);
        
        // Improve fuel efficiency:
        myRide.setMpg(40);

        System.out.print("My ");
        System.out.print(myRide.getMake() + " ");
        System.out.print(myRide.getModel() + " ");
        System.out.print("gets " + myRide.getMpg());
        System.out.print(" miles per gallon");
    }
}
```
</td>
</tr>
</tbody></table>

***
### Using `this` Keyword

Let's look again at the **instance variables** and **constructor method**:

```java
public class Car {
    // Instance variable:
    private String make;
    private String model;
    private int year;
    private int mpg;

    // Constructor method:
    public Car(String mk, String mdl, int yr, int miles) {
        make = mk;
        model = mdl;
        
        if (yr > 1970 && yr < 2025) {
            year = yr;
        }
        
        if (miles > 0) {
            mpg = miles;
        }
    }

    // other methods not shown
}
```

As we have seen, the role of the constructor method is to initialize the values of the instance fields. TO avoid confusion, different variable names have been used. For example:

```java
make = mk;
```
This statement assigns the instance field `make` the value of the parameter variable `mk`.

However, it is possible to use the same variable name to distinguish between the two variables, the `this` keyword can be used as follows:

```java
public class Car {
    // Instance variable:
    private String make;
    private String model;
    private int year;
    private int mpg;

    // Constructor method:
    public Car(String make, String model, int year, int mpg) {
        this.make = make;
        this.model = model;
        
        if (yr > 1970 && yr < 2025) {
            this.year = year;
        }
        
        if (miles > 0) {
            this.mpg = mpg;
        }
    }

    // other methods not shown
}
```
The keyword `this` refers to the object itself (it's instance variables and methods). So the assignment:

```java
this.make = make;
```
This is assigning the value of the parameter variable `make` to the instance variable `make`.

***
### Accessor Methods

Any method that returns data from instance variables is called an **accessor method**. This could be simply returning the value, like a **getter method**,

***
Other Examples
file name
