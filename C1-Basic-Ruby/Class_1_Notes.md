# Basic Ruby - Part 1

### Terms:

- **Data Types:** Data types in programming are ways to define different types of data. A data type is also a piece of information that tells how the computer should interpret it. Each data type is used in a different manner.
- **Console:** A console application is a program which runs in an command prompt window. Console programs do not have the flash, nor the event-driven capabilities of a Windows application, however, they still have their place. For example, where screen space is limited such as a bank ATM, or a device with a very simple display type.

## Ruby Data Types

---

### Strings

A string is a certain data type and is characterized by text. They are grouped by characters that can represent sentences and words. In order to define a string, you would need to use single quotes or double quotes around the text.

```ruby
    "This is an example of a string!"
```

There are a couple reasons to go with double quotes rather than single quotes. Double quotes allow for the use of apostrophes ans string interpolation. Single quotes do not. Here are a couple examples:

```ruby
    "This string isn't using single quotes" # Correct
    'This string isn't using double quotes' # incorrect
```

**String Concatenation:** String Concatenation is when you combine two strings using the '+' operator.

```ruby
    "This" + " is a string!" # "This is a string!"
```

---

### Numbers

A number represents a range of digits. There are two types of Numbers: integers and floats. An integer is a whole number (no decimal) whereas floats have a decimal place. Numbers and mathematical calculations go hand and hand.

```ruby
    1 # Integer
    1.1 # Float
    3.0 # Float
```

---

### Boolean

A boolean represents a unique value that is either true and false. We use booleans to solve problems that need logical solutions. We will explore booleans more when we talk about conditionals in the next class.

```ruby
   true
   false
```

---

### Hashes

A hash is a series of unique key-value pairs (Very similar to a JS object). In order to access a value, square brackets are needed [] after the hash. In between the square brackets, include the name of the key as a symbol.

The original syntax of a hash is as follows:

```ruby
    {:name => "Nolan Hovis", :age => 59}
```

The new (much prettier) way of writing hashes:

```ruby
    {name: "Nolan Hovis", age: 59}
```

**Accessing Data:**
Access data in a hash using keys like so:

```ruby
    {name: "Nolan Hovis", age: 59}[:name] # "Nolan Hovis"
```

---

### Symbols

Symbols are referred to as variable names in replacement to strings for higher performance rates. In order to define a symbol, use a colon :. Refer to hashes and the use of symbols to access values.

```ruby
    :this_is_a_sym
```

---

### Arrays

An array is a list of data enclosed in square brackets []. Each list item or element is separated by a comma ,. An array can hold different amounts of data types. Here is an example:

```ruby
    [1, "string", true, [], {hello: "world"}]
```

Getting access to array items:

```ruby
    [1, "string", true, [], {hello: "world"}][0] # 1
```

---

### Printing to the Console

Printing to the console is useful in many ways. We can use it to see values of certain code, to communicate to a use(In a console based program), etc. There are three ways in Ruby to print to the console:

- `puts`
- `print`
- `p`

```ruby
    puts "Hello World!" # prints to console with a new line
    p "Hello World!" # prints to the console with a new line
    print "Hello World!" # Prints to console without new line
```

#### Subtle differences between 'puts' and 'p':

- When printing an array:
  - 'p' will print the array object
  - 'puts' will iterate through the values

```ruby
    puts [1, 2, 3, 4]
    # 1
    # 2
    # 3
    # 4
    p [1, 2, 3, 4] # [1, 2, 3, 4]
```

---

### Variables

A variable contains data. Technically, the name of a variable references a specific memory location that contains data. To store a value in this memory location, we use the = sign. Keep in mind, whenever we store data in our computer's memory as the program runs, it is only temporary data. So when the program ends, the temporary data goes away.

```ruby
    message = "Hello, fellow coders!"
    puts message # "Hello, fellow coders!"
```

**Constant Variables**
In certain use cases, we like to make sure the value the variable contains will not change. To create this constraint, we can create what is called a constant variable. To create a constant variable, the variable name will be all uppercase. In case we accidentally change the value of this key, it will result in an error when compiled.

```ruby
    API_KEY = "ABC123"
    API_KEY = "fjdksla" # Error
```

---

### Naming Conventions

In the Frontend section we used `camelCase`. That is the standard for JS. The standard for ruby is called `snake_case`. This is where underscores are placed between each word like so:

```ruby
    this_is_a_variable = "using snake case"
```

---

### String Expressions and Methods

**String Concatenation:**

```ruby
    name = "Nolan"
    puts name + " " + "Hovis" # "Nolan Hovis
```

**String Interpolation:**

```ruby
name = "Nolan"
puts "#{name} Hovis" # "Nolan Hovis"
puts '#{name} Hovis' # "#{name} Hovis"
# Single Quotes do not support string interpolation
```

**String Methods:**

Strings have what are called built-in Ruby methods and belong to the string class. A class is a template for objects. An object has what are called attributes and methods. Any string created has access to "instance methods" in the String class.

```ruby
    message = "Hello"
    puts message.class # String
    puts message.length # 5
```

Sometimes you'll see a method that ends in a '?'. These are called predicate methods. They result in a boolean (true, false).

```ruby
    puts "Hello".empty? # false
    puts "".empty? # true
```

---

### Getting User Input

Getting user input allows us to receive data from our user for our application to use.

```ruby
    puts "What is your middle name?"
    middle_name = gets.chomp
    puts "Your middle name is #{middle_name}."
```

