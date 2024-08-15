### Task:

Create a Java program that reads two text files containing lists of integers, one per line. The program should merge the contents of the two input files into a single output file, maintaining the original order of the integers. Additionally, the program should create a separate output file containing the integers that are present in both input files.

Instructions:

1. Read integers from two text files called "input1.txt" and "input2.txt". Each integer is on a new line in the respective files.
2. Merge the contents of the two input files, maintaining the original order of the integers, and write the result to a new text file called "merged.txt".
3. Identify the integers that are present in both input files.
4. Write the integers that are present in both input files to a new text file called "common.txt".
5. Handle any exceptions that might occur during the process, such as `FileNotFoundException`, `IOException`, and `NumberFormatException`. Use try-catch blocks as needed.

### Contents

<ol> 
<li> Set Up Project Directory</li>
<li> Import Necessary Packages</li>
<li> Define Main Class and Main Mehtod</li>
<li> Read Integers From File</li>
<li> Write Integers From File</li>
<li> Main Method Implementation </li>
<li> Key Concepts </li>
</ol>


### 1. Set Up 
#### Ensure your project directory looks like this:

```java
Assignment_IO/
├── .idea/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── org.example/
│   │   │       └── MergeAndFindCommonIntegers.java
│   │   └── resources/
│   │       ├── input/
│   │       │   ├── input1.txt
│   │       │   └── input2.txt
│   │       └── output/
│   │           ├── merged.txt
│   │           └── common.txt
├── test/
├── .gitignore
├── pom.xml
```
### 2. Import Necessary Packages

##### In `MergeAndFindCommonIntegers.java`, start by importing the required classes for file I/O and collections:

```java
package org.example;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.util.ArrayList;
import java.util.HashSet;
import java.util.List;
import java.util.Set;
```

### 3. Main Method and Class

##### Create the class and define the `main` method, which will serve as the entry point for the program:

```java
public class MergeAndFindCommonIntegers {

    public static void main(String[] args) {
        // Implementation will go here
    }

}

```



### Read Integers From File

##### Implement a method to read integers from a a specified file and handle exceptions
```java
    private static List<Integer> readIntegersFromFile(String fileName) {
        List<Integer> integers = new ArrayList<>();
        try (BufferedReader br = new BufferedReader(new FileReader(fileName))) {
            String line;
            while ((line = br.readLine()) != null) {
                try {
                    // Parse each line as an integer and add it to the list
                    integers.add(Integer.parseInt(line.trim()));
                } catch (NumberFormatException e) {
                    // Handle invalid number format and print an error message
                    System.err.println("Invalid number format in file " + fileName + ": " + line);
                }
            }
        } catch (FileNotFoundException e) {
            // Handle case where the file is not found and print an error message
            System.err.println("File not found: " + fileName);
        } catch (IOException e) {
            // Handle general I/O exceptions and print an error message
            System.err.println("IOException while reading file " + fileName);
        }
        return integers; // Return the list of integers
    }
```

### 5 .Write Integers from File

##### Implement a Method to write a list of integers to a specified file

```java
    private static void writeIntegersToFile(List<Integer> integers, String fileName) {
        try (BufferedWriter bw = new BufferedWriter(new FileWriter(fileName))) {
            for (int number : integers) {
                // Write each integer to the file, followed by a new line
                bw.write(String.valueOf(number));
                bw.newLine();
            }
        } catch (IOException e) {
            // Handle general I/O exceptions and print an error message
            System.err.println("IOException while writing to file " + fileName);
        }
    }
```


### 6. Main Method Implementation

##### Implement the the logic in the main method to read the integers merge them find common integers and write the results to files

```java
    public static void main(String[] args) {
        // Step 1: Read integers from the first input file
        List<Integer> list1 = readIntegersFromFile("src/main/resources/input/input1.txt");

        // Step 1: Read integers from the second input file
        List<Integer> list2 = readIntegersFromFile("src/main/resources/input/input2.txt");

        // Step 2: Check if both lists were read successfully
        if (list1 != null && list2 != null) {
            // Step 2: Merge the contents of the two lists, maintaining the original order
            List<Integer> mergedList = new ArrayList<>(list1);
            mergedList.addAll(list2);

            // Step 4: Write the merged list to the output file "merged.txt"
            writeIntegersToFile(mergedList, "src/main/resources/output/merged.txt");

            // Step 3: Identify the integers that are present in both input files
            Set<Integer> commonSet = new HashSet<>(list1);
            commonSet.retainAll(list2); // Retain only the common elements

            // Convert the set of common integers to a list
            List<Integer> commonList = new ArrayList<>(commonSet);

            // Step 5: Write the common integers to the output file "common.txt"
            writeIntegersToFile(commonList, "src/main/resources/output/common.txt");
        }
    }

```

### 7. Key Concepts

<ol> 
<li> 1. File I/O</li>
<li> 2. Lists and Sets</li>
<li> 3. Exception Handling</li>
<li> 4. Loops and Conditionals</li>
<li> 5. Modular Programming</li>
</ol>

#### 1. File I/O
##### Reading From a File
###### BufferedReader and FileReader
<ul>
	<li>
	`FileReader` is used to open the file for reading
	</li>
	<li>
	`BufferedReader` reads the file line by line, which is efficient for text files
	</li>
