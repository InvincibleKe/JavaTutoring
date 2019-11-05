# Tutorial 2 - ArrayLists

Arrays are an important, core data structure in computer science, but they
aren't very useful in practice, mainly because we need to know their size when
we declare them meaning we can't easily increase their size later on if we need
more space, or even decrease their size if we have too few elements.
**ArrayLists** attempt to fix this issue!

## Declaring an ArrayList

We can declare array lists in the following way:
```Java
ArrayList<Integer> a = new ArrayList<>();
```

Note that with array lists when we define the type, we first use the angle
brackets `< ... >` (which are used for Java Generics, a later topic), with the
*class* of the type we want. So we cannot use `<int>` or `<double>`, instead we
use `<Integer>` and `<Double>`.

Adding items to an array list can be done using `.add(item)`. For instance:

```Java
ArrayList<Integer> a = new ArrayList<>();

a.add(1);
a.add(2);
...
```

Which adds the values to the array in the order they appear (so index 0 will
contain the value `1`, index 1 will have value `2` etc).

To remove elements from the array list we use `.remove(index)`:

```Java
ArrayList<Integer> a = new ArrayList<>();

a.add(1);
a.add(2);

a.remove(0); // Removes the item at index 0 from the Array List
```

When removing an item, the array list dynamically alters itself. This means that
in the above example, when we remove the element at index 0 (which is `1`), the
new element at index 0 becomes `2` (it automatically updates itself).

We can retrieve the element from a given index using `.get(index)`:
```Java
ArrayList<Integer> a = new ArrayList<>();

a.add(1);
a.add(2);

a.remove(0);
System.out.println(a.get(0));
```

Which will print `2` to the console.

We can get the length of an array list by using `.size()`:

```Java
ArrayList<Integer> a = new ArrayList<>();

a.add(1);
a.add(2);
a.size(); // Returns the value 2

a.remove(0);
a.size(); // Returns the value 1
```

Unfortunately we need to use `.size()` rather than `.length()` which would keep
things consistent with the standard array implementation, but the designers of
java like to add some confusion!

Additionally we can set an item in the array to a new value using
`.set(index, value)`.

```Java
ArrayList<Integer> a = new ArrayList<>();

a.add(1);
a.add(2);

a.set(0, 3); // Index 0 changed from 1 to 3
a.set(1, 4); // Index 1 changed from 2 to 4
```

We can also extend `add` with `.add(index, value)` which adds an item at the
specified index and pushes the item at the current index down by one along with
all other elements after it.

```Java
ArrayList<Integer> a = new ArrayList<>();

a.add(1);
a.add(2);

a.add(0, 3); // So 3 is now at index 0, pushing 1 to index 1 and 2  to index 2
```

> Many more useful methods can be found by checking out the ArrayList
documentation!

## Iterating over ArrayList

Iterating over an array list is fairly similar to iterating over a basic array,
but we just use some slightly different language.

We again defer to our friend the for loop for the iteration. The difference is
that instead of checking if we've hit the length of the array, we check the size
(thanks java) and then use the methods provided to us by the `ArrayList` class
to operate on the elements.

``` Java
ArrayList<Integer> a = new ArrayList<>();
a.add(8);
a.add(2);
a.add(0);
a.add(8);

for(int i = 0; i < a.size(); i++) {
    System.out.println(a.get(i));
    // Or any other processing!
}
```

If we want to operate on the array list changing the structure (i.e. remove or
add elements) it often isn't a good idea to do this on the list directly. As a
general rule of thumb, never change the structure of a list you're iterating
over. This can lead to a whole bunch of nasty index errors etc.
Instead we can create a new list and just add to that one!

If for instance we want to take an array list and repeat an element a number of
times specified by it's value (e.g. we have an 8, so we want an array with 8,
8 times) we can use the following code:

```Java
public static ArrayList<Integer> repeatElement(ArrayList<Integer> arr) {
    ArrayList<Integer> newList = new ArrayList<Integer>();
    for(int i = 0; i < arr.size(); i++) {
        for(int r = 0; r < arr.get(i); r++) {
            newList.add(arr.get(i));
        }
    }
}
```

If we apply this method to the array list `[8, 2, 0, 8]` we get the output:
`[8, 8, 8, 8, 8, 8, 8, 8, 2, 2, 8, 8, 8, 8, 8, 8, 8, 8]`. If we didn't use the
new array list, our program would not terminate since we'd see the first `8`
value so add 8 `8`s to the same array list, move to the next element, which is
now an `8`, so add 8 more `8`s etc. which would **never end**!