---

### Operators

Operators in ruby work very similar to the way they do in JS. They work as follows:

```ruby
    # Addition
    puts 1 + 1 # 2
    # Subtraction
    puts 1 - 1 # 0
    # Multiplication
    puts 2 * 2 # 4
    # Division
    puts 10 / 5 # 2
    # Modulus (Remainder)
    puts 11 % 5 # 1
    # Exponent
    puts 4 ** 3 # 64
```

**PEMDAS**
PEMDAS is an acronym that stands for Parentheses Exponent Multiplication Division Addition Subtraction. PEMDAS is a way to explain the order of operations when multiple operators are used in the same line. The same logic that applies in math applies in Ruby programming (and in most programming languages) as well.

```ruby
    puts (4 - 4 * 2 / 4) + 10 # 12
```

---

### Conditional Logic

**If Statements:**
If statements work the same as they do in JS. You set a condition, that if returned true, it runs a certain block of code.

Example:

```ruby
    # Shorthand
    name = "nolan"
    puts "Your name is #{name}" if name == "nolan"

```

```ruby
    # Longhand
    name = "nolan"
    if name == "nolan"
        puts "Your name is #{name}"
    end
```

You can add multiple conditions with `elsif`:

```ruby
    num = 2
    if num > 2
        puts "#{num} is greater than 2"
    elsif num < 2
        puts "#{num} is less than 2"
    else
        puts "#{num} is equal to 2"
    end
```

**Unless Statement**
The `unless` statement is similar to the `if` statement, however it will run the block of code if the condition is false.

Example:

```ruby
    # Shorthand
    num = 2
    puts "#{num} is not 2" unless num == 2
```

```ruby
    # Longhand
    num = 2
    unless num == 2
        puts "#{num} is not 2"
    end
```

`Unless` statements can only have an `else`. Their is no `unlelse` lol. However it isn't typical that you have an else with `unless` statements.

**Comparison Operators:** Comparison Operators are used to compare two values and result in a boolean.

```ruby
    1 == 1 # true
    1 != 1 # false
    1 > 0 # true
    1 < 0 # false
    3 >= 3 # true
    3 <= 3 # true
    3 <=> # 0
```

- **`==`:** Checks if the values are equal, not assigning value.
- **`!=`:** Checks if the values are not equal.
- **`>`:** Checks if value on the left is greater than the value on the right.
- **`<`:** Checks if value on the left is less than the value on the right.
- **`>=`:** Checks if value on the left is greater than or equal to the value on the right.
- **`<=`:** Checks if value on the left is less than or equal to the value on the right.
- **`<=>`:** This is called the spaceship operator. If the left value is less than the right value it returns `-1`. If they are equal it returns `0`. If the left value is greater than the right value it returns `1`.

**Logical Operators:**
Logical Operators help us get customize our conditions.

Example:

```ruby
    user = {
    name: 'Nolan',
    is_the_best: false
    }
    if user[:name] == 'Nolan' && user[:is_the_best] == true
    puts "#{user[:name]} is the best :)"
    elsif user[:name] == 'Nolan' && user[:is_the_best] == false
    puts "#{user[:name]} is not the best :("
    end
```

```ruby
    user = [{
    name: 'Nolan',
    is_the_best: false
    },
    {
    name: 'John',
    is_the_best: true
    }]
    if user[0][:name] == 'Nolan' || user[:is_the_best] == true
    puts "#{user[0][:name]} is the best :)"
    elsif user[0][:name] == 'Nolan' || user[:is_the_best] == false
    puts "#{user[0][:name]} is not the best :("
    end
```

**`&&`:** The 'and' operator makes it to where both, or all, conditions must be true for the whole expression to return true
**`||`:** The 'or' operator makes it to where only one condition in the whole expression needs to be true for the whole expression to be true.

**Ternary Operator:**
The ternary operator works with booleans. It is used to give specific value based on the condition of the boolean

example:

```ruby
is_cool = false
puts is_cool ? "You are so cool" : "You are not cool at all"
```

This will print "You are so cool" if `is_cool` is true, if `is_cool` is false it will print "you are not cool at all."

### Loops

Loops help us iterate through objects, arrays, and perform action repetitively.

- **Generic Loop:**
  example:

```ruby
    i = 0
    loop do
        puts i
        i += 1
        break if i > 10
    end
```

This will loop through displaying the value of `i` until `i` is equal to 10.
If we do not have a `break` case we will create an infinite loop that will crash our program. You always want a break case that will be met. The rest of the loops help us not to forget because they are required to write them in.

- **While Loop:**
  example:

```ruby
i = 0
while i < 10 do
    puts i
    i += 1
end
```

A `while` loop will run while a condition is true.

- **Unless Loop:**
  example:

```ruby
i = 0
until i > 10 do
    puts i
    i += 1
end
```

An `until` loop will run while a condition is false.

- **For Loop:**
  A `for` loop is good when we want to iterate over, for example, an array.

example:

```ruby
a = [1, 2, 3, 4]
for num in a do
  puts num
end
```

A `for` loop requires you to make a reference to each parameter as it loops inside an array. The break case is when it reaches the last item in the array.

### Check your learning

- What is the main difference between `p` and `puts`?
- What are methods that end with a '?' called in ruby?
- What is a hash?
- How do you access data on a hash?
- What is the difference between `if` and ``unless`?
- What is the difference between `&&` and ``||`?
- What is the difference between `while` loops and `until` loops?
