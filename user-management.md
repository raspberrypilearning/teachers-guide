# Managing updates and users

There are several options for handling multiple users and keeping SD cards up-to-date, ranging from the simple (but time consuming) to the complex (but quick) options.

## One Student, One Card

- The easiest way to manage multiple users on you Raspberry Pi Computers, is to provide each student with their own microSD card.
- microSD cards can be kept by the students, or more realistically be kept safe (and labelled) by the teacher. This way, all the student's work and their programming environment is kept safe on the card, and only they have access to it.

## Mounting a Windows Share

- It may be possible to gain access to your school's Windows shared directories, thereby allowing students to save their work in their school "home" folders. This will only help manage their files, and not their actual environment.
- You success at achieving this will depend on the network infrastructure, so you may need to consult your network administrator.
- Your Raspberry Pis will need a program called `cifs`.

``` bash
sudo apt-get update && sudo apt-get install cifs-utils
```

- On the Raspberry Pi, your students will need to create a directory where the Windows share can be mounted.

``` bash
mkdir /mnt/winHome
```

- Then a command like this should mount their home folder.

``` bash
mount -t cifs //SchoolServer/StudentFolders/YearFolder/StudentFolder -o username=aStudent,password=aPassword /mnt/winHome
```

- The actual `//SchoolServer/StudentFolders/YearFolder/StudentFolder` part of the command will depend on your network, so you'll need to ask your network manager what the **path** to the students' folders is.

- Once the folders are mounted, students can access their folder by typing:

``` bash
cd /mnt/winHome
```

## Using PiNet

- PiNet is a solution to managing both user files and their programming environment.
- With PiNet you use another computer (an old laptop or desktop will do), as a managing server. The Raspberry Pi's boot from the PiNet server, rather than from their SD cards, giving you complete management control of the users' files.
- Additionally, with PiNet, you can easily keep all the Raspberry Pis up-to-date, and install new software.
- Rather than detailing how to setup PiNet here, you are better off checking out the website, to see if it is the right solution for you. You can get full details of [PiNet by clicking here](http://pinet.org.uk/)
