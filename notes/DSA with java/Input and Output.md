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

```java
import java.io.*;
import java.util.*;
import java.text.*;
import java.math.*;
import java.util.regex.*;

public class basic {
static int solveMeFirst(int a, int b) {
return a+b;
 }
public static void main(String[] args) {
Scanner in = new Scanner(System.in);
int a;
a = in.nextInt();
int b;
b = in.nextInt();
int sum;
sum = solveMeFirst(a, b);
System.out.println(sum);
}
}
```

![[Pasted image 20240514175157.png]]

```java
   import java.io.*;

    import java.util.*;

  

    class Result {

        public static int simpleArraySum(List<Integer> ar) {

            int count =0;

            for (int i=0;i<ar.size();i++){

                count +=ar.get(i);

            }

            return count;

        }

  

    }

    public class basic {

        public static void main(String[] args) throws IOException {

            BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));

            BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter("E:\\DSA\\basics\\output.txt"));

            int arCount = Integer.parseInt(bufferedReader.readLine().trim());

            String[] arTemp = bufferedReader.readLine().replaceAll("\\s+$", "").split(" ");

  

            List<Integer> ar = new ArrayList<>();

  

            for (int i = 0; i < arCount; i++) {

                int arItem = Integer.parseInt(arTemp[i]);

                ar.add(arItem);

            }

  

            int result = Result.simpleArraySum(ar);

  

            bufferedWriter.write(String.valueOf(result));

            bufferedWriter.newLine();

  

            bufferedReader.close();

            bufferedWriter.close();

        }

    }
```

