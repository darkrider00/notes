
### Web Decode - picoctf

![[Pasted image 20250105143445.png]]

going to the website, going to about page inspecting we got some encoded value  `cGljb0NURnt3ZWJfc3VjYzNzc2Z1bGx5X2QzYzBkZWRfZGYwZGE3Mjd9`

decoding this 
|[From_Base64('A-Za-z0-9+/=',true,false)](https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true,false))|picoCTF{web_succ3ssfully_d3c0ded_df0da727}|

flag found 


### Unminify - picoctf

![[Pasted image 20250105143751.png]]


going to the website and inspecting it will give us the flag `picoCTF{pr3tty_c0d3_dbe259ce}`


### Intro to Burp - Picoctf

![[Pasted image 20250105160747.png]]


![[Pasted image 20250105160653.png]]

by removing the line containing otp we got the flag 
`picoCTF{#0TP_Bypvss_SuCc3$S_2e80f1fd}`


###Bookmarklet - picoctf

![[Pasted image 20250105161533.png]]

[Bookmarklets](https://en.wikipedia.org/wiki/Bookmarklet) are browser bookmarks that execute JavaScript instead of opening a webpage. They're also known as bookmark applets, favlets, or JavaScript bookmarks.


## Use Cases for Bookmarklets

With bookmarklets, you can manipulate the current page as the function will have the context of the current tab. This means you can:

- Click buttons virtually
    
- Modify the content
    
- Use the content of the page to open a new page
    
- Remove elements from the page

example bookmarklet: https://www.freecodecamp.org/news/what-are-bookmarklets/#heading-example-bookmarklets

found a js function containing encrypted flag 
![[Pasted image 20250105162110.png]]
ran that js code and got the output 


### local authority 

![[Pasted image 20250105162249.png]]

![[Pasted image 20250105163237.png]]

after entering some random credentials in network secure.js is loaded i opened and found the flag 
`picoCTF{j5_15_7r4n5p4r3n7_05df90c8}`


### Inspect HTML -picoctf

![[Pasted image 20250105163524.png]]

i went into source code and found the flag 

`<!--picoCTF{1n5p3t0r_0f_h7ml_fd5d57bd}-->`




