go to this link : https://drive.google.com/file/d/1xDrUH9rJGVpUGESiefTSk9BuhmWeYowl/view?usp=drivesdk

and download zip file then extract it and move the file to /opt/tools/burpsuite

open loader file change the name to get license on your name and click copy license and click on run and

```
0. If you have used other BurpSuite "licenses" before: 

In your home directory file like this: ~/.java/.userPrefs/burp remove the line with the license:

<entry key="license1" value="......


*****

Activate a new license:

1. Launch Loader:

java -jar Loader.jar

2. Run BurpSuite by simply clicking "Run" in Loader. Copy the key from Loader and paste it into BurpSuite.

3. Then select "Manual".

4. Copy from BurpSuite "Copy request" and paste into Loader Activation Request, then copy from Loader "Activation Responce" to BurpSuite Paste response and click "Next".

5. BurpSuite is activated, you can run it with the command (don't forget to replace <PATH>):


java --add-opens=java.desktop/javax.swing=ALL-UNNAMED \
--add-opens=java.base/java.lang=ALL-UNNAMED \
--add-opens=java.base/jdk.internal.org.objectweb.asm=ALL-UNNAMED \
--add-opens=java.base/jdk.internal.org.objectweb.asm.tree=ALL-UNNAMED \
--add-opens=java.base/jdk.internal.org.objectweb.asm.Opcodes=ALL-UNNAMED \
-javaagent:<PATH>/Loader.jar -noverify -jar <PATH>/burpsuite_pro_v2023.2.2
```


TO setup desktop file 
save this code in the /usr/share/application create a new file named burppro.desktop something

```
[Desktop Entry]
Name=burpsuite
Encoding=UTF-8
Exec=sh -c "java -jar /usr/bin/burpsuite"
Icon=kali-menu.png
StartupNotify=false
Terminal=false
Type=Application
Categories=03-04-web-crawlers;03-05-web-vulnerability-scanners;03-06-web-application-proxies;03-07-web-application-fuzzers;04-01-online-attacks;07-05-web-sniffers;top10;
X-Kali-Package=burpsuite
```

Change the EXEC file path to copied from loader command in loader.jar

![[1.png]]

![[2.png]]

![[3.png]]

![[4.png]]

![[5.png]]

![[6.png]]

![[7.png]]
