# Week 3 Lab Report
## Part 1
Below is my code for the Simplest Search Engine:
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;
// note that this code doesn't account for case-sensitive entries
class Handler implements URLHandler {
    ArrayList<String> list = new ArrayList<String>();
    ArrayList<String> finalSearch = new ArrayList<String>();
    public String handleRequest(URI url) {
        if (url.getPath().contains("/search")) {
            if(finalSearch.size() > 0) {
                finalSearch.removeAll(finalSearch);
            }
            String[] parameters = url.getQuery().split("=");
            if(parameters[0].equals("s")) {
                for(int i = 0; i < list.size(); i++) {
                    if(list.get(i).contains(parameters[1]) == true) {
                        finalSearch.add(list.get(i));
                    }
                }
                if(finalSearch.size() <= 0) {
                    return("No matches in the search engine found");
                }
                else {
                    String finalList = finalSearch.toString();
                    return ("Here are the following matches:" + finalList);
                }
            }
        }

        else if (url.getPath().contains("/add")) {
            String[] parameters = url.getQuery().split("=");
            if (parameters[0].equals("s")) {
                list.add(parameters[1]);
                String tempList = list.toString();
                return("String has been successfully entered into the search engine! This is the current search engine word bank" + tempList);
                }
            }   
        return ("welcome to cc's search engine!!! type /add?s=[enter any word here] after the url to add some terms to the search engine & type /search?s=[enter any word here] after the url to see if your words match up with the words inputted in the search engine!");  
    }
}


class SearchEngine {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
Here is an example of me adding words to the search engine (note: i already added a couple more words prior to this screenshot):

![image](images\better-testing-add.png)

When the `/add?s=yummy` action is inputted, the code first checks for whether `/search` or `/add` is being called. In this case, it's `/add` so my code takes the 2nd argument of the query (`parameters[1]`) and adds it to the end of the String ArrayList (`list`) I've created. I've also made it so that the web server shows the current word bank for a visual confirmation that it is properly adding words to the ArrayList.

![image](images\searching-a.png)

Using my previous word bank, the following command is `/search?=a`. Once again, the program first looks to see whether `/search` or `/add` is being called, and here it is `/search`. It then checks to see if the final output ArrayList (`finalSearch`) is empty in order to make sure that the output is unique to this command. After clearing out the final list, it then proceeds to iterate through the entire word bank to check for matches with the entered search argument and adds any words that match to `finalSearch`. It then verifies if there was at least 1 match, and since `finalSearch.size()` turns out to be greater than 0, it moves onto the next step. Lastly, the program turns 'finalSearch` into a String, and the results are displayed on the web server.

![image](images\searching-z.png)

Now, I am inputting `/search?=z` with my previous word bank. Again, the program goes through the same cycle as the previous step, except it differs at the verification for at least 1 match. When the program checks for `finalSearch.size()`, it results in 0 because there are no words in the word bank that contain the character `z`.

# Part 2 


I will be going over the issues with files `ArrayExamples.java` and `ListExamples.java`.

1. Beginning first with `ArrayExamples.java`, I will be looking at the `ReverseInPlace` method. As a reference, I've included the code snippets for `ReverseInPlace` along with the code I wrote for testing the method:
```  
// reverseInPlace code
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }

// my test code 

@Test
  public void testLongReverseInPlace() {
    int[] input1 = { 5, 4, 3, 2, 1 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 1, 2, 3, 4, 5 }, input1);
  }

```
- The **failure-inducing input** (the code of the test): {5, 4, 3, 2, 1}
- The **symptom** (the failing test output): ``expected [4] at index 3, got [2] instead`` ![image](images\reverseinplace-test-failed.jpg)
- The **bug** (the code fix needed): Since the method directly enacts changes onto the input array and works from index 0 to the last index, the original integers of the first few indices aren't properly saved anywhere and are overwritten with the new elements by the time the program needs to refer back to it at the end. A possible fix could be like this:
```
  static void reverseInPlace(int[] arr) {
    int[] newArray = arr.clone();
    for(int i = 0; i < newArray.length; i += 1) {
      arr[i] = newArray[newArray.length - i - 1];
    }
  }
```
- When the test runs with my input of {5, 4, 3, 2, 1}, the array goes through the for-loop. As a visualizer for what happens during the for-loop, I have written below the step as the program runs through each index:
    - start of program: {5, 4, 3, 2, 1}
    - index 0: {**1**, 4, 3, 2, 1}
    - index 1: {1, **2**, 3, 2, 1}
    - index 2: {1, 2, **3**, 2, 1}
    - index 3: {1, 2, 3, **2**, 1}
    - index 4: {1, 2, 3, 2, **1**}
    - end of program: {1, 2, 3, 2, 1}

- By running through the for-loop visually, we can start seeing the issue manifest itself at index 3 when the program tries to access the original index 1 value which had already been overwritten at the for-loop index 1 line. This aligns with the symptoms of the test that also points to index 3 being the location where the actual output starts to differ from the expected output.

2. The next file that I'm looking at is the `merge` method in `ListExamples.java`. As usual, I will be including below the code for the `merge` method as well as my test that failed.

```
// merge code
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) { 
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) { 
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index1 += 1; 
    }
    return result;
  }

// my test case
    @Test
    public void testMerge() {
        List<String> list1 = Arrays.asList("ab", "donut", "orange");
        List<String> list2 = Arrays.asList("a", "donut", "ornge");
        assertEquals(Arrays.asList("a", "ab", "donut", "donut", "orange", "ornge"), ListExamples.merge(list1, list2));
        // assertEquals(-13, "orange".compareTo("ornge"));
    }
```
- The **failure-inducing input** (the code of the test): `list1`{"ab", "donut", "orange"}, `list2`("a", "donut", "ornge")
- The **symptom** (the failing test output): ``java.lang.OutOfMemoryError: Java heap space``
![image](images\merge-test-failed.jpg)
- The **bug** (the code fix needed): When `index2 < list2.size()`, it enters the while loop and adds the element at `index2` of `list2` to the final list, but it never increments `index2`. Instead, it increments `index1` which has already been fully iterated through at this point of the code. Since `index2` is never incremented, the code never fully iterates through all of `list2` and will keep adding the same `index2` element of `list2` to the final copy indefinitely. A potential fix could look like this:
```
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) { 
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) { 
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index2 += 1; 
    }
    return result;
  }
```
- When we try to run a test with `list2` having a 'lower' alphabetical value than `list1` as my test has done, we encounter the issue with the while loop as mentioned in my explanation of the bug. Since `index2` isn't properly incremented, the while loop condition for ending is never met and so the code itself never stops adding the element at `index2` of `list2`. This is why the test runs into the ``java.lang.OutOfMemoryError: Java heap space`` since the code is stuck in an infinite loop. 



