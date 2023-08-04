# Javascript  

## 1.How Javascript Works:
Everything in JS happens inside the execution context. Imagine a sealed-off container inside which JS runs. It is an abstract concept that hold info about the env. within the current code is being executed.

![image](https://github.com/DarshanaPorwal07/Javascript/assets/49615580/857545ec-97cc-4df8-96e0-358698c36bf4)


In the container the first component is memory component and the 2nd one is code component

Memory component has all the variables and functions in key value pairs. It is also called Variable environment.

Code component is the place where code is executed one line at a time. It is also called the Thread of Execution.

JS is a synchronous, single-threaded language

#### Synchronous:- One command at a time.
#### Single-threaded:- In a specific synchronous order


## 2.How JS is executed & Call Stack:

When Js program is ran an execution context has been created.
The exceution context ha sbeen created in two phases:
### Memory creation phase - JS will allocate memory to variables and functions.
### Code execution phase
Let's consider the below example and its code execution steps:
![image](https://github.com/DarshanaPorwal07/Javascript/assets/49615580/95eccbb1-9438-4dd8-b7f9-8f594453a4ca)

The very first thing which JS does is memory creation phase, so it goes to line one of above code snippet, and allocates a memory space for variable 'n' and then goes to line two, and allocates a memory space for function 'square'. When allocating memory for n it stores 'undefined', a special value for 'n'. For 'square', it stores the whole code of the function inside its memory space. Then, as square2 and square4 are variables as well, it allocates memory and stores 'undefined' for them, and this is the end of first phase i.e. memory creation phase.

So O/P will look something like

![image](https://github.com/DarshanaPorwal07/Javascript/assets/49615580/3ccd0ba9-4e8f-47b3-af3d-cecb8fa35583)

Now, in 2nd phase i.e. code execution phase, it starts going through the whole code line by line. As it encounters var n = 2, it assigns 2 to 'n'. Until now, the value of 'n' was undefined. For function, there is nothing to execute. As these lines were already dealt with in memory creation phase.

Coming to line 6 i.e. var square2 = square(n), here functions are a bit different than any other language. A new execution context is created altogether. Again in this new execution context, in memory creation phase, we allocate memory to num and ans the two variables. And undefined is placed in them. Now, in code execution phase of this execution context, first 2 is assigned to num. Then var ans = num * num will store 4 in ans. After that, return ans returns the control of program back to where this function was invoked from.

![image](https://github.com/DarshanaPorwal07/Javascript/assets/49615580/5d9c236a-7827-4a2d-afde-d5c3f06c9e63)

When return keyword is encountered, It returns the control to the called line and also the function execution context is deleted. Same thing will be repeated for square4 and then after that is finished, the global execution context will be destroyed. So the final diagram before deletion would look something like:

![image](https://github.com/DarshanaPorwal07/Javascript/assets/49615580/49b57fb2-9df1-4d4c-bce5-f300d40ce79c)

Javascript manages code execution context creation and deletion with the the help of Call Stack.

Call Stack is a mechanism to keep track of its place in script that calls multiple function.

#### Call Stack maintains the order of execution of execution contexts. It is also known as Program Stack, Control Stack, Runtime stack, Machine Stack, Execution context stack.


## 3.Hoisting in JavaScript (variables & functions):
Let's observe the below code and it's explaination:

![image](https://github.com/DarshanaPorwal07/Javascript/assets/49615580/7890e799-26ef-4d82-b10e-6f178a19a940)

It should have been an outright error in many other languages, as it is not possible to even access something which is not even created (defined) yet But in JS, We know that in memory creation phase it assigns undefined and puts the content of function to function's memory. And in execution, it then executes whatever is asked. Here, as execution goes line by line and not after compiling, it could only print undefined and nothing else. This phenomenon, is not an error. However, if we remove var x = 7; then it gives error. Uncaught ReferenceError: x is not defined

Hoisting is a concept which enables us to extract values of variables and functions even before initialising/assigning value without getting error and this is happening due to the 1st phase (memory creation phase) of the Execution Context.

So in previous lecture, we learnt that execution context gets created in two phase, so even before code execution, memory is created so in case of variable, it will be initialized as undefined while in case of function the whole function code is placed in the memory. Example:

![image](https://github.com/DarshanaPorwal07/Javascript/assets/49615580/40b22778-f0dc-49ae-b0ed-e384f537b878)

Now let's observe a different example and try to understand the output.

![image](https://github.com/DarshanaPorwal07/Javascript/assets/49615580/2f677a09-9383-4354-ac10-93bd6b6e0320)


## 4.Functions and Variable Environments:

![image](https://github.com/DarshanaPorwal07/Javascript/assets/49615580/5b70961a-8f7a-4012-8b34-bf1e098ef78c)

Outputs:

10

100

1

#### Code Flow in terms of Execution Context:

The Global Execution Context (GEC) is created (the big box with Memory and Code subparts). Also GEC is pushed into Call Stack
Call Stack : GEC

In first phase of GEC (memory phase), variable x:undefined and a and b have their entire function code as value initialized

In second phase of GEC (execution phase), when the function is called, a new local Execution Context is created. After x = 1 assigned to GEC x, a() is called. So local EC for a is made inside code part of GEC.

Call Stack: [GEC, a()]

For local EC, a totally different x variable assigned undefined(x inside a()) in phase 1 , and in phase 2 it is assigned 10 and printed in console log. After printing, no more commands to run, so a() local EC is removed from both GEC and from Call stack
Call Stack: GEC

Cursor goes back to b() function call. Same steps repeat.
Call Stack :[GEC, b()] -> GEC (after printing yet another totally different x value as 100 in console log)

Finally GEC is deleted and also removed from call stack. Program ends.

![image](https://github.com/DarshanaPorwal07/Javascript/assets/49615580/8eb969fb-4218-46dd-a635-2f5a4e579996)


## 5.Shortest JS Program, window & this keyword

The shortest JS program is empty file. Because even then, JS engine does a lot of things. As always, even in this case, it creates the GEC which has memory space and the execution context.

JS engine creates something known as 'window'. It is an object, which is created in the global space. It contains lots of functions and variables. These functions and variables can be accessed from anywhere in the program. JS engine also creates a this keyword, which points to the window object at the global level. So, in summary, along with GEC, a global object (window) and a this variable are created.

In different engines, the name of global object changes. Window in browsers, but in nodeJS it is called something else. At global level, this === window

If we create any variable in the global scope, then the variables get attached to the global object.

eg:

![image](https://github.com/DarshanaPorwal07/Javascript/assets/49615580/1053ee6a-e711-4efe-895d-ec9e44467fae)

## 6.undefined vs not defined in JS

In first phase (memory allocation) JS assigns each variable a placeholder called undefined.

undefined is when memory is allocated for the variable, but no value is assigned yet.

If an object/variable is not even declared/found in memory allocation phase, and tried to access it then it is Not defined

Not Defined !== Undefined

When variable is declared but not assigned value, its current value is undefined. But when the variable itself is not declared but called in code, then it is not defined.

![image](https://github.com/DarshanaPorwal07/Javascript/assets/49615580/fa73cfa2-cdc1-416a-bc48-44cfd028e94d)

JS is a loosely typed / weakly typed language. It doesn't attach variables to any datatype. We can say var a = 5, and then change the value to boolean a = true or string a = 'hello' later on.
Never assign undefined to a variable manually. Let it happen on it's own accord.


## 7.The Scope Chain, Scope & Lexical Environment

Scope in Javascript is directly related to Lexical Environment.

Let's observe the below examples:

![image](https://github.com/DarshanaPorwal07/Javascript/assets/49615580/26b13963-7eb2-4d2b-b6cd-7ff3c96eaacd)

![image](https://github.com/DarshanaPorwal07/Javascript/assets/49615580/e3f51668-b108-4175-926b-1e8fee83c04b)

Let's try to understand the output in each of the cases above.
In case 1: function a is able to access variable b from Global scope.
In case 2: 10 is printed. It means that within nested function too, the global scope variable can be accessed.
In case 3: 100 is printed meaning local variable of the same name took precedence over a global variable.
In case 4: A function can access a global variable, but the global execution context can't access any local variable.

![image](https://github.com/DarshanaPorwal07/Javascript/assets/49615580/dd7c0669-1295-4fbd-a1af-6059e67b13ca)

![image](https://github.com/DarshanaPorwal07/Javascript/assets/49615580/d56d0375-ff00-4ab7-b8ee-c99f0305db18)
![image](https://github.com/DarshanaPorwal07/Javascript/assets/49615580/dcbc29b8-865d-4db1-a645-25b94d637b4d)

So, Lexical Environment = local memory + lexical env of its parent. Hence, Lexical Environement is the local memory along with the lexical environment of its parent

Lexical: In hierarchy, In order

Whenever an Execution Context is created, a Lexical environment(LE) is also created and is referenced in the local Execution Context(in memory space).

The process of going one by one to parent and checking for values is called scope chain or Lexcial environment chain.

![image](https://github.com/DarshanaPorwal07/Javascript/assets/49615580/25914e54-0d6e-49dd-a8d6-0aca9b151d4a)

Lexical or Static scope refers to the accessibility of variables, functions and object based on physical location in source code.

![image](https://github.com/DarshanaPorwal07/Javascript/assets/49615580/74ce5635-effd-43ab-b8cf-59d661a0fad4)

TLDR; An inner function can access variables which are in outer functions even if inner function is nested deep. In any other case, a function can't access variables not in its scope.


## 8.let & const in JS, Temporal Dead Zone:

let and const declarations are hoisted. But its different from var

![image](https://github.com/DarshanaPorwal07/Javascript/assets/49615580/367cd7af-7bdb-4f8a-9bc4-89aa6a4258af)

It looks like let isn't hoisted, but it is, let's understand

Both a and b are actually initialized as undefined in hoisting stage. But var b is inside the storage space of GLOBAL, and a is in a separate memory object called script, where it can be accessed only after assigning some value to it first ie. one can access 'a' only if it is assigned. Thus, it throws error.

#### Temporal Dead Zone : Time since when the let variable was hoisted until it is initialized some value.

So any line till before "let a = 10" is the TDZ for a
Since a is not accessible on global, its not accessible in window/this also. window.b or this.b -> 15; But window.a or this.a ->undefined, just like window.x->undefined (x isn't declared anywhere)
#### Reference Error are thrown when variables are in temporal dead zone.
#### Syntax Error doesn't even let us run single line of code.













