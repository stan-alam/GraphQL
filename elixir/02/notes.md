## Functional programming in Elixir 02


# Syntax -- representing values

In Elixir values are anything that can represent data. Numbers of gerbils purchased,
the text in a blog post, the price of a nintendo game, the text password of a login.

This means that everything a program receives as input, or does some computation that results
in a generated value is a value.

```

iex> 500
500

```


500 here is a value. In this case it is a *Literal**. Which represent values that humans can understand.

Elixir will take the literal s and do the work to transform them into a format that machines can use.
The literal value 500 has a type of Integer. While "hello" has a type of String.t

## Executing Code to obtain results

Just like linear algebraic equations: These are expressions. The simplest expression is a value

```
iex> 20
20

```

The number 20 is an expression that evaluates to the same value that is typed/

```

iex> 1 + 1
2

```
The number 1 is a value the + is the operator acting on the values, the other value is also a 1. The result
is 2.

## Logical Expressions :
:space_invader:
logical expressions are used to create conditions to control the program flow. **Elixir has two versions of the same logical operator --e.g. the logical OR and ||**

```
Erlang/OTP 19 [erts-8.1] [source-e7be63d] [64-bit] [async-threads:10] [hipe] [kernel-poll:false]

Interactive Elixir (1.3.3) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)> nil && l
** (CompileError) iex:1: undefined function l/0
    (stdlib) lists.erl:1354: :lists.mapfoldl/3
    (stdlib) lists.erl:1355: :lists.mapfoldl/3
    (stdlib) lists.erl:1354: :lists.mapfoldl/3
    (elixir) expanding macro: Kernel.&&/2
iex(1)> true and true
true
iex(2)> not true
false
iex(3)> 1 and true
** (ArgumentError) argument error: 1

iex(3)> true and 1
1
iex(4)> nil && "Hello, Multiverse(s)"
nil
iex(5)> true && "Hello, Multiverse(s)"
"Hello, Multiverse(s)"
iex(6)> "Hello Multivers" && true     
true
iex(7)> nill || 1
** (CompileError) iex:7: undefined function nill/0
    (elixir) expanding macro: Kernel.||/2
             iex:7: (file)
iex(7)> nill || l
** (CompileError) iex:7: undefined function nill/0
    (elixir) expanding macro: Kernel.||/2
             iex:7: (file)
iex(7)> nil || 1
1
iex(8)> !nil
true
iex(9)> !"Hello Multiverse(s)"
false
iex(10)>   
```

## Binding Values in Variables

Variables are containers that hold values. Think of it as a box with a label on it. You can't see what's inside but the label name is a hint.

```
iex(10)> x = 419        
419
iex(11)> x
419
iex(12)>

```
You can run mathematical operations on these variables as much as you want. Just like in Python REPL and NodeJS repl, Ruby repl, too!
Again, just as with any language use descriptive names for variables, be verbose.

```Ruby   
total_cost = product_price * quanitity
total_distance = avg_velocity * total_time
force = mass * acceleration

```

## Creating Anonymous functions

In elixir think of functions as subprograms. THey receive an input and do some computation, and then return some type of output.
The function body contains all the expressions to do a computation. The last expression value in the function body is the functions output.

```
ex(15)> name = "Johnson"
"Johnson"
iex(16)> "Hello" <> name <> "!"
"HelloJohnson!"
iex(17)> "Hello " <> name <> "!"
"Hello Johnson!"
iex(18)> name = "Don"
"Don"
iex(19)> "Hello" <> name <>
...(19)>  
...(19)> "!"
"HelloDon!"
iex(20)> "Hello " <> name <>
...(20)> "?"
"Hello Don?"
iex(21)>

```

Here we used the <> operator to join strings with the *name* variable. To transform these expressions into a function, we should transform the *name* variable in a parameter and the string concatenation in a function body.

```
iex(21)> hello = fn name -> "Hello " <> name <> "!" end
#Function<6.52032458/1 in :erl_eval.expr/5>
iex(22)> hello.("Robert")
"Hello Robert!"
iex(23)>

```
The function is invoked when using the *dot* operator. Pass values into the parentheses.

## Anonymous functions can be invoked with different values in the arguments.

## Anonymous functions aka Lambda Functions have no global name and are bound (must be bound) to a variable to be reused.

**fn is the beginning of the function, the** *name* **is the function's parameter.** Whoever is invoking the function must provide a value for the internal variables of the function to act on aka the parameters. Calling a function you must pass the values in the same order they are defined.

**-> operator** -- which indicates the following expression will be the body of the function clause. **the function body is the expression "Hello"
<> name <> "!".** *the return value** is the value of the last expression. The above example, there's only **one** expression, so the value of that expression will returned. **end** marks the end of the function definition.

## fn/end are special forms that cannot be overwritten by the developer with any framework..marketplace

You could use the **string-interpolation** to replace **<>**

```
iex(23)> hello = fn name -> "Hello #{name}" end
#Function<6.52032458/1 in :erl_eval.expr/5>
iex(24)> hello.("SpongeBob")
"Hello SpongeBob"
iex(25)>

```
In this example all the expressions inside of the brackets in the **#{}** will be coerced into a string at runtime. e.g. You can do THis

```
  iex(25)> "1 + 1 = #{1+1}"
  "1 + 1 = 2"
  iex(26)>

```
Most Lambda functions are created on one line. You could also make them on multiline

```
iex(26)> greetings = fn name ->
...(26)> greetings = "Hello #{name}"
...(26)> "#{greetings}! you must be  #{name}"
...(26)> end
#Function<6.52032458/1 in :erl_eval.expr/5>
iex(27)> greetings.("Georgie")
"Hello Georgie! you must be  Georgie"
iex(28)>

```

**creating functions without args**

You can create functions without args. You will have to admit them.

```
Interactive Elixir (1.3.3) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)> one_plus_one = fn -> 1 + 1 end
#Function<20.52032458/0 in :erl_eval.expr/5>
iex(2)> one_plus_one.()
2
iex(3)>


```

We can create functions with more than one argument. We will need to seperate them with commas.

e.g

```

iex(3)> total_price = fn price, quantity -> price * quantity end
#Function<12.52032458/2 in :erl_eval.expr/5>
iex(4)> total_price.(5, 6)
30
iex(5)>


```

Elixir has a limit of 255 characters that it will accept as a function parameter Just like JS. **keep the number of parameters below 5**
If you find yourself having to use 5 + n parameters, you should try using a data structures -- like tuples, lists, structs, or maps or most likely you just need to split your function up. Stay modular.

## Functions as First-Class-Citizens

Functions are first class citizens does not mean they get to fly first class. It means that are like any value. It's an important feature that comes from **lambda calculus.**

In IEX functions are values of **type** function. We will build a function like so :

```

iex(5)> total_price = fn price, fee -> price + fee.(price) end
#Function<12.52032458/2 in :erl_eval.expr/5>
iex(6)>

```

Here the function *total_price* receives two arguments. The first function is a number that will represent the price. **The** *tax* **parameter expects a function. We will call the given function, passing the price. The final result of the function is the result of the price plus the result of the tax function. Do you follow?**
