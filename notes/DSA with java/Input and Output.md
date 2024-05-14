Using Scanner Class
```
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        // Your code here
    }
}
```

To use commonly used utility classes in Java, you can import the java.util package.

**import java.util.*;** imports all classes and interfaces from the java.util package. 

You can then use classes from the **java.util** package, such as **Scanner**, **ArrayList**, **HashMap**, and others, as needed in your Java program. Importing only the classes you use can help keep your code more **efficient** and **maintainable**, as you won't have unnecessary overhead from importing unused libraries.


To use **BufferedReader**, first, we create an object of the InputStreamReader class. This object specifies where the input originates from.

InputStreamReader is = new InputStreamReader(System.in);
**InputStreamReader** **object** ‘is’ designates input from the keyboard. System.in represents the **standard** **input**, which is usually your keyboard. But it could be something else, like a file or network stream, depending on what you point it to.

### **Initializing BufferedReader**

Now, create a **BufferedReader** **object** and pass the **InputStreamReader** **object** into it. This BufferedReader will be responsible for reading and processing the input.
```
InputStreamReader is = new InputStreamReader(System.in);
BufferedReader bf = new BufferedReader(in);
```

![[Pasted image 20240514164739.png]]

![[Pasted image 20240514172019.png]]


