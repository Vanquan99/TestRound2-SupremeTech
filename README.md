# Android Internship 2022 - Test Round 2 - SupremeTech

[Please click this](https://coderbyte.com/sl-candidate?promo=supremetechcoltd-j377u:algorithm-assessment-1vp6bd6z2l) to start the Coderbyte Test.

[Round 1](https://github.com/Vanquan99/TestRound-SupremeTech)
[Round 2](https://github.com/Vanquan99/TestRound2-SupremeTech)
[Round 3](https://github.com/Vanquan99/TestRound3-SupremeTech)

### Kindly note down some important details related to this Test:

- The CoderByte Online Test is conducted in English.

- Do not cheat. We appreciate your own value more than the scores.

### Test Android Engineer (Intern/Fresher)
>Java REST GET Simple
In the Java file, write a program to perform a GET request on the route: 
https://coderbyte.com/api/challenges/json/rest-get-simple
and then print to the console the hobbies property in the following format:
ITEM1, ITEM2, ...
Example output:
running, painting

# CODE
```
import java.io.*;
import java.net.MalformedURLException;
import java.net.URL;
import java.net.URLConnection;
import java.util.stream.Collectors;


public class Main {

    public static String getStringFromStream(final InputStream inputStream) {
        String result = null;
        BufferedReader streamReader = null;
        try {
            streamReader = new BufferedReader(new InputStreamReader(inputStream, "UTF-8"));
            result = streamReader.lines().collect(Collectors.joining("\n"));
        } catch (UnsupportedEncodingException e) {
            e.printStackTrace();
            return null;
        } finally {
            try {
                if(streamReader != null) 
                    streamReader.close();
                if(inputStream != null)
                    inputStream.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }

        return result;
    }

    public static String simpleParseArrayProperty(String json, final String propertyName) {
        if(json == null)
            return null;
        int lastIndex = json.lastIndexOf(String.format("\"%s\"", propertyName));
        json = json.substring(lastIndex);
        lastIndex = json.lastIndexOf("[");
        json = json.substring(lastIndex+1);
        return json = json
                .replaceAll("[\\]}\"]", "")
                .replaceAll("\\,", ", ")
                .trim();
    }

    public static void main(String[] args) {
        System.setProperty("http.agent", "Chrome");
        try {
            URL url = new URL("https://coderbyte.com/api/challenges/json/rest-get-simple");
            try {
                URLConnection connection = url.openConnection();
                InputStream inputStream = connection.getInputStream();
                System.out.println(simpleParseArrayProperty(getStringFromStream(inputStream), "hobbies"));
            } catch (IOException e) {
                e.printStackTrace();
            }
        } catch (MalformedURLException e) {
            e.printStackTrace();
        }
    }
}
```

