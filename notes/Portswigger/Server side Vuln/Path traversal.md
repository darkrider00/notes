- Application code and data.
- Credentials for back-end systems.
- Sensitive operating system files.

Imagine a shopping application that displays images of items for sale. This might load an image using the following HTML:

`<img src="/loadImage?filename=218.png">`

- loadimage - takes filename parameter and returns content of specified file
- the images stored on disk in the specified location (the application will read the specified path)
- n attacker can request the following URL to retrieve the `/etc/passwd` file from the server's filesystem:
`https://insecure-website.com/loadImage?filename=../../../etc/passwd`

- sequence is valid within a file path means stepup one level in the directory structure
- ../ 3 consecutive sequences step up from /var/www/images to the file system root, so file is read

On Windows, both `../` and `..\` are valid directory traversal sequences. The following is an example of an equivalent attack against a Windows-based server:
`https://insecure-website.com/loadImage?filename=..\..\..\windows\win.ini`

