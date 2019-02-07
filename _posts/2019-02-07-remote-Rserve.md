---
layout:     post
title:      Connect to Rserve in VirtualBox
subtitle:   intro
date:       2019-02-07
author:     Zhenhua Wang
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - Tableau
    - R
---

> 

1. download Rserve from "Rforge"
2. R CMD INSTALL Rserve_1.8-6.tar.gz
3. if you run R CMD Rserve and get "Rserve not found", you should first add link to your Rserve
   ln -s path/to/Rserve  Rserve(which can be found using system.file("libs", "Rserve", package="Rserve") inside R)
4. create a Rserve configuration file (e.g. Rserv.conf)
   remote enable
5. R CMD Rserve --RS-conf Rserv.conf --RS-port 9123