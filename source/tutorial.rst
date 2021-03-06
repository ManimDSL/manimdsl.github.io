Language Tour
=====================================

VAlgoLang is a statically typed language designed to leverage the Manim visualisation library to enable educators to succinctly express and visualise algorithms. The core language is small by design.

This tour will take you through some of the basic constructs of the language, many of which will be familiar to those with any programming background.
It is assumed you have at least very basic knowledge of programming in any other language (such as Python, JavaScript or Java). 


Note that this is an open source project and we welcome suggestions and improvements! If you would like to make a contribution feel free to submit a pull request `here <https://github.com/VAlgoLang/VAlgoLang/tree/master/>`_.


The Basics
----------

Variables
^^^^^^^^^^^^

Declaring and assigning a variable looks a lot like it does in any other language. 

Note that depending on your code style during declaration you may choose to omit or specify the type of the variable.

.. code :: javascript
    
    let x = 4;
    let y: number = 4;
    let x: boolean = false; 


Arithmetic Expressions
^^^^^^^^^^^^^^^^^^^^^^

Arithmetic expressions also look a lot like in any other programming language (for good reason!). 

.. code :: javascript
    
    let x = 4.5;
    x = (x * 2) + 3; // x = 12

String Expressions
^^^^^^^^^^^^^^^^^^^

Expressions of type ``string`` can be manipulated further:

**Concatenation**

String expressions can be concatenated with expressions of any other type using the ``+`` operator. This will have the effect
of joining the ``string`` value of the expressions together and returning the joined string.

.. code :: javascript
    
    let x = 4.5;
    let y = "x is equal to ";
    let concatenated = y + x; // "x is equal to 4.5"
    let otherway = x + " it works both ways"; // "4.5 it works both ways"


**Character Access**

Single characters in a string expression can be accessed via the array-access operator ``[]``. This returns the ``char`` at the given index.

.. code :: javascript

    let alphabet = "abcdefghijklmnopqrstuvwxyz";
    let a = alphabet[0] // 'a';
    let d = alphabet[3] // 'd';

Boolean Expressions
^^^^^^^^^^^^^^^^^^^
Boolean expressions for many are quite familiar, as we have taken inspiration from other programming languages.

**Equality**

For equality we have two binary operators: equals ``==``, not equals ``!=``. 

.. code :: javascript

    let x = 5;
    let y = x == 5; // y = true
    let z = x != 6; // z = true

**Comparison**

For comparison we have the following binary operators: less than ``<``, greater than ``>``, less than or equal ``<=`` and greater than or equal ``>=``.

.. code :: javascript
    
    let x = 5;
    let y = x < 3;  // y = false
    let z = x > 4;  // z = true
    let a = x <= 5; // a = true
    let b = x >= 6; // b = false

**Logical Operators**

These have been implemented with the following binary operators: logical and ``&&``, logical or ``||`` and the unary not operator ``!``.

.. code :: javascript

    let x = true;
    let y = x && false; // y = false
    let z = x || y;     // z = true
    let y = !x;         // y = false


*Precedence*

The precedence for the boolean logical operators is as follows:

=========  ============ 
Operator    Precedence
---------  ------------
  ``!``        High 
  ``&&``       Medium
  ``||``       Low 
=========  ============

Examples

===================== ========= ==========================
 ``A || B && C``        means     ``A || (B && C)``
``A && B || C && D``    means    ``(A && B) || (C && D)``
``A && B && C || D``    means    ``((A && B) && C) || D``
``!A && B || C``        means    ``((!A) && B) || C``
===================== ========= ==========================

Constructors
^^^^^^^^^^^^

Data structures baked into the language have constructors. These can be invoked by directly instantiating an instance of the data structure.

Note that if a data structure (as below) takes generic type arguments in their constructor they must not be omitted.

.. code :: javascript
    
    let stack = Stack<number>();


Control structures
^^^^^^^^^^^^^^^^^^

The if-then and if-then-else Statements
#############################################

The ``if-then`` statement is the most basic of all control flow statements. It tells your program to execute a section of code **only if** a condition evaluates
to true. Otherwise the program will jump to the end of the ``if-then`` statement. For example:

