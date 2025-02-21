# Manage files and directories

Linux environment set up on an EC2 instance, using Amazon Linux 2023 AMI.

### Create, copy, move files and directories, use tree, locate command.

- Making test directories

<img src=images/lab-1/image-1.png width=500>

- Creating a file and moving the file

<img src=images/lab-1/image-2.png width=500>

- Creating empty files, copying files, moving whole directories

<img src=images/lab-1/image-3.png width=500>

- Locating files

<img src=images/lab-1/image-4.png width=500>

### Show the full path name of your home directory.

- Print the working directory (which currently is home, marked by ~) or alternatively, print the environment variable `$HOME`

<img src=images/lab-1/image-5.png width=500>

### Change permission file/directory (read, write, execute).

- Checking the permission of dir1, removing the owner's execute permission, so I can't `cd` into it. Adding the permission back lets me execute commands onto the directory again.

<img src=images/lab-1/image-6.png width=500>

- Writing test content into a test file, then removing read and write permissions sequentially. Tested with `cat` and `echo`.

<img src=images/lab-1/image-7.png width=500>

### Compress, extract files and directories with zip, tar, 7z, …

- Current working directory:

<img src=images/lab-1/image-8.png width=300>

- Archiving and compressing dir1 and dir2 into test.tar.gz, then decompressing and extracting into tardir

<img src=images/lab-1/image-9.png width=500>

- Flags used:
  - `-z` puts the archive through gzip for compression/decompression
  - `-c` means create archive
  - `-f` specifies the filename of the resulting/target (compressed) archive
  - `-x` means extract from archive
  - `-C` changes the directory, allowing tar to extract to directories other than current working directory.

### Edit file by `vim`, `nano`.

- Only results will be shown, since demonstration of use for text editors are best shown directly or over video

- Editing with `vim`

<img src=images/lab-1/image-10.png width=500>

- Editing with `nano`

<img src=images/lab-1/image-11.png width=500>

### Use winscp transfer files from other machine to Ubuntu

Transferring windows files to remote EC2 Amazon Linux server.

- Open WinSCP, fill in info taken from Amazon EC2 console

<img src=images/lab-1/image-12.png width=500>

- Advanced > SSH > Authentication, select the correct key pair file

<img src=images/lab-1/image-13.png width=500>

- Log in. The remote server's files will be shown on the left.

<img src=images/lab-1/image-14.png width=500>

- Transferring files is then a simple drag-and-drop

<img src=images/lab-1/image-15.png width=500>

- Checking the file on the remote server

<img src=images/lab-1/image-16.png width=500>