# Work Sheet 1 - The Hello World App

So, welcome back! Here, we shall brief you on how to mke your first app.

Now, assuming you are in VS Code and have installed everything as highlighted in Worksheet 0, let's begin!

## Task 1.1 - Getting Started

**Please ensure your VS Code is opened in a blank folder, i.e. on the left hand side, you see the folder name and then no files below - not doing so means the rest of these tasks do not work, and it may break something on your computer if done carelessly!**

First, I want you to have the terminal open, and run the command
```
npm init
```

This should give you options, like the name, version, etc - you can ignore this by simply pressing enter (and we take the default values the system sets).

At the end, you have the option to accept or reject the data. Please accept (by pressing enter or actually typing `yes`).

Now, we are initialised! We now need to install stuff for our project. Please run:
```
npm i express
```

Express.js is the thing that makes a web app actually exist.

Please also create the file `index.js` - it should be located in the same folder as the newly generated `package.json`. This is your code file. 

## Aside 1.2 - A Brief on JavaScript

JavaScript, like Python, allows for stuff such as comparisons, string manipulations and more. We are also using nodejs so you can install other things to do cool things.

[https://www.w3schools.com/js/](https://www.w3schools.com/js/) provides a good tutorial on JavaScript.

## Task 1.3 - Hello World

Now, lets make our first web app.

Below is my skeleton code. I have commented it (and commented lines don't get executed) - comments in JavaScript start with `//` and anything after it on a single line does not get executed. You can also put comments in between `/*` and `*/` and anything in between won't get executed.

```js
// sets up expressjs - a library we need to make the app
const express = require("express");
const app = express();
const port = 3030; // this is a port number you can set, here for instance once you start the app, localhost:3030 will run the app. This can take up any value between 0 and 65535 in theory, but practically it should be a high number i.e. in the thousands. 3030, 8080, 3000 all work. You can also do some truly cursed options like 42069 for example.

// the main app sequence - to 
app.use(async(req,res) => { // here req is an object that gives us context about the request made from a browser (e.g. what it wants), and res is a callback for the, well, response

    // here, we extract key contextual information which may be of use to you
    let method = req.method.toUpperCase(); // the method is what the person viewing our website wants. e.g. "GET" to get data or "POST" to give us data
    let queryStringParameters = req.query; // the query string. For example at the end of every webpage, you could have ?key1=val1&key2=val2, and this dataset maps key1 to val1 and key2 to val2.
    let headers = req.headers; // the headers - a beginner need not worry with this.
    let body = req.body ? JSON.stringify(req.body) : null; // the body - relevant mainly for POST requests as this is how we get told data, particularly from web forms
    let path = req.path; // the path, e.g. if we load localhost:3030/hello, we get "/hello" here.

    // now we load content and give a response. 
    if(path == "/" && method=="GET"){ // so anything in between these curly braces, { and }, will be for if we load localhost:3030/ and want something
        res.set("Content-Type", "text/plain"); // this is a header - these are standardised for media types - https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/MIME_types/Common_types
        res
            .status(200) // we give a status of 200, which means "Okay!" - here are the common status codes - https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status
            .send("Hello World"); // this is the content we sent back.
    }
    
    else { // this is for the case we don't have a response, e.g. if we try to send something to localhost:3030/ (as a POST), or indeed if the page doesn't exist, e.g. localhost:3030/catphotos
        res.set("Content-Type","text/plain");
        res
            .status(404) // the infamous 404 not found
            .send("Page Not Found")
    }
});

// but wait! we have defined what the app does. Now, we need the app to listen out for requests:

app.listen(port, () => {
    console.log(`Local server running at http://localhost:${port}`);
});
```

Now, in your terminal, write:
```
node index.js
```

Once you get a message like:
```
Local server running at http://localhost:3030
```

It is up and running! Go to your browser and to that link, and there you'll see the words `Hello World`. And, indeed,
if you go to `http://localhost:3030/catphotos`, you will see `Page Not Found`.

**Exercise 1.3.1** -
Try and change these messages. Maybe say "Welcome Onboard" for the front page, and something more creative than "Page Not Found" - and see if it works.

**HINT** - if you change your code, you will need to close and open the program - as it doesn't automatically refresh. Click on your terminal and do `Ctrl+C` or `Cmd+C` and this should terminate. Now, either retype `node index.js` or press the up arrow to autofill that (from the last line you executed) and it should run refreshed.

**Links**

[1] [https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/MIME_types/Common_types](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/MIME_types/Common_types)

[2] [https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status)

## Task 1.4 - HTML

Now, we outputted stuff as a `text/plain` and as you see in the browser, this is quite ugly looking.

Therefore, let us use HTML. There is a course at [https://www.w3schools.com/html/](https://www.w3schools.com/html/) to show you the basics of HTML - and switching tabs to `CSS` to style it.

**Exercise 1.4.1** - Create a new file, in the same folder as `index.js` and call it `frontPage.html`. Now, using the tutorials, make a nicer looking webpage to say the words `Hello World`. Be as creative as you want. Copy the actual html stuff into this `frontPage.html` file, and save it.

**Sub-Task 1.4.2** - now that you have done 1.4.1, lets amend the code.

First, amongst
```js
const express = require("express");
const app = express();
const port = 3030;
```

Add, on the line after this
```js
const fs = require("fs");
```

This imports the file system. Now, let us change:
```js
res.set("Content-Type", "text/plain"); // this is a header - these are standardised for media types - https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/MIME_types/Common_types
res
    .status(200) // we give a status of 200, which means "Okay!" - here are the common status codes - https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status
    .send("Hello World"); // this is the content we sent back.
```
to:
```js
res.set("Content-Type","text/html"); //now we are sending HTML
res
    .status(200)
    .send(fs.readFileSync("./frontPage.html").toString()); // reads that file you made
```

**Exercise 1.4.3** - can you make a prettier "page not found" page and make that work?

**Aside 1.4.4** - I told you earlier you have to restart the program when you make changes. However, now since the front page and page not found page points to a separate HTML file, although that relation is hard coded, the HTML file itself isn't. So, if you want to change anything in your HTML file now, you can do so, save it, and without restarting the program, refresh your webpage to see the changes! Note that if you ever add new pages though, you will need to indeed restart.

**Exercise 1.4.5** - now, using the `img` tags in HTML, lets make a new HTML file for cat photos, and make a webpage, `/catphotos` (method is `GET`).

To help you, a few cat photo URLs (you can use this directly in `src`):
- https://upload.wikimedia.org/wikipedia/commons/e/e0/Cat_demonstrating_static_cling_with_styrofoam_peanuts.jpg
- https://upload.wikimedia.org/wikipedia/commons/thumb/1/15/Cat_August_2010-4.jpg/2560px-Cat_August_2010-4.jpg
- https://upload.wikimedia.org/wikipedia/commons/5/53/Sheba1.JPG