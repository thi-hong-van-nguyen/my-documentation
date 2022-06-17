# JAVA
##
- In Eclipse, create a new project. Inside src folder, create a new package with same name with the project name. 
- Then click on the new package, create new Class with Capitalized name, check static checkbox.

Inside Main file:
```
package project_name;

public class Main {
	public static void main(String[] args) {
		// primitive 
		int first_num = 8;
		double num2 = 7.0;
		boolean bol = false;
		char character = 't';
		char numCharacter = '8';
		String str = "this is a string.";		
	}
}

```

### Print something from the user input:
```
package project_name
import java.util.Scanner;

public class Main {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		String scanned = sc.nextLine(); // for string input
	        int scanned = sc.nextInt(); // for integer input
	        bollean scanned = sc.nextBoolean(); // true false input
	        double scanned = sc.nextDouble(); // an integer or float
		
		System.out.println(scanned);
	}
}

```

### Convert a string into integer
```
String str = "578";
int x = Integer.parseInt(scanned);
```

### compare two strings:
```
Scanner sc = new Scanner(System.in);
String str = sc.nextLine();
sc.equals("Some string here");	
```

### ARRAY:
```
String[] strArr = new String[5];
strArr[0] = "hello";
strArr[1] = "world";
int[] intArr = new int[5];

// another way to assign values to an array:
String[] arr = {"hello", "world", "goodday"};
```

### FOR LOOP:
```
for (int i = 0; i <= 10; i++){
	// logic in here
}
// in case we want to loop through everything in the array:
int[] arr = {1, 4, 6, 2};
for (int element:arr) {
	System.out.println(element) // output: 1, 4, 6, 2 are printed 4 times 
}
```

### SET and LIST
- Set and HashSet
```
import java.util.set;
import java.util.HashSet;

Set<Integer> a = new HashSet<Integer>();
a.add(4);
a.add(1);
// Note that HashSet will remove duplicate elements and all the elements will NOT be in order of inputting
```
- ArrayList
```
import Java.util.ArrayList;

ArrayList<Integer> b = new ArrayList<Integer>();
b.add(2);
t.set(index, value);
b.subList(index, index) // not counting the last index.
// Note that ArrayList do NOT remove duplicate and the elements will be in input order
```

- LinkedHashSet
```
import Java.util.LinkedHashSet;

LinkedHashSet<Integer> b = new LinkedHashSet<Integer>();
b.add(2);
// Note that ArrayList remove duplicate and the elements will be in alpha/number order
```
