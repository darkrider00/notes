1. Create a repository or [fork the md repo 1.3k](https://linked-blog-starter.vercel.app/publish-your-obsidian-notes-with-linked-blog-starter) in github
2. [Download Git 547](https://git-scm.com/downloads)
3. Create a [personal access token 1.1k](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token#creating-a-personal-access-token-classic) from github

configure your github account with gitbash
```console
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```

![[Pasted image 20240325153324.png]]
1. Install the [Obsidian Git 1.4k](https://github.com/denolehov/obsidian-git/wiki/Installation) community plugin
2. Create a folder to store the repository. (e.g. `remote-blog/`). Set scopes to repo & expiration to no expiration
3. Run the command (CMD/Ctrl + P): `Clone an existing remote repo`
or open git bash in the same folder you want to take notes and execute the commands

```
git remote add origin https://github.com/darkrider00/test.git
git branch -M main
gid add .
git commit -m "intial commit"
git push -u origin main
```

now add the initialized git folder in obsidian vault and enable the setting to push for every 2 min so in that way you don't have to commit and push the files every time

or you can push every time before you close obsidian

TO sync 
we can use syncthing and download it in both android and pc 
it will open in a localhost and looks like this 
![[Pasted image 20240325154309.png]]
click on actions and show id and scan it using syncthing app in mobile to connect with devices 
and you'll be asked a prompt that requesting to add a device click on okay and add the device 
![[Pasted image 20240325154529.png]]
click on new and add label , id , path  that folder will be used by both Ur android device and pc 
make sure you give initialized git folder in the path since that folder will act as backup folder


