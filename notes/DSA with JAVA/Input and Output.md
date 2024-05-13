java.util includes scanner class

![[Pasted image 20240513094909.png]]

### Using BufferReader object

```java
InputStreamReader is = new InputStreamReader(System.in);
```
First we create an obj od inputstreamreader class this class specifies ehere the input originates from
- inputstreamreader obj designates from input from keyboard system.in represents standard input 
#### initializing
```java
InputStreamReader is = new InputStreamReader(System.in);
BufferedReader bf = new BufferedReader(in);
```
inputstreamreader is used to convert raw based input to char based input 
bufferReader is used to buffer input stream 

Readline()- read complete lines (returns a String)
Integer.parseInt()- convert into int

