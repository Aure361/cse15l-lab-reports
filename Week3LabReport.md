## Part One

**Code**

`import java.io.IOException;`

`import java.net.URI;`

`import java.util.ArrayList;`

`class Handler implements URLHandler {`

    ArrayList<String> stringList = new ArrayList<>();
    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("Stringlist: ");
        } else if (url.getPath().equals("/Stringlist")) {
            return String.format("Stringlist is now: " + stringList);
        } else {
            System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    stringList.add(parameters[1]);
                    return String.format("Has been added to StringList: " + parameters[1]);
                }
            }
            return "404 Not Found!";
        }
    }
`}`

`class NumberServer {`

    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
`}`

> Loading server

![Image](lab3serverpic1.png)


- The method handleRequest(URI url) is called. The relevant arguments are either nothing after the 4000 or "/". If these values are found in the url, then once the request is processed it will show a server that displays "Stringlist:"

> Adding strings to server

![Image](lab3serverpic2.png)

- The method handleRequest(URI url) is called. The relevant arguments are "/add". If these values are found in the url, the string found after the query will be added to a string list. Then the server will display "Has been added to Stringlist: *string added*"

> Displaying updated Stringlist

![Image](lab3serverpic3.png)

- The method handleRequest(URI url) is called. The relevant arguments are "/Stringlist". If these values are found in the url, then it will return a string format of the stringlist. The server will display "Stringlist is now: *list of strings*"

## Part Two
