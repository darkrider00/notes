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

// 3rd problem //

// The rating for Alice's challenge is the triplet a = (a[0], a[1], a[2]), and the rating for Bob's challenge is the triplet b = (b[0], b[1], b[2]).

// The task is to find their comparison points by comparing a[0] with b[0], a[1] with b[1], and a[2] with b[2].

// If a[i] > b[i], then Alice is awarded 1 point.

// If a[i] < b[i], then Bob is awarded 1 point.

// If a[i] = b[i], then neither person receives a point.

// Comparison points is the total points a person earned.

// Given a and b, determine their respective comparison points.
// Constraints
// 1 ≤ a[i] ≤ 100

// 1 ≤ b[i] ≤ 100

// Sample Input 0

// 5 6 7

// 3 6 10

// Sample Output 0

// 1 1

```
import java.io.*;

import java.util.*;

class Result {

    public static List<Integer> compareTriplets(List<Integer> a, List<Integer> b) {

        int alice = 0, bob = 0;

        for (int i = 0; i < a.size(); i++) {

            if (a.get(i) > b.get(i)) {

                alice++;

            } else if (a.get(i) < b.get(i)) {

                bob++;

            }

        }

        List<Integer> result = new ArrayList<>();

        result.add(alice);

        result.add(bob);

        return result;

    }

}

public class basic {

    public static void main(String[] args) throws IOException {

        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));

        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(("output.txt")));

  

        String[] aTemp = bufferedReader.readLine().replaceAll("\\s+$", "").split(" ");

  

        List<Integer> a = new ArrayList<>();

  

        for (int i = 0; i < 3; i++) {

            int aItem = Integer.parseInt(aTemp[i]);

            a.add(aItem);

        }

  

        String[] bTemp = bufferedReader.readLine().replaceAll("\\s+$", "").split(" ");

  

        List<Integer> b = new ArrayList<>();

  

        for (int i = 0; i < 3; i++) {

            int bItem = Integer.parseInt(bTemp[i]);

            b.add(bItem);

        }

  

        List<Integer> result = Result.compareTriplets(a, b);

  

        for (int i = 0; i < result.size(); i++) {

            bufferedWriter.write(String.valueOf(result.get(i)));

  

            if (i != result.size() - 1) {

                bufferedWriter.write(" ");

            }

        }

  

        bufferedWriter.newLine();

  

        bufferedReader.close();

        bufferedWriter.close();

    }

}
```

![[Pasted image 20240514182759.png]]

**Sample Input**

```
5
1000000001 1000000002 1000000003 1000000004 1000000005
```

**Output**

```
5000000015
```
The program :
```
import java.io.*;

import java.math.*;

import java.security.*;

import java.text.*;

import java.util.*;

import java.util.concurrent.*;

import java.util.regex.*;

  

class Result {

  

    /*

     * Complete the 'aVeryBigSum' function below.

     *

     * The function is expected to return a LONG_INTEGER.

     * The function accepts LONG_INTEGER_ARRAY ar as parameter.

     */

  

    public static long aVeryBigSum(List<Long> ar) {

    long sum =0;

    for(int i=0;i<ar.size();i++){

        sum=sum +ar.get(i);

    }

    return sum;

    }

  

}

  

public class Solution {

    public static void main(String[] args) throws IOException {

        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));

        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

  

        int arCount = Integer.parseInt(bufferedReader.readLine().trim());

  

        String[] arTemp = bufferedReader.readLine().replaceAll("\\s+$", "").split(" ");

  

        List<Long> ar = new ArrayList<>();

  

        for (int i = 0; i < arCount; i++) {

            long arItem = Long.parseLong(arTemp[i]);

            ar.add(arItem);

        }

  

        long result = Result.aVeryBigSum(ar);

  

        bufferedWriter.write(String.valueOf(result));

        bufferedWriter.newLine();

  

        bufferedReader.close();

        bufferedWriter.close();

    }

}
```

![[Pasted image 20240514183946.png]]

