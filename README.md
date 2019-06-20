DevMax - MAXimum DEVelopment on limited platforms
=================================================

DevMax is a Universal Windows Platform (UWP) Application for C/C++ Software Development Environment (IDE).
You can get the app **FOR FREE** on [Microsoft Store](https://www.microsoft.com/en-us/p/devmax/9mzqlt5d5b39).

FEATURES
--------
 1. __Embedded C/C++ Interpreter, Compiler and Linker__
    - None of the professional IDE supports C/C++ Interpreter!
    - The addition of an interpreter allows one to test codes without waiting for compilation and linkage; bringing the convenience of Python development to C/C++ development.
 2. __Visual Studio (VS) Code inspired user interface__; but unlike VS Code
    - DevMax is written completely in C++, not the inefficient TypeScript.
    - DevMax is much more lightweight at the expense of having less powerful features and inability to support extension.
 3. __Extreme efficiency__: Compared to the full Visual Studio 2019 suite,
    - DevMax is extremely light: the app itself is about 40 MB installed complete with C/C++ compiler and linker all in a single package; compared to 3GB of basic Visual Studio installation for Desktop Development or 700MB just to get the editor (not including an additional 3GB for the Windows SDK C++ headers and libraries)!
    - DevMax does not pollute your system: It does not put files all over the places. Visual Studio produces a hoard of folders in Program Files, puts a bunch of packages in `C:\ProgramData\Microsoft\VisualStudio`, application configurations in `%localappdata%`, ... and writes about 100MB of data to the registry!
    - DevMax uses much less memory, leading to higher battery life, than Visual Studio (Code): DevMax does not perform irredundant stuffs such as collecting telemetry and pulling news from Microsoft. Typical usage consumes about 10-40MB of memory (more during compilation); compared to about 800MB (300MB) of VS (Code)!
    - (To be restored after 2.7) <del>DevMax is also much more efficient than typical IDE: Most IDE compiles code by executing external (command line) compiler such as `gcc`, `cl.exe`, ... As the compiler and linker are already linked into the app, DevMax needs not launch multiple command line program to compile your code. Files are also cached between different compilation so it can compile way faster than Visual Studio.</del>
    - Last but not least, it takes a few seconds to install DevMax (depending on network connection) while for VS, you will usually hear the following conversation between software engineer and friend:
        __A__: _What did you do for your first day at work?_
        __B__: _Installing Visual Studio._

Of course, DevMax might not be a tool appropriate for everyone since it does not provide all the convenience and service (such as debugging) of Visual Studio.
It suits developers with moderate need; for instance, students trying to learn C/C++ programming or hard core experience developers who knows how to perform diagnostic logging, write unit tests, etc. and requires little live debugging support.
(The original goal of DevMax is to develop our own Windows Store application. In fact, DevMax is used to develop itself! We mainly use DevMax to develop and Visual Studio Team Service to build and test the app.)

HISTORY
-------

__Version 2.7.0.0__
 * Complete migration to C++/WinRT
 * Complete UI redesign:
    - Feature a menu bar, full window and much more compact layout
    - Resizable the file explorer panel, single click to open/close folder
 * Editor:
    - Implement the standard "drag to select" gesture in editor
    - Fix "double tap to select word"
    - Change cursor to I-shaped appropriately
    - Auto focus on line number, search/replace text boxes when those tools are opened
    - Press enter to search when focus on Find text box
 * Support compilation/link in embedded compiler
    - No longer support C++ Compiler sister app
    - For interpreter, need to `#define _CRT_STDIO_ARBITRARY_WIDE_SPECIFIERS` when `#include stdio.h` due to non-ISO conformance headers (for `printf` et al.) from Microsoft.
    - Doesn't work with C++ headers due to linkage requirements (need loading of additional `*.lib` when interpreting)

__Version 2.6.5.0__
 * Add color-highlighting for compilation output of the embedded (Win32 desktop) compiler
 * Still figuring out why it sometimes crash for the app's internal projects
     - Might remove support for internal projects in the future: the desktop compiler seems much better
 * Partially converted to C++/WinRT for speed improvement

__Version 2.6.4.0__
 * Add setting to switch between
     - the new embedded (Win32 desktop) compiler and
     - the classical (UWP) C++ compiler app
when running compilation.

__Version 2.6.3.0__
 * Now with embedded interpreter thank to Desktop Bridge
     - No longer need to install sister app C++ Compiler to interpret programs
     - Also, can't compile with C++ Compiler app
     - Project can be located outside of the app's dedicated folders: open project anywhere
     - Can't compile yet since we haven't port the system headers and libraries look-up
 * Request 'runFullTrust' to release full version with embedded compiler

__Version 2.6.2.0__
 * Add button to move output panel to a new window
    - Useful when there are multiple screens

__Version 2.6.1.0__
 * The output panel now take the whole space available instead of splitting with editor; `Ctrl + D` now toggles the output panel
   - No longer need to leave the keyboard to close the panel.

__Version 2.5.9.0 - 2.6.0.0__
 * Launch compilation/interpretation in a background process to avoid crashing the app when compiler crashes.
    - Requires C++ Compiler app version 2.6.0.0.
    - No longer compile via app protocol.
    - No longer need to open C++ Compiler app before running build definitions.
 * Add `Ctrl + D` shortcut to show the output panel for compilation/interpretation output.

__Version 2.5.2.0__
 * Add close button `[X]` next to file name

__Version 2.5.1.0__
 * Fix inefficient line number rendering (can now smoothly scroll large files like those C++/WinRT headers)

__Version 2.5.0.0__
 * Use the new system's `TreeView`
 * Open project in any location (if the project file `project.json` is present)
 * Improvements in code editor

__Version 2.4-2.4.4__
 * Interpreter support (require C++ Compiler 2.4.2)
 * Minor enhancement

__Version 2.2.5__
 * Fix crash when doing block indentation using tab

__Version 2.2.4__
 * Handle settings save/load properly

__Version 2.2.3__
 * Fix communication protocol with C++ Compiler app

__Version 2.2.2__
 * Fix crash, load projects cloned in our Git It app
 * Support building Win32 GUI application with C++ Compiler 2.2 update

__Version 2.1 and 2.2__
 * Lots of improvements to editor such as code suggestion and type highlighting
 * Switch to non-XAML code and some UI enhancements

__Version 2.0__

 * A lot of improvements to internal system and editors with more than 200 code revisions such as lazy folder browsing, C++ and XML syntax highlighting
 * Add editor settings for tab size, highlight matching braces, line wrapping, auto code indent
 * Register file types `*.cpp`, `*.h`, `*.c`, `*.hpp` with DevMax
 * Add `Ctrl + Tab` to insert tab as `Tab` is preserved by the system to move between UI elements)
 * (DESKTOP ONLY) Support compilation of C/C++ source into object files and linking objects into executable.