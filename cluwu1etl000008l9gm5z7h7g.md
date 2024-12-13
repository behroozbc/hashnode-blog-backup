---
title: "NumPy replacement in the .NET world( C# and F#)"
datePublished: Fri Apr 12 2024 15:38:08 GMT+0000 (Coordinated Universal Time)
cuid: cluwu1etl000008l9gm5z7h7g
slug: numpy-replacement-in-the-net-world
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/zGuBURGGmdY/upload/b29bf04e640f5117fac7c7ce36236df1.jpeg
tags: ai, csharp, machine-learning, net, f, dotnet, dotnetcore, numpy

---

NumPy is a popular Python library that provides powerful tools for working with arrays, matrices, and numerical computations. In this blog post, I will introduce some of packages to use it in the .NET application and systems and write your program in C# and F#.

## What is NumPy?

NumPy is a Python library that provides a high-performance multidimensional array object and tools for working with these arrays. It is the fundamental package for scientific computing with Python, as it offers comprehensive mathematical functions, random number generators, linear algebra routines, Fourier transforms, and more. NumPy can also be used as an efficient multi-dimensional container of generic data, and it supports a wide range of hardware and computing platforms. NumPy arrays are fast and versatile, and they follow the concepts of vectorization, indexing, and broadcasting. NumPy arrays can be created from various data types such as lists, tuples, etc., and they can be accessed by using square brackets or advanced indexing methods. NumPy arrays can also be sliced to create new arrays that hold a range of elements from the original array. NumPy allows a wide range of operations that can be performed on arrays, such as arithmetic, logical, bitwise, comparison, etc. NumPy also has an ecosystem of applications that use its array capabilities for various domains such as astronomy, image processing, machine learning, statistics, etc. NumPy is an open-source project that is developed and maintained publicly on GitHub by a vibrant, responsive, and diverse community.

## What alternative exist in .NET world for Numpy

I found 3 good options in .NET world. I tested them check their prons and cons. And I will introduce them to you.

### NumpyDotNet ( Best choice)

This library is very good and supports all the functionality of Numpy. Their developers write all Numpy's features in C#, and it has good performance because it is pure C#. Moreover, this library supports 100% of Numpy's features. Due to the fact that all of the underlying data is pure .NET System.Array types, they can be used like any other .NET array.

Also, This package is my recommendation for your project. You can take a look at its [Github page](https://github.com/Quansight-Labs/numpy.net) and give them stars to support them.

I will write a post about how you can use this package.

You can install this package with the below NuGet command. To find other ways you can check their [Nuget page](https://www.nuget.org/packages/NumpyDotNet/)

```plaintext
NuGet\Install-Package NumpyDotNet
```

### [SciSharp/NumSharp](https://github.com/SciSharp/NumSharp)

NumSharp is a C# library akin to Python's NumPy, offering a suite of numerical computing tools. It simplifies complex math and data tasks, supports multi-dimensional arrays, linear algebra, and statistics, and integrates with [ML.NET](http://ML.NET) for data science and machine learning projects. Its familiar syntax eases the transition for those accustomed to NumPy. If you need more information you can check their [GitHub pages](https://github.com/SciSharp/NumSharp).

It used in many ML library but in my local test I cannot run it and get an error. you can see [this GitHub issue](https://github.com/SciSharp/NumSharp/issues/505).

You can install this package with the below NuGet command. To find other ways you can check their [Nuget page](https://www.nuget.org/packages/NumSharp/)

```plaintext
NuGet\Install-Package NumSharp -Version 0.30.0
```

### SciSharp/[Numpy.NET](http://Numpy.NET)

[Numpy.NET](http://Numpy.NET) is a comprehensive library that provides C# and F# bindings to the well-known NumPy library, which is a cornerstone in the Python community for scientific computing. It offers .NET developers the ability to utilize a wide range of functionalities that are native to NumPy, such as multi-dimensional arrays and matrices, linear algebra operations, Fourier transforms, and more. This is achieved through a strongly-typed API that is compatible with the .NET framework, making it a powerful tool for developers working in the fields of machine learning, AI, and data science. The library ensures ease of installation and compatibility with different versions of Python and NumPy, catering to various development needs. For those who require a seamless integration without the need for a local Python installation, [Numpy.NET](http://Numpy.NET) includes a packaged Python environment, simplifying the setup process and allowing developers to focus on building their applications. An interesting thing about the Numpy.NET, it does not require installing python or clash with your local python installation, because it uses [Python.Included](https://github.com/henon/Python.Included)**.** If you need more information you can check their [GitHub pages](https://github.com/SciSharp/Numpy.NET).

**Note: This library uses more rescores than other rivals because it uses python behind the scene.**

You can install this package with the below NuGet command. To find other ways you can check their [Nuget page](https://www.nuget.org/packages/Numpy/).

```plaintext
NuGet\Install-Package Numpy -Version 3.11.1.33
```

## Finality

You can use Numpy in your projects without sensing you are in the .Net world thanks to these great packages. I provide a short review of them and how you can use them. If you have any questions about it you can ask them in the comments.