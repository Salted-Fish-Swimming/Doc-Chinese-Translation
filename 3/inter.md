# Uniqueness type ( 独有类型 )

In computing, a unique type guarantees that an object is used in a single-threaded way, with at most a single reference to it. If a value has a unique type, a function applied to it can be optimized to update the value in-place in the object code. Such in-place updates improve the efficiency of functional languages while maintaining referential transparency. Unique types can also be used to integrate functional and imperative programming.
在计算中，唯一类型保证对象以单线程的方式使用，最多只有一个对它的引用。如果值具有唯一类型，则可以优化应用于该值的函数，以在目标代码中就地更新该值。这种就地更新提高了函数式语言的效率，同时保持了引用的透明性。惟一类型还可以用于集成函数式编程和命令式编程。

## Introduction ( 介绍 )

Uniqueness typing is best explained using an example. Consider a function readLine that reads the next line of text from a given file:
唯一性类型最好用一个例子来解释。考虑一个函数readLine，它从给定文件中读取下一行文本:

```
function readLine(File f) returns String
    return line where
        String line = doImperativeReadLineSystemCall(f)
    end
end
```

Now `doImperativeReadLineSystemCall` reads the next line from the file using an OS-level system call which has the side effect of changing the current position in the file. But this violates referential transparency because calling it multiple times with the same argument will return different results each time as the current position in the file gets moved. This in turn makes `readLine` violate referential transparency because it calls `doImperativeReadLineSystemCall`.
现在`doImperativeReadLineSystemCall`使用操作系统级的系统调用从文件中读取下一行，其副作用是改变文件中的当前位置。但这违反了引用透明性，因为使用相同的参数多次调用它，每次都会返回不同的结果，因为文件中的当前位置被移动了。这反过来又使`readLine`违反了引用透明性，因为它调用`doImperativeReadLineSystemCall`。

However, using uniqueness typing, we can construct a new version of `readLine` that is referentially transparent even though it's built on top of a function that's not referentially transparent:
然而，使用唯一性类型，我们可以构造一个新版本的`readLine`，它是引用透明的，即使它构建在一个不引用透明的函数之上:

```
function readLine2(unique File f) returns (unique File, String)
    return (differentF, line) where
        String line = doImperativeReadLineSystemCall(f)
        File differentF = newFileFromExistingFile(f)
    end
end
```

The unique declaration specifies that the type of f is unique; that is to say that f may never be referred to again by the caller of readLine2 after readLine2 returns, and this restriction is enforced by the type system. And since readLine2 does not return f itself but rather a new, different file object differentF, this means that it's impossible for readLine2 to be called with f as an argument ever again, thus preserving referential transparency while allowing for side effects to occur. 
`unique`声明指定`f`的类型是唯一的;也就是说，在`readLine2`返回后，f可能再也不会被`readLine2`的调用者引用，这种限制是由类型系统强制执行的。由于`readLine2`并不返回f本身，而是返回一个新的不同的文件对象`differentF`，这意味着不可能再以`f`作为参数调用`readLine2`，从而在允许发生副作用的同时保留引用透明性。

## Programming languages ( 编程语言 )

Uniqueness types are implemented in functional programming languages such as Clean, Mercury, SAC and Idris. They are sometimes used for doing I/O operations in functional languages in lieu of monads.

A compiler extension has been developed for the Scala programming language which uses annotations to handle uniqueness in the context of message passing between actors.[1]

## Relationship to linear typing ( 与线性类型的关系 )

A unique type is very similar to a linear type, to the point that the terms are often used interchangeably, but there is in fact a distinction: actual linear typing allows a non-linear value to be typecast to a linear form, while still retaining multiple references to it. Uniqueness guarantees that a value has no other references to it, while linearity guarantees that no more references can be made to a value.[2]

Linearity and uniqueness can be seen as particularly distinct when in relation to non-linearity and non-uniqueness modalities, but can then also be unified in a single type system. [3]

## See also ( 参见 )

- Linear type
- Linear logic

## References

1. Haller, P.; Odersky, M. (2010), "Capabilities for uniqueness and borrowing", ECOOP 2010—Object-Oriented Programming, pp. 354–378
2. Wadler, Philip (17–19 June 1991). "Is there a use for linear logic?". ACM SIGPLAN symposium on partial evaluation and semantics-based program manipulation (PEPM '91). pp. 255–273. doi:10.1145/115865.115894. ISBN 0-89791-433-3.
3. Marshall, Daniel; Vollmer, Michael; Orchard, Dominic (7 April 2022). "Linearity and Uniqueness: An Entente Cordiale". ESOP'22. doi:10.1007/978-3-030-99336-8_13.

## External links

- Bibliography on Linear Logic
- Uniqueness Typing Simplified


