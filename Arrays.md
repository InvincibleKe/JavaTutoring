# Tutorial 1 - Arrays

## Array Declaration
Arrays are a fairly useful data structure present in (pretty much) all
programming languages, which allow us to store a list of items of the same type.

We can, for instance, declare an array:

```Java
int[] statArr = {1, 2, 3, 4};
```

Which contains the integer values `1, 2, 3` and `4`. This method of creating
arrays is usually used when we know what we want to store in the array before
the program is run. If we don't know the values until run-time (e.g. if user
entered values are placed in an array), then we have an alternative way of
declaring an array which will hold values defined at a later point. We do this
in the following way:

```Java
int[] lateArr = new int[4];
```

Which declares an array of length 4 (it can hold 4 values). However, the array
doesn't hold any values, so we need to look at array access.

## Array Access

We can access these values contained in the array by using the appropriate
index values. In the case of `statArr`:

|Index|Value|
|-----|-----|
|0    |`1`    |
|1    |`2`    |
|2    |`3`    |
|3    |`4`    |

Therefore we can type things like `statArr[1]` which gives us the value `2`. To
assign values to an array index (which we have to do in the case of `lateArr`)
we can type `lateArr[0] = 5;` which assigns the integer value `5` to the zeroth
element of `lateArr`.
> By default if we declare an array, but don't provide values (with lateArr for
instance) all elements of the array are set to 0 (which is guaranteed by the
Java language).

## Some useful things arrays give us

By default arrays give us access to their length. If we have the array
`char[] greeting = {'h', 'e', 'l', 'l', 'o'};` then we can use `greeting.length`
which gives us the length of the array (5 in this case). This allows us to
easily get the last element of the array:

```Java
char[] greeting = {'h', 'e', 'l', 'l', 'o'};
char last = greeting[greeting.length-1];
```
So `last` will hold the value `'o'` since we access index 4.

## Array Iteration

We often find it useful to iterate through arrays for various reasons, whether
we want to calculate, search, or alter the elements stored in an array.

Array iteration should become second nature and is done in a standard way:

```Java
double[] a = {50.0, 60.0, 10.0, 20.0};

for(int i = 0; i < a.length; i++) {
    System.out.println(a[i]);
}
```
The above for loop just prints each value of the array `a`, but within the for
loop we can do any kind of processing we want on the elements of the array. For
instance we can square all the values of an array:

```Java
double[] a = {1, 2, 3, 4};

for(int i = 0; i < a.length; i++) {
    a[i] *= a[i]; // which is equivalent to a[i] = a[i] * a[i];
}
```

## 2D Array Iteration
To make arrays more useful, we can increase the number of dimensions we can
operate over!

We can define multi-dimensional arrays in the following way:
```Java
int[][] arr2d = {{1,2}, {3}, {4,5,6,7}};
```

Iterating through this is slightly more involved than the 1D alternative:

```Java
int[][] arr2d = {{1,2}, {3}, {4,5,6,7}};

// Use a for loop to loop through the array as normal
for(int i = 0; i < arr2d.length; i++) {
    // Use an inner for loop to loop over the inner dimension
    for(int j = 0; j < arr2d[i].length; j++) {
        // Print the individual elements of the array
        System.out.println(arr2d[i][j]);
    }
}
```

As the above example indicates, if we have a 2D array and we want to access each
element of the array, we need to have a **nested for loop** which operates over
each dimension in turn.

If we have a square array:

```Java
int[][] squareArray = {{1,2,3}, {4,5,6}, {7,8,9}};
```

Where which we can imagine as:

|`1` |`2` |`3` |
|-----|-----|---|
|`4`    |`5`    |`6` |
|`7`    |`8`    |`9` |

So we can iterate through this array using two for loops:

```Java
int[][] squareArray = {{1,2,3}, {4,5,6}, {7,8,9}};

// Use a for loop to loop through the array
for(int i = 0; i < squareArray.length; i++) {
    // loop over the inner dimension
    for(int j = 0; j < squareArray[i].length; j++) {
        System.out.println(squareArray[i][j]);
    }
}
```

The slowest incrementing index is `i` which corresponds to the row of the array,
therefore we access the array going from top left, across the array (left to
right), then drop down a row to the next one.
This would print the numbers in order `1,2,3,4,5,6,7,8,9`.

If instead we made the subtle change of `System.out.println(squareArray[j][i])`
(swapping the `i` and `j` indices) we instead are accessing the array column
first which prints the values in the order: `1,4,7,2,5,8,3,6,9`. As we go down
the column first then across to the next column etc.

> Note that the above example will not work if the array isn't square!
