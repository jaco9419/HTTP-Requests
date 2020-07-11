# HTTP-Requests
Comparing ways to do HTTP Requests using Codecademy and FreeCodeCamp

## Get XMLHttp Request Method (FreeCodeCamp)

You can also request data from an external source. This is where APIs come into play.

Remember that APIs - or Application Programming Interfaces - are tools that computers use to communicate with one another. You'll learn how to update HTML with the data we get from APIs using a technology called AJAX.

Most web APIs transfer data in a format called JSON. JSON stands for JavaScript Object Notation.

JSON syntax looks very similar to JavaScript object literal notation. JSON has object properties and their current values, sandwiched between a { and a }.

These properties and their values are often referred to as "key-value pairs".

However, JSON transmitted by APIs are sent as bytes, and your application receives it as a string. These can be converted into JavaScript objects, but they are not JavaScript objects by default. The JSON.parse method parses the string and constructs the JavaScript object described by it.

You can request the JSON from freeCodeCamp's Cat Photo API. Here's the code you can put in your click event to do this:

<pre><code>const req = new XMLHttpRequest();
req.open("GET",'/json/cats.json',true);
req.send();
req.onload = function(){
  const json = JSON.parse(req.responseText);
  document.getElementsByClassName('message')[0].innerHTML = JSON.stringify(json);
};</code></pre>

Here's a review of what each piece is doing. The JavaScript XMLHttpRequest object has a number of properties and methods that are used to transfer data. First, an instance of the XMLHttpRequest object is created and saved in the req variable. Next, the open method initializes a request - this example is requesting data from an API, therefore is a "GET" request. The second argument for open is the URL of the API you are requesting data from. The third argument is a Boolean value where true makes it an asynchronous request. The send method sends the request. Finally, the onload event handler parses the returned data and applies the JSON.stringify method to convert the JavaScript object into a string. This string is then inserted as the message text.

### Example Rendering Images from Data Sources

<pre></code>document.addEventListener('DOMContentLoaded', function(){
    document.getElementById('getMessage').onclick = function(){
      const req=new XMLHttpRequest();
      req.open("GET",'/json/cats.json',true);
      req.send();
      req.onload = function(){
        const json = JSON.parse(req.responseText);
        let html = "";
        //Pre-filter JSON to Get the Data You Need
        json = json.filter(val => {
          return (val.id == 1);
        })
        json.forEach(function(val) {
          html += "<div class = 'cat'>";
          html += `<img src = "${val.imageLink}" alt="${val.altText}">`;
          html += "</div><br>";
        });
        document.getElementsByClassName('message')[0].innerHTML=html;
      };
     };
  });</code></pre>

## GET XMLHttp Request Method (Codecademy)

<pre><code>const xhr = new XMLHttpRequest;
const url = 'https://api-to-call.com/endpoint';

xhr.responseType = 'json';
xhr.onreadystatechange = () => {
  if (xhr.readyState === XMLHttpRequest.DONE) {
  return xhr.response;
  }
};

xhr.open('GET', url);
xhr.send();</pre></code>

## Get fetch method (FreeCodeCamp)

Another way to request external data is to use the JavaScript fetch() method. It is equivalent to XMLHttpRequest, but the syntax is considered easier to understand.

Here is the code for making a GET request to /json/cats.json

<pre><code>fetch('/json/cats.json')
    .then(response => response.json())
    .then(data => {
        document.getElementById('message').innerHTML = JSON.stringify(data);
    })</code></pre>
    
Take a look at each piece of this code.

The first line is the one that makes the request. So, fetch(URL) makes a GET request to the URL specified. The method returns a Promise.

After a Promise is returned, if the request was successful, the then method is executed, which takes the response and converts it to JSON format.

The then method also returns a Promise, which is handled by the next then method. The argument in the second then is the JSON object you are looking for!

Now, it selects the element that will receive the data by using document.getElementById(). Then it modifies the HTML code of the element by inserting a string created from the JSON object returned from the request.

## Get fetch method (Codecademy)

<pre><code>fetch(endpoint, {cache: 'no-cache'})
.then(response => {
  if (response.ok) {
    return response.json();
  }
  throw new Error('Request failed!');
}, networkError => {
  console.log(networkError.message)
})
.then(jsonResponse => {
  renderResponse(jsonResponse);
})</code></pre>

## POST XMLHttp Request Method (FreeCodeCamp)

In the previous examples, you received data from an external resource. You can also send data to an external resource, as long as that resource supports AJAX requests and you know the URL.

JavaScript's XMLHttpRequest method is also used to post data to a server. Here's an example:

<pre><code>const xhr = new XMLHttpRequest();
xhr.open('POST', url, true);
xhr.setRequestHeader('Content-Type', 'application/json; charset=UTF-8');
xhr.onreadystatechange = function () {
  if (xhr.readyState === 4 && xhr.status === 201){
    const serverResponse = JSON.parse(xhr.response);
    document.getElementsByClassName('message')[0].textContent = serverResponse.userName + serverResponse.suffix;
  }
};
const body = JSON.stringify({ userName: userName, suffix: ' loves cats!' });
xhr.send(body);</code></pre>

You've seen several of these methods before. Here the open method initializes the request as a "POST" to the given URL of the external resource, and uses the true Boolean to make it asynchronous. The setRequestHeader method sets the value of an HTTP request header, which contains information about the sender and the request. It must be called after the open method, but before the send method. The two parameters are the name of the header and the value to set as the body of that header. Next, the onreadystatechange event listener handles a change in the state of the request. A readyState of 4 means the operation is complete, and a status of 201 means it was a successful request. The document's HTML can be updated. Finally, the send method sends the request with the body value, which the userName key was given by the user in the input field.

## POST XMLHttp Request Method (Codecademy)

<pre><code>const xhr = new XMLHttpRequest;
const url = 'https://api-to-call.com/endpoint';
const data = JSON.stringify({id: '200'});

xhr.responseType = 'json';
xhr.onreadystatechange = () => {
if (xhr.readyState === XMLHttpRequest.DONE) {
return xhr.response;
}
}

xhr.open('POST', url);
xhr.send(data);</code></pre>

## Check Geographical location

<pre><code>if (navigator.geolocation){
navigator.geolocation.getCurrentPosition(function(position) {
document.getElementById('data').innerHTML="latitude: " + 
position.coords.latitude + "<br>longitude: " + position.coords.longitude;
});
}</code></pre>

<hr>
The contents in this file are extractions from FreeCodeCamp and Codecademy
