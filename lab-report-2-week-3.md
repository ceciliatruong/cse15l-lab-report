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



