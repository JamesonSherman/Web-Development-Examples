notes for install:
npm init
npm install express --save
node app.js //to run

so the express application is broken down into a few steps
1. is that of the file folder system.
the main body of the express folder will hold your js files needed to run the program
views holds the ejs or embedded javascript templates. these allow you to manipulate js via routes
then there is the public folder. this folder holds our css


/root folder
app.js
includes:
a couple includes are needed for express and for your sanity

var express = require("express");  //requires express
var app = express();                // sets a variable to be used by express
app.use(express.static("public"));  allows app to use a static folder like public for css
app.set("view engine", "ejs");  //removes the need to use .ejs on the end of the file renders

app.get requests and listen:

/*
this type of app.get is the simple root folder. it simply renders whatever ejs file from the views folder
you prefer
*/
app.get("/", function(request,response){
response.render("home");
});


/*
this syntax is a variable syntax for displaying custom content
the : allows us to do a custom item response
the render object allows us to pass the variable as an object to ejs. 
*/
app.get("/fallinlovewith/:thing", function(request,response){
    let thing = request.params.thing;
    response.render("love",{thingvar: thing});
});


/*
this get is how we send multiple items and renders.

*/
app.get("/posts", function(request, response){
var posts = [
{title: "post1", author: "Susy"},
{title: "post2", author: "Colt"},
{title: "post3", author: "dillion"},
{title: "post4", author: "Bob"}]
response.render("posts", {posts: posts});
});


/*
this app.listen allows us to connect and listen ona  port and return a function on connection.
*/
app.listen(3000,function(){
    console.log("listening on 3000");
});

/*
this is a special one as this is a post request. this allows us to

*/

app.post("/addfriend", function(request,response){
   let friend = request.body.newfriendform;
   friends.push(friend);
response.redirect("/friends");
});


ejs:
types of closing symbols:
<% 'Scriptlet' tag, for control-flow, no output
<%_ ‘Whitespace Slurping’ Scriptlet tag, strips all whitespace before it
<%= Outputs the value into the template (HTML escaped)
<%- Outputs the unescaped value into the template
<%# Comment tag, no execution, no output
<%% Outputs a literal '<%'
%> Plain ending tag
-%> Trim-mode ('newline slurp') tag, trims following newline
_%> ‘Whitespace Slurping’ ending tag, removes all whitespace after it


this system using the tags above allows us to call custom items in ejs.
example:
<% posts.forEach(function(post){ %>
    <li> <%=post.title %> - <strong><%= post.author %></strong> </li>
<% }) %>

we wrap the parts of our code in the <% style symbols for use. if you pass something you can use the object
passed in the ejs file

partials header footer:
you can also make what are called ejs partials
these are callable code for parts of your other files.
example:
<%include partials/header%>
<%include partials/footer%>

this allows express to know where to call.


public:
public is a nifty folder to store images and css!
make sure you use the / infront of the file name and the app.use(express.static("public"));
in conjunction with:
<link rel="stylesheet" href="/app.css">
