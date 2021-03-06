---
layout: page
title: "Introduction to the Shell"
comments: true
date: 2017-03-17
---

## Learning objectives
---

* Explain what the `shell` is and how to use the `shell` to navigate the file system and execute commands.
* Describe the principles and strategies for working at the command line.
* Apply the `shell` to make computing more reproducible and more powerful.
* Construct searches for characters or patterns in a text file using the `grep` command
* Employ output redirection.
* Explain how to use the pipe `|` character to chain together commands.


## Starting with the shell
---

Now that we are connected to the cloud, we have file directories available to us to explore. Let's learn a few commands by investigating the folders in the `dc_sample_data` directory:

```
$ cd dc_sample_data
```

> `cd` stands for 'change directory'

Let's see what is inside the folder. Type:

```
$ ls
```

You will see:

```
sra_metadata  untrimmed_fastq
```

> `ls` stands for 'list' and it lists the contents of a directory.

There are two items listed.  What are they? We can use a command line "modifier" with `ls` to get more information; this modifier is called an argument (more below).

```
$ ls -F

# option -F = adds symbols to highlight directory contents

sra_metadata/  untrimmed_fastq/
```

Anything with a `/` after it is a directory. Things with a `*` after them are programs. If there are no decorations after the name, it's a file.

You can also use the command `ls -l` to see whether items in a directory are files or directories.

```
$ ls -l

# option -l = 'list in long format'
```

```
drwxr-x--- 2 dcuser dcuser 4096 Jul 30 11:37 sra_metadata
drwxr-xr-x 2 dcuser dcuser 4096 Jul 30 11:38 untrimmed_fastq
```

Let's go into the `untrimmed_fastq` directory and see what is in there.

```
$ cd untrimmed_fastq

$ ls -F
```

```
SRR097977.fastq  SRR098026.fastq
```

There are two items in this directory with no trailing slashes, so they are files.


### Arguments
---

Most commands take additional arguments that control their exact behavior. For example, `-F` and `-l` are arguments to `ls`.  The `ls` command, like many commands, takes a lot of arguments. Another useful one is '-a', which shows everything, including hidden files.

How do we know what arguments are available for particular commands? Most commonly used shell commands have a manual. You can access the manual using the `man` command. Try entering:

```
$ man ls
```

This will open the manual page for `ls`. Use the `space key` to go forward and `b` to go backwards. When you are done reading, just hit `q` to quit. The keyboard arrows also work.

Commands that are run from the shell can get extremely complicated. To see an example, open up the manual page for the `find` command. No one can possibly learn all of these arguments, of course. So you will probably find yourself referring to the manual page frequently.

> If the manual page within the terminal is hard to read and traverse, the manual exists online, use your web searching powers to get it! In addition to the arguments, you can also find good usage examples online; Google is your friend.

## The Unix directory file structure (a.k.a. where am I?)
---

As you've already just seen, you can move around in different directories
or folders at the command line. You are probably accustomed to navigating around the normal way using a GUI (GUI = Graphical User Interface, pronounced *gooey*), but you will find that it's not too difficult once you get the hang of it.

### Moving around the file system
---

Let's practice moving around a bit. Previously, we moved to the `untrimmed_fastq` directory.

To get there, we first changed directories from the folder of our username (dcuser) to
`dc_sample_data` then we changed directories to `untrimmed_fastq`

Let's draw out how that went.

Now let's draw some of the other files and folders we could have clicked on.

This is called a hierarchical file system structure, like an upside down tree
with root (/) at the base that looks like this:


![](../img/Slide1.jpg)

That root (`/`) is often also called the 'top' level.

When you are working at your computer or log in to a remote computer, you are on one of the branches of that tree, your home directory (`/home/dcuser`)

Now let's go do that same navigation at the command line.

Type:

```
$ cd
```

This puts you in your home directory. No matter where you are in the directory system, `cd` will always bring you back to your home directory.

Now using `cd` and `ls`, go in to the `untrimmed_fastq` directory and list its contents.

Let's also check to see where we are. Sometimes when we're wandering around
in the file system, it's easy to lose track of where we are and get lost.

If you want to know what directory you're currently in, type:

```
$ pwd
```

This stands for 'print working directory'. The directory you're currently working in.

What if we want to move back up and out of the `untrimmed_fastq` directory? Can we just
type `cd dc_sample_data`? Try it and see what happens.

To go 'back up a level' we need to use `..`

Type

```
$ cd ..
```

> `..` denotes parent directory, and you can use it anywhere in the system to go back to the parent directory.

Now do `ls` and `pwd`.


### Exercise
---

Now we're going to try a hunt.  Find a hidden directory in `dc_sample_data` and list its contents.  What is the name of the text file in the hidden directory?

