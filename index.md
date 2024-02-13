# CSE15L - Lab - Reports
# Lab Report 3 - Bugs and Commands
## Part 1 - Bug for `testReverseInPlace
## A Failure-Input
```java
@Test 
public void testReverseInPlace() {
    int[] input1 = { 5,4,3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3,4,5 }, input1);
}
```

## An input that doesn't induce a failure
```java
@Test 
public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
}
```

## Symptom:


## The Bug: 
##Before: 

##After:
