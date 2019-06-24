Project File Specification
==========================

The project description file `project.json` is a simple human-readable [JSON]() file. An example can be found in our [Getting Started](https://github.com/light-tech/DevMaxGettingStarted) repository.

Throughout this document, we assume `$ProjectDir` refers to where the project is located i.e. the folder containing the `project.json` file; for example `<...>/C++Projects/ExampleProject`. Then we have
 * the system include root is `$SysIncludeDir := $ProjectDir../../C++Include`; and
 * the system lib root is `$SysLibDir := $ProjectDir../../C++Lib`.

__Tip:__ You can access `$SysIncludeDir` by typing `%localappdata%\Publishers\8vrbkgtyqrt4j\C++Include` in File Explorer. Similarly, pasting `%localappdata%\Publishers\8vrbkgtyqrt4j\C++Lib` will bring you to `$SysLibDir`.

Project
-------

The whole file is a JSON object of "type" `PROJECT` consisting of the following members
```JavaScript
PROJECT {
	"version"           : INTEGER,
	"name"              : STRING,
	"build_commands"    : BUILD_COMMAND_MAP,
	"build_definitions" : ARRAY OF BUILD_DEFINITION
}
```

Build commands
--------------

`BUILD_COMMAND_MAP` is a JSON object treated as an association (i.e. a dictionary) from `STRING -> BUILD_COMMAND`.
```JavaScript
BUILD_COMMAND {
	"action"          : STRING "interpret" OR "compile" OR "link",
	"args"            : ARRAY OF STRING,
	"sys_include_dir" : ARRAY OF STRING,
	"include_dir"     : ARRAY OF STRING,
	"sys_lib_dir"     : ARRAY OF STRING
}
```
The interpretation of the other members are determined by the `action` key. In any case, the fields `sys_include_dir`, `include_dir` and `sys_lib_dir` are __RELATIVE__ paths to be expanded to absolute path by DevMax i.e. prepended with `$SysIncludeDir` and `$SysLibDir` respectively. The paths in `include_dir` are, on the other hand, interpreted relative to `$ProjectDir`.

Needless to say, `sys_lib_dir` is only considered when the action is `link` whereas the `*include_dir` are only considered for the other two actions.

The field `args` consists of the command line arguments (switches) you usually pass to clang compiler or linker.

Build definition
----------------

A `BUILD_DEFINITION` object consists of a name and an array of `BUILD_STEP`.
```JavaScript
BUILD_DEFINITION {
	"name"        : STRING,
	"build_steps" : ARRAY OF BUILD_STEP
}

BUILD_STEP {
	"command"  : STRING,
	"inputs"   : ARRAY OF STRING,
	"output"   : STRING,
	"log_file" : STRING (C++ Compiler >= 2.6.1)
}
```
The `command` field denote the name of a `BUILD_COMMAND` defined in parent `PROJECT` object. When executing a `BUILD_DEFINITION`, DevMax further adds the `inputs` and `output` to the command after prepending these relative paths with the path to the project. Strings specified in `inputs` and `output` are paths relative to `$ProjectDir`.

`BUILD_STEP` extends `BUILD_COMMAND` so if you don't specify `command`, you can put the whole definition of the object (i.e. `action`, `args`, etc.) in `BUILD_STEP` and an anonymous command will be created.

In version >= 2.6.1 of C++ Compiler, we added a new field `log_file` for the compilation log.

Example
-------

Let us take a simple example. We also illustrate using uninterpreted field to write comments, see the declaration of the `CompileC++` build command. (Note that JSON doesn't support C-style line/block comment.)

```JSON
{
"version":1,
"name":"Example project",
"build_commands": {
	"CompileC++" : {
		"action":"compile",
		"args":["-fms-extensions", "-fms-compatibility", "-x", "c++", "-std=c++14", "-w"],
		"sys_include_dir":["ucrt", "msvc"],
		"include_dir":[""],
		"comment":"The empty string in include_dir has the effect of adding the project folder to non-system header search path. For the record, any field not-interpreted by DevMax can be used to add comment like this."
	},
	"MakeExe" : {
		"action":"link",
		"args":["/defaultlib:msvcrt.lib", "/subsystem:Console"],
		"sys_lib_dir":["msvc", "winsdk"]
	},
},
"build_definitions": [
	{
		"name":"Build program",
		"build_steps": [
			{
				"command":"CompileC++",
				"inputs":["src/Source.cpp"]
			},
			{
				"command":"MakeExe",
				"inputs":["src/Source.o"],
				"output":"Source.exe"
			}
		]
	},
	{
		"name":"Inline/anonymous build command",
		"build_steps": [
			{
				"action":"compile",
				"args":["-fms-extensions", "-fms-compatibility", "-x", "c++", "-std=c++14", "-w"],
				"sys_include_dir":["ucrt", "msvc"],
				"include_dir":[""],
				"inputs":["src/Source.cpp"]
			}
		]
	}
]
}
```

Running the build definition `"Build program"` in DevMax UI has the effect similar to that of running two fairly long commands:
```Bash
clang -isystem $SysIncludeDir/ucrt -isystem $SysIncludeDir/msvc -I $ProjectDir -fms-extensions -fms-compatibility -x c++ -std=c++14 -w -c $ProjectDir/src/Source.cpp -o $ProjectDir/src/Source.o
link /libpath:$SysLibDir/msvc /libpath:$SysLibDir/winsdk /defaultlib:msvcrt.lib /subsystem:Console $ProjectDir/src/Source.o /out:$ProjectDir/Source.exe
```
It is safer than writing these commands if you need to quote arguments correctly.