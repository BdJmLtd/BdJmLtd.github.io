---
title:  "Nexus Repository Manager: Windows"
---

## 下载

地址：

```text
https://help.sonatype.com/repomanager3/product-information/download
```

## 解压和启动

```text
nexus-<version>/bin/
```

The bin folder contains the generic startup scripts for Unix-like platforms called `nexus`.
The Windows platform equivalent is called `nexus.exe`.

Start NXRM by running the file `nexus` from your command line.
To start the repository manager from application directory in the bin folder perform one of the following:

- on a Unix-like platform like Linux use the command: `./nexus run`
- in Windows, use the command: `nexus.exe /run`

> Starting the repository manager with the run command will leave it running in the current shell and display the log output.

The file is launched, and when complete, the log file displays a message “Started Sonatype Nexus.”
You are now able to start the repository manager.

Open your browser and type in the URL: `http://localhost:8081/`. The Nexus Repository Manager Welcome screen displays.

## Signing In to NXRM and Changing the Default Credentials

### Signing In

The first time you sign in to NXRM you will use the default username and password.
It is best practice to change this default to more secure credentials, private to you.

- From the NXRM Welcome screen, click **Sign in**. A Sign in pop up box is displayed.
- Enter the default username, which is “`admin`” and default password, which is “`admin123`.”
- Click **Sign in**. The Sign in dialog box is closed, and you are signed in into NXRM.

### Changing Your Default Account Profile

## Reference

- [Lesson 1: Installing and Starting Nexus Repository Manager](https://help.sonatype.com/learning/repository-manager-3/first-time-installation-and-setup/lesson-1%3A--installing-and-starting-nexus-repository-manager?preview=%2F16351968%2F16351969%2Fchange_PW.png)

