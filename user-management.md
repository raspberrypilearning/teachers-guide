# Managing updates and users

There are several options for handling multiple users and keeping SD cards up to date, ranging from the simple but time-consuming to the complex but quick options.

## One student, one card

- The easiest way to manage multiple users on your Raspberry Pis is to provide each student with their own micro SD card.

- Each micro SD card can be kept by the students, or, more realistically, can be kept safe (and labelled) by the teacher. This way, each student's work and their programming environment is kept safe on the card, and only they have access to it.

## Mounting a Windows share

- It may be possible to gain access to your school's Windows shared directories, thereby allowing students to save their work in their school "home" folders. This will only help manage their files, and not their actual environment.

- Your success with this will depend on the network infrastructure, so you may need to consult your network administrator.

- Your Raspberry Pis will need a program called CIFS, which you can install with the following command:

``` bash
sudo apt-get update && sudo apt-get install cifs-utils
```

- On the Raspberry Pi, your students will need to create a directory where the Windows share can be mounted:

``` bash
mkdir /mnt/winHome
```

- Then a command like this should mount their home folder:

``` bash
mount -t cifs //SchoolServer/StudentFolders/YearFolder/StudentFolder -o username=aStudent,password=aPassword /mnt/winHome
```

- The `//SchoolServer/StudentFolders/YearFolder/StudentFolder` part of the command will depend on your network, so you'll need to ask your network administrator for the **path** to the students' folders.

- Once the folders are mounted, students can access their folder by typing the following:

``` bash
cd /mnt/winHome
```

## Using PiNet

- PiNet is a solution to managing both user files and their programming environment.

- With PiNet you use another computer as a managing server; an old laptop or desktop will do. The Raspberry Pis boot from the PiNet server, rather than from their SD cards, giving you complete control of the users' files.

- Additionally, with PiNet you can easily keep all the Raspberry Pis up to date and install new software.

- Rather than detailing how to set up PiNet here, it's better to check out the website to see if it's the right solution for you. You can get full details of PiNet by visiting their [website](http://pinet.org.uk/).
