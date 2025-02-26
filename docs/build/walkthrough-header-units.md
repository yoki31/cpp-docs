---
description: "Learn more about C++ header units by converting a header file to a header unit by using Visual Studio 2019."
title: "Walkthrough: Build and import header units in Visual C++ projects"
ms.date: 01/10/2022
ms.custom: "conceptual"
author: "tylermsft"
ms.author: "twhitney"
helpviewer_keywords: ["import", "header unit", "ifc"]
---

# Walkthrough: Build and import header units in Microsoft Visual C++

This article is about building and importing header units by using Visual Studio 2019. See [Walkthrough: Import STL libraries as header units](walkthrough-import-stl-header-units.md) to learn specifically how to import Standard Template Library headers as header units.

Header units are the recommended alternative to [precompiled header files](creating-precompiled-header-files.md) (PCH). They're easier to set up and use than a [shared PCH](https://devblogs.microsoft.com/cppblog/shared-pch-usage-sample-in-visual-studio), but they provide similar performance benefits. Unlike a PCH, when a header unit changes, only it and what depends on it are rebuilt.

## Prerequisites

To use header units, you need Visual Studio 2019 16.10 or later.

## What is a header unit?

A header unit is a binary representation of a header file. A header unit ends with an *`.ifc`* extension. This format is also used for named modules.

An important difference between a header unit and a header file is that header units aren't affected by macro definitions. You can't `#define` a symbol that causes the header unit to behave differently when you import it. You can do that with a header file.

A similarity is that everything visible from a header file is also visible from a header unit.

Before you can import a header unit, you need to compile a header file into a header unit. An advantage of header units over PCH is that they can be used in distributed builds. For example, as long as you compile the *`.ifc`* and the program that imports it with the same compiler, and target the same platform and architecture, a header unit produced on one computer can be used on another.

Another advantage of header units over PCH is that there's more flexibility for differences between the compiler flags used to compile the header unit and the program that imports it. With a PCH, more compiler flags must be the same. With header units, only the following flags need to be the same:

- Exception handling options like **`/EHsc`**.
- **`/MD[d]`** or **`MT[d]`**.
- **`/D`**. You can define other macros when you build the program that imports the header unit. But the ones used to build the header unit should also be present and defined the same way when you build the program that imports the header unit.

## Ways to compile a header unit

There are several ways to compile a file into a header unit:

- **Automatically scan for header units**. This approach is best suited to smaller projects that include many different header files. See [Walkthrough: Import STL libraries as header units](walkthrough-import-stl-header-units.md#approach1) for a demonstration of this approach. This approach is better suited to smaller projects because it can't guarantee optimal build throughput. That's because it scans all the files to find what should be built into header units.

- **Build a shared header unit project**. This approach is best suited for larger projects and for when you want more control over the organization of the imported header units. You create a static library project (or projects) that contain the header units that you want. Then reference that library project (or projects) to import the header units. See [Walkthrough: Import STL libraries as header units](walkthrough-import-stl-header-units.md#approach2) for a demonstration of this approach.

- **Choose individual header units to build**. This approach gives you file-by-file control over which header files are treated as header units. It's also a good way to try out header units in your project. This approach is demonstrated in this walkthrough.

## Convert a project to use header units

Compile a header file as a header unit using the following steps in Visual Studio:

1. Create a new C++ console app project.
1. Replace the source file content as follows:

    ```cpp
    #include "Pythagorean.h"
    
    int main()
    {
        PrintPythagoreanTriple(2,3);
        return 0;
    }
    ```

1. Add a header file called `Pythagorean.h` and then replace its content with this code:

    ```cpp
    #ifndef PYTHAGOREAN
    #define PYTHAGOREAN

    #include <iostream>
    
    inline void PrintPythagoreanTriple(int a, int b)
    {
        std::cout << "Pythagorean triple a:" << a << " b:" << b << " c:" << a*a + b*b << std::endl;
    }
    #endif
    ```

To enable header units, first set the **C++ Language Standard** to [`/std:c++20`](./reference/std-specify-language-standard-version.md) or later:

1. On the Visual Studio main menu, select **Project** > **Properties**.
1. In the left pane of the project property pages window, select **Configuration Properties** > **General**.
1. In the **C++ Language Standard** list, select **ISO C++20 Standard (/std:c++20)** or later. In versions before Visual Studio 2019 version 16.11, select **Preview - Features from the Latest C++ Working Draft (/std:c++latest)**.

### Compile a header file as a header unit

In **Solution Explorer**, select the file you want to compile as a header unit (in this case, `Pythagorean.h`). Right-click the file and select **Properties**. Since this is a header file, set the **Item Type** property to **C/C++ compiler**. By default, header files have an **Item Type** of **C/C++ header**. Setting this property also sets **C/C++** > **Advanced** > **Compile As** to **Compile as C++ Header Unit (/exportHeader)**.
:::image type="content" source="media/change-item-type.png" alt-text="Screenshot that shows changing the item type to C/C++ compiler.":::

**Compile a source file as a header unit**:

If you want to compile a file that doesn't have an *`.h`* or *`.hpp`* extension as a header unit, set the **Compile As** property to **Compile as C++ Header Unit (/exportHeader)**.
:::image type="content" source="media/change-compile-as.png" alt-text="Screenshot that shows changing Compile As to Compile as C++ Header Unit.":::

### Change your code to import a header unit

In the source file for the example project that contains `main()`, change `#include "Pythagorean.h"` to `import "Pythagorean.h";`. Don't forget the trailing semicolon that's required for `import` statements.

When compiling a header unit from a system header, use angle brackets (`import <file>;`). If it's a project header, use `import "file";`.

Build the solution by selecting **Build** > **Build Solution** on the main menu. Run it to see that it produces the expected output: `Pythagorean triple a:2 b:3 c:13`

In your own projects, repeat this process to compile the header files you want to import as header units.

If you want to convert only a few header files to header units, this approach is a good one. But if you have many header files that you want to compile, and the convenience of having the build system automatically handle it outweighs the potential effect on build performance, you can have the build system scan for and build header units for you. See [Walkthrough: Import STL libraries as header units](walkthrough-import-stl-header-units.md#approach1) to learn how.

## See also

[Walkthrough: Import STL libraries as header units](walkthrough-import-stl-header-units.md#approach1)\
[Overview of modules in C++](../cpp/modules-cpp.md) \
[`/translateInclude`](./reference/translateinclude.md) \
[`/exportHeader`](./reference/module-exportheader.md) \
[`/headerUnit`](./reference/headerunit.md)
