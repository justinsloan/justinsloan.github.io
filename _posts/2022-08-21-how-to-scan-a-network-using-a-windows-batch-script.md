---
title: How to scan a network using a Windows batch script (or Bash script)
categories:
  - Help File
tags:
  - Windows
  - Batch
  - Tools
  - Bash
  - Linux
---

The company I work for uses [Lansweeper](https://www.lansweeper.com) to keep tabs on network assets, but Lansweeper is complete overkill when you just need to take a quick snapshot of critical systems. So I wrote a simple batch script that will ping every host in a list and report back on their status, as well as provide a report of the offline systems which may need further investigation. This gives me a quick idea of the health of the network when my workday begins, and helps me to focus in on areas that may become serious problems.

```batch
@echo off 
setlocal enabledelayedexpansion

set /a online=0
set /a offline=0

rem delete/clear offline.txt
break > offline.txt

CLS
echo  
echo Initiating Ping Sweep...

FOR /f %%i IN (hosts.txt) DO (
    ping %%i -n 1 > NUL

    if not errorlevel 1 (
        echo %date% %time%  %%i IS ONLINE
        set /a online+=1
    ) else (
        echo %date% %time%  %%i IS OFFLINE
        echo %date% %time%  %%i IS OFFLINE >> offline.txt
        set /a offline+=1
    )
    rem pause 1 second before next ping
    rem timeout -t 1 > nul
)

:done
echo *************************
echo      %online% hosts online
echo      %offline% hosts offline
echo *************************

FOR /f "delims=" %%i IN (offline.txt) DO (
    echo %%i
)

pause

:eof
exit /b
```

Before you begin your scan you need to define the list of hosts. To do this, create a text file called `hosts.txt` and put one host per line.

Example `hosts.txt`

```
192.168.0.1
10.0.0.1
server.mysite.com
PTRMAIN1
```
**EDIT:** Here's how to do it with Bash.
```
#! /bin/bash

upcount=0
downcount=0

while read `cat testhosts.txt`
do 
    if ping -c 1 -i 1 $host &> /dev/null
        then 
            echo "$host success"
            let upcount++
        else 
            echo "$host fail"
            let downcount++
    fi
done
echo "$upcount Systems up"
echo "$downcount Systems down"
```
