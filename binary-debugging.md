Before attempting to debug memory remember to use -g (-g2) to include debugging symbols and -O0 possibly if you want to make asm easier to read.

# Valgrind
`pacman -S valgrind`

A CPU emulator that can track memory usage among other things
Use `--tool=` to select usage mode
- memcheck
- ~~cachegrind~~
- callgrind
- ~~helgrind~~
- ~~drd~~
- ~~massif~~
- ~~dhat~~
- ~~lackey~~
- ~~exp-bbv~~
- ~~none~~

Just running `valgrind ./your-program` will check for memory leaks and show amount of memory used

## Kcachegrind
`pacman -S kcachegrind`

A GUI to visualize call stack info

First collect a dump with valgrind
```shell
$ valgrind --tool=callgrind ./your-program
```
output will be stored in a file called `callgrind.out.XXXX`

Now you can view the call stack with kcachegrind
```shell
$ kcachegrind ./callgrind.out.XXXX
```

# Heaptrack
`pacman -S heaptrack`

A GUI to analyse memory usage of a program

## Attaching to running process
(requires kernel.yama.ptrace_scope=0)
```shell
$ heaptrack -p $(pgrep your-program)
```
When the process exits heaptrack will automatically open a GUI showing memory usage