1. 실수로 할당 연산자를 사용 
======================

#### JavaScript는 다른 언어와 다르게 strict하지 않기 때문에 예기치 못한 결과를 초래할 수 있다. if 문에 실수로 비교연산자(==)가 아닌 할당연산자(=)를 사용하는 오류를 범할 수 있다.
    
    var x = 0;
    if (x == 10) {
    }

#### 이 if문은 false로 평가된다.

    var x = 0;
    if (x = 10) {
    }

#### 이 if문에서는 x에 10이 할당되는데 10은 true로 평가가 되기 때문에 if문은 true로 평가된다.

    var x = 0;
    if (x = 0) {
    }

#### 이 if문에서는 0을 할당하게 되는데 이떄 0은 false로 평가되기 때문에 이 if문은 타지 않는다.

2. Expecting Loose Comparison
=============================
#### In regular comparison, data type does not matter. This if statement returns true:
    var x = 10;
    var y = "10";
    if (x == y)
#### In strict comparison, data type does matter. This if statement returns false:
    var x = 10;
    var y = "10";
    if (x === y)
#### It is a common mistake to forget that switch statements use strict comparison.
#### This case switch will display an alert:
    var x = 10;
    switch(x) {
        case 10: alert("Hello");
    }
#### This case switch will not display an alert:
    var x = 10;
    switch(x) {
        case "10": alert("Hello");
    }

3. Confusing Addition & Concatenation
=====================================
#### Addition is about adding numbers.
#### Concatenation is about adding strings.
#### In JavaScript both operations use the same + operator.
#### Because of this, adding a number as a number will produce a different result from adding a number as a string:
    var x = 10 + 5;          // the result in x is 15
    var x = 10 + "5";        // the result in x is "105"
#### When adding two variables, it can be difficult to anticipate the result:
    var x = 10;
    var y = 5;
    var z = x + y;           // the result in z is 15
    
    var x = 10;
    var y = "5";
    var z = x + y;           // the result in z is "105"

4. Misunderstanding Floats
==========================
#### All numbers in JavaScript are stored as 64-bits Floating point numbers (Floats).
#### All programming languages, including JavaScript, have difficulties with precise floating point values:
    var x = 0.1;
    var y = 0.2;
    var z = x + y            // the result in z will not be 0.3
#### To solve the problem above, it helps to multiply and divide:
    var z = (x * 10 + y * 10) / 10;       // z will be 0.3
    
5. Breaking a JavaScript String
===============================
#### JavaScript will allow you to break a statement into two lines:
    var x =
    "Hello World!";
#### But, breaking a statement in the middle of a string will not work:
    var x = "Hello
    World!";
#### You must use a "backslash" if you must break a statement in a string:     
    var x = "Hello \
    World!";
    
