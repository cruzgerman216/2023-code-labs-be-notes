# Ruby Exercises - Part 1

## READ BEFORE STARTING

**Use Git or GitHub Desktop to commit each exercise to GitHub** <br>

**Use a cloud based service or an IDE**<br>

**Exercise 1.0: Ruby basics**

- Create a file called exercise-1.0.rb. 
- Print out the following data types in the console: number, string, boolean, hash, array and symbol
- Demonstrate the following mathematical operators: addition, subtraction, division, multiplication, exponent and modulus
- Use Concatenation to join the three following strings: "This is ", "an example of ", and "concatenation".
- Print the seventh character of "abcdefghijklmnopqrstuvwxyz".
- The overall distance that is covered over time is called average speed. Considering the formula s = d/t, s being the average, d being the total distance traveled and t being the total time taken. Declare variables d and t and set them to 30 and 10 respectively. Declare a variable called s and set that to average speed using the formula and the declared variables d and t.
- Demonstrate the ternary operator
- Give an example of the following operators: =, ==, !=, <, >, <= ,>=
- Give an example of the following operators: ||, &&
- Declare a variable called age. if age is less than 30, print "I am __INSERT_AGE_VARIABLE__ years old".

**Exercise 1.1: Print to the console** <br>
- Create a file named exercise-1.1.rb and use the p method to print the string "p" to the console.
- Use the puts method to print the string "puts" to the console.
- Use the print method to print the string "print" to the console.
- Declare a variable called my_name and assign it your name. Print the value of my_name to the console.
- Declare a variable called beginning_sentence and assign it the string "My name is ". Declare another variable called full_sentence and assign it the combination of beginning_sentence and my_name using the + operator. Print full_sentence to the console.

Result: 

``` 
> "p"
> puts
> My name is John.
```
**Exercise 1.2: Use escaping to output single quotes in a string** <br>
Create a ruby file called exercise-1.2.rb. 

- Output `'Single Quotes' is actually my favorite movie. It's great.` to the console (hint: backslashes)

**Exercise 1.3: Print out user input** <br>
Create a ruby file called exercise-1.3.rb. 

- Use `gets.chomp` to get the user input, then store it in a variable called user_input. Print into the console "You typed: " follow by what the user entered.
- Define a method named multiply_by_two with one parameter. Get the user input and use the method you defined to multiply that number by 2. Print the result.
- Define a method named divide_by_two with one parameter. Take in a user input and store and divide that value by two using divided_by_two. Print the result.

Result:
```
> Please enter a sentence: 
> I enjoy coding!
> You have typed 'I enjoy coding!'
> What number do you want to multiply by two?
> 5
> 5 multiplied by 2 is 10
> What number do you want to divide by two?
> 10
> 10 divided by 2 is 5
```

**Exercise 1.4: if/else Conditionals** <br>
Create a Ruby file called exercise-1.4.rb. 

1. Print out `What is your name?`. Get user input and store the input in a variable called name.
2. Use an `if` statement to see if the name entered by the user is "john". If so, print out `I found you!`.
3. Use an `else` statement to print out `You're not who I'm looking for ` follow by the name the user entered.
4. Use the built in string method `downcase` to downcase all letters of the user input in case the user enters `JoHn`.
5. Change the print statement to `What is your first name?` Store user input in a variable. Add another print statement, `What is your last name?`. Store user input in a variable. Use the `if` statement to check to see if the first name is `john` and last name is `doe`. 
6. Add an `elsif` statement to check if the first name and last name equate to `amy jeans`. If so, print `Amy! Help me look for John Doe.`

**Exercise 1.5: Printing user data**<br>
Create a Ruby file called exercise-1.5.rb.

Given the array of hashes:

```ruby 
users = [
    {
        name: "John Doe",
        age: 43
    },
    {
        name: "Amy Singer",
        age: 53
    },
    {
        name: "Jimmy Lendricks",
        age: 23
    }
]
```

Use a `while` loop to print the values of each hash such as "My name is ... and I am ...". If the first name starts with "Jimmy", print out "My name and age is confidential."

expected output: 
```
> My name is John Doe and I am 43.
> My name is Amy Singer and I am 54.
> My name and age is confidential.
```
**Exercise 1.6: Nested Loops** <br>
Create a Ruby file called exercise-1.6.rb.

Given the value: <br>
```
[[1,2,3],[[[4,5,6]]]]
```

Print each number in order. 

expected output: 

```
> 1
> 2
> 3
> 4
> 5
> 6

```
---


## Practice The Technical Interview
*Keep in mind, your skill level for solving algorithm challenges is separate from your skills in developing applications. In technical interviews, you may be told to solve these commonly used code challenges.*


**FizzBuzz** <br> 

Write a program that prints the numbers from 1 to 100.
But for multiples of three print “Fizz” instead of the
number and for the multiples of five print “Buzz”. For
numbers which are multiples of both three and five
print “FizzBuzz”.

**Valid Paranthesis ([leetcode](https://leetcode.com/problems/valid-parentheses/))** <br>

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.

Example 1: <br>

Input: s = "()" <br>
Output: true <br>

Example 2: <br>

Input: s = "()[]{}"  <br>
Output: true <br>

Example 3: <br>

Input: s = "(]" <br>
Output: false <br>

**Roman to Integer ([leetcode](https://leetcode.com/problems/roman-to-integer/))** <br>

Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.

```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```
For example, 2 is written as II in Roman numeral, just two one's added together. 12 is written as XII, which is simply X + II. The number 27 is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

I can be placed before V (5) and X (10) to make 4 and 9. 
X can be placed before L (50) and C (100) to make 40 and 90. 
C can be placed before D (500) and M (1000) to make 400 and 900.
Given a roman numeral, convert it to an integer.


Example 1:

```
Input: s = "III"
Output: 3
Explanation: III = 3.
```

Example 2:

```
Input: s = "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
```
Example 3:

```
Input: s = "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```
