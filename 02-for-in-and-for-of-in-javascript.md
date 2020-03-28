## For...in and For...of in Javascript

In Javascript, there are various loops which we can use to iterate over iterable objects (like. Arrays, Objects etc...)

- for
- for each...in
- for...in
- for...of
- for await...of
- while
- do while

We will be discussing for...in and for...of in this blog.

### for...in

The for...in loop is used to iterate over enumerable properties, including inherited enumerable properties.

This for...in loop can be used to iterate over Arrays, Strings, Objects but not Map or Set.

Let's understand this with a help of example.

#### for...in over Array

Here the iteration variable (i) is array index.

    let arr = ['Joey', 'Chandler', 'Ross'];
    for (let i in arr) {
        console.log(i);
    }

    // Output: 0, 1, 2

#### for...in over String

Here the iteration variable (i) is string index.

    let str = 'FRIENDS'
    for (let i in str) {
        console.log(i)
    }

    // Output: 0, 1, 2, 3, 4, 5, 6

#### for...in over Object

Here the iteration variable (i) is property of the object.

    let obj = {
        "name": "F.R.I.E.N.D.S.",
        "category": "American Sitcom",
        "totalEpisodes": 236
    }

    for (let i in obj) {
        console.log(i)
    }

    // Output: name, category, totalEpisodes

### for...of

The for...of loop is used to iterate over iterable objects like Arrays, Strings, Map, Sets and array like objects. This loop cannot be used over plain objects. It gives values instead of properties.

#### for...of over Array

Here the iteration variable (i) is items of array.

    let arr = ['Joey', 'Chandler', 'Ross']
    for (let i of arr) {
        console.log(i)
    }

    // Output: 'Joey', 'Chandler', 'Ross'

#### for...of over String

Here the iteration variable (i) is character of a string.

    let str = 'FRIENDS'
    for (let i of str) {
        console.log(i)
    }

    // Output: 'F', 'R', 'I', 'E', 'N', 'D', 'S'

#### for...of over Object

It cannot be used to iterate over plain objects.

    let obj = {
        "name": "F.R.I.E.N.D.S.",
        "category": "American Sitcom",
        "totalEpisodes": 236
    }

    for (let i of obj) {
        console.log(i)
    }

    // Output: Type Error: obj is not iterable

These were the for...in and for...of loops in Javascript.
