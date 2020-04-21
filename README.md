# PythonCompileTool
High level python compilation tool.

## What does it do?
With a given version number it downloads the python source from python.org if it doesnt
already exist in the selected directory (`--directory`) default is current users `Documents`.

It then reads reads what compiler options was used for the given python executable
and passes all those arguments + `--enable-optimizations` and `--with-lto` (unless `--without-optimizations` is given) + extra arguments you pass to `pct`\
If its not desired to copy options from another python install pass None.

Then `./configure` runs with all found options `make` with the given `--threads` and `makealtinstall` (will ask for sudo password).

## When is this useful?
The system python interpreter does not come compiled with optimizations enabled (at least mine didnt)
 and I believe that the deadsnakes ppa doesnt compile with optimizations either. 
 So if you want python with optimizations enabled it makes things a little easier.\
 When a new python release is out its very easy to copy the options from a specified python executable 
 to build the new version.


## Usage:
`./pct <version number> <python executable> <pct options> <extra options for configure script>`\
with options its possible to modify:
* Where the python source is downloaded to / directory  for compilation ends up. (`--directory`)
* Amount of jobs that are spawned concurrently for make (`--threads`)
* If optimizations should be included (included by default). (`--without-optimizations`)

## Examples:
Compile 3.8.2 with compile options from python3 + optimizations:\
`./pct 3.8.2 python3`

Compile python3.8.2 without copying compile options with optimizations:\
`./pct 3.8.2 None`

Compile 3.7.7 with your compile options from 3.8
`./pct 3.7.7 python3.8`

Compile 3.8.2 with compile options from python3 without optimizations:\
`./pct 3.8.2 python3 --without-optimizations` 

Compile 3.6.10 with compile options from python3 with pydebug and without optimizations:\
`./pct 3.6.10 python3 --without-optimizations --with-pydebug`