.. code :: javascript

    let x = 3;

    if(x < 5) {
        x = 5;
    }

    let y = x;

In the above example the condition ``x < 5`` is true as 3 is less than 5. So the program will execute the section of code inside the ``if-then`` and y will evaluate to 5.

The ``if-then-else`` statement provides another path of execution when the ``if-then`` condition evaluates to false. For example:

.. code :: javascript

    let x = 6;

    if(x < 5) {
        x = 5;
    } else {
        x = 10;
    }

    let y = x;

In the above example the ``if-then`` condition evaluates to false as 6 is greater than 5. So the program will execute the section of code inside the ``else`` block.

We can extend this even further by introducing ``else-if`` conditions where we can chain ``if-then-else`` statements together. This has the effect of going through the 
conditions in order and upon reaching the first condition that evaluates to true, that section of code is executed and then the program will jump to the end of the whole statement.
For example.

.. code :: javascript

    let x = 10;

    if(x < 4) {
        x = 5;
    } else if(x < 8) {
        x = 10;
    } else if(x < 12) {
        x = 15;
    } else {
        x = 20;
    }

    let y = x;

In the above example first the ``x < 4`` condition will evaluate to false, then the ``x < 8`` condition evaluates to false and finally the ``x < 12`` condition evaluates to true. The program
will then execute the section of code corresponding to the second ``else-if`` and ``y`` will evaluate to 15.

Loops
###############

Loops in VAlgoLang work much the same as they do in other programming languages. VAlgoLang has two types of loops: for loops and while loops. They are best demonstrated using the following examples.

For loops
~~~~~~~~~

.. code :: javascript

    let array = Array<number>(){4, 2, 1, 3};
    let n = array.size();

    for i in range(n) {
        if (i == 2) {
            continue;
        }
        for j in range(n - 1 - i) {
            if (array[j] > array[j + 1]) {
                array.swap(j, j + 1);
            }
        }
    }

The ``range`` keyword specifies the index value sequence that the loop iterates over. Similar to Python, ``range`` in VAlgoLang takes at most 3 arguments:

* ``start`` - (inclusive) start index value *[Optional - default is* ``0`` *]*
* ``end`` - (exclusive) end index value
* ``step`` - numeric difference between each number/character in the range sequence *[Optional - default is* ``1`` *]*


While loops
~~~~~~~~~~~~

.. code :: javascript

    let stack1 = Stack<number>(){1, 2, 3, 4, 5};
    let stack2 = Stack<number>();
    let i = 0;

    while (i < 3) {
        if (i == 1) {
            stack2.pop();
            break;
        }
        stack2.push(stack1.pop());
        i = i + 1;
    }

Within for loops and while loops, you can use the ``break`` keyword to terminate the loop at that point and resume execution after the loop, or the ``continue`` keyword to run the next iteration of the loop immediately.


Functions
^^^^^^^^^^^^

The ways to define functions and make function calls are similar as they are in other languages.

Note that the return type must be defined if you intend to return anything from the function. If the return type is not specified, the function is assumed to be of type ``void``, so no ``return`` statement is allowed inside the function.

Also note that the arguments passed into any function are passed by reference, meaning that the changes made to the parameters inside the function will affect the original variables passed in.

.. code :: kotlin
    
    fun func1(x: number): number {
        return x + 1;
    }

    fun func2(stack: Stack<number>) {  // function assumed to be void as no return type is specified
        stack.push(5);
    }
.. code :: javascript

    let x: number = func1(5);

Structuring Your Program
-------------------------

VAlgoLang has no specific requirement for the structure of the main body of the program. Like many of the other programming languages, watch out for syntax and semantic errors such as accessing an undeclared identifier, incompatible type assignments and so on.

The only thing to note is that if you wish to compile a program with functions, those functions need to be declared at the top of the file. The main body of the code (statements in global scope) should then follow these function definitions.

Controlling Your Animation
-----------------------------

To make dynamic changes to the end animation, you can insert special commands which won't show up in the code visualisation.

Customisations to things such as colours, fonts and other attributes can be made through an external stylesheet described :ref:`over here <stylesheet>`.

Sleep
^^^^^^^^^^^^

