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
