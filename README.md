# Ghidra Snippets
*Ghidra Snippets* is a collection of Python examples showing how to work with [Ghidra](https://ghidra-sre.org/) APIs. There are two primary APIs, the [Flat Program API][1] and the [Flat Decompiler API][2].

# Latest Release
**Ghidra v9.1** released 23 October 2019. [Download here][0].

# Primary Classes
* [GhidraProject][4]
* [Project][3]
* [Program][5]
* [ProgramDB][6]

# Working with Projects
A Ghidra *Project* (class [GhidraProject][4]) contains a logical set of program binaries related to a reverse engineering effort. Projects can be shared (collaborative) or non-shared (private). The snippets in this section deal with bulk import and analysis, locating project files on disk, and more.

### Get the name and location on disk of the current project
```python
# code here...
```

### List all programs in the current project
```python
# code here...
```

### Load a new program in the current project
```python
# code here...
```

### Remove an program from the current project
```python
# code here...
```

### Selecting an program to work with
```python
# code here...
```

# Working with Programs
A *Program* is a binary component within a Ghidra Project. The snippets in this section deal with gathering information about the Programs within a Project.

### List the current program's name and location on disk
```python
# code here...
```

### Reanalyze the current program
```python
# code here...
```

# Working with Functions
A *Function* is a subroutine within an Program. The snippets in this section deal with gathering information about Functions and modifying them within an Program.

### Enumerate all functions printing their name and address
```python
# Print name and address of all functions in the loaded binary
func = getFirstFunction()
while func is not None:
    print("Function: {} @ 0x{}".format(func.getName(), func.getEntryPoint()))
    func = getFunctionAfter(func)

# Example output:
# Function: _alloca_probe @ 0x1400a8e00
# Function: FUN_1400a8e70 @ 0x1400a8e70
# ... snip ...
```

### Get a function's name by address
```python
# code here...
```

### Get a function's address by name
```python
# code here...
```

# Working with Instructions
A blurb here about this section and working with Instructions...

### Get a function's address by name
```python
# code here...
```

# Working with Basic Blocks
Basic Blocks are collections of continuous non-branching instructions within Functions. They are joined by conditional and non-conditional branches, revealing valuable information about a program and function's code flow. This section deals with examples working with Basic Block models.

### Get a basic block model for a program
```python
# code here...
```

# Working with User Input
A blurb here about this section and working with user input...

### Ask the user to select a function and jump to it
```python
# code here...
```

# Working with the Decompiler
A blurb here about this section and working with the decompiler and P-Code...

### Print decompiled code for each function in the current program
```python
from ghidra.app.decompiler import DecompInterface
from ghidra.util.task import ConsoleTaskMonitor

program = getCurrentProgram()
ifc = DecompInterface()
ifc.openProgram(program)
functions = program.getFunctionManager().getFunctions(True)

ifc.toggleSyntaxTree(True) 			# Produce syntax trees 
ifc.toggleCCode(True)				# Produce C code

for function in list(functions):
    print("Function name: {}".format(function.getName()))
    res = ifc.decompileFunction(function, 0, ConsoleTaskMonitor())
    print(res.getDecompiledFunction().getC())
    break

hf = res.getHighFunction()
print(hf)
```

[0]: https://ghidra-sre.org/
[1]: https://ghidra.re/ghidra_docs/api/ghidra/program/flatapi/FlatProgramAPI.html
[2]: https://ghidra.re/ghidra_docs/api/ghidra/app/decompiler/flatapi/FlatDecompilerAPI.html
[3]: https://ghidra.re/ghidra_docs/api/ghidra/framework/model/Project.html
[4]: https://ghidra.re/ghidra_docs/api/ghidra/base/project/GhidraProject.html
[5]: https://ghidra.re/ghidra_docs/api/ghidra/program/model/listing/Program.html
[6]: https://ghidra.re/ghidra_docs/api/ghidra/program/database/ProgramDB.html