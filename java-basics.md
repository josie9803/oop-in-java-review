### Anonymous class

- instance of an unnamed class which is defined on the fly
- Anonymous classes are useful when you need a short custom class to use just once. For example: custom sorting, filtering files in a list, a button's callback.
- Types of anonymous:
  - Anonymous classes: unnamed classes
  - Anonymous objects: unnamed objects
- Example:

```java
    public static void main(String[] args) {
        ClickHandler buttonAction = new ClickHandler() {
            @Override
            public void handleClick(){
                System.out.println(“Clicked!”);
            }
        };
        setButtonCallback(buttonAction);
    }
```

### Printing with format

- Standard printing: System.out.print(), System.out.println().
- Formatted printing: `System.out.printf(<format string>,<arg0>,<arg1>,...)`
  - format string: **text** and **conversion specifiers**
  - arguments: replaced data for conversion specifiers
- Common Conversion Specifiers: %d, %x, %f, %s, %b, %n
  - `%d` decimal (int)
  - `%x` hexadecimal
  - `%f` float
  - `%s` String
  - `%b` boolean
  - `%n` new line (like \n)
- example: if want to print to the console a statement like this: _"Waldo! Is it true that you're 42?"_

  `System.out.printf("%s! Is it %b that you're %d %n","Waldo", true, 42);`

- Formatted printing with floats, columns, and commas groupings:
  - Round to 2 decimal-point places: `%.2f`
  - Use at least 5 columns to print: `%5d  %5.2f`
  - Print with comma groupings: `%,d  %,10.2f`
- Note: use `PrintWriter` //need to see again

### Sorting in Java

