DevMax - Maximal development on limited platforms
=================================================

Universal Windows Platform (UWP) Application for C/C++ Software Development Environment

**PLEASE READ THE APP DESCRIPTION BEFORE PURCHASE.**

DevMax is a C/C++ software development environment (IDE). The user interface is inspired mostly by Visual Studio (VS) Code but unlike VS Code
 * DevMax is written in C++, not the inefficient TypeScript;
 * DevMax is much more lightweight but it is less powerful and cannot support extension.

Compared to the full Visual Studio suite,
 * DevMax is extremely light: the app itself is about 2MB installed and with 30MB more, you get the C/C++ compiler and linker all in a single package (compared to 3GB of basic Visual Studio installation for Desktop Development or 700MB just to get the editor!).
 * DevMax does not pollute your system: it does not put files all over the places. Visual Studio produces a hoard of folders in Program Files, puts a bunch of packages in C:\ProgramData\Microsoft\VisualStudio, application configurations in %localappdata%, ... and writes about 100MB of data to the registry!)
 * DevMax uses much less memory than Visual Studio: DevMax does not perform irredundant stuffs such as collecting telemetry and pulling news from Microsoft. Typical usage consumes about 10-40MB of memory (more during compilation); compared to about 800MB of VS (for your information, VS launches not one but many different processes at runtime, for pulling news, checking updates, etc.; a typical 2GB RAM machine will nearly max out when running VS).
 * DevMax is also much more efficient than typical IDE: Most IDE compiles code by executing external (command line) compiler such as gcc, cl.exe, ... As the compiler and linker are already linked into the app, DevMax needs not launch multiple command line program to compile your code. Files are also cached between different compilation so it can compile way faster than Visual Studio.
 * DevMax and its sister app C++ Compiler run in separate windows and processes. If you have multiple screen, you can run each application in one screen to maximize your productivity. We do not believe such thing is possible with Visual Studio as of now: You cannot run the VS editor and the build console on separate windows.
 * Last but not least, it takes a few seconds to install DevMax while for VS, you will usually hear the following conversation between software engineer and friend:
     - What did you do for your first day at work?
     - Installing Visual Studio.

Of course, DevMax might not be a tool appropriate for everyone since it does not provide all the convenience and service (such as debugging) of Visual Studio. It suits developers with moderate need; for instance, students trying to learn C/C++ programming or hard core experience developers who knows how to perform diagnostic logging, write unit tests, etc. and requires little live debugging support. (The original goal of DevMax is to develop our own Windows Store application. In fact, DevMax is used to develop itself! We use DevMax to develop and Visual Studio Team Service to build and test the app.)

**USAGE NOTE:**

As of version 2.6.4.0, compilation of C++ programs can be performed using either
  1.   the embedded Win32 desktop C++ compiler; or
  2.   the sister UWP app C++ Compiler at https://github.com/light-tech/UniversalCppCompiler. Evidently, this requires installation of additional app that we couldn't distribute via the Store.

With option 1, the project folder could be located anywhere; whereas you are limited to the app's dedicated project folder in option 2. However, compilation doesn't work in option 1 yet; only interpretation is supported now.

HISTORY
-------

Version 2.7.0.0
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

Version 2.6.5.0
 * Add color-highlighting for compilation output of the embedded (Win32 desktop) compiler
 * Still figuring out why it sometimes crash for the app's internal projects
     - Might remove support for internal projects in the future: the desktop compiler seems much better
 * Partially converted to C++/WinRT for speed improvement

Version 2.6.4.0
 * Add setting to switch between
     - the new embedded (Win32 desktop) compiler and
     - the classical (UWP) C++ compiler app
when running compilation.

Version 2.6.3.0
 * Now with embedded interpreter thank to Desktop Bridge
     - No longer need to install sister app C++ Compiler to interpret programs
     - Also, can't compile with C++ Compiler app
     - Project can be located outside of the app's dedicated folders: open project anywhere
     - Can't compile yet since we haven't port the system headers and libraries look-up
 * Request 'runFullTrust' to release full version with embedded compiler

Version 2.6.2.0
 * Add button to move output panel to a new window
    - Useful when there are multiple screens

Version 2.6.1.0
 * The output panel now take the whole space available instead of splitting with editor; `Ctrl + D` now toggles the output panel
   - No longer need to leave the keyboard to close the panel.

Version 2.5.9.0 - 2.6.0.0
 * Launch compilation/interpretation in a background process to avoid crashing the app when compiler crashes.
    - Requires C++ Compiler app version 2.6.0.0.
    - No longer compile via app protocol.
    - No longer need to open C++ Compiler app before running build definitions.
 * Add `Ctrl + D` shortcut to show the output panel for compilation/interpretation output.

Version 2.5.2.0
 * Add close button `[X]` next to file name

Version 2.5.1.0
 * Fix inefficient line number rendering (can now smoothly scroll large files like those C++/WinRT headers)

Version 2.5.0.0
 * Use the new system's `TreeView`
 * Open project in any location (if the project file `project.json` is present)
 * Improvements in code editor

Version 2.4-2.4.4
 * Interpreter support (require C++ Compiler 2.4.2)
 * Minor enhancement

Version 2.2.5
 * Fix crash when doing block indentation using tab

Version 2.2.4
 * Handle settings save/load properly

Version 2.2.3
 * Fix communication protocol with C++ Compiler app

Version 2.2.2
 * Fix crash, load projects cloned in our Git It app
 * Support building Win32 GUI application with C++ Compiler 2.2 update

Version 2.1 and 2.2
 * Lots of improvements to editor such as code suggestion and type highlighting
 * Switch to non-XAML code and some UI enhancements

Version 2.0

 * A lot of improvements to internal system and editors with more than 200 code revisions such as lazy folder browsing, C++ and XML syntax highlighting
 * Add editor settings for tab size, highlight matching braces, line wrapping, auto code indent
 * Register file types `*.cpp`, `*.h`, `*.c`, `*.hpp` with DevMax
 * Add `Ctrl + Tab` to insert tab as `Tab` is preserved by the system to move between UI elements)
 * (DESKTOP ONLY) Support compilation of C/C++ source into object files and linking objects into executable.