The sleep command allows you to pause the animation at any code line for as many seconds as you would like. If you are constructing an online lecture this can give you some time to do a voice over.

.. code:: javascript
    
    ...
    sleep(2.5); // pauses the animation for 2.5 seconds before stepping onto the next line
    ...

.. _code_tracking:

Code Tracking
^^^^^^^^^^^^^^

On a statement level you can choose during code tracking to animate stepping into statements or stepping over them using the ``stepInto`` and ``stepOver`` blocks.

.. code:: kotlin
    
    ...
    @stepInto {
    let x = f(y);       // This will animate the execution of statements inside the function
    }

    @stepOver {
    let z = f(y);       // This will simply step over the statement
    }
    ...

.. _subtitlesannotation:

Subtitles
^^^^^^^^^^

A subtitle annotation allows you to add descriptive text to your animation. There are two types of subtitles:

``@subtitle`` - Whenever code execution reaches this annotation it will evaluate it.

``@subtitleOnce`` - This subtitle will only show once.

*Arguments:* ``text: string, duration: number, condition: boolean``;

``text`` - Subtitle text that will be displayed in the animation

``duration`` - Time in seconds that the subtitle will be displayed for (defaults to 5 seconds). A subtitle will be displayed for its specified duration or less if another subtitle needs to be shown.
 
``condition`` - The conditions for which when met, the subtitle will be displayed.

.. code:: kotlin
    
    ...
    let x = 5;

    while(x > 0) {
        x = x - 1;
        @subtitleOnce("x is now 3", 3, x == 3)  // When x is equal to 3 "x is now 3" will be displayed in the animation for 3 seconds.
    }
    ...

Speed
^^^^^^^^^^^^^^

A speed annotation allows you to specify the speed at which you want a block of code to be executed, relative to the current speed of the animation (all animations have default speed 1.0). 

To double the speed of a function call we might do something like this:

.. code:: kotlin

    ...
    @speed(2) {
    let x = slowFunction(y);
    }
    ...

Speed annotations also have a second, optional argument. This is a boolean flag indicating whether or not to speed up by the specified amount.
In the code below we speed up the inner loop by a factor of 3 after the first iteration is complete. This can be useful for when you want to conditionally speed through certain parts of your animation.


.. code:: kotlin


	...
	for i in range(5) {	
	  @speed(3, i >= 1) {
	  for j in range(5) {
	    ...
	  }
	  }
	}

Types
------------------------------

There are two "kinds" of types in this language at the moment. 

* Primitives, such as ``boolean``, ``char``, ``number`` and ``string``.
* Data structures, such as ``Stack<number>``. Data structures may define restrictions on the type parameters they permit.

.. _primitive_types:

Primitive Types
^^^^^^^^^^^^^^^

boolean
###############

Represents boolean values true or false.

.. code:: javascript

    let x: boolean = true;
    let y: boolean = false;

char
###############

Represents a 16-bit Unicode character.

.. code:: javascript

    let x: char = 'a';
    let y: char = '+';


number
###############

A number is an arbitrary representation of a numeric value that in our transpiler is represented using Double precision.

.. code:: javascript

    let x: number = 5;
    let y: number = 4.5;


string
###############

A string represents character strings.

.. code:: javascript

    let x: string = "Hi how are you";
    let y: string = "Hi you are so fantastic";


Conversion Functions
####################

``toChar``
~~~~~~~~~~

*Arguments:* ``value: number | char``; *Return type:* ``char``; *Throws:* ``Runtime Error: Invalid cast operation``

This method converts a ``number`` to its ASCII ``char`` value. It acts as an identity function when a ``char`` is given as input. 
The number is rounded to the nearest integer to perform the conversion.

.. code:: javascript

    toChar(97); // will return 'a'

``toNumber``
~~~~~~~~~~~~

*Arguments:* ``value: char | number | string``; *Return type:* ``number``; *Throws:* ``Runtime Error: Invalid cast operation``

This method converts a ``char`` to its ASCII code value. It acts as an identity function when a ``number`` is given as input. When a ``string`` is given as input if the string
is formatted like a number e.g. ``"123.2"`` its number value will be returned.

.. code:: javascript

    toNumber('a'); // will return 97
    toNumber("123"); // will return 123
    toNumber("adi"); // will throw a runtime error

