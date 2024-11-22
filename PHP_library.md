# [PHP Manual](https://www.php.net/manual/en/index.php)

## Question 1
**What does PHP stand for?**

A: PHP: Hypertext Preprocessor

Explanation: PHP is a recursive acronym that stands for "PHP: Hypertext Preprocessor." It is a popular server-side scripting language designed for web development.

---

## Question 2
**PHP Server scripts are surrounded by?**

A: `<?php ... ?>`

Explanation: PHP scripts are enclosed within the tags, allowing the server to interpret and execute the code within.

---

## Question 3
**The PHP syntax is most similar to:**

A: Perl and C

Explanation: PHP's syntax closely resembles that of Perl and C, making it familiar to developers who have experience with these languages.

---

## Question 4
**Which of the following are operators in PHP?**

A: `.`, `++`, `!==`

Explanation: Operators in PHP include arithmetic, logical, and comparison operators. In this example, `.`, `++`, and `!==` are examples of commonly used operators.

---

## Question 5
**What is the output of the following?**

$x = 12; 
$y = 12 + $x++; 
echo "y = $y x = $x";

A: y = 24 x = 13
    Explanation:
    The expression $x++ increments $x after its current value is used. Thus, $y is 24 (12 + 12) and $x becomes 13.

---

## Question 6
**What value will `var_dump` show that `echo` will not show?**

**A:** NULL  
**Explanation:**  
The `var_dump` function provides detailed information about variables, including data types and values like NULL, which `echo` does not show.

---

## Question 7
**What is a correct way to add a comment in PHP?**

**A:** `/* ... */`  
**Explanation:**  
In PHP, multi-line comments are wrapped in `/* ... */`. Single-line comments can be written with `//` or `#`.

---

## Question 8
**All variables in PHP start with [_________] symbol.**

**A:** `$`  
**Explanation:**  
In PHP, all variables start with a dollar sign `$`, followed by the variable name.

---

## Question 9
**What is the value returned by: `(int) 9.9 - 1`**

**A:** 8  
**Explanation:**  
In PHP, casting `9.9` to an int results in `9`. Subtracting `1` from `9` gives `8`.

---

## Question 10
**Use the [_____] operator to test if two values are identical in both value and type.**

**A:** `===`  
**Explanation:**  
The `===` operator checks for both value and type equality. It returns true only if the values and types are identical.

---

## Question 11
**What is the value of `$x`?**

$x = 1200 + "34";

**A:** `1234`
    **Explanation:**
    PHP treats "34" as a number during addition, so 1200 + 34 results in 1234.
---

### Question 12
**In PHP you can use both single quotes (' ') and double quotes (" ") for strings.**  
**A:** True  
**Explanation:**  
PHP supports both single and double quotes for defining strings, but double quotes allow variable interpolation and escape sequences.

---

### Question 13
**PHP and HTML cannot be intermingled in the same file.**  
**A:** False  
**Explanation:**  
PHP can be embedded within HTML, allowing dynamic content generation within a webpage.

---

### Question 14
**Which escape sequences can be used in single quoted (' ') strings in PHP?**  
**A:** \', \\  
**Explanation:**  
In PHP, single-quoted strings recognize only \' for an escaped single quote and \\ for a backslash.

---

### Question 15
**You cannot run PHP files from the command line.**  
**A:** False  
**Explanation:**  
PHP can be executed from the command line using the php command, making it versatile for scripts beyond web development.

---

### Question 16
**You can run PHP files on a server.**  
**A:** True  
**Explanation:**  
PHP is commonly used as a server-side scripting language, enabling it to generate dynamic web pages on a web server.

---

### Question 17
**In PHP, variable names are case sensitive.**  
**A:** True  
**Explanation:**  
In PHP, variables are case sensitive, meaning $Var and $var are different variables.

---

### Question 18
**In PHP, function names are not case sensitive.**  
**A:** True  
**Explanation:**  
PHP function names are not case sensitive, so calling myFunction() or MyFunction() will invoke the same function.

---

### Question 1
**In PHP, arrays can either be key/value (i.e., an associative array) or indexed by integers (i.e., a linear array).**  
**A:** True  
**Explanation:**  
PHP supports two types of arrays: associative arrays (key/value pairs) and indexed arrays (using integer keys starting from 0).

---

### Question 2
**Which symbol is used to associate a key to a value in an associative array?**  
**A:** =>  
**Explanation:**  
The => symbol is used in PHP to link a key with its corresponding value in an associative array.

---

### Question 3
**Fill in the blank to echo 'Arrays':**


