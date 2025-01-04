
Open your command prompt with administrator access and the follow the process below
### The commands

Now, type the following command: `slmgr.vbs /upk` Now it will give an message, click on OK

And now this command: `slmgr.vbs /cpky` It will give an message once again, and click on OK again

And now type this command: `slmgr.vbs /ckms` Once again click on OK when you get an message

### Edition upgradable check command

Now we are gonna check of your edition is supported to upgrade to Pro, run the following command to check this: `DISM /online /Get-TargetEditions` If you see "Professional" in the list, then you can upgrade your Windows edition to Pro for free!

### Running Windows Pro installer

Now, copy and paste this complete command:

`sc config LicenseManager start= auto & net start LicenseManager`

`sc config wuauserv start= auto & net start wuauserv`

`changepk.exe /productkey VK7JG-NPHTM-C97JM-9MPGT-3V66T`

`exit`

It will run an installer and you will see an message:"% complete"

Now wait until it's 100%


1. Open PowerShell (Not CMD). To do that, right-click on the Windows start menu and select PowerShell or Terminal.
2. Copy and paste the code below and press enter

```
irm https://get.activated.win | iex
```

3. You will see the activation options. Choose (1) HWID for Windows activation. Choose (2) Ohook for Office activation.
4. That's all.

More options

- Alternatively, you can use the following (It will be deprecated in the future.)

```
irm https://massgrave.dev/get | iex
```

- The URL `get.activated.win` might be blocked by some DNS services because it is a new domain.

---

### Method 2 - Traditional (Windows 7 and later)

