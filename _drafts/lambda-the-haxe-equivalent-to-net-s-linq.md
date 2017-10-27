---
layout: post
title: Lambda - the Haxe equivalent of .NET's LINQ
date: 2017-10-22 22:47
categories: ["programming"]
tags: ["programming", "haxe", ".NET"]
excerpt: A new blog post
comments: true
pinned: false
---

Most anyone who's written C# in the last 9 years[1^] has probably heard of LINQ.  I would imagine most of those people have also *written* a few LINQ statements in that time; the language feature is just too useful to pass up!

As a frequent[2^] user of the Haxe language, I recently stumbled upon [Lambda](http://api.haxe.org/Lambda.html).  From the linked documentation:

> The Lambda class is a collection of methods to support functional programming. It is ideally used with using Lambda and then acts as an extension to Iterable types.

> On static platforms, working with the Iterable structure might be slower than performing the operations directly on known types, such as Array and List.

One thing to note - the second paragraph does indicate that using Lambda *may* result in a performance penalty on static targets.  But, if this is acceptable within your application, Lambda is likely to be *very* useful.  This is especially true of C# developers who are used to LINQ - and that brings us to the main point of this article!

# Lambda - the Haxe equivalent of .NET's LINQ

In the code snippets that follow, the Haxe code will assume that `using Lambda` was specified, just as the C# code will assume the use of `import System.Linq` to utilize the static extension methods for `IEnumerable`.

Each section header will follow the format `LINQ Method Name => Lambda Method Name`, with the C# code example first, followed by the Haxe code example.


**Note on Haxe arrow function:** the Haxe code examples will be using standard anonymous functions for predicate functions.  Those looking for a more terse syntax will be happy to know that the next version of Haxe, Haxe 4, [will contain arrow functions](https://haxe.org/download/version/4.0.0-preview.1/).

Until the (stable) release of Haxe 4, arrow functions are also available via a few libraries on `haxelib`, such as `slambda` or `hxslam`.

## Where => filter

To start off, here's an example of using `Where` in C# to find all the even numbers in a collection:

```csharp
var someInts = new[] { 1, 2, 3, 4, 5 };
var onlyEvens = someInts.Where(n => n % 2 == 0);
```

To accomplish the same in Haxe, we can use Lambda's `filter`:

```haxe
var someInts = [1, 2, 3, 4, 5];
var onlyEvens = someInts.filter(function(n) n % 2 == 0);
```

[filter demo](https://try.haxe.org/#F39eE)

## FirstOrDefault => find


## Single


## Any => exists

LINQ:

```csharp
var someInts = new[] { 1, 2, 3, 4, 5 };
var anyEvenNumbers = someInts.Any(n => n % 2 == 0);
```

Lambda:

```haxe
var someInts = [1, 2, 3, 4, 5];
var anyEvenNumbers = someInts.exists(function(n) return n % 2 == 0);
```

## Contains => has

LINQ:

```csharp
var someInts = new[] { 1, 2, 3, 4, 5 };
var containsThree = someInts.Contains(3);
```
Lambda:

```haxe
var someInts = [1, 2, 3, 4, 5];
var containsThree = someInts.has(3);
```

## Select => map / mapi

LINQ:

```csharp
var someInts = new[] { 1, 2, 3, 4, 5 };
var squares = someInts.Select(n => n * n); // this is IEnumerable!
```
For the Lambda example, note that `map` returns a `List`, so it's *slightly* different from LINQ where the return value of `Select` is still a deferred execution `IEnumerable`.

```haxe
var someInts = [1, 2, 3, 4, 5];
var squares = someInts.map(function(n) return n * n); // this is a List!
```

### Bonus round!

The overload for `Select` with the signature `Select<TSource>(IEnumerable<TSource>, Func<TSource, Int32, TResult>)`, in which the second argument to the `selector` parameter is the index of the element from the source collection **also** has a corresponding Lambda counterpart, `mapi`.

LINQ:

```csharp
var someInts = new[] { 1, 2, 3, 4, 5 };
var indexAndInt = someInts.Select(index, n => $"{index}: {n}"); // this is IEnumerable!
```

Lambda:

```haxe
var someInts = [1, 2, 3, 4, 5];
var indexAndInt = someInts.mapi(function(index, n) return '${index}: ${n}'); // this is a List!
```
## SelectMany => flatten



## Aggregate

## Count => count

In this case, both LINQ and Lambda methods for counting seem to behave exactly the same.

## ToList => list

This one is straightforward - LINQ's `ToList` returns `List`, Lambda's `list` returns `List`.  Nothing else to say here!

---

[1]: LINQ was first introduced with the release of .NET Framework 3.5, on November 19th, 2017.

[2]: Though, I am clearly still discovering new parts of the standard library.