**Hint**: hidden files and folders in unix start with `.`, for example `.my_hidden_directory`.

**Another hint**: look through the `man` page for `ls` to list all directories.


### Full vs. Relative Paths
---

The `cd` command takes an argument which is the directory
name. Directories can be specified using either a **relative path** or a **full path**. As we know, the directories on the computer are arranged into a hierarchy. The full path tells you where a directory is in that hierarchy.

Navigate to the home directory (`cd `). Now, enter the `pwd`
command and you should see:

```
/home/dcuser
```

which is the full path for your home directory. This tells you that you are in a directory called `dcuser`, which sits inside a directory called `home` which sits inside the very top directory in the hierarchy. The very top of the hierarchy is a directory called `/` which is usually referred to as the **root directory**. So, to summarize: `dcuser` is a directory in `home` which is a directory in `/`.

Now enter the following command:

```
$ cd /home/dcuser/dc_sample_data/.hidden
```

This jumps to `.hidden`. Now go back to the home directory (`cd`).

Now type the following:

```bash
$ cd dc_sample_data/.hidden
```

This command had the same effect as the previous command - taking us to the `hidden` directory. But instead of specifying the full path (`/home/dcuser/dc_sample_data/.hidden`), we specified a *relative path*. In other words, we specified the path **relative to our current
directory**.

A full path always starts with a `/`, a relative path does
not.

A relative path is like getting directions from someone on the street. They tell you to "go right at the Stop sign, and
then turn left on Main Street". That works great if you're standing there together, but not so well if you're trying to tell someone how to get there from another country. A full path is like GPS coordinates. It tells you exactly where something is no matter where you are right now.

You can usually use either a full path or a relative path depending on what is most convenient. If we are in the home directory, it is more convenient to just enter the relative path since it involves less typing.

Over time, it will become easier for you to keep a mental note of the structure of the directories that you are using and how to quickly navigate amongst them.


### Examining the contents of other directories
---

By default, the `ls` commands lists the contents of the working directory (i.e. the directory you are in). You can always find the directory you are in using the `pwd` command. However, you can also give `ls` the names of other directories to view.

Navigate to the home directory if you are not already there.

Type:

```
$ cd
```

Then enter the command:

```
$ ls dc_sample_data
```

This will list the contents of the `dc_sample_data` directory without you having to navigate there.

The `cd` command works in a similar way. Try entering:

```
$ cd

$ cd dc_sample_data/untrimmed_fastq

$ pwd
```

You will jump directly to `untrimmed_fastq` without having to step through
the intermediate directory.


### Exercise
---

List the 'SRR097977.fastq' file from your home directory without changing directories


## Saving time with shortcuts
---

There are several shortcuts which you should know about, but today we are going to talk about only a few. As you continue to work with the shell and on the terminal a lot more, you will come across and hopefully adapt many other shortcuts.

Dealing with the home directory is very common. So, in the shell the tilde character, `~`, is a shortcut for your home directory. Navigate to the `dc_sample_data/sra_metadata/` directory:

```
$ cd

$ cd dc_sample_data/sra_metadata/
```

Then enter the command:

```
$ ls ~
```

This prints the contents of your home directory, without you having to
type the full path.

Another shortcut is the "..", which we encountered earlier:

```
$ ls ..
```

The shortcut `..` always refers to the directory above your current directory. So, it prints the contents of the `/home/dcuser/dc_sample_data`. You can chain
these together, so:

```
$ ls ../../
```

prints the contents of `/home/dcuser` which is your home
directory.

Finally, the special directory `.` always refers to your
current directory.

```
$ ls .
```

So, `ls`, `ls .`, and `ls ././././.` all do the
same thing, they print the contents of the current directory. This may seem like a useless shortcut right now, but it is needed to specify a destination, e.g. `cp ../data/counts.txt .` or `mv ~/james-scripts/parse-fasta.sh .`.

To summarize, while you are in your home directory, the commands `ls ~`, `ls ~/.`, and `ls /home/dcuser` all do exactly the same thing. These shortcuts are not necessary, but they are really convenient!


### Tab Completion
---

Tab completion is an important shortcut to know; it improves efficiency navigating the file system and helps avoid typos.

To practice with tab completion, let's first navigate to your home directory.

```
$ cd
```

Typing out directory names can waste a lot of time. When you start typing out the name of a directory, then hit the tab key, the shell will try to fill in the rest of the directory name. For example, type `cd` to get back to your home directy, then enter:

```
$ cd dc_<tab>
```

The shell will fill in the rest of the directory name for `dc_sample_data`. Now go to `dc_sample_data/untrimmed_fastq`

```
$ cd un<tab>
$ ls SR<tab><tab>
```

