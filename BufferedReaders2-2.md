# Tutorial 2 - Buffered Readers

We often find file access useful in Java. If we need to save any data, load data
or generally output results in a more permanent format for users, we need to
do some kind of file access. For this week we just look at **reading in** data
rather than writing it out.

## Getting data from a file
We can read data from an external file using buffered readers. The mechanics of
this are fairly convoluted and isn't something we as programmers need to
remember off-by-heart. Basically whenever it's time to do file access, use
Google to find the basic framework.

The basic file access code is as follows:

```Java
try {
    BufferedReader in = new BufferedReader(new FileReader("path to file"));
    // Some processing
    in.close();
} catch (IOException e) {
    // Return some failure condition
}
```

The `BufferedReader` gives us access to the contents of the file which is in a
buffer (which means that as we read it, the data we read disappears so we
can make sure we don't read it twice). The `FileReader` gives us access to files
that are external to the program (for instance a text file), then `in.close()`
tells the operating system we're done with file access, so cut the link between
the program and the external file. The `IOException` catch statement is
triggered if we cannot locate the specified file, or cannot open it (if we don't
have permission for instance). This should handle the exception gracefully,
and allow us to return an error to the user ("file does not exist/ cannot be
accessed"). The `'path to the file'` will be the location of the file with
respect to the location of the executing java code.

## Operating on file data
So we can open a file now! To process the file we can write code between
`BufferedReader ...` and `in.close()`. We have many options when handling the
file data, but we will focus on two specific methods:
- Processing data character by character
- Processing data line by line

#### Character by Character
This method processes the data from the file character by character. This is
especially useful if we need to have fine grain control over the contents of a
file (for instance if we wanted to make a program that turns all lower case
letters to upper case). The code for this is below:

```Java
int readChar;

try {
    BufferedReader in = new BufferedReader(new FileReader("path to file"));
    while((readChar = in.read()) != -1) {
        // We now have the character (as it's ascii value of int)
        // in the variable readChar which we can process!
    }
    in.close();
} catch (IOException e) {
    // Return some failure condition
}
```

The important new line in the code above is:
`while((readChar = in.read()) != -1)` which we'll break down now.
First off we have an assignment within the while condition
`(readChar = in.read())` which basically assigns the value of in.read() (the
character we read in) to the variable readChar (an integer type). This will be
the ascii value of the character read from file, which is just the integer
representation of the character. Next we check to see if the value we just read
and assigned to `readChar` is equal to `-1`. `-1` here indicates an end-of-file
(EOF) and tells us that we have read all of the file data and there is nothing
of interest left! If we have read an EOF, we stop the while loop, closing the
file.

Within the while loop we can process the character we're currently holding in
the variable `readChar`. So to print the contents of the file we can do:

```Java
int readChar;

try {
    BufferedReader in = new BufferedReader(new FileReader("path to file"));
    while((readChar = in.read()) != -1) {
        System.out.println((char)readChar);
    }
    in.close();
} catch (IOException e) {
    // Return some failure condition
}
```

Within the print statement we use `(char)readChar` since `readChar` is of type
`int`. This is called a **cast** from `int` to `char` which essentially forces
the value of `readChar` to be of type `char` in this situation, which converts
the integer to it's corresponding character value defined by the ascii
convention.

#### Line by Line
We may sometimes find it more useful to process a file line-by-line. This can be
achieved by making some slight alterations to the code we've seen previously:

```Java
String readString;

try {
    BufferedReader in = new BufferedReader(new FileReader("path to file"));
    while((readString = in.readLine()) != null) {
        // We now have the String in the variable
        // readString which we can process!
    }
    in.close();
} catch (IOException e) {
    // Return some failure condition
}
```

Where again, we take a line from the input data (`in.readLine()`) assign the
result to the variable `readString` while we don't get a `null` value, which is
EOF in the case of `readLine()`.

This comes in handy if we have a file full of data such as a csv (**C**omma
**S**eparated **V**alues) file. This kind of file (as the name suggests)
contains data separated by commas. With this knowledge we can get the values
stored in each row quite easily:

```Java
String readString;
String[] values;

try {
    BufferedReader in = new BufferedReader(new FileReader("path to file"));
    while((readString = in.readLine()) != null) {
        values = readString.split(",");
        // Process individual values
    }
    in.close();
} catch (IOException e) {
    // Return some failure condition
}
```

In this code we split the string we read in on the comma character:
`values = readString.split(',')` assigning the result to the string array
`values`. This means that if we have read in the line `"Hello",1,500` then the
`values` array will contain the elements `["Hello", "1", "500"]`
(all as strings) since we split on the comma (`,`).

> Other methods of processing a buffer exist, so check out the Java
documentation to explore this further!
