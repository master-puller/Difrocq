# Difroc
A simple tool for testing standalone programs with test cases.
Will only test using stdin and stdout against separate files. If difroc does not output anything when running a command, all the test cases have passed.
Due to it's versatility, this allows for debugging a program using other debugging utilities. One such example is valgrind (which has proved extremely useful)
`difroc valgrind ./a.out [opts]`

# About
Wrote this little script to test my c++ programs in a course I was doing, as it became tedious
writing lots of testing libs all the time.

Difroc now supports passing arguments to commands from files. This is mutually exclusive with piping to the commands stdin.

Usage: `$0 [OPTION] cmd [CMDOPTS]`
> Difroc runs cmd against every input file in dir and compares output
>  useful for testing standalone programs

**DIFROC is NOT SANITIZED. DO NOT USE WITH UNTRUSTED INPUT**

## Options:
```
    -d  (dir) [DIR]             directory of test files
          defaults to "./tests/"
    -i  (inext) [INEXT]          input file extension
            defaults to ".in"
    -I  (install)               installs difrocq to /usr/local/bin
    -U  (uninstall)              removes difroc from /usr/local/bin
    -f  (force)                 force run even if overwrites will occur
    -r  (runext) [RUNEXT]        run file extension
            default: ".run"
    -o  (outext) [OUTEXT]       output (test expected) file extension
            default: ".out"
    -c  (cleanup)                removes run files afterward
    -q  (quiet)                 only outputs which files mismatch
    -a  (args-input)             passes file contents as an argument"
                                    catted to args, no stdin"
    -g  (grep)                  greps run output for expected output
```
### Examples
`difroc -c -d ./tests/example/ cat`
cats every file that matches the glob `tests/example/*.in`, and compares them against `tests/example/*out`.
(Usually not useful, unless you're building a cat program I guess...)

`difroc -I`
Installs difroc to `/usr/local/bin` (it's only one file, but its convenient)

`difroc -U`
ditto but removes.

`difroc valgrind ./a.out hello world`
valgrind a.out hello world
with inputs piped from ./tests/
