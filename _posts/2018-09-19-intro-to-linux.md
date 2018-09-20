---
layout:     post
title:      introduction to linux
subtitle:   intro
date:       2018-09-19
author:     Zhenhua Wang
header-img: img/post-intro-linux.jpg
catalog: true
tags:
    - linux
---

> intro to linux

1.CMD
    * history -> show cmd you typed
      * history -c -> clear history
      * history -d (number) -> clear from that line
      * history --help
    * man -> mannual  
    * which -> search executables in $PATH
    * echo
      * -e -> enale backslash escapes
    * pwd -> show current dir (working dir)
    * touch -> create file
      * if already existed, it would only modifies is date intead of its content
    * cp -> copy file
      * -r -> copy dir and file
      * -v -> prints a line for every file copied
    * rmdir -> delete empty dir (safe than rm -rf!)
    * whoami -> show user name
    * getent -> 
    * chmod -> change permission
      * u (User)
      * g (Group)
      * o (Other)
      * + (Add Permission)
      * - (Remove Permission)
      * r (read)
      * w (write)
      * x (execute)
      * other permission -> there permission can add up, 5 = 4 + 1 = read and execute
        * 4 = read
        * 2 = write
        * 1 = execute
    * chown -> change ownership
    * chgrp -> change group
2. hotkey
   * CTRL+R            Dynamically search your command history
     * ENTER -> run the result you got
     * TAB -> put the result cmd into your shell intead of run it
   * CTRL+W            Delete previous word
   * CTRL+C            Kill the current command
   * CTRL+P            Recall the previous command from history
   * ALT+. (period)    Insert the last parameter from the previous command
3. special variables
   * $PATH
