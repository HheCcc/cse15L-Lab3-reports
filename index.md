# CSE15L - Lab - Reports
# Lab Report 3 - Bugs and Commands
## Part 1 - Bugs
This method from the `ArrayExamples.java` that the bugs are on: 
```java
public class ArrayExamples {
  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
## A Failure-Input: fails because it ends up with the same array instead of reversing it.
```java
@Test 
public void testReverseInPlace() {
    int[] input1 = { 5,4,3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3,4,5 }, input1);
}
```

## An input that doesn't induce a failure: because an array with a single element is already reversed in its own right.
```java
@Test 
public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
}
```

## Symptom:
![image](symptom.png)


## The Bug: 
## Before: 
```java
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
}

```

## After:
```java
static void reverseInPlace(int[] arr) {
    int[] tempArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
        tempArray[i] = arr[arr.length - i - 1];
    }
    for(int i = 0; i < arr.length; i += 1) {
    arr[i] = tempArray[i];
    }
}
```
## Brief describe:
I create another array that store the value then assign the reversed value back. Because before
the fix, the same array are being use to store elements, the first element lost when the first `for`
loop is excuted.

# Part 2 - Researching Commands
## -name
## Example1:
* Command: 
```java
find -name 911report
```
* Output
```java
./911report
```
## Example 2:
* Command: 
```java
find -name preface.txt
```
* Output: 
```java
./911report/preface.txt
```

## The `-name` command option is used to find files by their name within the directory hierarchy starting at a specified directory. It matches files that exactly meet the given pattern. This option is case-sensitive, meaning it will only find files that match the exact case of the provided pattern. It is useful for locating files when the full path is not known.
## -size
## Example1:
* Command: 
```java
find ./911report -size +1k
```
* Output:
```java
./911report
./911report/chapter-1.txt
./911report/chapter-10.txt
./911report/chapter-11.txt
./911report/chapter-12.txt
./911report/chapter-13.1.txt
./911report/chapter-13.2.txt
./911report/chapter-13.3.txt
./911report/chapter-13.4.txt
./911report/chapter-13.5.txt
./911report/chapter-2.txt
./911report/chapter-3.txt
./911report/chapter-5.txt
./911report/chapter-6.txt
./911report/chapter-7.txt
./911report/chapter-8.txt
./911report/chapter-9.txt
./911report/preface.txt
```
## Example 2:
* Command: 
```java
find ./plos/pmed.0020191.txt -size 1k
```
* Output: 
```java
./plos/pmed.0020191.txt
```
## The `-size` option is very useful for finding files that are taking up a significant amount of space, or to identify files that are below or above a certain size threshold.
## -type
## Example1:
* Command:
```java
find ./ -type d
```
* Output:
```java
./
./911report
./biomed
./government
./government/About_LSC
./government/Alcohol_Problems
./government/Env_Prot_Agen
./government/Gen_Account_Office
./government/Media
./government/Post_Rate_Comm
./plos
```
## Example2:
* Command:
```java
find ./911report -type f
```

* Output:
```java
./911report/chapter-1.txt
./911report/chapter-10.txt
./911report/chapter-11.txt
./911report/chapter-12.txt
./911report/chapter-13.1.txt
./911report/chapter-13.2.txt
./911report/chapter-13.3.txt
./911report/chapter-13.4.txt
./911report/chapter-13.5.txt
./911report/chapter-2.txt
./911report/chapter-3.txt
./911report/chapter-5.txt
./911report/chapter-6.txt
./911report/chapter-7.txt
./911report/chapter-8.txt
./911report/chapter-9.txt
./911report/preface.txt
```

## The `-type` option is particularly useful when you want to isolate your search to a particular kind of filesystem object, like when you're looking for directories that match a certain name pattern, or when you're trying to find all the symbolic links in a directory for review or maintenance.
## -iname
## Example1:
* Command:
```
find -iname "bio*"
```
* Output:
```java
./biomed
```
## Example2:
* Command:
```java
find -iname "chapter*.txt"
```

* Output:
```java
./911report/chapter-1.txt
./911report/chapter-10.txt
./911report/chapter-11.txt
./911report/chapter-12.txt
./911report/chapter-13.1.txt
./911report/chapter-13.2.txt
./911report/chapter-13.3.txt
./911report/chapter-13.4.txt
./911report/chapter-13.5.txt
./911report/chapter-2.txt
./911report/chapter-3.txt
./911report/chapter-5.txt
./911report/chapter-6.txt
./911report/chapter-7.txt
./911report/chapter-8.txt
./911report/chapter-9.txt
```

## The `-iname` option is particularly useful when you are unsure of the capitalization of the file names you are looking for, or when the file system contains file names with inconsistent capitalization patterns.

## Source:
* https://man7.org/linux/man-pages/man1/find.1.html
* https://www.redhat.com/sysadmin/linux-find-command
