# Sample 1: Method reference - findNeedles
This is a reference document for the `findNeedles` method. This method finds a set of words inside a string, and displays how many times each word appears in the string.

## Method

The following code sample represents a *find needles in haystack method* written in **Java**:

```java
public static void findNeedles(String haystack, String[] needles) {
	if (needles.length > 5) {
		System.err.println("Too many words!");
	} else {
		int[] countArray = new int[needles.length];
		for (int i = 0; i<needles.length; i++) {
			String[] words = haystack.split("[ \"\'\t\n\b\f\r]", 0);
			for (int j = 0; j<words.length; j++) {
				if (words[j].compareTo(needles[i]) == 0) {
					countArray[i]++;
				}
			}
		}
		for (int j = 0; j<needles.length; j++) {
			System.out.println(needles[j] + ": " + countArray[j]);
		}
	}
}
```

The following sections describe the `findNeedles` method in three parts for easier analysis:

- **Parameters:** This is what you need to pass.
- **Execution condition:** Describes the condition to use the method.
- **Haystack split and word comparison:** Describes how the method works.

### Parameters

The method receives two parameters:
```java
public static void findNeedles(String haystack, String[] needles) {
```
* `haystack`: the string containing the available words 
* `needles`: an array of words to find in the haystack 

### Execution condition

This method only works for a set of ***maximum*** *five words*. If the `needles` array contains more than five elements, an error message is displayed. If it contains five elements or less, the method creates an array to store the count of each word in `needles` and enters a loop described in the next section.

This code snippet illustrates the condition:

```java
...
	if (needles.length > 5) {
		System.err.println("Too many words!");
	else {
		int[] countArray = new int[needles.length];
...
```

### Haystack split and word comparison

The following `for` loop separates the `haystack` string into single words using the `split` Java method and stores them in a new array of strings called `words`. 

This code snippet illustrates the haystack split:
```Java
...
		for (int i = 0; i<needles.length; i++) {
			String[] words = haystack.split("[ \"\'\t\n\b\f\r]", 0);
			for (int j = 0; j<words.length; j++) {
				if (words[j].compareTo(needles[i]) == 0) {
					countArray[i]++;
				}
			}
		}
...
```
The `split` method takes two arguments: a *regular expression* and a *limit*. In this case:

* `"[\"\'\t\n\b\f\r]"` : This regular expression separates words from the text when it finds **double quotes**, **single quotes**, **tabs**, **blank spaces**, and **line breaks**.
* `0`: The `0` limit means that splitting will happen as many times as needed.

**Note:** To know more about the `split` method, visit the [String Class documentation](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#split) and navigate to the **split** section.

The inner `for` loop compares, using the `compareTo` Java method, each string of the `words` array with the word in the current position of the `needles` array. 

This code snippet illustrates the word comparison:

```Java
...
		for (int j = 0; j<needles.length; j++) {
			System.out.println(needles[j] + ": " + countArray[j]);
		}
	}
}
```
For each comparison, the code checks if the `compareTo` method returned a `0`, indicating a match between both words. If there is a match, it increases the counter for that word.

**Note:** To know more about the `compareTo` method, visit the [Comparable documentation](https://docs.oracle.com/javase/7/docs/api/java/lang/Comparable.html).

## Calling the method and displaying the output 

Calling the method returns each word in `needles` and the number of times that it was found inside the `haystack` string.

Here is an example of calling the method:
```Java
String[] needles = new String[]{"hello","hollo","hullo", "hillo", "hallo"};
    
findNeedles("hello\'hello\thello\bwhole'\nhullo'hullo hillo", needles);
```
Which returns the following:
```Bash
hello: 3
hollo: 0
hullo: 2
hillo: 1
hallo: 0
```

