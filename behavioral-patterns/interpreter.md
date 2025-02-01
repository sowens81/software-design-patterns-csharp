# Interpreter Pattern

## Overview

The **Interpreter** pattern defines a grammar for interpreting sentences in a language and provides an interpreter to interpret sentences. This pattern is used for designing interpreters for languages or expressions.

## When to Use

- When you have a language or expression that can be interpreted and executed.
- When you want to design a language interpreter or parser.
- When you need to represent sentences or commands in a structured format.

## Problem it Solves

Without the **Interpreter** pattern, parsing and interpreting complex expressions can be difficult and error-prone. The **Interpreter** pattern allows you to define the grammar of a language and how sentences in that language should be interpreted.

## Solution

The **Interpreter** pattern provides an interpreter class that evaluates expressions according to the grammar of the language. It can be used to interpret sentences or commands in a specific language or syntax.

## C# Code Example

``` C#
public interface IExpression
{
    int Interpret();
}

public class Number : IExpression
{
    private int _number;

    public Number(int number)
    {
        _number = number;
    }

    public int Interpret() => _number;
}

public class Add : IExpression
{
    private IExpression _left;
    private IExpression _right;

    public Add(IExpression left, IExpression right)
    {
        _left = left;
        _right = right;
    }

    public int Interpret() => _left.Interpret() + _right.Interpret();
}
```

## Visual Example

Imagine an **expression evaluator** that evaluates simple arithmetic expressions like "5 + 3". The **Interpreter** pattern can be used to interpret the components of this expression: numbers and operators. 

Each component (e.g., number, addition) can be implemented as an interpreter object, and the **Interpreter** pattern allows you to evaluate the expression by interpreting the components in sequence.

## Benefits

- **Easy to extend**: New expressions or operations can be added easily.
- **Structured representation**: Expressions are represented in a structured format that is easy to interpret.
