# command-line-cheat-sheet

## lsof

lists opened files.

- Everything is a file in Linux/Unix system.
- gives the information to find out the files which are opened by which process.
- it can list common regular files, a directory, a block special file, a shared library, a character special file, a regular pipe, a named pipe, an internet socket, a UNIX domain socket, and many others.
- can be combined with grep command can be used to do advanced searching and listing.

### Options

- -i - selects the listing of files any of whose Internet address matches the address specified in i.
- -n - inhibits the conversion of network numbers to host names for network files. (eg. TCP localhost:62510 (LISTEN) becomes TCP 127.0.0.1:62510 (LISTEN))
- -P - selects by the PID

```bash
# list all processes(= files) that are listening
sudo lsof | grep LISTEN

# see a specific port such as 22 #
sudo lsof -i:22
```

### Output

[Linux man page](https://man7.org/linux/man-pages/man8/lsof.8.html)

- COMMAND - the first nine characters of the name of the UNIX command associated with the process. Add +c w to show the first w characters of the command
- PID
- TID - a task ID. A blank TID column in Linux indicates a process - i.e., a non-task
- USER - the user ID number or login name of the user to whom the process belongs. Usually that is the same value reported by ps, but may differ when the process has changed its effective user ID.
- FD - File Descriptor number of the file, followed by the access mode: r(read), w(write), u(r&w),or a space/'-'(unknown)
- TYPE - type of the node associated with the file. eg. IPv4, IPv6
- NODE - node number of the local file or internet protocol (eg. TCP).
- SIZE - the size of the file or the file offset in bytes. 0t0 mean a file with the size 0 in decimal notation. All files with that reported size will be things like sockets, pipes, open TCP connections, devices and the like.
- NAME - the name of the mount point and file system on which the file resides

```bash
# A TCP connection named KaKaoTalk is running with process 19496 by user hayounlee with read & write access on IPv4 socket.
# The connection is established from the local address 192.168.0.38:52200 to the remote address 203.217.229.115:443
KakaoTalk 19496 hayounlee   32u  IPv4 0xe8fe10a0cfafdb5d      0t0  TCP 192.168.0.38:52200->203.217.229.115:443 (ESTABLISHED)
```
