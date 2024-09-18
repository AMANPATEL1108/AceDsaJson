<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Array in Java</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 20px;
        }
        h1, h2, h3 {
            color: #333;
        }
        pre {
            background-color: #f4f4f4;
            border: 1px solid #ddd;
            padding: 10px;
            overflow-x: auto;
        }
        code {
            font-family: monospace;
            background-color: #f4f4f4;
            padding: 2px 4px;
        }
    </style>
</head>
<body>
    <h1>aman</h1>
    <p>Arrays are fundamental data structures in Java used to store multiple values of the same type in a single variable. They offer a convenient way to manage collections of data. For example, if you need to store the ages of several people, instead of creating individual variables for each age, you can use an array to hold all ages in a single data structure.</p>

    <h2>Declaring Arrays</h2>
    <p>In Java, arrays are declared by specifying the type of elements and the square brackets <code>[]</code>. The type can be any data type, including primitive types (like <code>int</code>, <code>float</code>, etc.) and reference types (like <code>String</code>, <code>Object</code>, etc.).</p>

    <pre><code>Type[] arrayName;

Example:

String[] cars;
int[] numbers;
</code></pre>

    <h2>Initializing Arrays</h2>
    <p>Initialization is the process of assigning values to an array after declaring it. You can initialize arrays either at the time of declaration or separately after declaration.</p>

    <h3>Inline Initialization:</h3>
    <pre><code>String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};

int[] myNum = {10, 20, 30, 40};
</code></pre>

    <h3>Separate Initialization:</h3>
    <pre><code>String[] cars = new String[4];

cars[0] = "Volvo";
cars[1] = "BMW";
cars[2] = "Ford";
cars[3] = "Mazda";
</code></pre>

    <h2>Accessing Array Elements</h2>
    <p>Array elements are accessed using their index, which starts at 0. The syntax to access an element is:</p>

    <pre><code>arrayName[index];

</code></pre>

    <p>Example:</p>
    <pre><code>String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};

System.out.println(cars[0]); // Outputs Volvo
</code></pre>

    <h2>Modifying Array Elements</h2>
    <p>To change the value of an element in an array, you use the index and assign a new value to it.</p>

    <p>Example:</p>
    <pre><code>String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};

cars[0] = "Opel";
System.out.println(cars[0]); // Outputs Opel
</code></pre>

    <h2>Array Length</h2>
    <p>The length property of an array provides the number of elements in the array. It is useful for looping through arrays and ensuring you do not exceed the bounds of the array.</p>

    <p>Example:</p>
    <pre><code>String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};

System.out.println(cars.length); // Outputs 4
</code></pre>

    <h2>Looping Through Arrays</h2>
    <h3>For Loop:</h3>
    <p>A standard for loop is commonly used to iterate through the elements of an array. It requires initializing a counter, checking a condition, and updating the counter.</p>

    <p>Example:</p>
    <pre><code>String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};

for (int i = 0; i &lt; cars.length; i++) {
System.out.println(cars[i]);
}
</code></pre>

    <h3>For-Each Loop:</h3>
    <p>The enhanced for-each loop is designed for iterating over arrays and collections without needing an index. It is more readable and concise.</p>

    <p>Syntax:</p>
    <pre><code>for (Type element : arrayName) {

// Use element
}
</code></pre>

    <p>Example:</p>
    <pre><code>String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};

for (String car : cars) {
System.out.println(car);
}
</code></pre>

    <h2>Multidimensional Arrays</h2>
    <p>Java supports multidimensional arrays, which are essentially arrays of arrays. They are useful for representing more complex data structures like matrices or tables.</p>

    <p>Declaration:</p>
    <pre><code>int[][] matrix;

</code></pre>

    <p>Initialization:</p>
    <pre><code>int[][] matrix = {

{1, 2, 3},
{4, 5, 6},
{7, 8, 9}
};
</code></pre>

    <p>Accessing Elements:</p>
    <pre><code>System.out.println(matrix[0][1]); // Outputs 2

</code></pre>

    <h2>Real-Life Examples</h2>
    <h3>Calculating Average Age</h3>
    <p>Arrays are often used in real-world applications for statistical calculations, such as finding averages.</p>

    <p>Example:</p>
    <pre><code>int[] ages = {20, 22, 18, 35, 48, 26, 87, 70};

float sum = 0;
int length = ages.length;
for (int age : ages) {
sum += age;
}
float average = sum / length;
System.out.println("The average age is: " + average);
</code></pre>

    <h3>Finding the Lowest Age</h3>
    <p>Finding specific values in an array, such as the minimum or maximum value, is a common task.</p>

    <p>Example:</p>
    <pre><code>int[] ages = {20, 22, 18, 35, 48, 26, 87, 70};

int lowestAge = ages[0];
for (int age : ages) {
if (age &lt; lowestAge) {
lowestAge = age;
}
}
System.out.println("The lowest age is: " + lowestAge);
</code></pre>

    <h2>Advanced Array Concepts</h2>
    <h3>Dynamic Arrays</h3>
    <p>In Java, <code>ArrayList</code> from the <code>java.util</code> package provides a dynamic array that can grow and shrink as needed. Unlike fixed-size arrays, <code>ArrayList</code> offers methods to add, remove, and access elements easily.</p>

    <p>Example:</p>
    <pre><code>import java.util.ArrayList;

ArrayList&lt;String&gt; cars = new ArrayList&lt;&gt;();
cars.add("Volvo");
cars.add("BMW");
cars.add("Ford");
cars.add("Mazda");

for (String car : cars) {
System.out.println(car);
}
</code></pre>

    <h3>Jagged Arrays</h3>
    <p>Jagged arrays (arrays of arrays where sub-arrays can have different lengths) are useful for scenarios where the number of elements varies between sub-arrays.</p>

    <p>Example:</p>
    <pre><code>int[][] jaggedArray = new int[3][];

jaggedArray[0] = new int[2];
jaggedArray[1] = new int[3];
jaggedArray[2] = new int[1];

jaggedArray[0][0] = 1;
jaggedArray[0][1] = 2;
jaggedArray[1][0] = 3;
jaggedArray[1][1] = 4;
jaggedArray[1][2] = 5;
jaggedArray[2][0] = 6;
</code></pre>

    <h2>Conclusion</h2>
    <p>Arrays are a powerful tool in Java programming, offering efficient ways to store and manipulate collections of data. Understanding how to declare, initialize, access, modify, and iterate through arrays is fundamental for effective Java programming. Advanced concepts like dynamic arrays and jagged arrays further expand the versatility of arrays in Java applications.</p>

</body>
</html>
