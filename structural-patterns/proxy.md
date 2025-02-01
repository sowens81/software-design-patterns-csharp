# Proxy Pattern

## Overview

The **Proxy** pattern provides a surrogate or placeholder for another object to control access to it. It is used when you want to control access to an object by adding an additional level of indirection.

## When to Use

- When you want to control access to an object, such as lazy loading or access control.
- When you need to perform additional operations before or after accessing the real object, like logging or caching.
- When you want to provide a virtual object (such as a large data structure) to delay loading until it is actually needed.

## Problem it Solves

Without the **Proxy** pattern, clients might have direct access to the real object, which could be inefficient or problematic (for example, when loading a large resource). The **Proxy** allows control over how and when the object is accessed.

## Solution

The **Proxy** pattern acts as a middle layer that controls access to the real object. It can perform additional operations (such as security checks or caching) before delegating the request to the real object.

## C# Code Example

%%%
public interface IImage
{
    void Display();
}

public class RealImage : IImage
{
    private string _filename;

    public RealImage(string filename)
    {
        _filename = filename;
        LoadImage();
    }

    private void LoadImage()
    {
        Console.WriteLine($"Loading image: {_filename}");
    }

    public void Display()
    {
        Console.WriteLine($"Displaying image: {_filename}");
    }
}

public class ImageProxy : IImage
{
    private RealImage _realImage;
    private string _filename;

    public ImageProxy(string filename)
    {
        _filename = filename;
    }

    public void Display()
    {
        if (_realImage == null)
        {
            _realImage = new RealImage(_filename);
        }
        _realImage.Display();
    }
}
%%%

## Visual Example

Imagine displaying images in a photo viewer application. The **Proxy** pattern could be used to delay the loading of an image until it is actually needed (i.e., when the user clicks on it to view it). The **ImageProxy** can load the image only when required, saving system resources and improving performance by avoiding unnecessary loading of all images at once.

This allows you to avoid unnecessary resource usage when the images may not even be viewed, providing a performance boost.

## Benefits

- **Control access**: It allows for lazy loading, caching, and access control.
- **Efficiency**: Only loads the real object when it is actually needed, improving performance.
