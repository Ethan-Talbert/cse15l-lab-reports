# CSE 15L Week 3 Lab Report

In this lab report we will be discussing both my simple search engine I developed in lab during week 2 as well as some of the bugs I encountered in week 3. For the first part, scroll down normally, for the second part, click [here](#Part-2:-Finding-and-Rewriting-Bugs).

## Part 1: Simple Search Engine

For the first part of this report I will be talking about the simple search engine I developed last week. The goal of this program is to run a server that you can add entries into then retrieve using a simple search command. Here is my code:

```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    ArrayList<String> dictionary = new ArrayList<String>();

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("Welcome to the search engine! There are currently %d items stored.", dictionary.size());
        } else if (url.getPath().contains("/add")) {
            String[] parameters = url.getQuery().split("=");

            if (parameters[0].equals("s")) {
                if (parameters.length == 1) {
                    return "Please specify a word to add!";
                }
                dictionary.add(parameters[1]);
                return String.format("%s added to the dictionary!", parameters[1]);
            }
        } else if (url.getPath().contains("/search")) {
            String[] parameters = url.getQuery().split("=");

            if (parameters[0].equals("s")) {
                String searchTerm = "";
                if (parameters.length != 1) {
                    searchTerm = parameters[1];
                }

                ArrayList<String> temp = new ArrayList<String>();
                for (int i = 0; i < dictionary.size(); i ++) {
                    if (dictionary.get(i).contains(searchTerm)) {
                        temp.add(dictionary.get(i));
                    }
                }
                return this.formatArrayList(temp);
            }
        }
        return "404 Not Found!";
    }

    public String formatArrayList(ArrayList array) {
        // Formats the search array for the Handler class into readable text.
        if (array.size() == 0) {
            return "No matches found!";
        }
        String str = "Matches: ";

        for (int i = 0; i < array.size(); i ++) {
            str += array.get(i);
            if (i < array.size() - 1) {
                str += ", ";
            }
        }

        return str;
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

Most of the structure of this program I shamelessly took from the NumberServer.java code. The part that I created was everything inside the Handler class. Let's see how it works when I run it on my localhost server.

Here is what the program looks like when you access the root URL. It outputs a message about how many items are currently stored in the engine.

![Image 1]("images/week-3/part-1-1.png")



## Part 2: Finding and Rewriting Bugs
## Finishing Up

Thanks for reading this guide! Check out some of my other lab reports on this page!