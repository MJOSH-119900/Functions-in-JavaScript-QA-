**Higher-Order Functions, Array Methods & Destructuring**

**Section A:** Higher-Order Functions

Question 1

What is a Higher-Order Function? How does it differ from a regular function?

Question 2

What does it mean for functions to be "first-class citizens" in JavaScript?

Question 3

What is a callback function? How is it different from a regular function call?

Explain the concept of callbacks, describe when and why you would use one, and write an example where you:

1.  Define a named callback function
2.  Pass it to another function
3.  Invoke it from inside that outer function

Question 4

Explain the concept of closures and how they relate to higher-order functions.

Define what a closure is, explain why it is useful, and demonstrate with a code example of a function factory a higher-order function that returns a new function which "remembers" a value from its outer scope.

Question 5

What is the difference between synchronous and asynchronous callbacks?

Question 6

Analyse the following code and explain what happens step by step:

function applyTwice(fn, value) {

&nbsp; return fn(fn(value));

}

const addThree = x => x + 3;

console.log(applyTwice(addThree, 10));

In your answer:

1.  Trace through each line of execution
2.  State what the final output is and why
3.  Explain what concept(s) of higher-order functions this demonstrates

Question 7

What is function composition? Why is it considered a powerful pattern in functional programming?

Define function composition, explain its benefits (reusability, readability, separation of concerns), and write a compose function that takes two functions and returns a new function that applies them in sequence:

function compose(f, g) {

&nbsp; // your implementation

}

const double = x => x \* 2;

const addOne = x => x + 1;

const doubleThenAddOne = compose(addOne, double);

console.log(doubleThenAddOne(5)); // Should output 11

Question 8

Compare and contrast the following three approaches to writing a function that filters an array of numbers to keep only even numbers:

// Approach A — Traditional for loop

function getEvensA(numbers) {

&nbsp; const result = \[\];

&nbsp; for (let i = 0; i < numbers.length; i++) {

&nbsp;   if (numbers\[i\] % 2 === 0) result.push(numbers\[i\]);

&nbsp; }

&nbsp; return result;

}

// Approach B — forEach

function getEvensB(numbers) {

&nbsp; const result = \[\];

&nbsp; numbers.forEach(n => {

&nbsp;   if (n % 2 === 0) result.push(n);

&nbsp; });

&nbsp; return result;

}

// Approach C — filter

function getEvensC(numbers) {

&nbsp; return numbers.filter(n => n % 2 === 0);

}

Discuss readability, intent, immutability, and which approach you would recommend in a professional codebase and why.

Question 9

What are some real-world use cases of higher-order functions outside of array methods?

Identify and explain at least four real-world scenarios where higher-order functions are used. For each one, give a brief code example. Consider areas like:

- Event handling in the browser
- Middleware in web frameworks
- Validation logic
- Memoization or caching

Question 10

Explain the map() method. What does it do, what does it return, and when should you use it?

Question 11

Explain the filter() method and how it differs from map().

Question 12

Explain the reduce() method in detail.

Question 13

What is the difference between find() and filter()?

Question 14

Explain some() and every(). What problem does each solve?

Question 15

What is the difference between forEach() and map()? When should you use each one?

Question 16

What is method chaining? How does it work with array methods?

Question 17

Analyse the following code. Identify any bugs, explain what the developer intended, and write a corrected version:

const students = \[

&nbsp; { name: "Ada", score: 85, passed: true },

&nbsp; { name: "Ben", score: 42, passed: false },

&nbsp; { name: "Cara", score: 91, passed: true },

&nbsp; { name: "Dan", score: 55, passed: true },

\];

// Intent: Get the names of students who passed with a score above 60

const result = students

&nbsp; .map(s => s.score > 60)

&nbsp; .filter(s => s.passed)

&nbsp; .map(s => s.name);

console.log(result);

Question 18

Compare imperative and declarative programming styles using array methods as examples.

Section C: Destructuring

Question 19