When you hit the first tab, nothing happens. The reason is that there are multiple directories in the home directory which start with `SR`. Thus, the shell does not know which one to fill in. When you hit
tab again, the shell will list the possible choices.

### Wild cards

Navigate to the `~/dc_sample_data/untrimmed_fastq` directory. This directory contains FASTQ files from our RNA-Seq experiment.

The `*` character is a shortcut for "everything". Thus, if you enter `ls *`, you will see all of the contents of a given directory. Now try this command:

```
$ ls *fastq
```

This lists every file that ends with a `fastq`. This command:

```
$ ls SRR*
```

Lists every file in that starts with the characters `SRR`.

```
$ ls *977.fastq
```

Lists only the file that ends with '977.fastq'

So how does this actually work? Well...when the shell (bash) sees a word that contains the `*` character, it automatically looks for filenames that match the given pattern.

We can use the command 'echo' to see wilcards are they are intepreted by the shell.

```
$ echo *.fastq
```

```
SRR097977.fastq SRR098026.fastq
```

The `*` is expanded to include any file that ends with '.fastq'


### Exercise
---

1. Change directories to your home directory, and list the contents of `dc_sample_data/sra_metadata/` without changing directories again.

1. List the contents of the /bin directory. Do you see anything familiar in there? How can you tell these are programs rather than plain files?

1. Do each of the following using a single `ls` command without navigating to a different directory.

	1.  List all of the files in `/bin` that start with the letter 'c'.
	1.  List all of the files in `/bin` that contain the letter 'a'.
	1.  List all of the files in `/bin` that end with the letter 'o'.
	1. **BONUS**: List all of the files in '/bin' that contain the letter 'a' or 'c'


## Command History
---

You can easily access previous commands.  Hit the up arrow.
Hit it again.  You can step backwards through your command history.

The up arrow takes your backwards in the command history.

^-C will cancel the command you are writing, and give you a fresh prompt.

^-R will do a reverse-search through your command history.  This is very useful.

You can also review your recent commands with the `history` command.  Just enter:

```
$ history
```

To see a numbered list of recent commands, including this just issued `history` command.  You can reuse one of these commands directly by referring to the number of that command.

If your history looked like this:

```
259  ls *
260  ls /usr/bin/*.sh
261  ls *R1*fastq
```

Then you could repeat command #260 by simply entering:

```
$ !260
```

