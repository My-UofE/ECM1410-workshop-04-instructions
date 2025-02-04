# ECM1410 Workshop 04 Instructions


You should find you have files `RectangleApp.java` and `Rectangle.java` in your working folder. Open the files and check you can understand the code. 

Compile the files in the terminal:

```
javac RectangleApp.java
```

Note that this should compile both `RectangleApp.java` and `Rectangle.java` producing two `.class` files.

Then, run the program with command:

```
java RectangleApp
```

Read through the code, and compare to the output. 

Make sure you understand how the program is working. Ask a member of the etaching team if you have any questions.

We will now work to edit and extend the example program using the techniques and ideas of object orientated programming covered in the lectures.

### Part 1. Accessing object attributes using `this` 

The `this` keyword can be used within a class definition to refer to the current class instance. 

An advantage of this is to disambiguate variable references, e.g. suppose we 
wanted to be consistent throughout our code and use variable name `width` to store the width values.

We might end up with ambiguous code like that below:

```java
public Rectangle(double width, double height, double originX, double originY) {
    width = width;
    ...
```

Here we are trying to use `width` both as an attribute of the rectangle object, and as the first argument of the constructor.

The `this` keyword allows us to resolve this, by differentiating between the `width` passed as the constructor argument, and the rectangle attribute (accessed using `this.width`):

```java
public Rectangle(double width, double height, double originX, double originY) {
    this.width = width;
    ...
```

**TASK** 

Update the `Rectangle.java` constructor to use argument names as below, and change the constructor body, so that attributes are set via the `this` keyword, to ensure the code functions as expected.

```java
public Rectangle(double width, double height, double originX, double originY) {
    ...
```

Recompile and run `RectangleApp.java`  to check your program still functions.

**TASK** 

Overload the constructor by inserting the following code beneath the constructor you have been editing:

```java
// second constructor: 
// 
//
public Rectangle(double width, double height) {
    this(width, height, 0, 0)
}
```

This constructor allows us to instantiate a rectangle without providing all four arguments (i.e. we only need to pass width and height, not origin co-ordinates).

To test out this constructor uncomment the block of code in `RectangleApp.java` that defines `myRect2` and displays its attributes. Check you understand how the default origin co-ordinates for rectangles created by this constructor are set.

**TASK** 

Add a this constructor that allows the user to create a rectangle without providing any arguments. In this case its width and height should be set to 1, and its origin set to x=0, y=0.

Uncomment the code block that defines `myRect3` in `RectangleApp.java` to check your code.

Once you have completed this task commit and push your work with the message:

```
completed part 1
```

### Part 2. Adding more methods

#### Scaling the rectangles

Suppose we want to scale the rectangle. 

e.g. 

We could scale it by x2 in both the x and y directions and double its height and width. 

We could scale it by x3 in the y-direction only to triple its height.

We could scale it by x0.5 in the x-direction only to half its width.

** TASK **

Create an additional method `scale` that can implement this.

You should overload the method so that it can be called in two ways:

 - by providing a single scaling factor (to be applied to both width and height).
 - by providing two scaling factors (`scaleX` and `scaleY` to be applied to the width and height respectively).

**Hint.** Look at the `move` method as an example if you are unsure of how to go about this.

 Test your methods by adding the following lines and displaying the new dimensions of the rectangles.

```
 myRect1.scale(0.5); // should change width to 8, height to 4

 myRect2.scale(1,3); // should change height to 24

 myRect3.scale(15,10); // should scale to width 15, height 10
```

#### Comparing rectangle positions

Suppose we have two rectangle objects. We might want to determine if they overlap.

We can do this with a method taking the following form:

```java
public boolean isOverlappedWith(Rectangle r){]
   ...
}
```

For example, when completed we could then check if rectangle `myRect1` overlaps `myRect2` using code:

```java
boolean overlapping = myRect1.isOverlappedWith(myRect2);
```

Within the `isOverlappedWith` method we can use the attributes of `this` and `r` to compare the positions of the two rectangles. 

Edit your code to add this method. When you have finished you can test it on the following rectangles.

```
myRect4 = new Rectangle(30.0, 5.0, 10, 10); 
myRect5 = new Rectangle(50.0, 20.0, 0, 0); 
myRect6 = new Rectangle(20.0, 40.0, 500, 500); 

// myRect4 overlaps myRect5 so these should show as true
System.out.println( "myRect4 overlaps myRect5: " myRect4.isOverlappedWith(myRect5) ) ; 
System.out.println( "myRect5 overlaps myRect4: " myRect5.isOverlappedWith(myRect4) ) ;

// myRect4 does not overlap myRect6 so these should show as false
System.out.println( "myRect4 overlaps myRect6: " myRect4.isOverlappedWith(myRect6) ) ;
System.out.println( "myRect6 overlaps myRect4: " myRect6.isOverlappedWith(myRect4) ) ;
```

#### Finding the aspect ratio

 - Add a method calcRatio() for calculating the ratio of width to height.

 - Add a method isSquare() for determining if the rectangle is square or not.

Note: use the correct way of testing floating-point numbers for equality, as practiced in the first workshop, e.g. define a square as having ratio is within the range 0.999 and 1.001

Once you have completed this task commit and push your work with the message:

