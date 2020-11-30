## Discovering unexpected parts in Javascript

You probably already know javascript is a tricky language and it has some weird parts. We will talk about some unexpected things in javascript in this blog.

#### - Weird Comparison

```javascript
    console.log(1<2<3)  // true
    console.log(3>2>1)  // false
```

> **Explanation:**
> Let's see this step by step.
>
> _First comparison 1<2<3_
> 1<2 is true, true is 1
> 1<3 is true
> Hence, final output is true
>
> _Second Comparison 3>2>1_  
> 3>2 is true, true is 1
> 1>1 is false
> Hence, final output is false

If we edit the second comparison to

    console.log(3>2>=1) // true

It will return true.

#### - Octal Literals

    console.log(031) // 25

> **Explanation:**
> When a number has zero at start it is considered as Octal Number in javascript.
>
> Also, if the digits after zero is outside range (0,7) it will be considered as decimal number.

For example, 39 is not a valid octal number, hence if we add a zero as prefix to 39 it would be treated as a decimal number.

    console.log(039) // 39

For more details, checkout [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Numbers_and_dates)

#### - Accidental Global Variable

    function fun() {
        let x=y=10
    }

    fun()

    console.log(x) // x is not defined
    console.log(y) // 10

> **Explanation**
> In the above example, x is a local variable because it is declared in function scope.
> Whereas, y is neither declared in function scope nor in global scope. So, javascript interpreter takes it as
> window.y = 10
>
> Hence, y is available globally now.
> Here, we can say that y is an accidental global variable.

#### - Array is equal to not Array

    console.log([]==![]) // true

> **Explanation**
> The '==' operator converts both sides into numbers and then compares them. In this case,
>
> On left we have, an empty array which is equal to 0.
> On right we have, ![] i.e. Number( ! Boolean( [] ) ) which is 0.
> Hence, it returns true

#### - Adding arrays returns string

    console.log([1,2,3]+[4,5,6]) // '1,2,34,5,6'

> **Explanation**
> The javascript interpreter interprets as
>
> [1,2,3].toString() + [4,5,6].toString()
>
> Hence, it returns _'1,2,34,5,6'_

These were some unexpected things in js, which makes complete sense once you understand them.

Hope you learned something new today :)