</ul>
##### Writing to a File
###### BufferedWriter and FileWriter
<ul>
	<li>
	`FileWriter` is used to open the file for writing.
	</li>
	<li>
	`BufferedReader` writes data to the file efficiently
	</li>
</ul>

#### 2. Lists and Sets
##### Lists
<ul>
	<li>
	A `list` is an ordered collection of elements. Here we used `ArrayList`
	</li>
	<li>
	Useful for maintaining the order of elements read from a file
	</li>
</ul>
##### Set
<ul>
	<li>
	a `Set` is an unordered collection of elements. Here we used `ArrayList`
	</li>
	<li>
	Useful for identifying common elements between two lists
	</li>
</ul>
#### 3. Exception Handling
##### Try-Catch Blocks
<ul>
	<li>
	Used to handle exceptions (errors) that might occur during file operations or data processing
	</li>
	<li>
	Allows the program to handle errors gracefully without crashing
	</li>
</ul>
##### Common Exceptions
<ul>
	<li>
	`FileNotFoundException` thrown when a file is not found
	</li>
	<li>
	`IOException` Thrown for I/O errors
	</li>
	<li>
	`NumberFormatException` thrown when trying to parse an invalid integer from a string
</ul>
#### 4. Loops and Conditionals
##### Loops
###### For Loop
<ul>
	<li>
	Iterates over a list of integers to write them to a file
	</li>
	</ul>
###### While Loop
<ul>
	<li>
	Reads lines from a file until there are no more lines to read
	</li>
</ul>
##### Conditionals
###### If-Else Statements
<ul>
	<li>
	Used to check if lists were read successfully before proceeding
	</li>
	<li>
	Used to handle specific errors and provide feedback to the user
</ul>
#### 5. Modular Programming
###### Methods - Breaking down the program into smaller reusable methods for specific tasks
<ul>
	<li>
	`readIntegersFromFile` reads the integers from a file
	</li>
	<li>
	`writeIntegersFromFile` writes integers to file
</ul>
###### Helps organize code and make it more readable and maintainable




### 8. Step By Step

1. **Setting Up the Project:**
   - Create a new Java project and a class named `MergeAndFindCommonIntegers`.

2. **Import Necessary Packages:**
   ```java
   import java.io.*;
   import java.util.*;
   ```
   - Import `java.io.*` for file operations.
   - Import `java.util.*` for using lists and sets.

3. **Main Method:**
   - The entry point of the program.
   ```java
   public static void main(String[] args) {
   ```
   - All execution starts here.

4. **Reading Integers from Files:**
   - Call `readIntegersFromFile` to read from `input1.txt` and `input2.txt`.
   ```java
   List<Integer> list1 = readIntegersFromFile("input1.txt");
   List<Integer> list2 = readIntegersFromFile("input2.txt");
   ```

5. **Checking Lists:**
   - Ensure both lists are not null before proceeding.
   ```java
   if (list1 != null && list2 != null) {
   ```

6. **Merging Lists:**
   - Create a new list `mergedList` and add all elements from both lists.
   ```java
   List<Integer> mergedList = new ArrayList<>(list1);
   mergedList.addAll(list2);
   ```

7. **Writing Merged List to File:**
   - Call `writeIntegersToFile` to write the merged list to `merged.txt`.
   ```java
   writeIntegersToFile(mergedList, "merged.txt");
   ```

8. **Identifying Common Integers:**
   - Create a `HashSet` for common elements and retain only those present in both lists.
   ```java
   Set<Integer> commonSet = new HashSet<>(list1);
   commonSet.retainAll(list2);
   ```

9. **Convert Set to List:**
   - Convert the `HashSet` to a `List`.
   ```java
   List<Integer> commonList = new ArrayList<>(commonSet);
   ```

10. **Writing Common Integers to File:**
    - Call `writeIntegersToFile` to write the common list to `common.txt`.
    ```java
    writeIntegersToFile(commonList, "common.txt");
    ```

11. **Method to Read Integers from File:**
    - Read integers from a file, handling exceptions for file not found, I/O errors, and invalid number formats.
    ```java
    private static List<Integer> readIntegersFromFile(String fileName) {
        List<Integer> integers = new ArrayList<>();
        try (BufferedReader br = new BufferedReader(new FileReader(fileName))) {
            String line;
            while ((line = br.readLine()) != null) {
                try {
                    integers.add(Integer.parseInt(line.trim()));
                } catch (NumberFormatException e) {
                    System.err.println("Invalid number format in file " + fileName + ": " + line);
                }
            }
        } catch (FileNotFoundException e) {
            System.err.println("File not found: " + fileName);
        } catch (IOException e) {
            System.err.println("IOException while reading file " + fileName);
        }
        return integers;
    }
    ```

12. **Method to Write Integers to File:**
    - Write a list of integers to a file, handling I/O exceptions.
    ```java
    private static void writeIntegersToFile(List<Integer> integers, String fileName) {
        try (BufferedWriter bw = new BufferedWriter(new FileWriter(fileName))) {
            for (int number : integers) {
                bw.write(String.valueOf(number));
                bw.newLine();
            }
        } catch (IOException e) {
            System.err.println("IOException while writing to file " + fileName);
        }
    }
    ```

By breaking down the program into these key concepts and steps, you can build a solid understanding of how to handle file I/O, use lists and sets, handle exceptions, and organize your code into modular, reusable methods.