$stuff = array('course' => 'PHP-Intro', 'topic' => 'Arrays');
echo $stuff['topic'];

A: $stuff['topic']
    Explanation:
    To access the value 'Arrays', you refer to the key 'topic' in the associative array $stuff.
---

### Question 4
What is the output of the following code?

$stuff = array('course' => 'PHP-Intro', 'topic' => 'Arrays');
echo isset($stuff['section']);
A: False
    Explanation:
    The isset() function checks if a variable or array element exists. Since 'section' is not a key in $stuff, the result is False.

---

### Question 5
In PHP, you cannot make an array of associative arrays.
A: False
    Explanation:
    PHP allows you to create multidimensional arrays, including arrays of associative arrays, which can store complex data structures.

---

### Question 6
The [_____] function is used to rearrange an array in random order.
A: shuffle
    Explanation:
    The shuffle() function randomly reorders the elements in an array, altering the order every time it is called.

---

### Question 7
Which of these are built-in sorting functions provided by PHP?
A: asort(), sort(), ksort()
    Explanation:
    PHP offers several sorting functions:
    asort() sorts an array by its values while maintaining key association.
    sort() sorts the values without preserving keys.
    ksort() sorts an array by its keys.

---

### Question 8
What function is used to sort the array in alphabetical order of the keys?
A: ksort
    Explanation:
    ksort() sorts an array by its keys in alphabetical order while maintaining the key-value association.

---

### Question 9
What function is used to sort the values in an array and keep the keys intact?
A: asort
    Explanation:
    The asort() function sorts an array by its values while preserving the association between keys and values.

---

### Question 10
What function can be used to split a string into an array of words based on a delimiter? For instance, create a three-element array from the string 'I am great!!!'.
A: explode
    Explanation:
    The explode() function splits a string into an array based on a specified delimiter. For example, explode(' ', 'I am great!!!') would return an array with three elements: ['I', 'am', 'great!!!'].

---

### Question 11
var_dump will display the name, key/value pairs, and data types of a variable.
A: True
    Explanation:
    The var_dump() function provides a detailed output of a variable's type, value, and structure, making it useful for debugging.

---

### Question 1
Why should you use functions?
A:
Avoid repetitive code
Organize your code
Break complex code into logical chunks

    Explanation:
    Functions are crucial for avoiding code duplication, improving code organization, and splitting complex tasks into manageable pieces. These make the code easier to maintain and understand.

---

### Question 2
Which keyword defines a new function?
A: function
    Explanation:
    In PHP, the keyword function is used to define a new function, followed by the function's name and a pair of parentheses.

---

### Question 3
Return values are type-specific in PHP functions (a function only returns a value of a specified data type).
A: False
    Explanation:
    In PHP, functions are not type-specific; they can return values of any data type, including strings, integers, arrays, or objects.

---

### Question 4
What output does the following code produce?


function double($val){ 
    $val = $val * 2; 
    return $val; 
} 
$val = 15; 
$dval = double($val); 
echo "Value = $val Doubled = $dval";
A: Value = 15 Doubled = 30
    Explanation:
    The function double() takes a value, doubles it, and returns the result. The original variable $val remains unchanged at 15, while $dval holds the doubled value of 30.

---

### Question 5
Which keyword is used to use code from one PHP file in a different PHP file?
A: include
    Explanation:
    The include keyword allows you to import code from another PHP file, making it reusable and modular.

---

### Question 6
Which function prints out the internal configuration capabilities of your particular PHP installation?
A: phpinfo()
    Explanation:
    The phpinfo() function displays detailed information about the PHP environment, including extensions, version, and configuration options.

---

### Question 7
Adding an ampersand ( & ) to a function parameter indicates that you are using call by [_____] for that parameter.
A: reference
    Explanation:
    Adding an & before a parameter in a function passes the variable by reference, allowing the function to modify the original variable.

---

### Question 8
The keyword [_____] will expand the scope of a variable outside of its function.
A: global
    Explanation:
    The global keyword makes a variable accessible outside of its function scope, enabling the use of the variable within different functions.

---

### Question 9
The [_____] function is used to check if a function already exists or not.
A: function_exists
    Explanation:
    function_exists() is a PHP function that checks if a function is already defined, preventing re-declarations that could cause errors.

---

### Question 10
It is common to use uppercase and/or long names for global variables to avoid confusion or mistaken reuse.
A: True
    Explanation:
    Using uppercase or long names for global variables can help prevent naming conflicts or accidental overwriting of important data within large projects.