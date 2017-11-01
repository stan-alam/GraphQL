## Functional Elixir
:space_invader:
## Elixir Dynamic functional language

Lives in the Erlang ecosystem  with nine 9's of reliability.

**With a functional language like Elixir** you'll be able to use multicores of
the CPU** Shorter and more explicit code. **You must understand and follow core principles:**

## Immutability, functions, and declarative

**Working with Immutable Data** 

**Conventional languages use mutating shared values that require thread and lock mechanisms to
work with concurrency and parallelism.**

**Functional programming, all values created in the program are immutable**

**i.e by default each function will have a stable value**  This does not allow lock
mechanisms simplifying the parallel work. It changes everything when building software

e.g.

```Ruby

list = [1,2,3,4]
Enum.take(list, -1)
#=> [4]

list ++ [1]
# => [1,2,3,4,1]

IO.inspect list# => [1,2,3,4]

```

The list of values is immutable, no matter what operation is applied. If the list is immutable and each operation
has a safe value, it means the compiler can safely run these three lines in parallel without affecting the final
result.

The benefits of parallelism is there with just one function. The transformation for creating new values is not slow.
Elixir has smart data structures that reuse values in memory, making very operation of transformation efficient.

Ruby uses the Freeze method of Immutability. i.e. when you freeze an array you can't add anymore values or remove any either.
**You still can modify the stored objects** You can't use Freeze to create safe immutable value.


In functional programming, functions are the primary tool to build a program. You can't create a useful program without writing
or using functions. Functions receive data, complete with some operation, and return a vlaue. They are usually very short and
expressive.

## Functions are coalesced into larger functions to create a larger program. The complexity of building
## a larger application is reduced when the functions have these properties:

  **The values are immutable**

  **The function's result is only affected by the function's arguments**

  **The function doesn't generate effects beyond the value it returns**

Functions such as these are called *pure functions.* e.g.

```Ruby

add2 = fn (n) -> n + 1 end  
ad2.(3)
# => 5

```
Just like in mathematics, quite linear: It takes an input, processes it, and returns a value
Just as functions work.

Impure functions are not as predictable.

## Using values explicitly

**Functional programming always passes the values explicitly between the functions**
This allows for clean code to develop, and makes clear to the dev what the inputs and outputs are
**conventional OO languages use objects to store a state, providing methods to operate on those objects**
This means that the object's state and methods are attached to each other

If we change the object's state, the method invocation will result in a different value  


```Ruby

class MySet
  attr_reader : items

  def initialize()
    @items = []
  end

def push(item)
  items.push(item) unless items.include?(item)
end
end

set = MySet.new
set.push("apple")
puts set.items.inspect

# => ['apple']

set.push("apple")
puts set.items.inspect
# => ["apple"]

```

This shows a generation of complexity as the dependencies between methods and the states are affected by
the **object internal state.**

As software evolves the common path is for the **object to accumulate more and more internal states**
**You can see that the operation must be called from a method that belongs to the object that contains the data**
In functional programming gives the alternative : use MySet like This

```Ruby

defmodule MySet do
  defstruct items: []

  def push(set = %{items: items}, item) do
    if Enum.member?(items, item) do
    set
  else
    %{set | items: items ++ [item]}
  end
end
end

set = %MySet{}
set = MySet.push(set, "apple")
IO.inspect set.items
# => ["apple"]

set = MySet.push(set, "apple")
IO.inspect set.items
# => ["apple"]

```
**You can see that operations/methods are not attached to each other**

In Elixir the operation exists on its own. The data must be explicitly sent to the MySet.push function.
**Here the data must be sent to the function in an explicate manner.**

## Functions in Arguments

**Functions are the bread and butter of functional programming, and in functional programming, the functions themselves
can be used in the arguments and the results of functions**

```

      kermit@kermit 02 (develop) $ iex
      Erlang/OTP 19 [erts-8.1] [source-e7be63d] [64-bit] [async-threads:10] [hipe] [kernel-poll:false]

      Interactive Elixir (1.3.3) - press Ctrl+C to exit (type h() ENTER for help)
      iex(1)> Enum.map(["dogs", "cats", "gerbils"], &String.upcase/1)
      ["DOGS", "CATS", "GERBILS"]
      iex(2)>


```

It is indicated that the function called Enum.map is being executed and is being passed a list
containing the elements Dogs, cast, and gerbils, while a function called the String.upcase
uppercases all the items in the list. The result is now  a new list with uppercase elements.

**It's all about passing functions to other functions**
-----------------------------------------------------------------------------------------------------
:fish:

# Transforming values

Piping multiple functions with the pipe command (|>) which will allow you to combine multiple functions calls
and results. ---take a look see...

```Ruby

def titleize(title) do
  join_with_whitespace(
    capitalize_words(
      String.split(title)  
    )
  )
end

```

**which can be written like such**

```
def titleize(title) do
  |> String.split
  |> capitalize_words
  |> join_with_whitespace
end

```

You can see the use of pipes just like in bash. Pretty clean if you ask me.
The function *titleize* receives a title. The title will be split, transforming
a list (of words). The result is then sent to the second function. Which will be
a capitalized list of words. Then it is finally sent to the join_with_whitespace
function.


**Every building block is a function, and follow the principles of functional programming.**
e.g. Immutability helps things stay in order for concurrency


# Declarative

**Imperative programming focuses on HOW TO SOLVE A PROBLEM**

**While declarative programming such as Functional programming focuses on WHAT IS NECESSARY TO SOLVE A PROBLEM**

Declarative code requires less lines of code.

```js

var list = ["dogs", "gerbils", "hamsters"];

function upThisCase(list) {
  var newList = [];
  for (var i = 0; i < list.length; i++) {
    newList.push(list[i].toUpperCase());
    }
    return newList;
}

upThisCase(list);

// => ["DOGS", "GERBILS", "HAMSTERS"];
```

In the Imperative mindset requires a *control flow* structures like *for loop* to iterate over each element through the list
and keeping count by incrementing the i variable by each element's count.

**Functional programming in Elixir is like this**

```
    iex(2)> list = ["dogs", "gerbils", "hamster"]
    ["dogs", "gerbils", "hamster"]
    iex(3)> Enum.map(list, &String.upcase/1)
    ["DOGS", "GERBILS", "HAMSTER"]
    iex(4)>

```
This is saying that we want to map a list, applying the upcase transformation on each item.
The *map* function **builds a new collection using the result of the argument function**
This is basically the declarative approach of the previous javascript code.


## Review

      Functional programming is a paradigm. Which consists of its own ruls and design
      principles for building software. It is a different way of thinking when approaching
      a problem. **The functional paradigm focuses on building software using pure functions
      in an organized way that describes WHAT the software must do, NOT on HOW.**