[](https://github.com/massgravel/Microsoft-Activation-Scripts#method-2---traditional-windows-7-and-later)

Click here for info

1. [](https://github.com/massgravel/Microsoft-Activation-Scripts)[](https://dev.azure.com/massgrave/_git/Microsoft-Activation-Scripts)[](https://git.activated.win/massgrave/Microsoft-Activation-Scripts)

---

Note

- The IRM command in PowerShell downloads a script from a specified URL, and the IEX command executes it.
- Always double-check the URL before executing the command and verify the source if manually downloading files.
- Be cautious, as some spread malware disguised as MAS by using different URLs in the IRM command.

---

To run the scripts in unattended mode, check [here](https://massgrave.dev/command_line_switches).

```
Latest Version: 2.8
Release date: 9-Nov-2024
```

### [Troubleshooting / Help](https://massgrave.dev/troubleshoot)

[](https://github.com/massgravel/Microsoft-Activation-Scripts#troubleshooting--help)

### [Download Original Windows & Office](https://massgrave.dev/genuine-installation-media)

[](https://github.com/massgravel/Microsoft-Activation-Scripts#download-original-windows--office)

### Homepage - [https://massgrave.dev/](https://massgrave.dev/)

[](https://github.com/massgravel/Microsoft-Activation-Scripts#homepage---httpsmassgravedev)

[![1.1](https://camo.githubusercontent.com/374deb9342940d9cb30ebe1b1c1ec204b66616999e76b7ba9ffb619b82e5db1c/68747470733a2f2f6d61737367726176652e6465762f696d672f6c6f676f5f646973636f72642e706e67 "Chat with us without signup")](https://discord.gg/tVFN4N84PP) [![1.2](https://camo.githubusercontent.com/a0539f2543e8bfb937738fcfda669561db61626207ff2d2f9772b5bf5ef77857/68747470733a2f2f6d61737367726176652e6465762f696d672f6c6f676f5f6769746875622e706e67 "GitHub")](https://github.com/massgravel/Microsoft-Activation-Scripts) [![1.3](https://camo.githubusercontent.com/a63bfd01008442016351df59ebcacb5eab25af2d11cfb78b73d56b053ce57ae1/68747470733a2f2f6d61737367726176652e6465762f696d672f6c6f676f5f7265646469742e706e67 "Reddit")](https://www.reddit.com/r/MAS_Activator) [![1.4](https://camo.githubusercontent.com/28438047655d9090f40a5ac827e5d7949a3ccc8192f868d9d8209f83055f3800/68747470733a2f2f6d61737367726176652e6465762f696d672f6c6f676f5f782e706e67 "Follow us on X")](https://twitter.com/massgravel)

---

Made with Love ❤️

![Monica](chrome-extension://ofpnmcalabcbjgholdjcjblkibolbppb/static/global/src/static/monicaLogo.png)

Monica

![](chrome-extension://ofpnmcalabcbjgholdjcjblkibolbppb/static/searchEnhance/fast.png)Fast Model

Repo Summary

Supports the most advanced models to help you quickly understand the contents of the repo

Summarize this repo

## About

Open-source Windows and Office activator featuring HWID, Ohook, KMS38, and Online KMS activation methods, along with advanced troubleshooting.

[massgrave.dev](https://massgrave.dev/ "https://massgrave.dev")

### Topics

[microsoft](https://github.com/topics/microsoft "Topic: microsoft") [windows](https://github.com/topics/windows "Topic: windows") [kms](https://github.com/topics/kms "Topic: kms") [powershell](https://github.com/topics/powershell "Topic: powershell") [office](https://github.com/topics/office "Topic: office") [windows-10](https://github.com/topics/windows-10 "Topic: windows-10") [office365](https://github.com/topics/office365 "Topic: office365") [activator](https://github.com/topics/activator "Topic: activator") [hwid](https://github.com/topics/hwid "Topic: hwid") [windows-11](https://github.com/topics/windows-11 "Topic: windows-11") [microsoft365](https://github.com/topics/microsoft365 "Topic: microsoft365") [kms38](https://github.com/topics/kms38 "Topic: kms38") [massgrave](https://github.com/topics/massgrave "Topic: massgrave") [massgravel](https://github.com/topics/massgravel "Topic: massgravel") [ohook](https://github.com/topics/ohook "Topic: ohook")

### Resources

 [Readme](https://github.com/massgravel/Microsoft-Activation-Scripts#readme-ov-file)

### License

 [GPL-3.0 license](https://github.com/massgravel/Microsoft-Activation-Scripts#GPL-3.0-1-ov-file)

 [Activity](https://github.com/massgravel/Microsoft-Activation-Scripts/activity)

 [Custom properties](https://github.com/massgravel/Microsoft-Activation-Scripts/custom-properties)

### Stars

 [**102k** stars](https://github.com/massgravel/Microsoft-Activation-Scripts/stargazers)

### Watchers

 [**1k** watching](https://github.com/massgravel/Microsoft-Activation-Scripts/watchers)

### Forks

 [**9.9k** forks](https://github.com/massgravel/Microsoft-Activation-Scripts/forks)

[Report repository](https://github.com/contact/report-content?content_url=https%3A%2F%2Fgithub.com%2Fmassgravel%2FMicrosoft-Activation-Scripts&report=massgravel+%28user%29)

## [Releases 17](https://github.com/massgravel/Microsoft-Activation-Scripts/releases)

[

UWP Office support and bug fixesLatest

2 days ago



](https://github.com/massgravel/Microsoft-Activation-Scripts/releases/tag/2.8)

[+ 16 releases](https://github.com/massgravel/Microsoft-Activation-Scripts/releases)

## [Contributors8](https://github.com/massgravel/Microsoft-Activation-Scripts/graphs/contributors)

- [![@WindowsAddict](https://avatars.githubusercontent.com/u/40813939?s=64&v=4)](https://github.com/WindowsAddict)
- [![@nekoppai](https://avatars.githubusercontent.com/u/109633131?s=64&v=4)](https://github.com/nekoppai)
- [![@mspaintmsi](https://avatars.githubusercontent.com/u/41545165?s=64&v=4)](https://github.com/mspaintmsi)
- [![@thecatontheceiling](https://avatars.githubusercontent.com/u/75037904?s=64&v=4)](https://github.com/thecatontheceiling)
- [![@BandhiyaHardik](https://avatars.githubusercontent.com/u/110784317?s=64&v=4)](https://github.com/BandhiyaHardik)
- [![@ave9858](https://avatars.githubusercontent.com/u/112294121?s=64&v=4)](https://github.com/ave9858)
- [![@alouiadel](https://avatars.githubusercontent.com/u/149530892?s=64&v=4)](https://github.com/alouiadel)
- [![@KomashiFX](https://avatars.githubusercontent.com/u/54118714?s=64&v=4)](https://github.com/KomashiFX)

## Languages

- [Batchfile100.0%](https://github.com/massgravel/Microsoft-Activation-Scripts/search?l=batchfile)

## Footer

[](https://github.com/ "GitHub")© 2024 GitHub, Inc.

### Footer navigation

- [Terms](https://docs.github.com/site-policy/github-terms/github-terms-of-service)
- [Privacy](https://docs.github.com/site-policy/privacy-policies/github-privacy-statement)
- [Security](https://github.com/security)
- [Status](https://www.githubstatus.com/)
- [Docs](https://docs.github.com/)
- [Contact](https://support.github.com/?tags=dotcom-footer)
- Manage cookies
- Do not share my personal information

![Monica](chrome-extension://ofpnmcalabcbjgholdjcjblkibolbppb/static/global/src/static/monicaLogo.png)Ctrl+M

![](https://github.githubassets.com/favicons/favicon-dark.svg)

Ctrl J

Summarize

Translate to:English

Rewrite

Expand

Explain this

Grammar

Answer this question

Explain Codes

Add Quick Action

Manage Action

---

Memo

Highlight

Explain

![[Pasted image 20241111105008.png]]

