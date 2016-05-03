
## 学习Swift基础

你的第一课由Swift _playground_ 文件的形式展示，它是一种文件类型，可以让你改变并直接在Xcode代码交互，并立即看到结果。 _playground_ 对学习和实验非常有用，能加快你理解基本Swift概念。

>注意

>为了获得最佳体验，打开这课的 _playground_ 文件。

>[Download Playground](https://developer.apple.com/sample-code/swift/downloads/Start-Dev-iOS-Apps-01.zip)

### 学习目标

在课程结束时，你就可以:

*   区分常量和变量

*   知道何时使用隐式以及何时使用显式类型声明

*   了解使用可选和可选绑定的优势

*   区分可选和隐式解析可选

*   了解条件语句和循环的用途

*   使用条件分支语句`switch`

*   使用`where`子句中的条件语句来施加额外的约束

*   区分函数，方法和构造器

*   区分类，结构体和枚举

*   理解语法（背后的基本概念）继承和协议一致性

*   确定隐式类型和使用Xcode的快速帮助快捷方式（Option键）找到更多的信息

*   导入和使用 UIKit

### 基本类型

A _constant_ is a value that stays the same after it’s declared the first time, while a _variable_ is a value that can change. A constant is referred to as immutable, meaning that it can’t be changed, and a variable is mutable. If you know that a value won’t need to be changed in your code, declare it as a constant instead of a variable.

Use `let` to make a constant and `var` to make a variable.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">var</span> <span class="vc">myVariable</span> = <span class="m">42</span>`
2.  `<span class="vc">myVariable</span> = <span class="m">50</span>`
3.  `<span class="kt">let</span> <span class="vc">myConstant</span> = <span class="m">42</span>`

</div>

</div>

</section>

Every constant and variable in Swift has a type, but you don’t always have to write the type explicitly. Providing a value when you create a constant or variable lets the compiler infer its type. In the example above, the compiler infers that `myVariable` is an integer because its initial value is an integer. This is called _type inference_. Once a constant or variable has a type, that type can’t be changed.

If the initial value doesn’t provide enough information (or if there is no initial value), specify the type by writing it after the variable, separated by a colon.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">let</span> <span class="vc">implicitInteger</span> = <span class="m">70</span>`
2.  `<span class="kt">let</span> <span class="vc">implicitDouble</span> = <span class="m">70.0</span>`
3.  `<span class="kt">let</span> <span class="vc">explicitDouble</span>: <span class="n">Double</span> = <span class="m">70</span>`

</div>

</div>

</section>

<div class="note experiment"><a name="//apple_ref/doc/uid/TP40015214-CH3-SW12"></a>

<aside class="aside">

Experiment

In Xcode, Option-click the name of a constant or variable to see its inferred type. Try doing that with the constants in the code above.

</aside>

</div>

Values are never implicitly converted to another type. If you need to convert a value to a different type, explicitly make an instance of the desired type. Here, you convert an `Int` to a `String`.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">let</span> <span class="vc">label</span> = <span class="s">"The width is "</span>`
2.  `<span class="kt">let</span> <span class="vc">width</span> = <span class="m">94</span>`
3.  `<span class="kt">let</span> <span class="vc">widthLabel</span> = <span class="vc">label</span> + <span class="vc">String</span>(<span class="vc">width</span>)`

</div>

</div>

</section>

<div class="note experiment"><a name="//apple_ref/doc/uid/TP40015214-CH3-SW13"></a>

<aside class="aside">

Experiment

Try removing the conversion to `String` from the last line. What error do you get?

</aside>

</div>

There’s an even simpler way to include values in strings: Write the value in parentheses, and write a backslash (`\`) before the parentheses. This is known as _string interpolation_.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">let</span> <span class="vc">apples</span> = <span class="m">3</span>`
2.  `<span class="kt">let</span> <span class="vc">oranges</span> = <span class="m">5</span>`
3.  `<span class="kt">let</span> <span class="vc">appleSummary</span> = <span class="s">"I have</span> \(<span class="vc">apples</span>) <span class="s">apples."</span>`
4.  `<span class="kt">let</span> <span class="vc">fruitSummary</span> = <span class="s">"I have</span> \(<span class="vc">apples</span> + <span class="vc">oranges</span>) <span class="s">pieces of fruit."</span>`

</div>

</div>

</section>

Use <span class="x-name">[optionals](GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW11)</span> to work with values that might be missing. An optional value either contains a value or contains `nil` (no value) to indicate that a value is missing. Write a question mark (`?`) after the type of a value to mark the value as optional.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">let</span> <span class="vc">optionalInt</span>: <span class="n">Int</span>? = <span class="m">9</span>`

</div>

</div>

</section>

To get the underlying value from an optional, you _unwrap_ it. You’ll learn unwrapping optionals later, but the most straightforward way to do it involves the _force unwrap operator_ (`!`). Only use the unwrap operator if you’re sure the underlying value isn’t `nil`.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">let</span> <span class="vc">actualInt</span>: <span class="n">Int</span> = <span class="vc">optionalInt</span>!`

</div>

</div>

</section>

Optionals are pervasive in Swift, and are very useful for many situations where a value may or may not be present. They’re especially useful for attempted type conversions.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">var</span> <span class="vc">myString</span> = <span class="s">"7"</span>`
2.  `<span class="kt">var</span> <span class="vc">possibleInt</span> = <span class="vc">Int</span>(<span class="vc">myString</span>)`
3.  `<span class="vc">print</span>(<span class="vc">possibleInt</span>)`

</div>

</div>

</section>

In this code, the value of `possibleInt` is `7`, because `myString` contains the value of an integer. But if you change `myString` to be something that can’t be converted to an integer, `possibleInt` becomes `nil`.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="vc">myString</span> = <span class="s">"banana"</span>`
2.  `<span class="vc">possibleInt</span> = <span class="vc">Int</span>(<span class="vc">myString</span>)`
3.  `<span class="vc">print</span>(<span class="vc">possibleInt</span>)`

</div>

</div>

</section>

An <span class="x-name">[array](GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW28)</span> is a data type that keeps track of an ordered collection of items. Create arrays using brackets (`[]`), and access their elements by writing the index in brackets. Arrays start at index `0`.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">var</span> <span class="vc">ratingList</span> = [<span class="s">"Poor"</span>, <span class="s">"Fine"</span>, <span class="s">"Good"</span>, <span class="s">"Excellent"</span>]`
2.  `<span class="vc">ratingList</span>[<span class="m">1</span>] = <span class="s">"OK"</span>`
3.  `<span class="vc">ratingList</span>`

</div>

</div>

</section>

To create an empty array, use the initializer syntax. You’ll learn more about initializers in a little while.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="c">// Creates an empty array.</span>`
2.  `<span class="kt">let</span> <span class="vc">emptyArray</span> = [<span class="vc">String</span>]()`

</div>

</div>

</section>

You’ll notice that the code above has a comment. A _comment_ is a piece of text in a source code file that doesn’t get compiled as part of the program but provides context or useful information about individual pieces of code. A single-line comment appears after two slashes (`//`) and a multiline comment appears between a set of slashes and asterisks (`/*` … `*/`). You’ll see and write both types of comments throughout the source code in the lessons.

An _implicitly unwrapped optional_ is an optional that can also be used like a nonoptional value, without the need to unwrap the optional value each time it’s accessed. This is because an implicitly unwrapped optional is assumed to always have a value after that value is initially set, although the value can change. Implicitly unwrapped optional types are indicated with an exclamation mark (`!`) instead of a question mark (`?`).

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">var</span> <span class="vc">implicitlyUnwrappedOptionalInt</span>: <span class="n">Int</span>!`

</div>

</div>

</section>

You’ll rarely need to create implicitly unwrapped optionals in your own code. More often, you’ll see them used to keep track of outlets between an interface and source code (which you’ll learn about in a later lesson) and in the _APIs_ you’ll see throughout the lessons.

</section>

<section class="section"><a name="//apple_ref/doc/uid/TP40015214-CH3-SW4"></a>

### Control Flow

Swift has two types of control flow statements. _Conditional statements_, like `if` and `switch`, check whether a condition is true—that is, if its value evaluates to the Boolean `true`—before executing a piece of code. _Loops_, like `for`-`in` and `while`, execute the same piece of code multiple times.

An `if` statement checks whether a certain condition is true, and if it is, the `if` statement evaluates the code inside the statement. You can add an `else` clause to an `if` statement to define more complex behavior. An `else` clause can be used to chain `if` statements together, or it can stand on its own, in which case the `else` clause is executed if none of the chained `if` statements evaluate to `true`.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">let</span> <span class="vc">number</span> = <span class="m">23</span>`
2.  `<span class="kt">if</span> <span class="vc">number</span> < <span class="m">10</span> {`
3.  `<span class="vc">print</span>(<span class="s">"The number is small"</span>)`
4.  `} <span class="kt">else</span> <span class="kt">if</span> <span class="vc">number</span> > <span class="m">100</span> {`
5.  `<span class="vc">print</span>(<span class="s">"The number is pretty big"</span>)`
6.  `} <span class="kt">else</span> {`
7.  `<span class="vc">print</span>(<span class="s">"The number is between 10 and 100"</span>)`
8.  `}`

</div>

</div>

</section>

<div class="note experiment"><a name="//apple_ref/doc/uid/TP40015214-CH3-SW14"></a>

<aside class="aside">

Experiment

Change `number` to a different integer value to see how that affects which line prints.

</aside>

</div>

Statements can be nested to create complex, interesting behavior in a program. Here’s an example of an `if` statement with an `else` clause nested inside a `for`-`in` statement (which iterates through each item in a collection in order, one-by-one).

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">let</span> <span class="vc">individualScores</span> = [<span class="m">75</span>, <span class="m">43</span>, <span class="m">103</span>, <span class="m">87</span>, <span class="m">12</span>]`
2.  `<span class="kt">var</span> <span class="vc">teamScore</span> = <span class="m">0</span>`
3.  `<span class="kt">for</span> <span class="vc">score</span> <span class="kt">in</span> <span class="vc">individualScores</span> {`
4.  `<span class="kt">if</span> <span class="vc">score</span> > <span class="m">50</span> {`
5.  `<span class="vc">teamScore</span> += <span class="m">3</span>`
6.  `} <span class="kt">else</span> {`
7.  `<span class="vc">teamScore</span> += <span class="m">1</span>`
8.  `}`
9.  `}`
10.  `<span class="vc">print</span>(<span class="vc">teamScore</span>)`

</div>

</div>

</section>

Use _optional binding_ in an `if` statement to check whether an optional contains a value.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">var</span> <span class="vc">optionalName</span>: <span class="n">String</span>? = <span class="s">"John Appleseed"</span>`
2.  `<span class="kt">var</span> <span class="vc">greeting</span> = <span class="s">"Hello!"</span>`
3.  `<span class="kt">if</span> <span class="kt">let</span> <span class="vc">name</span> = <span class="vc">optionalName</span> {`
4.  `<span class="vc">greeting</span> = <span class="s">"Hello,</span> \(<span class="vc">name</span>)<span class="s">"</span>`
5.  `}`

</div>

</div>

</section>

<div class="note experiment"><a name="//apple_ref/doc/uid/TP40015214-CH3-SW15"></a>

<aside class="aside">

Experiment

Change `optionalName` to `nil`. What greeting do you get? Add an `else` clause that sets a different greeting if `optionalName` is `nil`.

</aside>

</div>

If the optional value is `nil`, the conditional is `false`, and the code in braces is skipped. Otherwise, the optional value is unwrapped and assigned to the constant after `let`, which makes the unwrapped value available inside the block of code.

You can use a single `if` statement to bind multiple values. A `where` clause can be added to a case to further scope the conditional statement. In this case, the `if` statement executes only if the binding is successful for all of these values and all conditions are met.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">var</span> <span class="vc">optionalHello</span>: <span class="n">String</span>? = <span class="s">"Hello"</span>`
2.  `<span class="kt">if</span> <span class="kt">let</span> <span class="vc">hello</span> = <span class="vc">optionalHello</span> <span class="kt">where</span> <span class="vc">hello</span>.<span class="vc">hasPrefix</span>(<span class="s">"H"</span>), <span class="kt">let</span> <span class="vc">name</span> = <span class="vc">optionalName</span> {`
3.  `<span class="vc">greeting</span> = <span class="s">"</span>\(<span class="vc">hello</span>)<span class="s">,</span> \(<span class="vc">name</span>)<span class="s">"</span>`
4.  `}`

</div>

</div>

</section>

Switches in Swift are quite powerful. A `switch` statement supports any kind of data and a wide variety of comparison operations—it isn’t limited to integers and tests for equality. In this example, the `switch` statement switches on the value of the `vegetable` string, comparing the value to each of its cases and executing the one that matches.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">let</span> <span class="vc">vegetable</span> = <span class="s">"red pepper"</span>`
2.  `<span class="kt">switch</span> <span class="vc">vegetable</span> {`
3.  `<span class="kt">case</span> <span class="s">"celery"</span>:`
4.  `<span class="kt">let</span> <span class="vc">vegetableComment</span> = <span class="s">"Add some raisins and make ants on a log."</span>`
5.  `<span class="kt">case</span> <span class="s">"cucumber"</span>, <span class="s">"watercress"</span>:`
6.  `<span class="kt">let</span> <span class="vc">vegetableComment</span> = <span class="s">"That would make a good tea sandwich."</span>`
7.  `<span class="kt">case</span> <span class="kt">let</span> <span class="vc">x</span> <span class="kt">where</span> <span class="vc">x</span>.<span class="vc">hasSuffix</span>(<span class="s">"pepper"</span>):`
8.  `<span class="kt">let</span> <span class="vc">vegetableComment</span> = <span class="s">"Is it a spicy</span> \(<span class="vc">x</span>)<span class="s">?"</span>`
9.  `<span class="kt">default</span>:`
10.  `<span class="kt">let</span> <span class="vc">vegetableComment</span> = <span class="s">"Everything tastes good in soup."</span>`
11.  `}`

</div>

</div>

</section>

<div class="note experiment"><a name="//apple_ref/doc/uid/TP40015214-CH3-SW16"></a>

<aside class="aside">

Experiment

Try removing the default case. What error do you get?

</aside>

</div>

Notice how `let` can be used in a pattern to assign the value that matched that part of a pattern to a constant. Just like in an `if` statement, a `where` clause can be added to a case to further scope the conditional statement. However, unlike in an `if` statement, a switch case that has multiple conditions separated by commas executes when any of the conditions are met.

After executing the code inside the switch case that matched, the program exits from the `switch` statement. Execution doesn’t continue to the next case, so you don’t need to explicitly break out of the `switch` statement at the end of each case’s code.

Switch statements must be exhaustive. A default case is required, unless it’s clear from the context that every possible case is satisfied, such as when the switch statement is switching on an enumeration. This requirement ensures that one of the switch cases always executes.

You can keep an index in a loop by using a `Range`. Use the _half-open range operator_ ( `..<`) to make a range of indexes.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">var</span> <span class="vc">firstForLoop</span> = <span class="m">0</span>`
2.  `<span class="kt">for</span> <span class="vc">i</span> <span class="kt">in</span> <span class="m">0</span>..<<span class="m">4</span> {`
3.  `<span class="vc">firstForLoop</span> += <span class="vc">i</span>`
4.  `}`
5.  `<span class="vc">print</span>(<span class="vc">firstForLoop</span>)`

</div>

</div>

</section>

The half-open range operator (`..<`) doesn’t include the upper number, so this range goes from `0` to `3` for a total of four loop iterations. Use the _closed range operator_ ( `...`) to make a range that includes both values.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">var</span> <span class="vc">secondForLoop</span> = <span class="m">0</span>`
2.  `<span class="kt">for</span> <span class="kt">_</span> <span class="kt">in</span> <span class="m">0</span>...<span class="m">4</span> {`
3.  `<span class="vc">secondForLoop</span> += <span class="m">1</span>`
4.  `}`
5.  `<span class="vc">print</span>(<span class="vc">secondForLoop</span>)`

</div>

</div>

</section>

This range goes from `0` to `4` for a total of five loop iterations. The _underscore_ (`_`) represents a wildcard, which you can use when you don’t need to know which iteration of the loop is currently executing.

</section>

<section class="section"><a name="//apple_ref/doc/uid/TP40015214-CH3-SW5"></a>

### Functions and Methods

A _function_ is a reusable, named piece of code that can be referred to from many places in a program.

Use `func` to declare a function. A function declaration can include zero or more _parameters_, written as `name: Type`, which are additional pieces of information that must be passed into the function when it’s called. Optionally, a function can have a return type, written after the `->`, which indicates what the function returns as its result. A function’s implementation goes inside of a pair of curly braces (`{}`).

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">func</span> <span class="vc">greet</span>(<span class="vc">name</span>: <span class="n">String</span>, <span class="vc">day</span>: <span class="n">String</span>) -> <span class="n">String</span> {`
2.  `<span class="kt">return</span> <span class="s">"Hello</span> \(<span class="vc">name</span>)<span class="s">, today is</span> \(<span class="vc">day</span>)<span class="s">."</span>`
3.  `}`

</div>

</div>

</section>

Call a function by following its name with a list of _arguments_ (the values you pass in to satisfy a function’s parameters) in parentheses. When you call a function, you pass in the first argument value without writing its name, and every subsequent value with its name.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="vc">greet</span>(<span class="s">"Anna"</span>, <span class="vc">day</span>: <span class="s">"Tuesday"</span>)`
2.  `<span class="vc">greet</span>(<span class="s">"Bob"</span>, <span class="vc">day</span>: <span class="s">"Friday"</span>)`
3.  `<span class="vc">greet</span>(<span class="s">"Charlie"</span>, <span class="vc">day</span>: <span class="s">"a nice day"</span>)`

</div>

</div>

</section>

Functions that are defined within a specific type are called _methods_. Methods are explicitly tied to the type they’re defined in, and can only be called on that type (or one of its subclasses, as you’ll learn about soon). In the earlier `switch` statement example, you saw a method that’s defined on the `String` type called `hasSuffix()`, shown again here:

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">let</span> <span class="vc">exampleString</span> = <span class="s">"hello"</span>`
2.  `<span class="kt">if</span> <span class="vc">exampleString</span>.<span class="vc">hasSuffix</span>(<span class="s">"lo"</span>) {`
3.  `<span class="vc">print</span>(<span class="s">"ends in lo"</span>)`
4.  `}`

</div>

</div>

</section>

As you see, you call a method using the dot syntax. When you call a method, you pass in the first argument value without writing its name, and every subsequent value with its name. For example, this method on `Array` takes two parameters, and you only pass in the name for the second one:

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">var</span> <span class="vc">array</span> = [<span class="s">"apple"</span>, <span class="s">"banana"</span>, <span class="s">"dragonfruit"</span>]`
2.  `<span class="vc">array</span>.<span class="vc">insert</span>(<span class="s">"cherry"</span>, <span class="vc">atIndex</span>: <span class="m">2</span>)`
3.  `<span class="vc">array</span>`

</div>

</div>

</section>

</section>

<section class="section"><a name="//apple_ref/doc/uid/TP40015214-CH3-SW6"></a>

### Classes and Initializers

In object-oriented programming, the behavior of a program is based largely on interactions between objects. An _object_ is an instance of a _class_, which can be thought of as a blueprint for that object. Classes store additional information about themselves in the form of _properties_, and define their behavior using methods.

Use `class` followed by the class’s name to define a class. A property declaration in a class is written the same way as a constant or variable declaration, except that it’s in the context of a class. Likewise, method and function declarations are written the same way. This example declares a `Shape` class with a `numberOfSides` property and a `simpleDescription()` method.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">class</span> <span class="vc">Shape</span> {`
2.  `<span class="kt">var</span> <span class="vc">numberOfSides</span> = <span class="m">0</span>`
3.  `<span class="kt">func</span> <span class="vc">simpleDescription</span>() -> <span class="n">String</span> {`
4.  `<span class="kt">return</span> <span class="s">"A shape with</span> \(<span class="vc">numberOfSides</span>) <span class="s">sides."</span>`
5.  `}`
6.  `}`

</div>

</div>

</section>

Create an instance of a class—an object—by putting parentheses after the class name. Use dot syntax to access the properties and methods of the instance. Here, `shape` is an object that’s an instance of the `Shape` class.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">var</span> <span class="vc">shape</span> = <span class="vc">Shape</span>()`
2.  `<span class="vc">shape</span>.<span class="vc">numberOfSides</span> = <span class="m">7</span>`
3.  `<span class="kt">var</span> <span class="vc">shapeDescription</span> = <span class="vc">shape</span>.<span class="vc">simpleDescription</span>()`

</div>

</div>

</section>

This `Shape` class is missing something important: an initializer. An _initializer_ is a method that prepares an instance of a class for use, which involves setting an initial value for each property and performing any other setup. Use `init` to create one. This example defines a new class, `NamedShape`, that has an initializer which takes in a name.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">class</span> <span class="vc">NamedShape</span> {`
2.  `<span class="kt">var</span> <span class="vc">numberOfSides</span> = <span class="m">0</span>`
3.  `<span class="kt">var</span> <span class="vc">name</span>: <span class="n">String</span>`

5.  `<span class="kt">init</span>(<span class="vc">name</span>: <span class="n">String</span>) {`
6.  `<span class="kt">self</span>.<span class="vc">name</span> = <span class="vc">name</span>`
7.  `}`

9.  `<span class="kt">func</span> <span class="vc">simpleDescription</span>() -> <span class="n">String</span> {`
10.  `<span class="kt">return</span> <span class="s">"A shape with</span> \(<span class="vc">numberOfSides</span>) <span class="s">sides."</span>`
11.  `}`
12.  `}`

</div>

</div>

</section>

Notice how `self` is used to distinguish the `name` property from the `name` argument to the initializer. Every property needs a value assigned—either in its declaration (as with `numberOfSides`) or in the initializer (as with `name`).

You don’t call an initializer by writing `init`; you call it by putting parentheses with the appropriate arguments after the class name. When you call an initializer, you include all arguments names along with their values.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">let</span> <span class="vc">namedShape</span> = <span class="vc">NamedShape</span>(<span class="vc">name</span>: <span class="s">"my named shape"</span>)`

</div>

</div>

</section>

Classes _inherit_ their behavior from their parent class. A class that inherits behavior from another class is called a _subclass_ of that class, and the parent class is called a _superclass_. Subclasses include their superclass name after their class name, separated by a colon. A class can inherit from only one superclass, although that class can inherit from another superclass, and so on, resulting in a _class hierarchy_.

Methods on a subclass that _override_ the superclass’s implementation are marked with `override`—overriding a method by accident, without `override`, is detected by the compiler as an error. The compiler also detects methods with `override` that don’t actually override any method in the superclass.

This example defines the `Square` class, a subclass of `NamedShape`.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">class</span> <span class="vc">Square</span>: <span class="n">NamedShape</span> {`
2.  `<span class="kt">var</span> <span class="vc">sideLength</span>: <span class="n">Double</span>`

4.  `<span class="kt">init</span>(<span class="vc">sideLength</span>: <span class="n">Double</span>, <span class="vc">name</span>: <span class="n">String</span>) {`
5.  `<span class="kt">self</span>.<span class="vc">sideLength</span> = <span class="vc">sideLength</span>`
6.  `<span class="kt">super</span>.<span class="kt">init</span>(<span class="vc">name</span>: <span class="vc">name</span>)`
7.  `<span class="vc">numberOfSides</span> = <span class="m">4</span>`
8.  `}`

10.  `<span class="kt">func</span> <span class="vc">area</span>() -> <span class="n">Double</span> {`
11.  `<span class="kt">return</span> <span class="vc">sideLength</span> * <span class="vc">sideLength</span>`
12.  `}`

14.  `<span class="kt">override</span> <span class="kt">func</span> <span class="vc">simpleDescription</span>() -> <span class="n">String</span> {`
15.  `<span class="kt">return</span> <span class="s">"A square with sides of length</span> \(<span class="vc">sideLength</span>)<span class="s">."</span>`
16.  `}`
17.  `}`
18.  `<span class="kt">let</span> <span class="vc">testSquare</span> = <span class="vc">Square</span>(<span class="vc">sideLength</span>: <span class="m">5.2</span>, <span class="vc">name</span>: <span class="s">"my test square"</span>)`
19.  `<span class="vc">testSquare</span>.<span class="vc">area</span>()`
20.  `<span class="vc">testSquare</span>.<span class="vc">simpleDescription</span>()`

</div>

</div>

</section>

Notice that the initializer for the `Square` class has three different steps:

1.  Setting the value of properties that the subclass, `Square`, declares.

2.  Calling the initializer of the superclass, `NamedShape`.

3.  Changing the value of properties defined by the superclass, `NamedShape`. Any additional setup work that uses methods, getters, or setters can also be done at this point.

Sometimes, initialization of an object needs to fail, such as when the values supplied as the arguments are outside of a certain range, or when data that’s expected to be there is missing. Initializers that may fail to successfully initialize an object are called failable initializers. A _failable initializer_ can return `nil` after initialization. Use `init?` to declare a failable initializer.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">class</span> <span class="vc">Circle</span>: <span class="n">NamedShape</span> {`
2.  `<span class="kt">var</span> <span class="vc">radius</span>: <span class="n">Double</span>`

4.  `<span class="kt">init</span>?(<span class="vc">radius</span>: <span class="n">Double</span>, <span class="vc">name</span>: <span class="n">String</span>) {`
5.  `<span class="kt">self</span>.<span class="vc">radius</span> = <span class="vc">radius</span>`
6.  `<span class="kt">super</span>.<span class="kt">init</span>(<span class="vc">name</span>: <span class="vc">name</span>)`
7.  `<span class="vc">numberOfSides</span> = <span class="m">1</span>`
8.  `<span class="kt">if</span> <span class="vc">radius</span> <= <span class="m">0</span> {`
9.  `<span class="kt">return</span> <span class="kt">nil</span>`
10.  `}`
11.  `}`

13.  `<span class="kt">override</span> <span class="kt">func</span> <span class="vc">simpleDescription</span>() -> <span class="n">String</span> {`
14.  `<span class="kt">return</span> <span class="s">"A circle with a radius of</span> \(<span class="vc">radius</span>)<span class="s">."</span>`
15.  `}`
16.  `}`
17.  `<span class="kt">let</span> <span class="vc">successfulCircle</span> = <span class="vc">Circle</span>(<span class="vc">radius</span>: <span class="m">4.2</span>, <span class="vc">name</span>: <span class="s">"successful circle"</span>)`
18.  `<span class="kt">let</span> <span class="vc">failedCircle</span> = <span class="vc">Circle</span>(<span class="vc">radius</span>: -<span class="m">7</span>, <span class="vc">name</span>: <span class="s">"failed circle"</span>)`

</div>

</div>

</section>

Initializers can also have a number of keywords associated with them. A _designated initializer_ does not require any keywords. This initializer acts as one of the primary initializers for a class; any initializer within a class must ultimately call through to a designated initializer.

The `convenience` keyword next to an initializer indicates a _convenience initializer_. Convenience initializers are secondary initializers. They can add additional behavior or customization, but must eventually call through to a designated initializer.

A `required` keyword next to an initializer indicates that every subclass of the class that has that initializer must implement its own version of the initializer (if it implements any initializer).

_Type casting_ is a way to check the type of an instance, and to treat that instance as if it’s a different superclass or subclass from somewhere else in its own class hierarchy.

A constant or variable of a certain class type may actually refer to an instance of a subclass behind the scenes. Where you believe this is the case, you can try to _downcast_ to the subclass type using a type cast operator.

Because downcasting can fail, the type cast operator comes in two different forms. The optional form, `as?`, returns an optional value of the type you are trying to downcast to. The forced form, `as!`, attempts the downcast and force-unwraps the result as a single compound action.

Use the _optional type cast operator_ (`as?`) when you’re not sure if the downcast will succeed. This form of the operator will always return an optional value, and the value will be `nil` if the downcast was not possible. This lets you check for a successful downcast.

Use the _forced type cast operator_ (`as!`) only when you’re sure that the downcast will always succeed. This form of the operator will trigger a runtime error if you try to downcast to an incorrect class type.

This example shows the use of the optional type cast operator (`as?`) to check whether a shape in an array of shapes is a square or a triangle. You increment the count of the `squares` and `triangles` variables by one each time the corresponding shape is found, printing the values at the end.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">class</span> <span class="vc">Triangle</span>: <span class="n">NamedShape</span> {`
2.  `<span class="kt">init</span>(<span class="vc">sideLength</span>: <span class="n">Double</span>, <span class="vc">name</span>: <span class="n">String</span>) {`
3.  `<span class="kt">super</span>.<span class="kt">init</span>(<span class="vc">name</span>: <span class="vc">name</span>)`
4.  `<span class="vc">numberOfSides</span> = <span class="m">3</span>`
5.  `}`
6.  `}`

8.  `<span class="kt">let</span> <span class="vc">shapesArray</span> = [<span class="vc">Triangle</span>(<span class="vc">sideLength</span>: <span class="m">1.5</span>, <span class="vc">name</span>: <span class="s">"triangle1"</span>), <span class="vc">Triangle</span>(<span class="vc">sideLength</span>: <span class="m">4.2</span>, <span class="vc">name</span>: <span class="s">"triangle2"</span>), <span class="vc">Square</span>(<span class="vc">sideLength</span>: <span class="m">3.2</span>, <span class="vc">name</span>: <span class="s">"square1"</span>), <span class="vc">Square</span>(<span class="vc">sideLength</span>: <span class="m">2.7</span>, <span class="vc">name</span>: <span class="s">"square2"</span>)]`
9.  `<span class="kt">var</span> <span class="vc">squares</span> = <span class="m">0</span>`
10.  `<span class="kt">var</span> <span class="vc">triangles</span> = <span class="m">0</span>`
11.  `<span class="kt">for</span> <span class="vc">shape</span> <span class="kt">in</span> <span class="vc">shapesArray</span> {`
12.  `<span class="kt">if</span> <span class="kt">let</span> <span class="vc">square</span> = <span class="vc">shape</span> <span class="kt">as</span>? <span class="n">Square</span> {`
13.  `<span class="vc">squares</span>++`
14.  `} <span class="kt">else</span> <span class="kt">if</span> <span class="kt">let</span> <span class="vc">triangle</span> = <span class="vc">shape</span> <span class="kt">as</span>? <span class="n">Triangle</span> {`
15.  `<span class="vc">triangles</span>++`
16.  `}`
17.  `}`
18.  `<span class="vc">print</span>(<span class="s">"</span>\(<span class="vc">squares</span>) <span class="s">squares and</span> \(<span class="vc">triangles</span>) <span class="s">triangles."</span>)`

</div>

</div>

</section>

<div class="note experiment"><a name="//apple_ref/doc/uid/TP40015214-CH3-SW17"></a>

<aside class="aside">

Experiment

Try replacing `as?` with `as!`. What error do you get?

</aside>

</div>

</section>

<section class="section"><a name="//apple_ref/doc/uid/TP40015214-CH3-SW8"></a>

### Enumerations and Structures

Classes aren’t the only ways to define data types in Swift. Enumerations and structures have similar capabilities to classes, but can be useful in different contexts.

_Enumerations_ define a common type for a group of related values and enable you to work with those values in a type-safe way within your code. Enumerations can have methods associated with them.

Use `enum` to create an enumeration.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">enum</span> <span class="vc">Rank</span>: <span class="n">Int</span> {`
2.  `<span class="kt">case</span> <span class="vc">Ace</span> = <span class="m">1</span>`
3.  `<span class="kt">case</span> <span class="vc">Two</span>, <span class="vc">Three</span>, <span class="vc">Four</span>, <span class="vc">Five</span>, <span class="vc">Six</span>, <span class="vc">Seven</span>, <span class="vc">Eight</span>, <span class="vc">Nine</span>, <span class="vc">Ten</span>`
4.  `<span class="kt">case</span> <span class="vc">Jack</span>, <span class="vc">Queen</span>, <span class="vc">King</span>`
5.  `<span class="kt">func</span> <span class="vc">simpleDescription</span>() -> <span class="n">String</span> {`
6.  `<span class="kt">switch</span> <span class="kt">self</span> {`
7.  `<span class="kt">case</span> .<span class="vc">Ace</span>:`
8.  `<span class="kt">return</span> <span class="s">"ace"</span>`
9.  `<span class="kt">case</span> .<span class="vc">Jack</span>:`
10.  `<span class="kt">return</span> <span class="s">"jack"</span>`
11.  `<span class="kt">case</span> .<span class="vc">Queen</span>:`
12.  `<span class="kt">return</span> <span class="s">"queen"</span>`
13.  `<span class="kt">case</span> .<span class="vc">King</span>:`
14.  `<span class="kt">return</span> <span class="s">"king"</span>`
15.  `<span class="kt">default</span>:`
16.  `<span class="kt">return</span> <span class="vc">String</span>(<span class="kt">self</span>.<span class="vc">rawValue</span>)`
17.  `}`
18.  `}`
19.  `}`
20.  `<span class="kt">let</span> <span class="vc">ace</span> = <span class="vc">Rank</span>.<span class="vc">Ace</span>`
21.  `<span class="kt">let</span> <span class="vc">aceRawValue</span> = <span class="vc">ace</span>.<span class="vc">rawValue</span>`

</div>

</div>

</section>

In the example above, the raw-value type of the enumeration is `Int`, so you have to specify only the first raw value. The rest of the raw values are assigned in order. You can also use strings or floating-point numbers as the raw type of an enumeration. Use the `rawValue` property to access the raw value of an enumeration member.

Use the `init?(rawValue:)` initializer to make an instance of an enumeration from a raw value.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">if</span> <span class="kt">let</span> <span class="vc">convertedRank</span> = <span class="vc">Rank</span>(<span class="vc">rawValue</span>: <span class="m">3</span>) {`
2.  `<span class="kt">let</span> <span class="vc">threeDescription</span> = <span class="vc">convertedRank</span>.<span class="vc">simpleDescription</span>()`
3.  `}`

</div>

</div>

</section>

The member values of an enumeration are actual values, not just another way of writing their raw values. In fact, in cases where there isn’t a meaningful raw value, you don’t have to provide one.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">enum</span> <span class="vc">Suit</span> {`
2.  `<span class="kt">case</span> <span class="vc">Spades</span>, <span class="vc">Hearts</span>, <span class="vc">Diamonds</span>, <span class="vc">Clubs</span>`
3.  `<span class="kt">func</span> <span class="vc">simpleDescription</span>() -> <span class="n">String</span> {`
4.  `<span class="kt">switch</span> <span class="kt">self</span> {`
5.  `<span class="kt">case</span> .<span class="vc">Spades</span>:`
6.  `<span class="kt">return</span> <span class="s">"spades"</span>`
7.  `<span class="kt">case</span> .<span class="vc">Hearts</span>:`
8.  `<span class="kt">return</span> <span class="s">"hearts"</span>`
9.  `<span class="kt">case</span> .<span class="vc">Diamonds</span>:`
10.  `<span class="kt">return</span> <span class="s">"diamonds"</span>`
11.  `<span class="kt">case</span> .<span class="vc">Clubs</span>:`
12.  `<span class="kt">return</span> <span class="s">"clubs"</span>`
13.  `}`
14.  `}`
15.  `}`
16.  `<span class="kt">let</span> <span class="vc">hearts</span> = <span class="vc">Suit</span>.<span class="vc">Hearts</span>`
17.  `<span class="kt">let</span> <span class="vc">heartsDescription</span> = <span class="vc">hearts</span>.<span class="vc">simpleDescription</span>()`

</div>

</div>

</section>

Notice the two ways that the `Hearts` member of the enumeration is referred to above: When a value is assigned to the `hearts` constant, the enumeration member `Suit.Hearts` is referred to by its full name because the constant doesn’t have an explicit type specified. Inside the switch, the enumeration member is referred to by the abbreviated form `.Hearts` because the value of `self` is already known to be a suit. You can use the abbreviated form anytime the value’s type is already known.

_Structures_ support many of the same behaviors as classes, including methods and initializers. One of the most important differences between structures and classes is that structures are always copied when they are passed around in your code, but classes are passed by reference. Structures are great for defining lightweight data types that don’t need to have capabilities like inheritance and type casting.

Use `struct` to create a structure.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">struct</span> <span class="vc">Card</span> {`
2.  `<span class="kt">var</span> <span class="vc">rank</span>: <span class="n">Rank</span>`
3.  `<span class="kt">var</span> <span class="vc">suit</span>: <span class="n">Suit</span>`
4.  `<span class="kt">func</span> <span class="vc">simpleDescription</span>() -> <span class="n">String</span> {`
5.  `<span class="kt">return</span> <span class="s">"The</span> \(<span class="vc">rank</span>.<span class="vc">simpleDescription</span>()) <span class="s">of</span> \(<span class="vc">suit</span>.<span class="vc">simpleDescription</span>())<span class="s">"</span>`
6.  `}`
7.  `}`
8.  `<span class="kt">let</span> <span class="vc">threeOfSpades</span> = <span class="vc">Card</span>(<span class="vc">rank</span>: .<span class="vc">Three</span>, <span class="vc">suit</span>: .<span class="vc">Spades</span>)`
9.  `<span class="kt">let</span> <span class="vc">threeOfSpadesDescription</span> = <span class="vc">threeOfSpades</span>.<span class="vc">simpleDescription</span>()`

</div>

</div>

</section>

</section>

<section class="section"><a name="//apple_ref/doc/uid/TP40015214-CH3-SW9"></a>

### Protocols

A _protocol_ defines a blueprint of methods, properties, and other requirements that suit a particular task or piece of functionality. The protocol doesn’t actually provide an implementation for any of these requirements—it only describes what an implementation will look like. The protocol can then be _adopted_ by a class, structure, or enumeration to provide an actual implementation of those requirements. Any type that satisfies the requirements of a protocol is said to _conform_ to that protocol.

Use `protocol` to declare a protocol.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">protocol</span> <span class="vc">ExampleProtocol</span> {`
2.  `<span class="kt">var</span> <span class="vc">simpleDescription</span>: <span class="n">String</span> { <span class="kt">get</span> }`
3.  `<span class="kt">func</span> <span class="vc">adjust</span>()`
4.  `}`

</div>

</div>

</section>

<div class="note"><a name="//apple_ref/doc/uid/TP40015214-CH3-SW10"></a>

<aside class="aside">

Note

The `{ get }` following the `simpleDescription` property indicates that it is _read-only_, meaning that the value of the property can be viewed, but never changed.

</aside>

</div>

Protocols can require that conforming types have specific instance properties, instance methods, type methods, operators, and subscripts. Protocols can require specific instance methods and type methods to be implemented by conforming types. These methods are written as part of the protocol’s definition in exactly the same way as for normal instance and type methods, but without curly braces or a method body.

Classes, structures, and enumerations adopt a protocol by listing its name after their name, separated by a colon. A type can adopt any number of protocols, which appear in a comma-separated list. If a class has a superclass, the superclass’s name must appear first in the list, followed by protocols. You conform to the protocol by implementing all of its requirements.

Here, `SimpleClass` adopts the `ExampleProtocol` protocol, and conforms to the protocol by implementing the `simpleDescription` property and `adjust()` method.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">class</span> <span class="vc">SimpleClass</span>: <span class="n">ExampleProtocol</span> {`
2.  `<span class="kt">var</span> <span class="vc">simpleDescription</span>: <span class="n">String</span> = <span class="s">"A very simple class."</span>`
3.  `<span class="kt">var</span> <span class="vc">anotherProperty</span>: <span class="n">Int</span> = <span class="m">69105</span>`
4.  `<span class="kt">func</span> <span class="vc">adjust</span>() {`
5.  `<span class="vc">simpleDescription</span> += <span class="s">" Now 100% adjusted."</span>`
6.  `}`
7.  `}`
8.  `<span class="kt">var</span> <span class="vc">a</span> = <span class="vc">SimpleClass</span>()`
9.  `<span class="vc">a</span>.<span class="vc">adjust</span>()`
10.  `<span class="kt">let</span> <span class="vc">aDescription</span> = <span class="vc">a</span>.<span class="vc">simpleDescription</span>`

</div>

</div>

</section>

Protocols are first-class types, which means they can be treated like other named types. For example, you can create an `ExampleProtocol` array and call `adjust()` on each of the instances in it (because any instance in that array would be guaranteed to implement `adjust()`, one of the protocol’s requirements).

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">class</span> <span class="vc">SimpleClass2</span>: <span class="n">ExampleProtocol</span> {`
2.  `<span class="kt">var</span> <span class="vc">simpleDescription</span>: <span class="n">String</span> = <span class="s">"Another very simple class."</span>`
3.  `<span class="kt">func</span> <span class="vc">adjust</span>() {`
4.  `<span class="vc">simpleDescription</span> += <span class="s">" Adjusted."</span>`
5.  `}`
6.  `}`

8.  `<span class="kt">var</span> <span class="vc">protocolArray</span>: [<span class="n">ExampleProtocol</span>] = [<span class="vc">SimpleClass</span>(), <span class="vc">SimpleClass</span>(), <span class="vc">SimpleClass2</span>()]`
9.  `<span class="kt">for</span> <span class="vc">instance</span> <span class="kt">in</span> <span class="vc">protocolArray</span> {`
10.  `<span class="vc">instance</span>.<span class="vc">adjust</span>()`
11.  `}`
12.  `<span class="vc">protocolArray</span>`

</div>

</div>

</section>

</section>

<section class="section"><a name="//apple_ref/doc/uid/TP40015214-CH3-SW11"></a>

### Swift and Cocoa Touch

Swift is designed to provide seamless interoperability with Cocoa Touch, the set of Apple frameworks you use to develop apps for iOS. As you walk through the rest of the lessons, it helps to have a basic understanding of how Swift interacts with Cocoa Touch.

So far, you’ve been working exclusively with data types from the Swift standard library. The _Swift standard library_ is a set of data types and capabilities designed for Swift and baked into the language. Types like `String` and `Array` are examples of data types you see in the standard library.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">let</span> <span class="vc">sampleString</span>: <span class="n">String</span> = <span class="s">"hello"</span>`
2.  `<span class="kt">let</span> <span class="vc">sampleArray</span>: <span class="n">Array</span> = [<span class="m">1</span>, <span class="m">2</span>, <span class="m">3.1415</span>, <span class="m">23</span>, <span class="m">42</span>]`

</div>

</div>

</section>

<div class="note experiment"><a name="//apple_ref/doc/uid/TP40015214-CH3-SW18"></a>

<aside class="aside">

Experiment

Read about types in the standard library by Option-clicking the type in Xcode. Option-click on `String` and `Array` in the code above while looking at this playground in Xcode.

</aside>

</div>

When writing iOS apps, you’ll be using more than the Swift standard library. One of the most frequently used frameworks in iOS app development is UIKit. _UIKit_ contains useful classes for working with the _UI (user interface)_ layer of your app.

To get access to UIKit, simply import it as a module into any Swift file or playground.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">import</span> <span class="vc">UIKit</span>`

</div>

</div>

</section>

After importing UIKit, you can use Swift syntax with UIKit types and with their methods, properties, and so on.

<section class="code-listing">

<div class="code-sample">

<div class="Swift">

1.  `<span class="kt">let</span> <span class="vc">redSquare</span> = <span class="vc">UIView</span>(<span class="vc">frame</span>: <span class="vc">CGRect</span>(<span class="vc">x</span>: <span class="m">0</span>, <span class="vc">y</span>: <span class="m">0</span>, <span class="vc">width</span>: <span class="m">44</span>, <span class="vc">height</span>: <span class="m">44</span>))`
2.  `<span class="vc">redSquare</span>.<span class="vc">backgroundColor</span> = <span class="vc">UIColor</span>.<span class="vc">redColor</span>()`

</div>

</div>

</section>

Many of the classes you’ll be introduced to in the lessons come from UIKit, so you’ll see this import statement often.

With this breadth of knowledge about Swift, you’re about to jump into making a full-fledged app in the next lesson. Although this lesson is the extent of playgrounds you’ll work with for now, remember that they can be a powerful tool in app development for anything from debugging, to visualizing complex code, to rapid prototyping.

</section>
