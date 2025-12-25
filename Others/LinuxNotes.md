# Linux
Geeks-For-Geeks Reference - https://www.geeksforgeeks.org/linux-unix/introduction-to-linux-operating-system/

SS64 A-Z Commands - https://ss64.com/

## What is Linux?
Linux is a free open-source operating system kernel.
Linux is based on the UNIX operating system.

## What is a Kernel?
A kernel is the core component of an operating system that acts as a bridge between software and the computer's hardware.

## What is Bash?
Bash is a Unix shell and a command-line interpreter that acts as an interface for running commands and writing scripts on Linux and macOS systems.

### Why do you need a './' to execute a script in Bash?
 - **PATH Environment Variable**: The PATH variable is a list of directories where the shell searches for executable commands. When you type a command like ls or grep, the shell looks for these executables in the directories listed in PATH.
 
 - **Current Directory Exclusion**: By default, the current working directory (.) is usually not included in the PATH for security reasons. This prevents accidental execution of potentially malicious scripts located in the current directory.

 - **Explicit Path Specification**: To execute a script located in the current directory, you must explicitly tell the shell where to find it. The ./ prefix does this by specifying the "current directory" (.) and then the script's name. This bypasses the PATH search and directly points to the executable in the current location.

**Note**: Executable Permission: Regardless of using ./ or having the script in PATH, the script file must also have execute permissions (chmod +x scriptname) to be run as an executable.

## What is Shell?
The Shell is also software or It can be determined as the interface to the kernel. It takes commands from the user and interprets them. The Shell transmits these commands to the kernel, which then performs the requested operations. Users can just enter the commend and using the kernel's function that specific task is performed accordingly.

### Different Shells
    - Bourne Shell (sh)
    - C Shell (csh)
    - Korn Shell (ksh)
    - Bash (Bourne Again Shell)
    - Z Shell (zsh)
    - Fish (Friendly Interactive Shell)

## What is distributions?
Distributions bundle the Linux kernel with other software, such as desktop environments, system utilities, and applications, to create a user-friendly OS.

### Examples of Linux Distributions (Distros)
    - Debian
    - Ubuntu (Based on Debian)
    - RHEL (Red Hat Enterprise Linux)
    - CentOS (Built from the same source code as RHEL)

## What is Operating System (OS)?
An operating system (OS) is the core software that manages a computer's hardware and software resources, acting as an intermediary between the user and the computer.

### Examples of Operating Systems
    - MS-DOS
    - Windows Operating System 
    - LINUX Operating System
    - Solaris Operating System
    - Symbian Operating System
    - Android Mobile Operating System
    - iOS Mobile Operating System
    - FreeBSD 
    - Chrome OS
    - Mac OS

### Operating System (OS) Architecture

Hardware > Kernel > Shell > Applications

## What is ISO?
International Organization for Standardization (ISO)
An **ISO image** is a single file containing the exact contents and file structure of an optical disc like a CD, DVD, or Blu-ray. 
It's used to:
    - back up or archive the data from a physical disc
    - distribute software
    - mount a virtual disc on a computer. 

## What is a Virtual Machine (VM)?
A virtual machine (VM) is a software-based, virtual computer that runs on a physical computer, allowing you to run a separate operating system and applications within it. It acts like a complete, independent computer, using a portion of the host computer's resources like CPU, memory, and storage.

### Examples of Virtual Machines
    - Oracle VM Virtual Box
    - VMWare Workstation
    - Microsoft Hyper-V
    - Parallels Desktop

## What are Guest Additions?
Guest Additions are a set of drivers and utilities installed inside a Virtual Machine (guest OS) to imporve performance and integration with the host system.

Most commonly associated with Oracle Virtual Box but similar tools exist in other hypervisors (like VMware Tools for VMware or Hyper-V Integration Services for Hyper-V)

### Examples of features Guest Additions provide
    - Better Video Performnace
    - Shared Clipboard
    - Shared Folders
    - Mouse Pointer Integration
    - Time Synchronization
    - Seamless Mode
    - Automated Logins

## What is GNU? (GNU's Not Unix) ~ Recursive Joke
Free and Open-Source Operating System Project started in 1983 by Richard Stallman. The goal was to create a **Unix-Operating System** that was **completely free software**, allowing users to **run, modify, share and study** software freely.

The GNU Project core tools that make up a working operating system
    - GNU Bash (Command-line Shell)
    - GNU Coreutils (Bash tools like ls, cp, mv, cat, echo)
    - GNU Compiler Collection (GCC)
    - GNU C Library (glibc)
    - GNU Make (Tool for building and compiling software)
    - GNU Emacs (popular text editor)

## What is GNOME?
GNOME is a free and open-source desktop environment for Linux that provides a user-friendly graphical interface for users to interact with their operating system.

## vim
Vim, which stands for "Vi Improved," is a free and open-source, cross-platform text editor based on the original vi editor.

## Atom
Atom was a free, open-source, and "hackable" text editor for macOS, Linux, and Windows, developed by GitHub.
https://atom-editor.cc/

## Environment Variables in Linux
Geeks for Geeks Reference - https://www.geeksforgeeks.org/linux-unix/environment-variables-in-linux-unix/

    Examples:
        - HOME
        - PATH
        - USER
        - HOSTNAME
        - EDITOR

## Purpose of shebang (#!) in Shell Scripts?
To specify the path to the interpreter that should execute the script.

Example: 

```Bash
     #!/usr/bin.env bash #-> Bash Interpreter
     #!/usr/bin.env python #-> Python Interpreter
```

## What is checksum in Bash?
 - In the context of a Bash shell, a checksum is an alphanumeric value generated from a file's contents using a cryptographic hashing algorithm. It acts as a digital fingerprint for that file, uniquely representing its data.

Purpose of Checksums in Bash:
    - **Data Integrity Verification**:
        The primary use of checksums is to verify that a file has not been corrupted or altered during transmission, storage, or processing. If the calculated checksum of a file matches a previously known, trusted checksum, it confirms the file's integrity. 
    - **File Comparison**:
        Checksums can be used to quickly determine if two files are identical without needing to compare their entire contents byte-by-byte. If their checksums match, the files are considered the same.
    
Example:

    ```Bash
        cksum example.txt
    ```

Other Checksums:
    - md5sum
    - sha1sum
    - sha256sum
