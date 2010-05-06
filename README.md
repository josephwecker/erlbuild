# ErlBuild #
Quick makefile replacement for Erlang projects.

## Current Features

* Sane defaults (convention over configuration)
* Only compiles when it needs to.
* Can package targets up into an escript-executable file.
* Exits with error codes as necessary.
* Quiet on stdout, info on stderr.
* Self-contained- no dependencies other than erlang (escript)
* Hopefully understandable error messages and warnings

## Usage

erlbuild (-f OtherEBFile) (target=all)

When you run erlbuild it looks for either an "ebfile" or ".ebfile" (in that
order) in the current directory unless a different file is specified with the
-f option.

It opens that file and looks for the specified target.  If no target is
specified it looks for "all."  If that target is not defined it simply runs the
topmost target in the file.  If there are no targets defined at all, it simply
runs a target with all default values- which basically looks for all ".erl"
files in the "src" directory, includes the "include" directory- and compiles
and outputs beams to the "ebin" directory.

### ebfile format

All parameters are optional.

The ebfile (or .ebfile) will have any number of targets defined like this:

    {target_name, [
      {option, value}, ...
      ]}.
    ...

Targets are generally only meant to compile one chunk of source files- so if
you want to compile source files from several directories it would be more
appropriate in erlbuild to have those as different erlbuild targets and then
combine them in a single target.

The options are (with their default values):

<table border="1px">
<tr><th>Option</th><th>Type</th><th>Default</th><th>Example</th></tr>

<tr><td>other_targets</td>
<td>List of targets:atoms</td>
<td>[]</td>
<td>[main, test]</td></tr>

<tr><td>external_ebfiles</td>
<td>List of external ebfiles:string|atom</td>
<td>[]</td>
<td>[otherone, "tools/another/.ebfile"]</td></tr>

<tr><td>src_dir</td>
<td>Directory to find sources:string|atom</td>
<td>src</td>
<td>"../elsewhere/sources"</td></tr>

<tr><td>sources</td>
<td>List of sources or glob of sources to compile:string|atom</td>
<td>"*.erl"</td>
<td>[first, second, "third.erl"]</td></tr>

<tr><td>includes</td>
<td>List of include directories</td>
<td>[include]</td>
<td>[include, "/src/kernel/erlang-inc"]</td></tr>

<tr><td>dest_dir</td>
<td>discover (escript->"bin", beams->"ebin")|atom|string</td>
<td>discover</td>
<td>"../ebin"</td></tr>

<tr><td>dest_type</td>
<td>discover (exp. "main/1" -> escript else beams)|beams|escript</td>
<td>beams</td>
<td>escript</td></tr>

<tr><td>exec_name</td>
<td>discover (exported "main/1" = mod_name) or atom|string</td>
<td>discover</td>
<td>my_executable</td></tr>
</table>

## Examples


## To Install


## Current Issues

* Only tested on Mac OSX and Linux

## Future

* Copying / moving / directory manipulation
* Have a bootstrapper so I can modularize the code a little better
* Good globber
* Integrate unit-testing
* Integrate dialyzer
* Integrate quickcheck (?)
* Precompiled build binary for slight speed improvement
* Colored output if desired


# MIT License #
Copyright (c) 2010 Joseph Wecker

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.

