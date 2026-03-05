# Work Sheet 2 - A Less Pathetic App

Currently, our app is pathetic. It loads a webpage, albeit one now including cats, but you can't do anything. What if I want to log in and send my cat pictures?

Well, let's create an app where one can:
- Log In
- Send Cat Photos

> Of course the internet is not a nice place, so you probably need better security measures - and probably some moderation - either using AI or a human. But, since you're not doing that, we don't need to do this in this worksheet.

## Task 2.1 - Log In

So, as an aside, I mentioned we have the `GET` function - well, we also have a `POST` function, which allows the person to send stuff to our server - using methods including a HTML webform.

A HTML Webform is just a way we can implement, on our public website, a form where people can put stuff in, and stuff happens. 
More detail is available at [https://www.w3schools.com/html/html_forms.asp](https://www.w3schools.com/html/html_forms.asp).

**Exercise 2.1.1** Can you implement a form on the website which will:
- Action to `/login`
- Use method `post`
- Include: a username input, a password input, and of course a submit button
- Add a label to the username and password inputs
- For the username and password inputs, put the `name` attribute as `username` and `password` respectively.

Now, raw HTML looks bland. In worksheet 1, we did inline styling, where we specify the style of an individual block, but we can do this systematically using CSS. Either by using a separate file, or having one big shared file - good for maintaining a brand identity for example.

Now, lets try to do this for a single file. In the head tag, you can add:
```html
<style>
    p {
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
    #hello {
        border: 1px solid white;
        background: blue;
    }
    .labelOne {
        color: black;
    }
</style>
```

Here, we specify that:
- Anything in a paragraph (i.e. enclosed in `<p>` and `</p>`) has a particular font. Now, the font-family is an interesting specification since it orders priority, as not all browsers have the same fonts loaded! In my case, it will prioritise Segoe UI, then Tahoma, then Geneva, then Verdana, and if all else fails, just any old sans-serif font will do.
- Anything with `id` attribute in the html set to `hello` will have a blue background with a white solid border. For IDs in CSS, it must begin with the `#`, e.g. `#he;llo`.
- Anything with `class` attribute set in html set to `labelOne` will be black. For classes in CSS, it must begin with the `.`, e.g. `.labelOne`.

Note that `id` and `class`, although similar, have differences. You can have something wih an id and a class (or multiple classes), e.g.:
```html
<p class="labelOne exampleClassTwo" id="hello">Hello</p>
```
and here, the rules for `.labelOne`, `#hello`, and if we set it, `.exampleClassTwo` will all be followed.

It should be noted that a class can be used multiple times, but each id name should be used once.

**Exercise 2.1.2** can you now make it prettier, so:
- All `input` have a `max-width` of 250px. Add a border, 2px solid in any colour you want, and perhaps add `padding` to be `5px` and `border-radius` to be `5px`
- The `label` colour is nicer
- The Submit button to have a different background colour of your choosing, and of course text colour to contrast
    - If you can, can you make the background colour change when you hover over it? You may need to Google this one.

## Task 2.2 - Handling the Login Request

Now that we have a form that sends data to `/login`, we need our server to actually **handle the POST request**.

First, we need to tell Express to understand form data. Near the top of your `index.js`, after creating the app, add:

```js
app.use(express.urlencoded({ extended: true }));
````

This allows us to read the form data sent from the browser.

Now, inside your request handler, add a new condition:

```js
if(path == "/login" && method == "POST"){
    let username = req.body.username;
    let password = req.body.password;

    res.set("Content-Type","text/plain");
    res
        .status(200)
        .send(`Hello ${username}, your login request was received!`);
}
```

Here we extract the values from the form using `req.body`.

## Exercise 2.2.1

Try submitting the form on your webpage.

If everything works correctly, you should see a page confirming the username you entered.

Try submitting different usernames and see the response change.

## Task 2.3 - Where Next?

Congratulations — you now have a web app that can:

* Serve HTML pages
* Display images
* Accept user input through forms
* Process POST requests on the server

In a real application, the next steps would include:

* Storing user accounts in a database
* Authenticating passwords securely
* Allowing users to upload cat photos
* Displaying user-submitted content

But for now, you have built the foundations of a **real web application**. Give yourself a pat on the back!