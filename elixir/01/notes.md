## Functional Elixir

## Elixir Dynamic functional language

Lives in the Erlang ecosystem  with nine 9's of reliability.

**With a functional language like Elixir** you'll be able to use multicores of
the CPU** Shorter and more explicit code. **You must understand and follow core principles:**

## Immutability, functions, and declarative

<span style="color:red">some **Working with Immutable Data** text</span>

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
**Here the data must be sent to the function in an explicate manner.
