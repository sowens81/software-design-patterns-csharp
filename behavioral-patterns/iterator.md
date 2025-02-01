# Iterator Pattern

## Overview

The **Iterator** pattern provides a way to access elements of a collection sequentially without exposing the underlying structure. It allows for traversal of a collection without the need for the client to know the internal details of the collection.

## When to Use

- When you need to iterate over a collection without exposing its internal representation.
- When you want to provide a way to traverse collections without using indices or explicit loops.
- When you need to support different traversal types (e.g., forward, reverse) for collections.

## Problem it Solves

Without the **Iterator** pattern, traversing a collection could expose the internal structure of the collection to the client. This can make the code more difficult to maintain. The **Iterator** pattern hides the complexity of traversing the collection and provides a uniform way to iterate over it.

## Solution

The **Iterator** pattern defines an iterator object that provides a way to traverse the collection. The client interacts with the iterator, which manages the traversal logic internally.

## C# Code Example

%%%
public interface IIterator
{
    bool HasNext();
    object Next();
}

public class ConcreteIterator : IIterator
{
    private readonly List<string> _items;
    private int _position = 0;

    public ConcreteIterator(List<string> items)
    {
        _items = items;
    }

    public bool HasNext() => _position < _items.Count;

    public object Next() => _items[_position++];
}

public class Collection
{
    private List<string> _items = new List<string>();

    public void AddItem(string item)
    {
        _items.Add(item);
    }

    public IIterator CreateIterator() => new ConcreteIterator(_items);
}
%%%

## Visual Example

Consider a **book collection** where you want to iterate over all books in the collection. The **Iterator** pattern can be used to traverse the books sequentially, without exposing the internal list structure.

The **Iterator** pattern allows you to create different types of iterators (e.g., forward or reverse) and helps manage the iteration logic.

## Benefits

- **Separation of concerns**: The client doesn’t need to know about the internal structure of the collection.
- **Flexibility**: Different types of iteration can be supported.
