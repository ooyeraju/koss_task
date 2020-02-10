# Getting Started with JSON

At first we need to understand what is JOSN and the basic syntax of JSON.
JSON stands for JavaScript Object Notation and according to [W3School](https://www.w3schools.com/js/js_json_intro.asp) it is a light weight format for storing data.

### JSON Data types and Syntax

JSON has these many Data types and follow this simple syntax.
* Strings
* Boolean
* Numbers
* Object
* Array
* Null

```json
{
  "Name": "Watson", 
  "Male": true, 
  "age": 27,
  "address": {
    "streetAddress": "21 2nd Street",
    "city": "New York",
    "state": "NY"
  }, 
  "children": ["Jhon", "Marry"], 
  "spouse": null 
}
```
## To view images from Subreddit
 
Since the JSON link was given has to many lines of code so we need to copy that whole text to any IDE and format it(in my case it was VS Code). Just to see where is the link of the images that we are going to display. To do this one can just do CTRL + F and look for .jpg and get to this.

```json
{
    "kind": "Listing",
    "data": {
        "modhash": "",
        "dist": 26,
        "children": [
            {
              "data": {
                  "approved_at_utc": null,
                  
                  
                  "url": "https://i.redd.it/ugmxx1vl7of41.jpg",
                  
                  "is_video": false
              }
            }]
        }
}
```
So, the required link was found inside object named 'data' which was a part of 'children' array which itself was a part of another object named data. 

Upnext we needed to import this url and display this as a image in a simple website.
So a simple website was created as given below.

```html
  <script>
    var xmlhttp = new XMLHttpRequest(); // to import data from any website
    xmlhttp.onreadystatechange = function () {
      if (this.readyState == 4 && this.status == 200) { // 4 means the request has been finished and the response is ready . 
        var obj = JSON.parse(this.responseText);
        var posts = obj.data.children;
        var html_code = '';
        for (var i = 1; i < posts.length; i++) {
          html_code += '<li><b>' + posts[i].data.title + '<br></b><img height = 500 width = 500 src ="' + posts[i].data.url + '" /></li>';
        }
        document.getElementById("demo").innerHTML = html_code;
      }
    };
    xmlhttp.open("GET", "http://www.reddit.com/r/pics.json", true);
    xmlhttp.send();
  </script>
```
Here, XMLHttpRequest is a built-in browser object that allows to make HTTP requests in JavaScript and use myFunction() to display the array. `readyState=4` is used to check if the request has been finished and the response is ready. `status=200` means status is OK. 

JavaScript has a built in function to convert a string, written in JSON format, into native JavaScript objects: `JSON.parse()` So, if you receive data from a server, in JSON format, you can use it like any other JavaScript object.


Now we make a loop and pass every url starting from 1 since the url of 0th element don't contain an image. Apart from the image we also pass the title of the image to make things clear.

After this we use `document.getElementById("demo")` to pass the id of list that we have made in html.

We then use `xmlhttp.open` to get the location of JSON file. And `xmlhttp.send()` to send post data.

