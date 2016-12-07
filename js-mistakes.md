1. 실수로 할당 연산자를 사용 
======================

JavaScript는 다른 언어와 다르게 strict하지 않기 때문에 예기치 못한 결과를 초래할 수 있다. **if** 문에 실수로 비교연산자(==)가 아닌 할당연산자(=)를 사용하는 오류를 범할 수 있다.
    
    var x = 0;
    if (x == 10) {
    }

이 if문은 false로 평가된다.

    var x = 0;
    if (x = 10) {
    }

이 **if**문에서는 x에 10이 할당되는데 10은 **true**로 평가가 되기 때문에 if문은 true로 평가된다.

    var x = 0;
    if (x = 0) {
    }

이 **if**문에서는 0을 할당하게 되는데 이떄 0은 **false**로 평가되기 때문에 이 if문은 타지 않는다.

2. Expecting Loose Comparison
=============================
In regular comparison, data type does not matter. This if statement returns true:

    var x = 10;
    var y = "10";
    if (x == y)

In strict comparison, data type does matter. This if statement returns false:

    var x = 10;
    var y = "10";
    if (x === y)

It is a common mistake to forget that switch statements use strict comparison.
This case switch will display an alert:

    var x = 10;
    switch(x) {
        case 10: alert("Hello");
    }

This case switch will not display an alert:

    var x = 10;
    switch(x) {
        case "10": alert("Hello");
    }

3. Confusing Addition & Concatenation
=====================================
**Addition** is about adding **numbers**.
**Concatenation** is about adding **strings**.
In JavaScript both operations use the same + operator.
Because of this, adding a number as a number will produce a different result from adding a number as a string:

    var x = 10 + 5;          // the result in x is 15
    var x = 10 + "5";        // the result in x is "105"

When adding two variables, it can be difficult to anticipate the result:

    var x = 10;
    var y = 5;
    var z = x + y;           // the result in z is 15
    
    var x = 10;
    var y = "5";
    var z = x + y;           // the result in z is "105"

4. Misunderstanding Floats
==========================
All numbers in JavaScript are stored as 64-bits **Floating point numbers** (Floats).
All programming languages, including JavaScript, have difficulties with precise floating point values:

    var x = 0.1;
    var y = 0.2;
    var z = x + y            // the result in z will not be 0.3
    
To solve the problem above, it helps to multiply and divide:

    var z = (x * 10 + y * 10) / 10;       // z will be 0.3
    
5. Breaking a JavaScript String
===============================
JavaScript will allow you to break a statement into two lines:

    var x =
    "Hello World!";

But, breaking a statement in the middle of a string will not work:

    var x = "Hello
    World!";

You must use a "backslash" if you must break a statement in a string:     

    var x = "Hello \
    World!";

6. Misplacing Semicolon
=======================
Because of a misplaced semicolon, this code block will execute regardless of the value of x:

    if (x == 19);
    {
        // code block  
    }
    
7. Breaking a Return Statement
==============================
It is a default JavaScript behavior to close a statement automatically at the end of a line.
Because of this, these two examples will return the same result:

    function myFunction(a) {
        var power = 10  
        return a * power
    }
    
    function myFunction(a) {
        var power = 10;
        return a * power;
    }   

JavaScript will also allow you to break a statement into two lines.
Because of this, example 3 will also return the same result:

    function myFunction(a) {
        var
        power = 10;  
        return a * power;
    }

But, what will happen if you break the return statement in two lines like this:

    function myFunction(a) {
        var
        power = 10;  
        return
        a * power;
    }

The function will return undefined!
Why? Because JavaScript thinks you meant:
    
    function myFunction(a) {
        var
        power = 10;  
        return;
        a * power;
    }
    
Explanation :
If a statement is incomplete like:

    var

JavaScript will try to complete the statement by reading the next line:

    power = 10;

But since this statement is complete:

    return
    
JavaScript will automatically close it like this:

    return;
    
This happens because closing (ending) statements with semicolon is optional in JavaScript.
JavaScript will close the return statement at the end of the line, because it is a complete statement.
=> Never break a return statement.

8. Accessing Arrays with Named Indexes
======================================
Many programming languages support arrays with named indexes.
Arrays with named indexes are called associative arrays (or hashes).
JavaScript does not support arrays with named indexes.
In JavaScript, arrays use numbered indexes:

    var person = [];
    person[0] = "John";
    person[1] = "Doe";
    person[2] = 46;
    var x = person.length;         // person.length will return 3
    var y = person[0];             // person[0] will return "John"

In JavaScript, objects use named indexes.
If you use a named index, when accessing an array, JavaScript will redefine the array to a standard object.
After the automatic redefinition, array methods and properties will produce undefined or incorrect results:

    var person = [];
    person["firstName"] = "John";
    person["lastName"] = "Doe";
    person["age"] = 46;
    var x = person.length;         // person.length will return 0
    var y = person[0];             // person[0] will return undefined
    
9. Ending an Array Definition with a Comma
==========================================
    
Incorrect:

    points = [40, 100, 1, 5, 25, 10,];

Some JSON and JavaScript engines will fail, or behave unexpectedly.
Correct:

    points = [40, 100, 1, 5, 25, 10];
    
10. Ending an Object Definition with a Comma
============================================

Incorrect:

    person = {firstName:"John", lastName:"Doe", age:46,}

Some JSON and JavaScript engines will fail, or behave unexpectedly.    
Correct:

    person = {firstName:"John", lastName:"Doe", age:46}
    
11. Undefined is Not Null
=========================
With JavaScript, **null** is for objects, **undefined** is for variables, properties, and methods.
To be null, an object has to be defined, otherwise it will be undefined.
If you want to test if an object exists, this will throw an error if the object is undefined:

Incorrect:

    if (myObj !== null && typeof myObj !== "undefined") 

Because of this, you must test typeof() first:    
Correct:

    if (typeof myObj !== "undefined" && myObj !== null) 
    
12. Expecting Block Level Scope
===============================
JavaScript **does not** create a new scope for each code block.
It is true in many programming languages, but **not true** in JavaScript.
It is a common mistake, among new JavaScript developers, to believe that this code returns undefined:

    for (var i = 0; i < 10; i++) {
        // some code
    }
    return i;
