---
description: "Learn more about: C operators"
title: "C operators"
ms.date: 04/07/2022
helpviewer_keywords: ["ternary operators", "operators [C]", "symbols, operators", "binary operators", "associativity of operators", "binary data, binary expressions"]
ms.assetid: 13bc4c8e-2dc9-4b23-9f3a-25064e8777ed
---
# C operators

The C operators are a subset of the [C++ built-in operators](../cpp/cpp-built-in-operators-precedence-and-associativity.md).

There are three types of operators. A unary expression consists of either a unary operator followed by an operand, or the **`sizeof`** or **`_Alignof`** keyword followed by an expression. The expression can be either the name of a variable or a cast expression. If the expression is a cast expression, it must be enclosed in parentheses. A binary expression consists of two operands joined by a binary operator. A ternary expression consists of three operands joined by the conditional-expression operator.

C includes the following unary operators:

| Symbol | Name |
|--|--|
| **`-`** **`~`** **`!`** | Negation and complement operators |
| **`*`** **`&`** | Indirection and address-of operators |
| **`_Alignof`** | Alignment operator (since C11) |
| **`sizeof`** | Size operator |
| **`+`** | Unary plus operator |
| **`++`** **`--`** | Unary increment and decrement operators |

Binary operators associate from left to right. C provides the following binary operators:

| Symbol | Name |
|--|--|
| **`*`** **`/`** **`%`** | Multiplicative operators |
| **`+`** **`-`** | Additive operators |
| **`<<`** **`>>`** | Shift operators |
| **`<`** **`>`** **`<=`** **`>=`** **`==`** **`!=`** | Relational operators |
| **`&`** **`|`** **`^`** | Bitwise operators |
| **`&&`** **`||`** | Logical operators |
| **`,`** | Sequential-evaluation operator |

The base operator (**`:>`**), supported by previous versions of the Microsoft 16-bit C compiler, is described in [C Language syntax summary](../c-language/c-language-syntax-summary.md).

The conditional-expression operator has lower precedence than binary expressions and differs from them in being right associative.

Expressions with operators also include assignment expressions, which use unary or binary assignment operators. The unary assignment operators are the increment (**`++`**) and decrement (**`--`**) operators; the binary assignment operators are the simple-assignment operator (**`=`**) and the compound-assignment operators. Each compound-assignment operator is a combination of another binary operator with the simple-assignment operator.

## See also

- [Expressions and assignments](../c-language/expressions-and-assignments.md)
