###Terminal Guide###

1) Navigation

cd Documents ;Change Directory.
ls ;List files and directories.
pwd ;List files and directories.

###

2) File and Directory Operations

mkdir NewDirectory ;Create a new directory.
touch filename.txt ;Create an empty file or update the access and modification times of a file.
cp file.txt /path/to/destination ;Copy files or directories.
mv oldfile.txt newfile.txt ;Move or rename files or directories.

###

3) File Viewing and Editing

cat filename.txt ;Display the contents of a file.
nano filename.txt ;Text editors for creating or modifying files.
OR
vim filename.txt ;Text editors for creating or modifying files.

###

4) File Deleting

rm filename.txt ;Remove files or directories.

###

5) Searching

grep "pattern" file.txt ;Search for patterns in files.

###

6) System Information

top ;Display system activity and processes.
df -h ;Show disk space usage.

###

7) User and Permissions
whoami ;Display the current username.
chmod 755 filename ;Change file permissions.

###

8) Package Management (if using Homebrew)

brew install packageName ;Homebrew package manager commands.

###

9)Networking

ping example.com ;Send network requests to a specific host.
ifconfig OR ipconfig ;Display network interface configuration.

###

10) SSH

ssh username@hostname ;Connect to a remote server via SSH.

###

11) ls Manual Page

man ls ;manual page for the ls command, providing detailed information about its usage and options.

###

12) sudo fs_usage

Real-time statistics about file system activity, showing which processes are accessing files.

###

13) lsof

(short for "list open files") is used in Unix-like operating systems to display a list of all open files and the processes that opened them

###

14) top
Run this to get a live view of processes and memory usage

15) free -h *Check
This provides a quick summary of memory usage

16) vmstat -s *Check
This is helpful for checking memory along with CPU usage

17) ps aux | grep [process_name]
To get memory usage for a specific process, use:

18) htop
If you have htop installed, it provides a more user-friendly view