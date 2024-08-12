
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