(That's an exclamation mark `!`).  You will be glad you learned this when you try to re-run very complicated commands.


### Exercise
---

1. Find the line number in your history for the last exercise (listing files in /bin) and reissue that command.


## Examining Files
---

We now know how to move around the file system and look at the contents of directories, but how do we look at the contents of files?

The easiest way (but really not the ideal way in most situations) to examine a file is to just print out all of the contents using the command `cat`. Enter the following command:

```
$ cd ~/dc_sample_data/sra_metadata
$ cat SraRunTable.txt
```

This prints out the all the contents of the the `SraRunTable.txt` to the screen.

> `cat` stands for concatenate; it has many uses and printing the contents of a files onto the terminal is one of them.

What does this file contain?

`cat` is a terrific command, but when the file is really big, it should be avoided; `less`, is preferred for files larger than a few bytes. Let's take a look at the fastq files in `~/dc_sample_data/untrimmed_fastq`. These files are quite large, so we probably do not want to use the `cat` command to look at them. Instead, we can use the `less` command.

Move to the `untrimmed_fastq` directory and enter the following command:

```
$ cd ~/dc_sample_data/untrimmed_fastq/
$ less SRR098026.fastq
```

`less` opens the file, and lets you navigate through it. The commands are identical to the `man` program.

#### Some commands in `less`

| key     | action |
| ------- | ---------- |
| "space" | to go forward |
|  "b"    | to go backwarsd |
|  "g"    | to go to the beginning |
|  "G"    | to go to the end |
|  "q"    | to quit |

`less` also gives you a way of searching through files. Just hit the `/` key to begin a search. Enter the name of the word you would like to search for and hit enter. It will jump to the next location where that word is found. If you hit `/` then "enter", `less` will just repeat the previous search. `less` searches from the current location and works its way forward. If you are at the end of the file and search the word, `less` will not find it. You need to go to the beginning of the file and search. Type `q` to escape the program.

For instance, let's search for the sequence `GTTGATC` in our file. You can see that we go right to that sequence and can see what it looks like.

Remember, the `man` program actually uses `less` internally and therefore uses the same commands, so you can search documentation using "/" as well!

There's another way that we can look at files, and in this case, just look at part of them. This can be particularly useful if we just want to see the beginning or end of the file, or see how it's formatted.

The commands are `head` and `tail` and they just let you look at the beginning and end of a file respectively.

```
$ head SRR098026.fastq

$ tail SRR098026.fastq
```

The `-n` option to either of these commands can be used to print the first or last `n` lines of a file. To print the first line of the file use:

```
$ head -n 1 SRR098026.fastq
```

## Creating, moving, copying, symlinking, and removing.
---

Now we can move around in the file structure, look at files, and search files. But what if we want to do normal things like copy files or move them around or get rid of them.

Our raw data in this case is fastq files.  We don't want to change the original files, so let's make a copy to work with.

Lets copy the file using the `cp` command. The copy command requires 2 things, the name of the file to copy, and the location to copy it to. Navigate to the `untrimmed_fastq` directory and enter:

```
$ cp SRR098026.fastq SRR098026-copy.fastq

$ ls -F
```

```
SRR097977.fastq  SRR098026-copy.fastq  SRR098026.fastq
```

Now SRR098026-copy.fastq has been created as a copy of SRR098026.fastq

Let's make a `backup` directory where we can put this file.

The `mkdir` command is used to make a directory. Just enter `mkdir` followed by a space, then the directory name.

```
$ mkdir backup
```

We can now move our backed up file in to this directory. We can move files around using the command `mv`. Enter this command:

```
$ mv *-copy.fastq backup

$ ls -al backup
```

```
total 52
drwxrwxr-x 2 dcuser dcuser  4096 Jul 30 15:31 .
drwxr-xr-x 3 dcuser dcuser  4096 Jul 30 15:31 ..
-rw-r--r-- 1 dcuser dcuser 43421 Jul 30 15:28 R098026-copy.fastq
```

The `mv` command is also how you rename files. Since this file is so important, let's rename it:

```
$ cd backup

$ mv SRR098026-copy.fastq SRR098026-copy.fastq_DO_NOT_TOUCH!

$ ls
```

```
SRR098026-copy.fastq_DO_NOT_TOUCH!
```

Sometimes we may want to work in a certain directory because programs can save output there. In that case we may want to make "symbolic links" or "symlinks" to files in other directories. The command `ln` is used to make links, we will add the `-s` flag to make them symbolic. Let's create a new directory called `symlinks` and navigate into it.

```
mkdir symlinks
cd symlinks
```

Now we will create the symlinks:

```
ln -s ../untrimmed_fastq/*.fastq .
```

Lets see if the symlinks were made:
```
ls -lahF
```

```
total 8.0K
drwxrwxr-x 2 dcuser dcuser 4.0K Mar 18 20:31 ./
drwxrwxr-x 6 dcuser dcuser 4.0K Mar 18 20:28 ../
lrwxrwxrwx 1 dcuser dcuser   34 Mar 18 20:31 SRR097977.fastq -> ../untrimmed_fastq/SRR097977.fastq
lrwxrwxrwx 1 dcuser dcuser   34 Mar 18 20:31 SRR098026.fastq -> ../untrimmed_fastq/SRR098026.fastq
```

The `->` operator tells us that these are symlinks and give us the path to the linked file. Is this path absolute or relative?


Finally, we decided this was silly and want to start over.

```
cd ../untrimmed_fastq/
$ rm SRR098026-copy.fastq_DO_NOT_TOUCH!
```

> The `rm` command permanently removes the file. Be careful with this command. The shell doesn't just nicely put the files in the Trash, they're really gone!
>
> Same with moving and renaming files. It will **not** ask you if you are sure that you want to "replace existing file".


### Exercise
---

1.  Change directories to the `untrimmed_fastq` folder and create a backup directory called `new_backup`
1.  Copy both fastq files files there with 1 command


By default, `rm`, will NOT delete directories. You can tell `rm` to delete a directory using the `-r` option. Let's delete our `backup` and `new_backup` directories we just made. Enter the following command:

```
$ rm -r backup
$ rm -r new_backup
```


## Writing files
---

We've been able to do a lot of work with files that already exist, but what if we want to write our own files. Obviously, we're not going to type in a FASTA file, but you'll see as we go through other tutorials, there are a lot of reasons we'll want to write a file, or edit an existing file.

To write in files, we're going to use the program `nano`. We're going to create a file within your home directory with the name `awesome.sh`.

```
$ cd
$ nano awesome.sh
```

Now you have something that looks like:

![nano1.png](../img/nano1.png)

Type in your command, so it looks like:

![nano2.png](../img/nano2.png)

Now we want to save the file and exit. At the bottom of nano, you see the "^X Exit". That means that we use Ctrl-X to exit. Type `Ctrl-X`. It will ask if you want to save it. Type `y` for yes. Then it asks if you want that file name. Hit `Enter`.

Now you've written a file. You can take a look at it with `less` or `cat`, or open it up again and edit it.

We're going to come back and use this file in just after lunch.
