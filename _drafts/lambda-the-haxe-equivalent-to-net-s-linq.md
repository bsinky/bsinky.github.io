---
layout: post
title: Lambda - the Haxe equivalent of .NET's LINQ
date: 2017-10-22 22:47
categories: ["programming"]
tags: ["programming", "haxe", ".NET"]
summary: C# programmers familiar with .NET and LINQ may come to Haxe looking for similar features - and they're in luck! In this post we'll go through Lambda - a collection of methods intended to be used as static extensions to add functional programming features to Haxe!
comments: true
pinned: false
---

Most anyone who's written C# in the last 9 years[^1] has probably heard of LINQ.  I would imagine most of those people have also *written* a few LINQ statements in that time; the language feature is just too useful to pass up!

As a frequent[^2] user of the Haxe language, I recently stumbled upon [Lambda](http://api.haxe.org/Lambda.html).  From the linked documentation:

> The Lambda class is a collection of methods to support functional programming. It is ideally used with using Lambda and then acts as an extension to Iterable types.

> On static platforms, working with the Iterable structure might be slower than performing the operations directly on known types, such as Array and List.

Do note, the second paragraph indicates that using Lambda *may* result in a performance penalty on static targets.  If efficiency is important above all else in your application, you might steer clear of Lambda.  But, if sacrificing a little performance is acceptable within your application, Lambda is likely to be *very* useful.  This is especially true of C# developers who are used to LINQ - and that brings us to the main point of this article!

### Contents
{:.no_toc}
- test
{:toc}

# Lambda - the Haxe equivalent of .NET's LINQ
{:.no_toc}

In the code snippets that follow, the Haxe code will assume that `using Lambda` was specified, just as the C# code will assume the use of `import System.Linq` to utilize the static extension methods for `IEnumerable`.

Each section header will follow the format `LINQ Method Name => Lambda Method Name`, with the C# code example first, followed by the Haxe code example.


**Note on Haxe arrow function:** the Haxe code examples will be using standard anonymous functions for predicate functions.  Those looking for a more terse syntax will be happy to know that the next version of Haxe, Haxe 4, [will contain arrow functions](https://haxe.org/download/version/4.0.0-preview.1/).

Until the (stable) release of Haxe 4, arrow functions are also available via a few libraries on `haxelib`, such as `slambda` or `hxslam`.

## Where => filter

LINQ:

```csharp
var someInts = new[] { 1, 2, 3, 4, 5 };
var onlyEvens = someInts.Where(n => n % 2 == 0);
```

Lambda:

```as3
var someInts = [1, 2, 3, 4, 5];
var onlyEvens = someInts.filter(function(n) n % 2 == 0);
```

## FirstOrDefault => find


LINQ:

```csharp
var someInts = new[] { 1, 2, 3, 4, 5 };
var divisibleByThree = someInts.FirstOrDefault(n => n % 3 == 0);
```

Lambda:

```as3
var someInts = [1, 2, 3, 4, 5];
var divisibleByThree = someInts.find(function(n) return n % 3 == 0);
```

## Any => exists / empty

A few remarks on this one; LINQ's `Any` has 2 overloads, one that accepts a predicate, and one that does not.  For the example that accepts a predicate, Lambda's `exists` will do.

LINQ:

```csharp
var someInts = new[] { 1, 2, 3, 4, 5 };
var anyEvenNumbers = someInts.Any(n => n % 2 == 0);
```

Lambda:

```as3
var someInts = [1, 2, 3, 4, 5];
var anyEvenNumbers = someInts.exists(function(n) return n % 2 == 0);
```

For the `Any` overload that does not accept a predicate, Lambda's `empty` is the answer.

LINQ:

```csharp
var someInts = new[] { 1, 2, 3, 4, 5 };
var anyNumbers = someInts.Any(); // no predicate; "does the IEnumerable contain anything?"
```

Lambda:

```as3
var someInts = [1, 2, 3, 4, 5];
var anyNumbers = !someInts.empty(); // empty is simply the inverse of Any with no parameters.
```

## Contains => has

LINQ:

```csharp
var someInts = new[] { 1, 2, 3, 4, 5 };
var containsThree = someInts.Contains(3);
```
Lambda:

```as3
var someInts = [1, 2, 3, 4, 5];
var containsThree = someInts.has(3);
```

## Select => map

LINQ:

```csharp
var someInts = new[] { 1, 2, 3, 4, 5 };
var squares = someInts.Select(n => n * n); // this is IEnumerable!
```
For the Lambda example, note that `map` returns a `List`, so it's *slightly* different from LINQ where the return value of `Select` is still a deferred execution `IEnumerable`.

```as3
var someInts = [1, 2, 3, 4, 5];
var squares = someInts.map(function(n) return n * n); // this is a List!
```

### Select => mapi (Bonus round!)

The overload for `Select` with the signature `Select<TSource>(IEnumerable<TSource>, Func<TSource, Int32, TResult>)`, in which the second argument to the `selector` parameter is the index of the element from the source collection **also** has a corresponding Lambda counterpart, `mapi`.

LINQ:

```csharp
var someInts = new[] { 1, 2, 3, 4, 5 };
var indexAndInt = someInts.Select(index, n => $"{index}: {n}"); // this is IEnumerable!
```

Lambda:

```as3
var someInts = [1, 2, 3, 4, 5];
var indexAndInt = someInts.mapi(function(index, n) return '${index}: ${n}'); // this is a List!
```

## SelectMany => flatten

LINQ:

```csharp
var listOfLists = new [] { new[] { 1, 2, 3 }, new[] { 4, 5, 6 }, new[] {7, 8, 9}};
var flattenedList = listOfLists.SelectMany(n => n);
```

For the Lambda example, note that `flatten` returns a `List` instead of a concatenated `Iterable`.  Also, `flatten` accepts no arguments - it *always* simply flattens the `Iterable<Iterable<A>>` into a single `List`, no `selector` function required.

```as3
var listOfLists = [[1, 2, 3], [4, 5, 6], [7, 8, 9]];
var flattenedList = listOfLists.flatten();
```

## Aggregate => fold

What LINQ calls `Aggregate` is an operation more commonly known as `fold`, as Lambda (and other languages) calls it), or `reduce` (JavaScript, and others).  `Aggregate` and `fold` are similar, one difference to note is `Aggregate` accepts the `seed` as its first argument, while `fold` accepts `seed` as the last argument.

```csharp
var numbers = Enumerable.Range(1, 10);
// Yes, LINQ also provides Sum, Aggregate is used here simply for illustration
var sumOfOneThroughTen = numbers.Aggregate(0, (a, b) => a + b);
```

Lambda:

```as3
var numbers = [ for (x in 1...11) x ];
var sumOfOneThroughTen = numbers.fold(function(a, b) return a + b, 0);
```

## Count => count

In this case, both LINQ and Lambda methods seem to behave exactly the same.

## ToList => list

This one is straightforward - LINQ's `ToList` returns `List`, Lambda's `list` returns `List`.  Nothing else to say here!

## ToArray => array

In this case, both LINQ and Lambda methods seem to behave exactly the same.

## Concat => concat

In this case, both LINQ and Lambda methods seem to behave *similarly*, but it should be noted that, again, the result of LINQ's `Concat` is `IEnumerable` while the result of Lambda's `concat` is a concrete `List` and not simply an `Iterable`.

## Single

Lambda doesn't contain a replacement for LINQ's `Single`, which is fine, as this lies outside of Lambda's functional programming goals.  That's not to say those coming to Haxe, from C# or not, might not need the functionality of `Single` from time to time.  Of course, implementing a `Single` replacement in Haxe is very possible, and straightforward.  One such implementation might look like the following, do note that this implementation doesn't match LINQ's `Single` in every regard.  Notably, it will simply return `null` for an empty `Iterable`.

<script src="https://gist.github.com/bsinky/fa75287a8946d7296fc8f5e906b2a136.js"></script>

## GroupBy

`GroupBy` is another LINQ extension method for which there is no replacement.  Again though, should a Haxe `groupBy` be needed, it need only be implemented! Here's an example of how `groupBy` could be implemented, but be aware that this implementation could be done more efficiently!

<script src="https://gist.github.com/bsinky/6dcc4226f5b06b04d48af9790398e60e.js"></script>


---

[^1]: LINQ was first introduced with the release of .NET Framework 3.5, on November 19th, 2017.  ([Wikipedia](https://en.wikipedia.org/wiki/.NET_Framework_version_history#.NET_Framework_3.5))

[^2]: Though, I am clearly still discovering new parts of the standard library!
