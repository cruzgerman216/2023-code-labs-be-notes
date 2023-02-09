# Basic Ruby - Part 2

### Methods

Methods in Ruby are blocks of reusable code that we can call on to perform an action.

To construct a method in Ruby we do as follows:

```ruby
def method_name
    # some code goes here
end
```

Say we wanted a method that just outputs "Hello," we would write it like this:

```ruby
def intro
    puts "Hello"
end
```

Then if we wanted to execute this method we would call upon it like so:

```ruby
def intro
    puts "Hello"
end
intro
intro() # either way is fine
```

If we wanted to get specific with our introductory we could add a parameter and pass arguments to it as shown:

```ruby
def intro(name)
    puts "Hello #{name}"
end

intro("Nolan")
```

We can even set default values on our parameters:

```ruby
def intro(name = "John")
    puts "Hello #{name}"
end

intro("Nolan")
intro()
```

---

### Enumerable Methods

- **`each` method:** Calling 'each' on an array will iterate through that array and will yield each element to a code block, where a task can be performed.

```ruby
students = [
  {
    name: "John",
    present: true
  },
  {
    name: "Sally",
    present: true
  },
  {
    name: "Lacy",
    present: false
  },
  {
    name: "Arnold",
    present: true
  },
  {
    name: "Harold",
    present: false
  },
]

students.each {|student| puts "Hello, #{student[:name]}"}
```

- **`each_with_index` method:** Same as the `each` method, however it will give you access to the index.

```ruby
students = [...]

students.each_with_index do |student, i|
  puts "Group 1: #{student[:name]}" if i.even?
  puts "Group 2: #{student[:name]}" if i.odd?
end
```

- In this case we have two references that we need. The first is what we refer to each individual iteration, the second is for the index.

- **`map` method:** The `map` method (also called `collect`) transforms each element from an array according to whatever block you pass to it and returns the transformed elements in a new array.

```ruby
students = [...]

new_arr = students.map do |student|
  student[:name].upcase
end
p new_arr
puts new_arr
```

- Since the `map` method returns a new array we stored it in the variable `new_arr` to its results.

- **`select` method:** The `select` method ( also called `inject` ) passes every item in an array to a block and returns a new array with only the items for which the condition you set in the block evaluated to be true.

```ruby
students = [...]

new_arr = students.select do |student|
  student[:present] == true
end
puts new_arr
p new_arr

```

- **`reduce` method:** the `reduce` method ( also called 'filter' ) is possibly the most difficult to grasp enumerable method. The idea is it reduces an array or hash down to a single object. You should use `reduce` when you want to get an output of a single value.

```ruby
numbers_to_add = [10, 15, 20, 25]

puts numbers_to_add.reduce {|sum, number| sum + number}
```

- Using the `reduce` method to add an array of numbers is very useful. `sum`, or the first reference is the `accumulator` and it is used to keep track of past changes. `number` is each value in the array.

---

### Classes

Ruby classes are a way for us to tell our program what something is. If we want an application that has books, we need to tell our application what a book is as well as what can be done to a book.

To establish a class we use the keyword `class` followed by the name of the class using title case ( also known as Pascal Case ).

```ruby
class Book

end
```

We can make a what is referred to as a class variable using `@@`.

```ruby
class Book
    @@book_count = 0
    @@book_list = []
end
```

Here we have two class variables one for the number of books and one for the list of books.

Lets let our application know that we can add books to these class variables with a class method:

```ruby
class Book
    @@book_count = 0
    @@book_list = []

    def add_book(name)
      @@book_count += 1
      @@book_list.push(name)
    end
end
```

Now lets make a method that will allow us to see how many books we have and the names of the books.

```ruby
class Book
    @@book_count = 0
    @@book_list = []

    def add_book(name)
      @@book_count += 1
      @@book_list.push(name)
    end

    def print_books
      puts "You have #{@@book_count} books"
      @@book_list.each { |book| puts book}
    end
end
```

Now we can create a book and see that it is created by creating a book instance:

```ruby
class Book
    @@book_count = 0
    @@book_list = []

    def add_book(name)
      @@book_count += 1
      @@book_list.push(name)
    end

    def print_books
      puts "You have #{@@book_count} books"
      @@book_list.each { |book| puts book}
    end
end

book_1 = Book.new()
book_1.add_book("Harry Potter")
book_1.print_books
```

Create a second instance of a book, add a new book and see what happens

```ruby
class Book
    @@book_count = 0
    @@book_list = []

    def add_book(name)
      @@book_count += 1
      @@book_list.push(name)
    end

    def print_books
      puts "You have #{@@book_count} books"
      @@book_list.each { |book| puts book}
    end
end

book_1 = Book.new()
book_1.add_book("Harry Potter")
book_1.print_books

book_2 = Book.new()
book_2.add_book("Tom Sawyer")
book_2.print_books
```

Notice that we have two instances of books, however the class variables we have are updated as one. That is how class variables work. They are variables that apply to every instance of a class. If we wanted multiple lists of books we would need to change our class variables to instance variables. For instance variables we need the `initialize` method. The initialize method is similar to the constructor in JS classes.

```ruby
class Book
    def initialize
        @book_count = 0
        @book_list = []
    end

    def add_book(name)
      @book_count += 1
      @book_list.push(name)
    end

    def print_books
      puts "You have #{@book_count} books"
      @book_list.each { |book| puts book}
    end
end

book_1 = Book.new()
book_1.add_book("Harry Potter")
book_1.print_books

book_2 = Book.new()
book_2.add_book("Tom Sawyer")
book_2.print_books
```

Instance variables are indicated by only one `@` symbol. These are specific to each instance of a class. So now we have to instances of book lists that don't conflict with each other.
<br/>
To make our book class even more accessible we can use the `attr_accessor`.

```ruby
class Book
    attr_accessor :book_count, :book_list
    def initialize
        @book_count = 0
        @book_list = []
    end

    def add_book(name)
      @book_count += 1
      @book_list.push(name)
    end

    def print_books
      puts "You have #{@book_count} books"
      @book_list.each { |book| puts book}
    end
end

book_1 = Book.new()
book_1.add_book("Harry Potter")
# book_1.print_books
puts book_1.book_list

book_2 = Book.new()
book_2.add_book("Tom Sawyer")
# book_2.print_books
puts book_2.book_list
```

The `attr_accessor` gives us quick read and write access to attributes on our classes. You can also use `attr_reader` to give only read access and `attr_writer` to give only write access.