- built in static sorting function `.sort()` for Collection: `arrays`, `ArrayList`, etc
- Example: `java.util.Collections.sort( myCars );`
- [Useful interfaces](#useful-classesinterfaces-in-java): `Comparable` and `Comparator`
- Note: Elements in the collection must implement the `Comparable<T>` (generic) interface

### Wrapper classes (a feature of Java)

- A class encapsulates the functionality of a primitive data type into an object
- Wrapper classes are useful where objects are required. For examples, Collections such as `ArrayList` or `HashMap` can only store objects but not primitive data types.
- In Java, immutable wrappers for primitive data types are: `Integer, Double, Boolean, Character, etc`
- Example:

```java
    // Create the ArrayList
    List<Double> values = new ArrayList<>();
    // Make a Double wrapper object from the double value.
    values.add(new Double(6));
    values.add(new Double(0));
    values.add(4);
    // Shuffle (generate a random permutation):
    java.util.Collections.shuffle(values);
```

- Note: In modern Java, **_autoboxing_** and **_unboxing_** make it more convenient to switch between primitive types and their corresponding wrapper classes automatically:

```java
    // Using primitive data type
    int primitiveInt = 42;

    // Using wrapper class
    Integer wrappedInt = Integer.valueOf(primitiveInt);

    // Unboxing: Converting wrapper class object back to primitive type
    int unwrappedInt = wrappedInt.intValue();
```

to

```java
    // Autoboxing: primitive to wrapper
    Integer autoboxedInt = 42;

    // Unboxing: wrapper to primitive
    int unboxedInt = autoboxedInt;
```

Modified example above:

```java
    // Use autoboxing to add double values to the List
    values.add(6.0);
    values.add(0.0);
    values.add(4.0);
```

## Useful classes/interfaces in Java

`File` class: used to work with files

- Example:

```java
    File file = new File(“C:/t/file.txt”);
    //common methods:
    file.getAbsolutePath();
    file.exist();
    file.isDirectory();
    file.length();
    file.listFiles();
    file.listFiles(FileFilter filter);
```

`FileFilter` interface

- How to use?
  - Write a custom-filter class which implements FileFilter interface.
  - Instantiate our custom-filter.
- Example: write the custom-filter using anonymous class

```java
    private static void demoFileFilter() {
        // Create the custom-filter (an anonymous class)
        FileFilter filter = new FileFilter() {
            @Override public boolean accept(File file) {
                return file.getName().endsWith(".txt"); }
            };

        // Use the filter (with callback)
        File folder = new File("C:/t/");
        File[] fileList = folder.listFiles(filter); //our custom-filter is used here

        for (File subFile : fileList) {
            System.out.println(" sub file: " + subFile.getAbsolutePath());
        }
    }
```

- Example: write the custom-filter using anonymous object of an anonymous class

```java
    private static void demoFileFilter() {
        File folder = new File("C:\\t\\");
        // Create filter (anonymous object of an anonymous class)
        // basically we don't have the object named "filter" here
        File[] fileList = folder.listFiles(new FileFilter() {
            @Override
            public boolean accept(File file) {
                return file.getName().endsWith(".txt"); }
        });

        for (File subFile : fileList) {
            System.out.println(" sub file: " + subFile.getAbsolutePath());
        }
    }
```

`Comparable`

- interface defines **natural order** (aka one ordering).
- Note: Elements in the collection must implement the `Comparable<T>` (generic) interface
- Example:

```java
    class Pen implements Comparable<Pen> {
        String colour;
        int filled;
        // ... Some content omitted...
        @Override
        public int compareTo(Pen other) {
            return colour.compareTo(other.colour);
        }
    }
```

```java
    public static void main(String[] args) {

        // Create the list with some items:
        List<Pen> list = new ArrayList<>();
        list.add(new Pen("Green", 14));
        list.add(new Pen("Orange", 20));
        list.add(new Pen("Blue", 75));

        // Sort the list
        java.util.Collections.sort(list);

        // Output the list.
        for (Pen item : list) {
            System.out.println(item);
        }
    }
```

- Back to above note: instead of using compareTo, can we add to list then use
  colllections.sort(list.getColor)?
  —> no, cuz list doesn’t have .getColor()
- Note #2: `String` class already implements Comparable interface, so we don’t need to write sort() alphabetically by ourselves.

`Comparator`

- interface defines **multiple order**
- Note: We need multiple classes representing each type of ordering we want. Each of them must implement `Comparator<T>` generic interface.
- Example:

```java
    class PenSortByFilled implements Comparator<Pen> {
        // Return a negative number if o1 < o2
        // Return 0 if equal.
        // Return a positive number if o1 > o2.
        @Override
        public int compare(Pen o1, Pen o2) {
            return o1.getFilled() - o2.getFilled(); }
    }
```

```java
    public static void main(String[] args) {
        // Create the list with some items:
        List<Pen> list = new ArrayList<>();
        list.add(new Pen("Green", 14));
        list.add(new Pen("Orange", 20));
        list.add(new Pen("Blue", 75));

        // Sort the list
        Collections.sort(list, new PenSortByFilled());
        //or
        //java.util.Collections.sort(list, new PenSortByFilled());

        // Output the list.
        for (Pen item : list) {
        System.out.println(item);
        }

        //NOTE:
        //PenSortByFilled() not anonymous class bcuz it has a name
        //but is an anonymous object cuz theres nothing pointing to it
    }
```

## Strategy Pattern

- encapsulating an algorithm into a class
- Example: `FileFilter` and `Comparator` interfaces

### Inner classes (a feature of Java)

- A class that is wrapped inside another class.
- Inner classes are useful for showing the tight relationship between inner class and outer class, used when we need an [anonymous class](#anonymous-class), etc (more on chatGPT)
- Types of inner classes:
  - Anonymous inner class
    - Note: Anonymous class cannot be an outer class.
  - Member inner class
    //more on chatGPT
- Accessibility:
  An inner class can access all variables & methods visible in the enclosing scope:
  - fields & methods of inner class.
  - fields & methods of containing object (or local variables and parameters).
    - need to be **final or effectively final**
      - because: inner class runs much later than containing function.
      - then parameters and local variables no longer exist.
    - then how **final or effectively final** would help?
      - Java inner class automatically creates a reference to containing object and needed local variables/parameters. --> **capturing variables**
        - If variable not final, Java does not know which value to capture.
- Example:

```java
    void foo(int x) {
        // Don't change x!
        // x = 42;
        model.addObserver(new Observer() {
            @Override
            public void event() {
                System.out.println("VAL: " + x); }
            });
    }
```

### Lambda expressions (a feature of Java)

- A shorter syntax to represent anonymous class, anonymous function.
- Lambda expressions are useful when interface has _only one method_ (called **functional interface**). (It's awkward to create anonymous classes for small interfaces.)
  - Compactness
  - Clarity: not state the type of argument
- Example:

```java
    // using an anonymous inner class
    void foo(int x) {
        myModel.addObserver(new DaObserver() {
        @Override
        public void dataChanged(int newVal) {
            System.out.println(newVal); }
        });
    }
```

```java
    //using lambda expressions
    void foo(int x) {
        myModel.addObserver((newVal) ->
            System.out.println(newVal);
        );
    }
    //NOTE: cannot use method references
```

### Method references (a feature of Java)

- An even shorter syntax/notion in replace of [lambda expressions](#lambda-expressions-a-feature-of-java).
- Method references are useful when lambda expressions just simply _call a method and pass along its parameters_.
- Example:

```java
interface Observer {
    void event(String description);
}
class Model {
    public void addObserver(Observer obs) {
        //...
    }
}
class Client {
    public void regObserver() {
    Model model = new Model();
    // Option 1: Anonymous Class
    model.addObserver(new Observer() {
        @Override
        public void event(String description) {
            handleEvent(description);
    }
    });

    // Option 2: Lambda
    model.addObserver(msg -> handleEvent(msg));

    // Option 3: Method Reference
    model.addObserver(this::handleEvent);
    }
    private void handleEvent(String description) {
        System.out.println(description);
    }
}
```

### Stream (a feature of Java)

- A sequence of objects/elements supporting a pipeline of operations.
  - stream can be processed sequentially or in parallel.
- **Stream pipeline**: a sequence of operations applied to a stream to perform a specific computation (combine stream operations to process elements in a stream), containing 3 parts:
  - source stream: provides the stream
  - intermediate operations: operates on stream; returns stream (ex: `filter, sorted, map`)
  - terminal operations: collects result as desired for return (ex: `count, collect, reduce, forEach`)
- Example:

```java
    List<Double> heights_m = Arrays.asList(10.0, 30.0, 20.0, 60.0, 50.0);
    heights_m.stream()
             .map(x -> x * x)
             .forEach(x -> System.out.println(x));
```

- Special streams:
  - Streams operate on a sequence of objects.
  - `IntStream LongStream DoubleStream` operate on a sequence of primitives.
- **Fluent API**
