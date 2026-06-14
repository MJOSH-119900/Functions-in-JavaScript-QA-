**Higher-Order Functions, Array Methods & Destructuring Answers to
Question**

1.  A higher-order function is a function that either takes one or more
    functions as arguments, returns a function as its result, or does
    both.

**The main difference lies in what data types the function can accept or
manipulate.**

-   **Regular Functions**: Accept only standard data types (like
    numbers, strings, or booleans) as inputs and return standard data
    types as outputs.

-   **Higher-Order Functions**: Treat functions as \"first-class
    citizens,\" meaning they treat functions just like any other value
    or variable.

2.  For functions to be **\"first-class citizens\"** means they are
    treated like any other variable or value in the language. They have
    no special restrictions and can be passed around, stored, and
    manipulated dynamically at runtime. And because it does the
    following:

-   **Assigned to Variables:** You can store a function inside a
    > variable, an object property, or an array element.

> *const greet = function() { return \"Hello!\"; };*
>
> *const user = { sayHi: greet*
>
> *};*

-   **Passed as Arguments:** You can inject a function into another
    > function as an input. This is the foundation of **callbacks.**

> *function runOperation(operation, value) {*
>
> *return operation(value);*
>
> *}*

-   **Returned from Other Functions:** A function can generate and
    > output a completely new function.

> *function createGreeter(greeting) { return function(name) {*
>
> *return \`\${greeting}, \${name}!\`; };*
>
> *}*

-   **Given Properties and Methods:** Because functions are technically
    > objects in JavaScript, you can attach custom properties or methods
    > directly to them.

> *function game() {}*
>
> *game.highScore = 100; // Adding a property to the function*

3.  A **callback function** is a function passed into another function
    as an argument, which is then executed (called back) inside that
    outer function. In JavaScript, some tasks take time, like fetching
    data from a server or waiting for a user click. Callbacks prevent
    the entire browser from freezing while waiting.

**When and Why You Use Callbacks**

You use callbacks to control the flow of execution in your program.

i.  To Handle Asynchronous Operations (When): JavaScript runs on a
    > single thread, meaning it can only do one thing at a time. If you
    > request data from a database, the code cannot just pause and
    > freeze the screen while waiting.

-   Why: Callbacks allow you to say, \"Go fetch this data, and whenever
    > it finally arrives, run this callback function to display it.\"
    > This keeps your application responsive.

ii. 2\. To Create Reusable, Flexible Code (Why): Instead of writing
    > multiple functions that do almost the same thing, you can write
    > one master function that handles the logic framework, and use
    > callbacks to swap out the specific behavior.

-   Why: It separates what needs to be done from when it should be done.

> Code Example:
>
> *// 1. Define a named callback function*
>
> *function displayFormattedPrice(finalPrice) {*
>
> *console.log(\`Total Price (with tax):
> \$\${finalPrice.toFixed(2)}\`);*
>
> *}*
>
> *// 2. Define the outer function that accepts a callback*
>
> *function calculateTotal(price, taxRate, callback) {*
>
> *console.log(\"Calculating total\...\");*
>
> *const tax = price \* taxRate;*
>
> *const total = price + tax;*
>
> *// 3. Invoke the callback function from inside this outer function*
>
> *// We pass the calculation result back to the callback*
>
> *callback(total);*
>
> *}*
>
> *// Execution: Pass the named callback (without parenthesis!) into the
> outer function*
>
> *calculateTotal(100, 0.08, displayFormattedPrice);*
>
> **Code Breakdown**

-   displayFormattedPrice is the named callback. It expects a number and
    > formats it nicely.

-   We pass it to calculateTotal by its name only. If we added
    > parenthesis like displayFormattedPrice(), it would run
    > immediately, which we do not want.

-   Inside calculateTotal, the parameter callback becomes a reference to
    > our function. Calling callback(total) is what actually triggers
    > our code to run and print the result.

4.  A **closure** is the combination of a function bundled together with
    references to its surrounding state (the **lexical environment**).
    In simple terms, a closure gives an inner function access to the
    outer function's scope even after the outer function has finished
    executing.

**Relationship to Higher-Order Functions**

A **higher-order function** provides the mechanism (by returning an
inner function) while on the other hand A **closure** is the result. It
is the living memory backpack that the returned inner function carries
with it, holding onto the outer function\'s variables.

Why Closures Are Useful

-   Data Privacy / Encapsulation: They allow you to create private
    > variables that cannot be accessed or modified from the outside
    > world.

-   State Preservation: They allow a function to retain state between
    > execution calls without relying on global variables.

-   Function Customization: They power function factories, letting you
    > generate specialized configurations of a single function
    > framework.

> Code Example:
>
> *// The Higher-Order Function (Factory)*
>
> *function createMultiplier(multiplier) {*
>
> *// The inner function forms a closure over the \'multiplier\'
> variable*
>
> *return function (num) {*
>
> *return num \* multiplier;*
>
> *};*
>
> *}*
>
> *// Generate specific functions*
>
> *const double = createMultiplier(2); // \'double\' remembers
> multiplier = 2*
>
> *const triple = createMultiplier(3); // \'triple\' remembers
> multiplier = 3*
>
> *// Invoke the returned functions*
>
> *console.log(double(5)); // Output: 10*
>
> *console.log(triple(5)); // Output: 15*
>
> *console.log(double(10)); // Output: 20 (still remembers 2)*

5.  **Synchronous Callbacks**: Execute **immediately** during the
    execution of the higher-order function. They block the remaining
    code from running until they finish. The code runs strictly
    top-to-bottom. Line 3 must finish completely before line 6 can run.
    ***While***

**Asynchronous Callbacks**: Execute **later**, after an external
operation (like a timer, file read, or API fetch) completes. They do not
block the surrounding code. The code skips the callback, prints \"End\"
first, and then executes the callback 2 seconds later once the timer
expires.

Key Comparison

  -----------------------------------------------------------------------
  Feature         Synchronous Callback    Asynchronous Callback
  --------------- ----------------------- -------------------------------
  Execution       Immediate, in-order     Delayed, out-of-order
  Timing                                  

  Blocking        Blocks the next line of Non-blocking
  Behavior        code                    

  Use Case        Data transformation,    Network requests, timers,
                  looping                 events

  JavaScript      .map(), .filter(),      setTimeout(), fetch().then(),
  Examples        .forEach()              addEventListener()
  -----------------------------------------------------------------------

Code Example

+------------------------------+---------------------------------------+
| Synchronous Callback         | Asynchronous Callback (Non-Blocking)  |
| (Blocking)                   |                                       |
|                              | Javascript                            |
| Javascript                   |                                       |
|                              | *console.log(\"Start\");*             |
| *console.log(\"Start\");*    |                                       |
|                              | *setTimeout(function() {*             |
| *\[1, 2,                     |                                       |
| 3\].forEach(function(num) {* | *console.log(\"Inside the timeout\"); |
|                              | // Asynchronous callback*             |
| *console.log(\`Processing:   |                                       |
| \${num}\`); // Synchronous   | *}, 2000);*                           |
| callback*                    |                                       |
|                              | *console.log(\"End\");*               |
| *});*                        |                                       |
|                              | *// OUTPUT ORDER:*                    |
| *console.log(\"End\");*      |                                       |
|                              | *// 1. Start*                         |
| *// OUTPUT ORDER:*           |                                       |
|                              | *// 2. End*                           |
| *// 1. Start*                |                                       |
|                              | *// 3. Inside the timeout (after 2    |
| *// 2. Processing: 1*        | seconds)*                             |
|                              |                                       |
| *// 3. Processing: 2*        |                                       |
|                              |                                       |
| *// 4. Processing: 3*        |                                       |
|                              |                                       |
| *// 5. End*                  |                                       |
+==============================+=======================================+
+------------------------------+---------------------------------------+

**Why the Distinction Matters**

If you pass a synchronous callback that takes 10 seconds to run (like
processing a massive image), your browser tab will completely freeze.

By using an asynchronous callback, JavaScript hands the heavy lifting to
the browser background environment, allowing the user interface to stay
completely smooth and responsive while waiting for the task to finish.

6.  This code demonstrates the exact mechanics of how a higher-order
    function passes and executes behavior dynamically.

Here is the exact Step-by-Step order in which the JavaScript engine
executes the code:

i.  **Line 1--3 (Definition):** The engine reads and stores the
    applyTwice function definition in memory. It does not run yet.

ii. **Line 5 (Definition):** The engine reads and stores the arrow
    function addThree in memory.

iii. **Line 7 (Invocation):** The engine evaluates console.log(). To
     print the result, it must first execute the inner expression:
     applyTwice(addThree, 10). 

iv. **Entering applyTwice:** Control jumps inside applyTwice. The
    parameters are assigned values:

v.  fn becomes a reference to the addThree function.

vi. value becomes the number 10.

vii. **Evaluating the Inner Function Call:** The return statement reads
     return fn(fn(value)). The engine evaluates from the inside out,
     starting with the inner call: fn(value) which translates to
     addThree(10).

viii. **Executing addThree(10):** Control jumps to addThree. It
      evaluates 10 + 3, completes, and returns 13. \[3\]

ix. **Evaluating the Outer Function Call:** The return statement now
    evaluates the outer function with the new result: fn(13) which
    translates to addThree(13). \[4\]

x.  **Executing addThree(13):** Control jumps to addThree again. It
    evaluates 13 + 3, completes, and returns 16.

xi. **Exiting applyTwice:** The function applyTwice returns the final
    value 16 back to console.log.

xii. **Printing Output:** console.log(16) runs, printing 16 to the
     console.

**Final Output and Why**

-   **Final Output:** 16

-   **Why:** The number 10 had the mathematical operation + 3 applied to
    > it exactly two times sequentially: (10 + 3) + 3 = 16.

> **Higher-Order Function Concepts Demonstrated**
>
> This code perfectly illustrates two foundational functional
> programming pillars:

-   **Functions as First-Class Citizens:** The addThree function is
    > treated exactly like a standard piece of data. It is passed by
    > name as an argument into applyTwice without being executed
    > prematurely.

-   **Higher-Order Function Mechanism:** applyTwice fits the exact
    > definition of a higher-order function because it accepts a
    > function (fn) as an input parameter. \[6\]

> **Callback Execution:** addThree acts as a synchronous callback
> function. It is handed over to applyTwice, which retains full control
> over when and how many times to invoke it.

7.  **Function composition** is the process of combining two or more
    functions to produce a new function. Executing the combined function
    passes the output of the first function as the input to the next
    function (\\(f(g(x))\\)).

**Why It Is Powerful (Benefits)**

-   **Reusability**: You can build small, single-purpose utility
    functions and assemble them into complex workflows without rewriting
    code.

-   **Readability**: It eliminates deeply nested function calls (like
    addOne(double(5))) and creates a clean, linear pipeline.

-   **Separation of Concerns**: Each function handles exactly one
    isolated task, making debugging and testing highly predictable.

> Code Example
>
> *function compose(f, g) {*
>
> *// Returns a new function that executes right-to-left*
>
> *return function(x) {*
>
> *return f(g(x));*
>
> *};*
>
> *}*
>
> *const double = x =\> x \* 2;*
>
> *const addOne = x =\> x + 1;*
>
> *// double runs first (inside), then addOne runs on that result
> (outside)*
>
> *const doubleThenAddOne = compose(addOne, double);*
>
> *console.log(doubleThenAddOne(5)); // Output: 11\\*

8.  Comparison

+-----------+--------------------+---------------------+---------------+
| Feature   | 9.  Approach A     | 10. Approach B      | 11. Approach  |
|           |     (for loop)     |     (forEach)       |     C         |
|           |                    |                     |     (filter)  |
+===========+====================+=====================+===============+
| Re        | 12. Low (heavy     | 13. Moderate        | 14. High      |
| adability |     syntax         |     (cleaner loop)  |               |
|           |     boilerplate)   |                     | (declarative, |
|           |                    |                     |     single    |
|           |                    |                     |     line)     |
+-----------+--------------------+---------------------+---------------+
| Intent    | 15. Hidden         | 16. Partially clear | 17. Explicit  |
|           |     (focuses on    |     (focuses on     |     (focuses  |
|           |     *how* to loop) |     iteration)      |     on *what* |
|           |                    |                     |     data to   |
|           |                    |                     |     keep)     |
+-----------+--------------------+---------------------+---------------+
| Imm       | 18. Imperative     | 19. Imperative      | 20. Pure      |
| utability |     (mutates       |     (mutates        |     (returns  |
|           |     external       |     external result |     a new     |
|           |     result array)  |     array)          |     array     |
|           |                    |                     |     natively) |
+-----------+--------------------+---------------------+---------------+
| Error     | 21. High           | 22. Low (handles    | 23. None      |
| Proneness |     (off-by-one    |     indices         |               |
|           |     index errors)  |     automatically)  |    (abstracts |
|           |                    |                     |     loop      |
|           |                    |                     |               |
|           |                    |                     |   completely) |
+-----------+--------------------+---------------------+---------------+

> **Key Trade-offs**

a.  **Approach A: Traditional for loop**

-   **Pros**: Marginally faster performance on massive data sets
    > (millions of items).

-   **Cons**: Noisy boilerplate (let i = 0). It forces you to manually
    > manage array indices, distracting from the actual filter logic.

b.  **Approach B: forEach**

-   **Pros**: Eliminates index management boilerplate.

-   **Cons**: It is a mismatch of intent. forEach is meant for
    > side-effects (e.g., saving to a database). Using it to build a new
    > array requires manually mutating an external state variable
    > (result).

c.  **Approach C: filter**

-   **Pros**: Impeccable clarity. It guarantees immutability by
    returning a brand new array without touching the original array.

-   **Cons**: Slight performance overhead due to the callback function
    creation (negligible in 99% of applications).

**Approach C (filter) is highly recommended.**

> **Why:**

1.  **Declarative Architecture**: Developers scanning the codebase
    instantly know the function\'s goal without reading the inner
    implementation.

2.  **Immutability**: Avoiding shared, mutable state makes code highly
    predictable, easier to test, and safe from unexpected bugs.

3.  **Chainability**: The output of .filter() can be immediately chained
    into other array operations like .map() or .reduce().

> **Code Example**
>
> *// Professional chaining example*
>
> *const processed = numbers*
>
> *.filter(n =\> n % 2 === 0)*
>
> *.map(n =\> n \* 2);*

9.  So**me real-world use cases of higher-order functions outside of
    array methods?**

```{=html}
<!-- -->
```
i.  **Event Handling (Debouncing):** In browsers, events like typing,
    > scrolling, or resizing fire rapidly. A higher-order function can
    > delay the execution of an action until the user finishes the
    > activity, preventing browser lag and unnecessary server requests.

> Code:
>
> *// HOF: Delays execution of the passed action function*
>
> *function debounce(action, delay) {*
>
> *let timer;*
>
> *return function(\...args) {*
>
> *clearTimeout(timer);*
>
> *timer = setTimeout(() =\> action(\...args), delay);*
>
> *};*
>
> *}*
>
> *// Usage: Only calls the API 500ms AFTER the user stops typing*
>
> *const saveInput = debounce((text) =\> console.log(\`Saving:
> \${text}\`), 500);*
>
> *document.getElementById(\"search\").addEventListener(\"input\",(e)*
> *=\>* *saveInput(e.target.value));*

ii. Middleware in Web Frameworks (Authentication): Web servers use
    > higher-order functions to intercept incoming network requests.
    > They validate authorization credentials or user permissions before
    > letting the request reach the core application logic.

> Code:
>
> *// HOF: Enhances a route handler with role authentication logic*
>
> *function requireRole(allowedRole) {*
>
> *return function(req, res, next) {*
>
> *if (req.user.role !== allowedRole) {*
>
> *return res.status(403).send(\"Forbidden\");*
>
> *}*
>
> *next(); // Move to the actual route logic*
>
> *};*
>
> *}*
>
> *// Usage (Express.js style middleware pipeline)*
>
> *app.get(\"/admin/dashboard\", requireRole(\"admin\"), (req, res) =\>
> {*
>
> *res.send(\"Welcome Admin!\");*
>
> *});*

iii. Validation Logic (Data Guardrails): Higher-order functions can
     > validate incoming parameter types or data formatting dynamically.
     > This separates boring sanitization checks from core business
     > rules.

> Code:
>
> *// HOF: Validates arguments before executing the core function*
>
> *function validateNumbers(coreFunction) {*
>
> *return function(\...args) {*
>
> *if (args.some(arg =\> typeof arg !== \'number\')) {*
>
> *throw new Error(\"Invalid Input: All arguments must be numbers.\");*
>
> *}*
>
> *return coreFunction(\...args);*
>
> *};*
>
> *}*
>
> *// Usage*
>
> *const multiply = (a, b) =\> a \* b;*
>
> *const safeMultiply = validateNumbers(multiply);*
>
> *console.log(safeMultiply(4, 5)); // Output: 20*
>
> *// safeMultiply(4, \"five\"); // Throws Error immediately*

iv. Memoization (Caching Results): Higher-order functions can add an
    > in-memory cache to slow or heavy computational operations. It
    > intercepts arguments, checks if it already solved that exact math
    > before, and serves the answer instantly without recalculating.

> Code:
>
> *// HOF: Caches results based on identical inputs*
>
> *function memoize(fn) {*
>
> *const cache = {};*
>
> *return function(arg) {*
>
> *if (arg in cache) return cache\[arg\]; // Return cached result*
>
> *const result = fn(arg);*
>
> *cache\[arg\] = result; // Save new result*
>
> *return result;*
>
> *};*
>
> *}*
>
> *// Usage*
>
> *const expensiveCube = (n) =\> n \* n \* n;*
>
> *const cachedCube = memoize(expensiveCube);*
>
> *console.log(cachedCube(100)); // Calculated and saved (Output:
> 1000000)*
>
> *console.log(cachedCube(100)); // Returned instantly from cache
> memory*

9.  The .map() method loops through every element in an array and passes
    each element into a callback function to transform it.

> **What It Returns**
>
> It returns a **brand-new array** containing the transformed values.
> The original array remains completely unchanged (immutable).
>
> **When to Use It**
>
> Use .map() when you need to transform every item in a collection into
> a new format, maintaining a strict 1:1 relationship between input and
> output size.
>
> Code:
>
> const numbers =;
>
> // Transforms every number by multiplying it by 10
>
> const doubled = numbers.map(num =\> num \* 10);
>
> console.log(doubled); // Output: \[10, 20, 30\] (New array)
>
> console.log(numbers); // Output: \[1, 2, 3\] (Original array
> unchanged)

10. The .filter() method evaluates every element in an array against a
    test condition inside a callback function. It returns a **brand-new
    array** containing only the elements that passed the test (where the
    callback returned true). If no items pass, it returns an empty array
    \[\].

Key Differences: .filter() vs. .map()

  ------------------------------------------------------------------------
  Feature            .filter()                    .map()
  ------------------ ---------------------------- ------------------------
  Primary Purpose    Selects a subset of existing Transforms every piece
                     data                         of data

  Callback Return    Must return a boolean        Returns the new
                     (true/false)                 transformed value

  Output Array       Can be shorter than the      Always matches the
  Length             original array               original array length
  ------------------------------------------------------------------------

Code Example:

*const numbers =;*

*// 1. filter(): Keeps only even numbers (changes array size)*

*const evens = numbers.filter(n =\> n % 2 === 0);*

*console.log(evens); // Output: \[2, 4\]*

*// 2. map(): Multiplies every number by 2 (changes values, keeps size)*

*const doubled = numbers.map(n =\> n \* 2);*

*console.log(doubled); // Output: \[2, 4, 6, 8\]*

11. **What It Does:** The .reduce() method processes an array from left
    to right, combining all elements into a **single output value**
    (such as a number, string, object, or new array) using an
    \"accumulator\" variable \[C1\].

The Syntax

> *array.reduce((accumulator, currentValue) =\> {*
>
> *return accumulator + currentValue;*
>
> *}, initialValue)*

-   ***Accumulator**: The running total or collected state passed from
    the previous iteration \[C1\].*

-   ***Current Value**: The specific element currently being processed
    in the loop.*

-   ***Initial Value**: The starting value assigned to the accumulator
    before the loop begins \[C1\].*

> Step-by-Step Code Example (Summing Numbers)
>
> *const numbers =;*
>
> *// Summing numbers starting from 0*
>
> *const totalSum = numbers.reduce((acc, curr) =\> {*
>
> *return acc + curr;*
>
> *}, 0);*
>
> *console.log(totalSum); // Output: 10*

**Behind-the-Scenes Trace:**

  -----------------------------------------------------------------------------
  Iteration   Accumulator (acc) Current Value       Calculation   Next
                                (curr)                            Accumulator
                                                                  Value
  ----------- ----------------- ------------------- ------------- -------------
  Start       0 (Initial Value) ---                 ---           ---

  1st         0                 1                   0 + 1         1

  2nd         1                 2                   1 + 2         3

  3rd         3                 3                   3 + 3         6

  4th         6                 4                   6 + 4         **10** (Final
                                                                  Return)
  -----------------------------------------------------------------------------

**Advanced Real-World Example (Grouping Data)**

> .reduce() is not just for math; you can use it to reshape data
> structures, like counting occurrences of items.
>
> *const fruitBasket = \[\'apple\', \'banana\', \'apple\', \'orange\',
> \'banana\', \'apple\'\];*
>
> *const countTally = fruitBasket.reduce((tally, fruit) =\> {*
>
> *tally\[fruit\] = (tally\[fruit\] \|\| 0) + 1;*
>
> *return tally;*
>
> *}, {}); // Starting with an empty object {}*
>
> *console.log(countTally);*
>
> *// Output: { apple: 3, banana: 2, orange: 1 }*

9.  The difference between .find() and .filter() lies in how many items
    they look for and what data type they return.

> **The Core Difference**

i.  .filter(): Searches the entire array and returns a new array
    containing *all* matching elements.

ii. .find(): Stops searching the moment it matches the condition and
    returns only that first element as a single value

**Quick Comparison**

  -------------------------------------------------------------------------------
  Feature           .filter()                      .find()
  ----------------- ------------------------------ ------------------------------
  **Search          Scans every single item.       Stops scanning at the first
  Behavior**                                       match.

  **Return Type**   Always an **Array** \[\].      A **Single Value**
                                                   (Object/Number/String/etc.).

  **If no match     Returns an empty array \[\].   Returns undefined.
  found**                                          

  **Performance**   Slower on large arrays (always 
                    loops through all items).      
  -------------------------------------------------------------------------------

CODE:

> *const users = \[*
>
> *{ id: 1, role: \'admin\', name: \'Alice\' },*
>
> *{ id: 2, role: \'user\', name: \'Bob\' },*
>
> *{ id: 3, role: \'admin\', name: \'Charlie\' }*
>
> *\];*
>
> *// 1. filter() --- Finds ALL admins*
>
> *const allAdmins = users.filter(user =\> user.role === \'admin\');*
>
> *console.log(allAdmins);*
>
> *// Output: \[ { id: 1, role: \'admin\', name: \'Alice\' }, { id: 3,
> role: \'admin\', \... } \]*
>
> *// 2. find() --- Finds ONLY the first admin it encounters*
>
> *const firstAdmin = users.find(user =\> user.role === \'admin\');*
>
> *console.log(firstAdmin);*
>
> *// Output: { id: 1, role: \'admin\', name: \'Alice\' } (Not an
> array!)*

9.  Both .some() and .every() solve the problem of **validating bulk
    data** across an array without writing messy for loops or tracking
    flags manually.

Instead of extracting data, they answer a simple question with a boolean
(true or false).

a.  **The some() Method**

-   What problem it solves: Checking if an array contains at least one
    > item that meets a specific condition.

-   Behaviours: It loops through the array and stops (exits early) the
    > exact moment it finds a match.

Code Example

> *const userStatus = \[\'offline\', \'offline\', \'active\',
> \'offline\'\];*
>
> *// Problem: Is anyone online right now?*
>
> *const isAnyoneOnline = userStatus.some(status =\> status ===
> \'active\');*
>
> *console.log(isAnyoneOnline); // Output: true*

b.  **The every() Method**

-   What problem it solves: Checking if all items in an array meet a
    specific condition without exception.

-   Behaviours: It loops through the array and stops (exits early) the
    exact moment it finds an item that *fails* the test.

Code Example

> *const cartItems = \[*
>
> *{ name: \'Shirt\', inStock: true },*
>
> *{ name: \'Shoes\', inStock: true },*
>
> *{ name: \'Hat\', inStock: false }*
>
> *\];*
>
> *// Problem: Can we ship this order immediately? (Requires all items
> in stock)*
>
> *const canShipNow = cartItems.every(item =\> item.inStock === true);*
>
> *console.log(canShipNow); // Output: false (because of the Hat)*

**Summary Comparison**

  ------------------------------------------------------------------------
  Method         Human Translation            Stops Scanning When\...
  -------------- ---------------------------- ----------------------------
  .some()        **\"Is there at least        **It hits the first true
                 one?\"**                     result.**

  .every()       **\"Is it true for           **It hits the first false
                 everything?\"**              result.**
  ------------------------------------------------------------------------

9.  The core difference between .forEach() and .map() lies in **whether
    or not they create a new array**. The **.forEach()** performs an
    action on every element in an array but discards any return values.
    It always returns undefined. While on the other hand;

**.map()** **a**utomatically transforms every element and returns a
**brand-new array** containing those transformed results.

**Quick Comparison**

  ------------------------------------------------------------------------
  Feature            .forEach()                         .map()
  ------------------ ---------------------------------- ------------------
  Return Value       undefined                          A new array of the
                                                        same length

  Primary Goal       Executing **side effects**         **Data
                                                        transformation**

  Immutability       Often mutates external variables   Leaves the
                     or original data                   original array
                                                        completely
                                                        untouched

  Chainability       Cannot be chained (ends the line)  Can be immediately
                                                        chained with
                                                        .filter(), etc.
  ------------------------------------------------------------------------

Code Comparison

a.  Using **.map()** for Transformation

> *const prices =;*
>
> *// Automatically converts to a new array of formatted strings*
>
> *const formattedPrices = prices.map(price =\> \`\$\${price}.00\`);*
>
> *console.log(formattedPrices); // Output: \[\"\$10.00\", \"\$20.00\",
> \"\$30.00\"\]*

b.  Using **.forEach()** for Side Effects

> *const prices =;*
>
> *// Modifies external state (the DOM/UI) directly*
>
> *prices.forEach(price =\> {*
>
> *const element = document.createElement(\'div\');*
>
> *element.innerText = \`Price: \$\${price}\`;*
>
> *document.body.appendChild(element);*
>
> *});*
>
> *// Notice: No new array is created or returned here.*

i.  Use .map() when:

    -   You are converting an array of raw data into a new format (e.g.,
        pulling user IDs out of an array of user objects).

    -   You are using React to transform an array of data objects into
        HTML/JSX elements.

    -   You want to chain array operations together
        (array.map().filter()).

ii. Use .forEach() when:

    -   You do not want a new array.

    -   You need to perform a \"side effect\" that interacts with the
        outside world, like saving items to a database, updating a
        global variable, logging to the console, or inserting elements
        into the DOM.

    9.  **Method chaining** is a programming pattern where multiple
        methods are called sequentially on a single object in a single
        line of code. It works by having each method return an object
        that the *next* method can immediately act upon.

> In JavaScript, this looks like a pipeline where data flows through a
> series of operations from left to right.
>
> **How it Works with Array Methods**
>
> Array methods like .map(), .filter(), and .sort() naturally support
> chaining because they are pure functions that return a brand-new
> array.
>
> Since the output of the first method is an array, you can immediately
> append another array method right onto it.
>
> **The Code Mechanics**

i.  const numbers =;

> // Without chaining:
>
> const evens = numbers.filter(n =\> n % 2 === 0); // Returns \[2, 4\]
>
> const doubled = evens.map(n =\> n \* 2); // Returns \[4, 8\]
>
> **Note:** Without chaining, you have to create messy temporary
> variables

ii. const numbers =;

> // With chaining:
>
> const result = numbers
>
> .filter(n =\> n % 2 === 0) // Step 1: Returns \[2, 4\]
>
> .map(n =\> n \* 2); // Step 2: Acts on, returns \[4, 8\]
>
> console.log(result); // Output: \[4, 8\]
>
> **Note:** With method chaining, you connect them directly. The output
> of .filter() becomes the input for .map()
>
> **The Rules of Chaining**
>
> To chain array methods successfully, you must pay attention to what
> each method returns:

-   Chainable Methods: Methods that return an array (e.g., .filter(),
    .map(), .sort(), .slice(), .concat()).

-   **Terminal Methods**: Methods that break the chain because they
    return something *other* than an array.

    -   .reduce() returns a single value (number, object, string).

    -   .find() returns a single element or undefined.

    -   .some() and .every() return a boolean.

    -   .forEach() returns undefined (always breaks the chain
        immediately).

Example of a Pipeline Ending in a Terminal Method

*const products = \[*

> *{ name: \'Laptop\', price: 1000, category: \'Electronics\' },*
>
> *{ name: \'Shirt\', price: 25, category: \'Clothing\' },*
>
> *{ name: \'Phone\', price: 500, category: \'Electronics\' }*
>
> *\];*
>
> *const totalElectronicsCost = products*
>
> *.filter(p =\> p.category === \'Electronics\') // Returns Array of 2
> items*
>
> *.map(p =\> p.price) // Returns Array: \[1000, 500\]*
>
> *.reduce((sum, price) =\> sum + price, 0); // Terminal: Returns Number
> 1500*
>
> *console.log(totalElectronicsCost); // Output: 1500*
>
> **Why Use It**

-   **Eliminates Noise**: Removes the need to name and store temporary,
    single-use variables.

-   **Readability**: Reads like a sentence describing data
    transformation (\"Take products, *filter* by electronics, *extract*
    the prices, then *sum* them up\").

    9.  The fundamental bug in this chain is a **misplacement of array
        methods** which destroys the data structure before it can be
        filtered.

> Here is what happens step-by-step in the broken code:

-   .map(s =\> s.score \> 60) runs first: .map() transforms every
    element. Instead of student objects, it evaluates the condition and
    returns an array of booleans: \[true, false, true, false\].

-   .filter(s =\> s.passed) runs second: It attempts to read .passed on
    those booleans (true.passed, false.passed). Since booleans do not
    have a passed property, they evaluate to undefined (falsy) \[C1\].
    The chain completely breaks here, returning an empty array \[\].

-   .map(s =\> s.name) runs third: It executes on an empty array and
    outputs \[\].

> **The Developer\'s Intention**
>
> The developer wanted to create a data pipeline to:

i.  Narrow down the list to only students who both marked passed: true
    **and** had a score \> 60.

ii. Extract just the string name values of those surviving students.

> **The Corrected Version**
>
> To fix this, you must filter the objects first while the structure is
> intact, and then map to the names last.
>
> *const students = \[*
>
> *{ name: \"Ada\", score: 85, passed: true },*
>
> *{ name: \"Ben\", score: 42, passed: false },*
>
> *{ name: \"Cara\", score: 91, passed: true },*
>
> *{ name: \"Dan\", score: 55, passed: true }, // Will be filtered out
> (score \<= 60)*
>
> *\];*
>
> *// Corrected Pipeline: Filter objects first, transform to strings
> last*
>
> *const result = students*
>
> *.filter(s =\> s.passed && s.score \> 60) // Keeps matching student
> OBJECTS*
>
> *.map(s =\> s.name); // Extracts just the names from those objects*
>
> *console.log(result);*
>
> *// Output: \[\"Ada\", \"Cara\"\]*

**Note:Why This Works**

-   **.filter()** checks the properties of the full objects and keeps
    only Ada and Cara.

-   **.map()** runs exactly twice (on Ada and Cara\'s objects) to
    cleanly extract \[\"Ada\", \"Cara\"\].

    9.  The fundamental difference between these two programming
        paradigms comes down to **how** vs. **what**:

```{=html}
<!-- -->
```
-   **Imperative Programming**: Focuses on explicitly writing out the
    step-by-step instructions. You tell the computer exactly *how* to
    achieve a result by managing loops, indices, and state changes
    manually.

-   **Declarative Programming**: Focuses on describing the desired
    outcome. You tell the computer *what* you want to achieve, leaving
    the underlying step-by-step execution to the language\'s
    abstractions (like higher-order functions).

> Side-by-Side Code Comparison:
>
> Imagine we have an array of prices and want to double only the prices
> that are over N10. Example *const prices =;*

i.  The Imperative Approach (How): Here, we manually manage an index
    > counter (i), control the loop boundaries, and explicitly mutate a
    > results array.

> *Code:*
>
> *const highPricesImperative = \[\];*
>
> *for (let i = 0; i \< prices.length; i++) {*
>
> *if (prices\[i\] \> 10) {*
>
> *highPricesImperative.push(prices\[i\] \* 2);*
>
> *}*
>
> *}*
>
> *console.log(highPricesImperative); // Output: \[24, 40\]*

ii. The Declarative Approach (What): Here, we use array higher-order
    > methods to describe the business logic pipeline directly.

> *Code:*
>
> *const highPricesDeclarative = prices*
>
> *.filter(price =\> price \> 10)*
>
> *.map(price =\> price \* 2);*
>
> *console.log(highPricesDeclarative); // Output: \[24, 40\]*

**Key Comparison Points**

  -----------------------------------------------------------------------
  Feature         Imperative Style (for loop)      Declarative Style
                                                   (filter / map)
  --------------- -------------------------------- ----------------------
  Code Focus      Implementation details           Business logic and
                  (counters, indices)              data flow

  State           Mutates external data structures Promotes
  Management      directly                         **immutability**
                                                   (returns new data)

  Readability     Low (requires reading lines to   High (reads like a
                  deduce intent)                   sentence)

  Bugs            Higher risk (off-by-one errors,  Lower risk (loop
                  infinite loops)                  mechanics are hidden
                                                   and tested)
  -----------------------------------------------------------------------

**Why Modern JavaScript Favors Declarative Code**

Professional codebases heavily prefer declarative array methods because
they provide **separation of concerns**. The JavaScript engine handles
the optimal way to iterate through the memory, while you, the developer,
only have to worry about writing the pure condition or transformation
logic.

9.  In simple terms, destructuring means \"breaking down a structure.\"
    In JavaScript, it takes a complex data structure (like a large
    object or an array) and splits it apart so you can easily pull out
    the exact pieces you want and save them directly into standard
    variables.

> **The Problem It Solves**
>
> Before destructuring, extracting data from complex objects or arrays
> required a lot of repetitive, boilerplate code.
>
> **The Old Way (Problem)**
>
> You had to manually assign every single property to a variable, one
> line at a time. This quickly became cluttered, especially when dealing
> with deeply nested API responses.
>
> *const user = { id: 101, username: \"dev_alice\", role: \"admin\" };*
>
> *// Repetitive assignment boilerplate*
>
> *const id = user.id;*
>
> *const username = user.username;*
>
> *const role = user.role;*
>
> **The New Way (Solution)**
>
> Destructuring allows you to extract all of those properties
> simultaneously in a single, clean line of code.
>
> *const user = { id: 101, username: \"dev_alice\", role: \"admin\" };*
>
> *// Destructuring unpacks properties instantly*
>
> *const { id, username, role } = user;*
>
> Key Capabilities of Destructuring

i.  Array Destructuring: Unpacks values based on their index position
    > inside the array.

> *const coordinates = \[40.7128, -74.0060\];*
>
> *// Assigns index 0 to lat, and index 1 to lng*
>
> *const \[lat, lng\] = coordinates;*

ii. Assigning Default Values: Prevents your code from crashing or
    > returning undefined if a property doesn\'t exist in the source
    > object.

> *const user = { name: \"Bob\" };*
>
> *// If role doesn\'t exist, it defaults to \"guest\"*
>
> *const { name, role = \"guest\" } = user;*

iii. Renaming Variables: Allows you to extract a property but save it
     > under a completely different variable name to avoid naming
     > conflicts.

> *const response = { data_id: 999 };*
>
> *// Extracts \'data_id\' but names the local variable \'userId\'*
>
> *const { data_id: userId } = response;*
>
> *console.log(userId); // Output: 999*

iv. Function Parameter Destructuring: You can destructure objects right
    > inside a function\'s parameter list, which is an incredibly
    > popular pattern in frameworks like React

> *// Instead of passing \'props\' and writing \'props.title\'*
>
> *function Card({ title, description }) {*
>
> *console.log(\`Title: \${title}\`);*
>
> *}*

10. Explanation of array destructuring features with code examples for
    each.

```{=html}
<!-- -->
```
i.  Basic array destructuringUnpacks values sequentially based on their
    > exact index position.

> *const rgb = \[\"red\", \"green\", \"blue\"\];*
>
> *// Matches variables to indices 0, 1, and 2*
>
> *const \[firstColor, secondColor, thirdColor\] = rgb;*
>
> *console.log(firstColor); // Output: \"red\"*
>
> *console.log(secondColor); // Output: \"green\"*

ii. Skipping Elements Using Empty Commas: Ignores specific index slots
    > by padding the pattern with empty spaces separated by commas.

> *const planets = \[\"Mercury\", \"Venus\", \"Earth\", \"Mars\"\];*
>
> *const settings = \[\"dark-mode\"\];*
>
> *// \'layout\' falls back to the default because index 1 is empty*
>
> *const \[theme, layout = \"grid\"\] = settings;*
>
> *console.log(theme); // Output: \"dark-mode\"*
>
> *console.log(layout); // Output: \"grid\"*
>
> *// Skips indices 1 and 2*
>
> *const \[closest, , , fourth\] = planets;*
>
> *console.log(closest); // Output: \"Mercury\"*
>
> *console.log(fourth); // Output: \"Mars\"*

iii. Assigning Default Values: Prevents a variable from becoming
     > undefined if the source array does not have an item at that index
     > position.

iv. Using the Rest Operator (\...): Gathers all remaining, unassigned
    > array elements and bundles them dynamically into a completely new
    > subarray.

> *const raceResults = \[\"Alice\", \"Bob\", \"Charlie\", \"David\"\];*
>
> *// Captures first place, then groups everyone else*
>
> *const \[winner, \...runnersUp\] = raceResults;*
>
> *console.log(winner); // Output: \"Alice\"*
>
> *console.log(runnersUp); // Output: \[\"Bob\", \"Charlie\",
> \"David\"\]*

v.  Swapping Two Variables: Reorders memory assignments directly by
    > aligning references inside matching array brackets, eliminating
    > the old requirement for a third temporary holding variable.

> *let playerA = \"Sword\";*
>
> *let playerB = \"Shield\";*
>
> *// Swaps the contents of both variables simultaneously*
>
> *\[playerA, playerB\] = \[playerB, playerA\];*
>
> *console.log(playerA); // Output: \"Shield\"*
>
> *console.log(playerB); // Output: \"Sword\"*

9.  Explanation of object destructuring features with code examples for
    each:

```{=html}
<!-- -->
```
i.  Basic Object Destructuring: Extracts values from an object using
    keys, assigning them to new variables with the exact same name.
    Unlike arrays, the order of properties does not matter.

> *const user = { name: \"Alice\", age: 25 };*
>
> *// Creates \'name\' and \'age\' variables automatically*
>
> *const { name, age } = user;*
>
> *console.log(name); // Output: \"Alice\"*
>
> *console.log(age); // Output: 25*

ii. **Renaming a Destructured Variable:** Uses a colon (:) to map an
    > existing object key to a completely different local variable name.
    > This is ideal for preventing naming conflicts.

> *const response = { host_id: \"srv_902\" };*
>
> *// Extracts \'host_id\' but saves it into a variable named
> \'serverID\'*
>
> *const { host_id: serverID } = response;*
>
> *console.log(serverID); // Output: \"srv_902\"*

iii. Assigning Default Values: Uses an equals sign (=) to assign a
     > fallback value if a property is completely missing or evaluates
     > to undefined inside the source object.

> *const configuration = { theme: \"dark\" };*
>
> *// \'sidebar\' defaults to true because it doesn\'t exist in the
> object*
>
> *const { theme, sidebar = true } = configuration;*
>
> *console.log(sidebar); // Output: true*

iv. Using Nested Object Destructuring: Mirrors the deep structural
    > hierarchy of the parent object to drill down and target inner
    > properties directly.

> *const employee = {*
>
> *id: 1,*
>
> *metadata: { role: \"Engineer\", shift: \"Night\" }*
>
> *};*
>
> *// Extracts \'role\' from inside the \'metadata\' sub-object*
>
> *const { metadata: { role } } = employee;*
>
> *console.log(role); // Output: \"Engineer\"*
>
> *// Note: The intermediate parent variable \'metadata\' is NOT
> created.*

v.  Combining Renaming and Default Values: Combines the colon (:) syntax
    and the equals sign (=) in a single assignment block to rename a
    property while safely providing an absolute fallback value.

> *const profile = { status: \"active\" };*
>
> *// 1. Looks for \'isAdmin\'*
>
> *// 2. Renames it to \'hasAdminPrivileges\'*
>
> *// 3. Defaults it to false because it is missing*
>
> *const { isAdmin: hasAdminPrivileges = false } = profile;*
>
> *console.log(hasAdminPrivileges); // Output: false*

9.  Function parameter destructuring means unpacking properties from an
    object (or elements from an array) directly inside the parentheses
    where a function defines its inputs.

> Instead of accepting a single object variable and unpacking it inside
> the function body, you declare exactly which properties the function
> needs right at the gate.
>
> *Code Example: displayUser*
>
> *// The user data object*
>
> *const userProfile = {*
>
> *id: 452,*
>
> *username: \"code_traveler\",*
>
> *email: \"traveler@dev.com\",*
>
> *role: \"premium\"*
>
> *};*
>
> *// Parameter Destructuring: Unpacking directly in the argument list*
>
> *function displayUser({ username, role, status = \"active\" }) {*
>
> *console.log(\`User: \${username} \| Status: \${status} \| Access:
> \${role}\`);*
>
> *}*
>
> *// Execution: Pass the full object normally*
>
> *displayUser(userProfile);*
>
> *// Output: User: code_traveler \| Status: active \| Access: premium*
>
> **Why It Is Considered a Best Practice (Advantages)**
>
> Accepting destructured parameters is vastly superior to accepting a
> full object (like function displayUser(user)) and accessing properties
> inside (user.username) for four major reasons:

i.  Self-Documenting Code (Clear Intent): The function signature acts as
    an immediate receipt of what data the function actually cares about.
    Anyone reading the code instantly knows what properties the object
    must contain without reading the entire function body.

ii. Safe Fallbacks via Default Values: You can inject default parameters
    cleanly on the fly (like status = \"active\" above). If a property
    is missing from the incoming object, your code handles it gracefully
    instead of returning undefined or crashing.

iii. Eliminates Repetitive Code: It completely cuts out the noise of
     typing a parent variable name over and over again (e.g., writing
     user.name, user.email, user.role), leading to tighter, cleaner code
     blocks.

iv. Perfect Integration with Frameworks: This pattern is the
    foundational standard for modern UI frameworks like React. React
    components natively accept an object called props, and parameter
    destructuring is how developers cleanly isolate individual values:

> *// Standard React Component pattern*
>
> *function Button({ label, onClick, disabled = false }) {*
>
> *return \<button onClick={onClick}
> disabled={disabled}\>{label}\</button\>;*
>
> *}*

10. Combining destructuring with higher-order array methods allows you
    to unpack properties directly within the callback function\'s
    parameter list. This completely skips the step of assigning
    temporary reference names to each element during iteration.

> **Code Demonstration**
>
> Here is a store inventory array used for both examples:
>
> *const inventory = \[*
>
> *{ id: 101, name: \"Wireless Mouse\", price: 25, inStock: true },*
>
> *{ id: 102, name: \"Mechanical Keyboard\", price: 120, inStock: false
> },*
>
> *{ id: 103, name: \"USB-C Cable\", price: 15, inStock: true },*
>
> *{ id: 104, name: \"4K Monitor\", price: 350, inStock: true }*
>
> *\];*

i.  Example with .map(): Instead of accepting item and returning
    > item.name, we unpack name and price directly at the parameter
    > level.

> *// Map Callback: Unpacks name and price from each item object*
>
> *const productLabels = inventory.map(({ name, price }) =\> {*
>
> *return \`\${name} - \$\${price}\`;*
>
> *});*
>
> *console.log(productLabels);*
>
> *// Output: \[\"Wireless Mouse - \$25\", \"Mechanical Keyboard -
> \$120\", \...\]*

ii. Example with .filter(): Instead of checking item.inStock and
    > item.price, we pluck inStock and price natively inside the
    > predicate signature.

> *// Filter Predicate: Unpacks price and inStock to run the condition
> checks*
>
> *const affordableAndAvailable = inventory.filter(({ price, inStock })
> =\> {*
>
> *return inStock && price \< 50;*
>
> *});*
>
> *console.log(affordableAndAvailable);*
>
> *// Output: \[ { id: 101, name: \"Wireless Mouse\", \... }, { id: 103,
> \... } \]*
>
> Why This Improves Code Readability
>
> Using destructuring inside array methods is significantly cleaner than
> using standard item.property notation for three main reasons:

-   Reduces Visual Clutter: It removes repetitive parent object prefixes
    > (item.name, item.price, item.inStock). The code focuses purely on
    > the variables holding the data, reducing noise.

-   Declares Intent Immediately: By looking at the callback parameter
    > list ({ price, inStock }), a developer scanning the pipeline
    > instantly knows exactly which properties the operation relies on
    > to execute.

-   Enables Tighter Arrow Functions: Removing the item. prefix allows
    > code to fit comfortably onto a single line. This lets you use
    > implicit returns seamlessly, making your pipelines look clean and
    > declarative:

> **Code:**
>
> *// Highly scannable production pipeline*
>
> *const cheapItems = inventory.filter(({ price }) =\> price \< 30);*

9.  The destructuring expression breaks down the data object by
    combining object destructuring, nested destructuring, and array
    destructuring with element skipping.

> Here is how the JavaScript engine reads the expression from left to
> right:

i.  **user: { \... } (Nested Object Destructuring)**: The engine targets
    the user property inside data. Because of the colon and curly
    braces, it drills directly inside without creating a user variable.

ii. **name (Basic Object Destructuring)**: Inside the user object, it
    finds the name key and extracts its value.

iii. **scores: \[first, , third\] (Nested Array Destructuring & Element
     Skipping)**: It targets the scores array inside user.

     -   first captures the item at index 0.

     -   The empty comma , , skips the item at index 1.

     -   third captures the item at index 2.

iv. address: { city } (Nested Object Destructuring): It targets the
    address object inside user. It drills straight down to extract city
    without creating an address variable.

v.  status (Basic Object Destructuring): The engine steps back out to
    the top level of the data object to extract the status property.

> **Variable Values After Execution**

-   **name** = \"Zara\" (String extracted from data.user.name)

-   **first** = 88 (Number from index 0 of data.user.scores)

-   **third** = 95 (Number from index 2 of data.user.scores)

-   **city** = \"Lagos\" (String extracted from data.user.address.city)

-   **status** = \"active\" (String extracted from data.status)

    9.  JavaScript:

> **const students = \[**
>
> **  { id: 1, name: \"Ada Okafor\",   ** **scores: \[78, 85, 90, 72\], 
> submitted: true,  track: \"Frontend\" },**
>
> **  { id: 2, name: \"Ben Musa\",     ** **scores: \[55, 60, 48, 52\], 
> submitted: true,  track: \"Backend\"  },**
>
> **  { id: 3, name: \"Cara Eze\",     ** **scores: \[92, 95, 88, 97\], 
> submitted: true,  track: \"Frontend\" },**
>
> **  { id: 4, name: \"Dan Adeyemi\",  scores: \[40, 35, 50, 45\], 
> submitted: false, track: \"Backend\"  },**
>
> **  { id: 5, name: \"Efe Obi\",      ** **scores: \[70, 75, 68, 80\], 
> submitted: true,  track: \"Frontend\" },**
>
> **  { id: 6, name: \"Fola Sule\",    ** **scores: \[88, 91, 85, 93\], 
> submitted: true,  track: \"Backend\"  },**
>
> **  { id: 7, name: \"Grace Nwosu\",  ** **scores: \[60, 55, 65, 58\], 
> submitted: true,  track: \"Frontend\" },**
>
> **  { id: 8, name: \"Hank Bello\",   ** **scores: \[30, 45, 28, 40\], 
> submitted: false, track: \"Backend\"  },**
>
> **\];**

// Helper utility function to calculate average of a scores array

const getAverage = (scores) =\> scores.reduce((sum, score) =\> sum +
score, 0) / scores.length;

/\*\*

\* 1. Filter Valid Submissions and calculate individual averages

\* Returns array of objects: { name, averageScore }

\*/

function getValidStudentAverages(studentList) {

return studentList

.filter(({ submitted }) =\> submitted)

.map(({ name, scores }) =\> ({

name,

averageScore: Number(getAverage(scores).toFixed(2))

}));

}

/\*\*

\* 2. Get students by specific track who scored above a threshold on
their FIRST assignment

\* Returns array of names

\*/

function getTopPerformersByTrack(studentList, targetTrack, threshold =
70) {

return studentList

.filter(({ track, scores: \[firstAssignment\] }) =\> track ===
targetTrack && firstAssignment \> threshold)

.map(({ name }) =\> name);

}

/\*\*

\* 3. Find the absolute top scoring student based on overall average

\* Returns a single student object or undefined

\*/

function getTopCohortStudent(studentList) {

if (studentList.length === 0) return undefined;

return studentList.reduce((topStudent, currentStudent) =\> {

const topAvg = getAverage(topStudent.scores);

const currentAvg = getAverage(currentStudent.scores);

return currentAvg \> topAvg ? currentStudent : topStudent;

});

}

/\*\*

\* 4. Generate a summary object grouped by track

\* Returns object: { Frontend: { count, avg }, Backend: { count, avg } }

\*/

function generateTrackReport(studentList) {

// First pass: Group counts and total accumulated points per track
\[C1\]

const initialData = studentList.reduce((report, { track, scores }) =\> {

if (!report\[track\]) {

report\[track\] = { count: 0, totalScoreSum: 0, totalScoreCount: 0 };

}

report\[track\].count += 1;

report\[track\].totalScoreSum += scores.reduce((sum, s) =\> sum + s, 0);

report\[track\].totalScoreCount += scores.length;

return report;

}, {});

// Second pass: Transform totals into track averages

return Object.keys(initialData).reduce((finalReport, track) =\> {

const { count, totalScoreSum, totalScoreCount } = initialData\[track\];

finalReport\[track\] = {

studentCount: count,

trackAverage: Number((totalScoreSum / totalScoreCount).toFixed(2))

};

return finalReport;

}, {});

}

// \-\-- VERIFICATION / LOGGING TO VS CODE CONSOLE \-\--

console.log(\"\-\-- Valid Student Averages \-\--\");

console.log(getValidStudentAverages(students));

console.log(\"\\n\-\-- Top Performers (Frontend \> 70 First Score)
\-\--\");

console.log(getTopPerformersByTrack(students, \"Frontend\", 70));

console.log(\"\\n\-\-- Top Cohort Student \-\--\");

const { name, scores } = getTopCohortStudent(students);

console.log(\`Highest average student: \${name} (Avg:
\${getAverage(scores)})\`);

console.log(\"\\n\-\-- Track Report Breakdown \-\--\");

console.dir(generateTrackReport(students), { depth: null });
