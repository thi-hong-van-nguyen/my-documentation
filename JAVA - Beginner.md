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

### Array:
```
String[] strArr = new String[5];
int[] intArr = new int[5];


```