.. _data_structures:

Data Structures
^^^^^^^^^^^^^^^

A rule of thumb is that data structures are the types of things you might have learnt in a CS class (trees, lists, and so on) and which you might find interesting to animate.
All primitives begin with a lower case letter while data structures will begin with a capitalised letter.

For those of you interested in the nuts and bolts, this distinction was made to make it clear in the type system for the programmer what sorts of variables should be centre-stage in the animation.

A comprehensive list of data structures "baked in" to the language is detailed below.

Stack<T>
###############

This has the following inbuilt methods:

``push``
~~~~~~~~~

*Arguments:* ``item: T``; *Return type:* ``void``

Pushes an item onto the top of the stack.

``pop``
~~~~~~~~~

*Arguments:* None; *Return type:* ``T``

Pops off the top element of the stack and returns this value.

``peek``
~~~~~~~~~

*Arguments:* None; *Return type:* ``T``

Returns the element on top of the stack without removing it.

``size``
~~~~~~~~~

*Arguments:* None; *Return type:* ``number``

Returns the current size of the stack.

``isEmpty``
~~~~~~~~~~~~~~

*Arguments:* None; *Return type:* ``boolean``

Returns ``true`` if the stack is currently empty.


Array<T>
###############

This has the following inbuilt methods:


``swap``
~~~~~~~~~

*Arguments:* ``index1: number``, ``index2: number``, (optional) ``longSwap: boolean``; *Return type:* ``void``

Swaps the elements at ``index1`` and ``index2`` in the array. The optional ``longSwap`` argument can be set to ``true`` in order to make the animation slightly longer, with a visualisation of the ``temp`` variable often seen when swapping array elements programmatically. The default value is ``false``, resulting in a 'quick swap'.


``size``
~~~~~~~~~

*Arguments:* None; *Return type:* ``number``

Returns the fixed size of the array.

List<T>
###############

This has the following inbuilt methods:


``prepend``
~~~~~~~~~~~~~~

*Arguments:* ``item: T``; *Return type:* ``void``

Adds an item to the front of the list.


``append``
~~~~~~~~~~~~~~

*Arguments:* ``item: T``; *Return type:* ``void``

Adds an item to the end of the list.


``size``
~~~~~~~~~

*Arguments:* None; *Return type:* ``number``

Returns the current size of the list.


Tree<T>
###############

The tree type encapsulates an underlying Node<T> object. The distinction between the Node and Tree types exist to allow you to specify exactly which nodes in a subtree should be animated.
To animate a Node simply construct a Tree from it as defined below.

This has the following inbuilt methods:

``constructor``
~~~~~~~~~~~~~~~

*Arguments:* ``root: Node<T>?``; 

Constructs a Tree from a Root node, marking the node and all current and future children to be able to be animated as a data structure.

``root``
~~~~~~~~~

*Arguments:* None; *Return type:* ``Node<T>?``

Accesses underlying Root node of tree.

Node<T>
###############

This has the following inbuilt methods:

``constructor``
~~~~~~~~~~~~~~~

*Arguments:* ``root: T``; 

Constructs a Node from the value it will contain.

``left``
~~~~~~~~~

*Arguments:* None; *Return type:* ``Node<T>?``

Accesses left subtree. Returns null if no left subtree.

``right``
~~~~~~~~~

*Arguments:* None; *Return type:* ``Node<T>?``

Accesses right subtree. Returns null if no right subtree.

``value``
~~~~~~~~~

*Arguments:* None; *Return type:* ``T``

Extracts the value from the node.


An example of a typical Node and Tree usage might be as follows:

.. code:: javascript

    let head = Node<number>(1); // Creates a node with value 1 
    let tree = Tree<Node<number>>(head); // Constructs a renderable tree from this node
    tree.root.left = Node<number>(0); // Appends a rendered node with value 0 to the left of the root of the tree

Examples
############


To make this more concrete, note how the ``Stack<number>`` in the following animation is the focus of the attention as it is the primary data structure being used.


.. raw:: html

        <video src="_static/intro.mp4" frameborder="0" allowfullscreen style=" width: 80%; height: 80%;" controls></video> 