What is destructuring in JavaScript? What problem does it solve?

Question 20

Explain the following array destructuring features with code examples for each:

1.  Basic array destructuring
2.  Skipping elements using empty commas
3.  Assigning default values
4.  Using the rest operator (...) to collect remaining elements
5.  Swapping two variables without a temporary variable

Question 21

Explain the following object destructuring features with code examples for each:

1.  Basic object destructuring
2.  Renaming a destructured variable
3.  Assigning default values
4.  Nested object destructuring
5.  Combining renaming and default values in the same expression

Question 22

What is destructuring in function parameters? Why is it considered a best practice?

Explain how you can destructure directly in a function's parameter list. Write a function displayUser that accepts a user object and uses parameter destructuring. Then explain the advantages of this pattern over accepting the full object and accessing properties inside the function body.

Question 23

How does destructuring work with array methods? Explain and demonstrate with two examples.

Show how destructuring can be combined with:

1.  map() — destructuring each object inside the map callback to make the transformation cleaner
2.  filter() — destructuring in the filter predicate

Then explain how this combination improves code readability compared to using item.property notation repeatedly.

Question 24

Analyse this code. Explain what each destructuring line does and what the values of all variables will be after execution:

const data = {

&nbsp; user: {

&nbsp;   id: 101,

&nbsp;   name: "Zara",

&nbsp;   scores: \[88, 76, 95, 62\],

&nbsp;   address: {

&nbsp;     city: "Lagos",

&nbsp;     country: "Nigeria"

&nbsp;   }

&nbsp; },

&nbsp; status: "active"

};

const { user: { name, scores: \[first, , third\], address: { city } }, status } = data;

console.log(name);

console.log(first);

console.log(third);

console.log(city);

console.log(status);

Walk through the destructuring expression step by step, naming every pattern being used.

**Project 1:** Student Grade Analyzer

**Background**

You have been given a dataset of students from a bootcamp cohort. Your task is to build a grade analyzer that processes this data and produces meaningful reports.

**Dataset**

Use the following dataset exactly as provided:

const students = \[

&nbsp; { id: 1, name: "Ada Okafor",    scores: \[78, 85, 90, 72\],  submitted: true,  track: "Frontend" },

&nbsp; { id: 2, name: "Ben Musa",      scores: \[55, 60, 48, 52\],  submitted: true,  track: "Backend"  },

&nbsp; { id: 3, name: "Cara Eze",      scores: \[92, 95, 88, 97\],  submitted: true,  track: "Frontend" },

&nbsp; { id: 4, name: "Dan Adeyemi",   scores: \[40, 35, 50, 45\],  submitted: false, track: "Backend"  },

&nbsp; { id: 5, name: "Efe Obi",       scores: \[70, 75, 68, 80\],  submitted: true,  track: "Frontend" },

&nbsp; { id: 6, name: "Fola Sule",     scores: \[88, 91, 85, 93\],  submitted: true,  track: "Backend"  },

&nbsp; { id: 7, name: "Grace Nwosu",   scores: \[60, 55, 65, 58\],  submitted: true,  track: "Frontend" },

&nbsp; { id: 8, name: "Hank Bello",    scores: \[30, 45, 28, 40\],  submitted: false, track: "Backend"  },

\];

Requirements

Implement each of the following as a separate named function. Each function must use the array methods and destructuring techniques taught in this course, no plain for loops allowed.

1\. calculateAverage(student) Accepts a student object. Destructure the scores array from it. Return the student's average score rounded to 2 decimal places.

2\. classifyGrade(average) Accepts a number and returns a letter grade:

- 70 and above → "Pass"
- 50–69 → "Borderline"
- Below 50 → "Fail"

3\. getFullReport(students) Uses map() to transform the students array. For each student, return a new object with:

- name (destructured from the student)
- track (destructured from the student)
- average (from calculateAverage)
- grade (from classifyGrade)
- submitted (destructured from the student)

