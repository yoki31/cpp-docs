---
description: "Learn more about: /TSAWARE (Create Terminal Server aware application)"
title: "/TSAWARE (Create Terminal Server aware application)"
ms.date: 03/02/2022
f1_keywords: ["/tsaware", "VC.Project.VCLinkerTool.TerminalServerAware"]
helpviewer_keywords: ["Terminal Server", "/TSAWARE linker option", "Terminal Server, Terminal Server-aware applications", "-TSAWARE linker option", "TSAWARE linker option"]
ms.assetid: fe1c1846-de5b-4839-b562-93fbfe36cd29
---
# `/TSAWARE` (Create Terminal Server aware application)

> **`/TSAWARE`**\[**`:NO`**]

## Remarks

The **`/TSAWARE`** option sets a flag in the `IMAGE_OPTIONAL_HEADER` `DllCharacteristics` field in the program image's optional header. When this flag is set, Terminal Server won't make certain changes to the application.

When an application isn't Terminal Server aware (also known as a legacy application), Terminal Server makes certain modifications to the legacy application to make it work properly in a multiuser environment. For example, Terminal Server creates a virtual *`Windows`* folder, such that each user gets a *`Windows`* folder instead of getting the system's *`Windows`* directory. This virtual folder gives users access to their own INI files. In addition, Terminal Server makes some adjustments to the registry for a legacy application. These modifications slow the loading of the legacy application on Terminal Server.

If an application is Terminal Server aware, it must not rely on INI files or write to the `HKEY_CURRENT_USER` registry during setup.

If you use **`/TSAWARE`** and your application still uses INI files, the files will be shared by all users of the system. If that's acceptable, you can still link your application with **`/TSAWARE`**; otherwise you need to use **`/TSAWARE:NO`**.

The **`/TSAWARE`** option is enabled by default for Windows and console applications. For more information, see [`/SUBSYSTEM`](subsystem-specify-subsystem.md) and [`/VERSION`](version-version-information.md).

**`/TSAWARE`** isn't valid for drivers or DLLs.

If an application was linked with **`/TSAWARE`**, [`DUMPBIN /HEADERS`](headers.md) will display information to that effect.

### To set this linker option in the Visual Studio development environment

1. Open the project's **Property Pages** dialog box. For details, see [Set C++ compiler and build properties in Visual Studio](../working-with-project-properties.md).

1. Select the **Configuration Properties** > **Linker** > **System** property page.

1. Modify the **Terminal Server** property.

### To set this linker option programmatically

- See <xref:Microsoft.VisualStudio.VCProjectEngine.VCLinkerTool.TerminalServerAware%2A>.

## See also

[MSVC linker reference](linking.md)<br/>
[MSVC Linker Options](linker-options.md)<br/>
[Storing User-Specific Information](/windows/win32/TermServ/storing-user-specific-information)<br/>
[Legacy Applications in a Terminal Services Environment](/previous-versions/aa382957(v=vs.85))
