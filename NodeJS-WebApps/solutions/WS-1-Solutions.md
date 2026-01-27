# Worksheet 1 - Solutions

**Exercise 1.3.1**

Simply, we change the words `Hello World` and `Page Not Found` to whatever you desire.

**Exercise 1.4.1**

Here, I made a boring page:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Hello World</title>
    <style>
        body {
            background: #8e2157;
            color: white;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        p {
            color: wheat
        }
    </style>
</head>
<body>

<h1>Hello World</h1>
<p>
    This is my website!
</p>

</body>
</html>
```
and of course saved into `frontPage.html`

**Exercise 1.4.3**
I made the following (but of course this isn't the mandatory design) and saved into `error404.html`
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Not Found!</title>
    <style>
        body {
            background: #8e2157;
            color: white;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        p {
            color: wheat
        }
    </style>
</head>
<body>

<h1>Page not found</h1>
<p>
    <b>You are lost</b>. Try not to be lost.
</p>

</body>
</html>
```

Quite brutal messaging. Anyway, we amend:
```js
res.set("Content-Type","text/plain");
res
    .status(404) // the infamous 404 not found
    .send("Page Not Found")
```
to:
```js
res.set("Content-Type","text/html");
res
    .status(200)
    .send(fs.readFileSync("./error404.html").toString());
```

**Exercise 1.4.5** -
here I made the document `cat.html` with content:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Cat Photos</title>
    <style>
        body {
            background: #8e2157;
            color: white;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        p {
            color: wheat
        }
    </style>
</head>
<body>

<h1>Look at These Cats!</h1>

<img src="https://upload.wikimedia.org/wikipedia/commons/e/e0/Cat_demonstrating_static_cling_with_styrofoam_peanuts.jpg" style="max-height: 250px;">
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/15/Cat_August_2010-4.jpg/2560px-Cat_August_2010-4.jpg" style="max-height: 250px;">
<img src="https://upload.wikimedia.org/wikipedia/commons/5/53/Sheba1.JPG" style="max-height: 250px;">

</body>
</html>
```
and I changed the server file (`index.js`) adding 
```js
if(...){ 
    ...
}

else if(path == "/catphotos" && method=="GET"){
    res.set("Content-Type","text/html");
    res
        .status(200)
        .send(fs.readFileSync("./cat.html").toString());
}

else {
    ...
}
```
(of course the first and last blocks are stuff we already have, and I am just showing what I added)