4\. getTopStudents(students) Returns only students with an average score of 70 or above, using filter(). The result should be a transformed array (using map()) containing only name and average.

5\. getTrackSummary(students) Uses reduce() to group students by track. Return an object shaped like:

{

&nbsp; Frontend: { count: 0, totalAverage: 0, averageScore: 0 },

&nbsp; Backend:  { count: 0, totalAverage: 0, averageScore: 0 }

}

6\. hasFailingStudents(students) Uses some() to return true if any student has an average below 50.

7\. allSubmitted(students) Uses every() to return true only if every student has submitted: true.

8\. findStudent(students, id) Uses find() to locate and return a student object by their id. If not found, return null.

**Project 2:** E-Commerce Cart System

**Background**

You are building the data-processing logic for a small e-commerce cart system. There is no UI, just JavaScript functions that work with a cart dataset and return computed results.

**Dataset**

const products = \[

&nbsp; { id: "p1", name: "Wireless Mouse",     category: "Electronics", price: 25.99,  inStock: true  },

&nbsp; { id: "p2", name: "Mechanical Keyboard", category: "Electronics", price: 89.99,  inStock: true  },

&nbsp; { id: "p3", name: "Desk Lamp",           category: "Office",      price: 34.50,  inStock: false },

&nbsp; { id: "p4", name: "Notebook (A5)",       category: "Stationery",  price: 4.99,   inStock: true  },

&nbsp; { id: "p5", name: "USB-C Hub",           category: "Electronics", price: 49.00,  inStock: true  },

&nbsp; { id: "p6", name: "Ergonomic Chair",     category: "Office",      price: 299.00, inStock: true  },

&nbsp; { id: "p7", name: "Ballpoint Pens x10",  category: "Stationery",  price: 3.49,   inStock: true  },

&nbsp; { id: "p8", name: "Monitor Stand",       category: "Office",      price: 55.00,  inStock: false },

\];

const cart = \[

&nbsp; { productId: "p1", quantity: 2 },

&nbsp; { productId: "p2", quantity: 1 },

&nbsp; { productId: "p4", quantity: 5 },

&nbsp; { productId: "p6", quantity: 1 },

\];

Requirements

1\. getAvailableProducts(products) Returns only products where inStock is true. Use filter() and destructure inStock in the callback.

2\. getProductsByCategory(products, category) Returns all products matching the given category. Use filter().

3\. applyDiscount(discountPercent) A higher-order function (function factory) that takes a discount percentage and returns a new function. That returned function accepts a product object and returns a new product object with the discounted price included:

const apply10Percent = applyDiscount(10);

const discountedProducts = products.map(apply10Percent);

4\. buildCartItems(cart, products) Uses map() to enrich each cart item. For each item in cart, find the matching product (using find()) and return a new object containing:

- name (from product)
- category (from product)
- price (from product)
- quantity (from cart item)
- lineTotal (price × quantity)

Use destructuring when extracting values from both the cart item and the product.

5\. getCartSummary(cartItems) Uses reduce() to return a summary object:

{

&nbsp; totalItems: 9,       // sum of all quantities

&nbsp; totalCost: 399.94,   // sum of all lineTotals

&nbsp; averageItemPrice: 0  // totalCost / totalItems

}

6\. groupByCategory(cartItems) Uses reduce() to group the enriched cart items by category. Return an object where keys are category names and values are arrays of cart items in that category.

7\. createPriceSorter(order) A higher-order function that accepts "asc" or "desc" and returns a comparator function suitable for use with .sort():

const sortAsc  = createPriceSorter("asc");

const sortDesc = createPriceSorter("desc");

const cheapFirst     = \[...products\].sort(sortAsc);

const expensiveFirst = \[...products\].sort(sortDesc);

8\. processCart(cart, products, discountPercent) A pipeline function that:

1.  Builds the enriched cart items using buildCartItems()
2.  Applies the discount using applyDiscount() and map()
3.  Returns both the enriched items and the cart summary