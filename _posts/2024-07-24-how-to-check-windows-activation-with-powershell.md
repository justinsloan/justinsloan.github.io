---
title: How to check Windows activation status with PowerShell
categories:
  - Docs
tags:
  - Windows
  - PowerShell
---

Windows includes a simple Visual Basic script that checks if Windows is properly activated. You can run the script by opening the Run box (WIN+R) or a Command Prompt and entering `slmgr /xpr`. This will open a notification dialog with the current Windows activation status.

However, by wrapping the VB script in a PowerShell command, you can suppress the user-facing dialog and get the response printed directly to your terminal.

### The Invoke-Command

The syntax for running the script and capturing the output is pretty straightforward:

```sh
    Invoke-Command { (cscript /Nologo "C:\Windows\System32\slmgr.vbs" /xpr) -join '' }
```

A positive response will look something like this:

```sh
    Windows(R), Professional edition:    The machine is permanently activated.
```

### Running Invoke-Command on a remote workstation

Even better, we can run the command on a remote machine or even an entire enterprise fleet of Windows workstations, making Windows license auditing easy for system administrators.

To run the command on a remote machine, simply add `-ComputerName <remote-machine>` to the end of the command, where `<remote-machine>` is the Windows Device Name:

```sh
    Invoke-Command { (cscript /Nologo "C:\Windows\System32\slmgr.vbs" /xpr) -join '' } -ComputerName <remote-machine>
```

You generally do not need to have admin privileges to check activation status.
