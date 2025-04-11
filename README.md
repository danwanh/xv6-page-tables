# xv6 Page Tables Lab

## Description
This lab is designed to deepen understanding of xv6’s virtual memory and system call mechanisms. It is part of my *Operating Systems* course.
It extends the xv6 operating system with two features:
1. `vmprint()`: A kernel function to visualize the hierarchical page table of a process.
2. `pgaccess()`: A new system call to detect which pages have been accessed by inspecting the access bits (`PTE_A`) in the RISC-V page table.
 ## How to Test
Compile and run xv6:
```sh
$ make qemu
```
## Testing the page table printing
Run a user program with the `--print_pagetable` option:
```sh
<command> --print_pagetable
```
Replace <command> with any executable such as `init`, `echo`, etc.

If the user does not want to print the page table, simply omit the `--print_pagetable` flag.

For example: 
```sh
init --print_pagetable
```
Output:
```sh
page table 0x0000000087f34000
 ..0: pte 0x0000000021fd4401 pa 0x0000000087f51000
 .. ..0: pte 0x0000000021fd1401 pa 0x0000000087f45000
 .. .. ..0: pte 0x0000000021fcdc1b pa 0x0000000087f37000
 .. .. ..1: pte 0x0000000021fd1017 pa 0x0000000087f44000
 .. .. ..2: pte 0x0000000021fd4007 pa 0x0000000087f50000
 .. .. ..3: pte 0x0000000021fc7017 pa 0x0000000087f1c000
 ..255: pte 0x0000000021fcd401 pa 0x0000000087f35000
 .. ..511: pte 0x0000000021fcd801 pa 0x0000000087f36000
 .. .. ..510: pte 0x0000000021fc9407 pa 0x0000000087f25000
 .. .. ..511: pte 0x000000002000180b pa 0x0000000080006000
init: starting sh
```

## Testing accessed pages detection
To test the pgaccess() system call:

- A custom test function is implemented in `pgtbltest.c` that manually accesses pages at indices 0, 2, and 4.

- If the output correctly indicates these pages as accessed, it confirms that pgaccess() is working properly
Run:
```sh
pgtbltest
```
Ouput:
```sh
pgaccess_test starting
pgaccess_test: OK
```