```
completed part 2
```

### Part 3. The access modifier

As mentioned in the lecture, a well-encapsulated class always hide their attributes to avoid the object’s state (or attributes) being directly changed outside of the class. 

To achieve this we need set all the instance attributes to private, and provide public setter and getter methods to modify and view the attributes.

**TASK**
Edit the Rectangle.java file so that the Rectangle class is well-encapsulated.

Hint. This requires changes similar to the following:

```
// change to private attributes
private double width; // private attribute
```

```
// for each attribute provide getter method
public double getWidth(){ 
  return width;
}
```

```
// for each attribute provide setter method
public void setWidth(double width){
  this.width = width;
}
```

When you think you have completed this, try to compile `Rectangle.java` (not `RectangleApp.java`!) and work through any issues.

You can then try to compile `RectangleApp.java` note that this will fail because now we can only access attributes using the getter/setter methods. Update the code accordingly, until both files compile and run correctly.

Once you have completed this task commit and push your work with the message:

```
completed part 3
```

### Part 4. Object reference

Now add code to the bottom of RectangleApp to create three rectangles as follows.

```
Rectangle r1 = new Rectangle(10.0,5.0);
Rectangle r2 = new Rectangle(10.0,5.0);
Rectangle r3 = r2;
```

Then use println() to print the three rectangle's 'value'.

```
System.out.println("r1: " + r1);
System.out.println("r2: " + r2);
System.out.println("r3: " + r3);
```

When run the program, you will see the output like this: Rectangle@7852e922, which is the class name together with the hashcode of the object in hexadecimal (you may understand it as the memory address for each object). 

You may see the hashcode of `r1` and `r2` are different, because whenever you `new` an object, the compiler will allocate a new block of memory for it.

However you should see that `r2` and `r3` have the same hash code. This is because the variable `r3` was assigned using `r3 = r2` so that it is a reference to the same object in memory. 

This means that whenever you change any attribute’s value for one object, the other object’s attribute value also changes. 

In other words, you may treat them as one object, but with two handles (`r2` and `r3`). 

Try adding the following statement:

```
r2.zoom(0.5);
System.out.println("r2 width: " + r2.getWidth());
System.out.println("r3 width: " + r3.getWidth());
```

Now rerun the program and check that the width of `r2` and `r3` were both updated.

Once you have completed this task commit and push your work with the message:

```
completed part 4
```

### Part 5. toString() method

Every well-designed Java class should contain a public method called `tostring()` that returns a short description of the instance (in a return type of `String`). 

The `toString()` method can be called explicitly (via `objectName.toString()`) just like any other method; or implicitly through `println()` or `print()`. 

If an instance is passed to the `println(objectName)` function, the `toString()` method of that instance will be invoked implicitly. 

Add the following `toString()` method to the Rectangle class:

```java
// Return a description of a rectangle in the form of
// Rectangle[x=*,y=*,w=*,h=*]
public String toString(){
return "Rectangle[x="+originX+",y="+originY+",w="+width+",h="+height+"]";
}
```

Re-compile and re-run RectangleApp.java, and you should see the outputs of the following statements are different.

```
System.out.println("r1: " + r1);
System.out.println("r2: " + r2);
System.out.println("r3: " + r3);
```

This is because if a class doesn’t have the `toString()` method, the compiler will output the default `className@hashcode`. If a class has defined the `toString()` method, the compiler will output the form which you customize.

As metioned above, you may call `toString()` method explicitly, just like any other methods, e.g.

```
System.out.println("r1: " + r1.toString());
```

Once you have completed this task commit and push your work with the message:

```
completed part 5
```

### Part 6. Circles

You have worked to define a Rectangles class in an object-orientated way.  Let's now practise further by defining a `Circle` class.

You should create two files:

 - `Circle.java` containing the Circle class definition
 - `CircleApp.java` containing the `main()` method. Use this file to creat some example objects and test out your methods.
 
You should code the following attributes, methods and constructors in the `Circle` class.

**Attributes:** (all set to be ’private’)

 - radius
 - originX
 - originY

**Constructors**

 - a constructor with three arguments (radius and originX, originY)
 - a constructor with one argument (radius) defaults to origin at (0,0)
 - a no-arg constructor, defaults to radius 1 and origin at (0,0)

**Methods**

 - getRadius / setRadius
 - getOriginX / setOriginX
 - getOriginY / setOriginY

 - getArea: Compute the area
 - getCircumference: Compute the circumference.
 - move: Move the circle 
 - toString: Describe the basic information of a circle by defining the toString() method.
 - scale: Scale the circle by a factor.
 - isOverlappedWith: Determine if a circle is overlapped with another circle. 
 - isEnclosedBy: Determine if one circle is enclosed within another circle. 
 
For the last two methods there are two options. We have already seen how to define an instance method:

```
public boolean isOverlappedWith(Circle c)
```

However there is another option to define a static method, which is not part of an instance, and called with two arguments (the circles to compare):

```
public static boolean areOverlapping(Circle c1, Circle c2)
```

Add the above static method to your class.

Ensure that your `Circle.java` and `CircleApp.java` files compile, and that you test out the class methods fully in your `CircleApp.java` file.

Once you are happy with your work commit and push your work with the message:

```
completed part 6
```
