# Worksheet 2 - Solutions

**Exercise 2.1.1**

Simply, I added the following in my body after the `Hello World` text (or whatever you replaced it with in WS1)

```html
<form action="/login" method="post">
    <label>Username</label>
    <input name="username">
    <label>Password</label>
    <input name="Password" type="password">
    <input class="submitButton" type="submit">
</form>
```

**Exercise 2.1.2**

Here's what I added. Inside `<body>` and `</body>`, I added `<style>` and `</style>` on two separate lines. In between that, I added:
```css
input {
    max-width: 250px;
    border: 2px solid blueviolet;
    padding: 5px;
    border-radius: 5px;
}
label {
    color: yellow;
}
.submitButton {
    background-color: blueviolet;
    color:white
}
.submitButton:hover {
    background-color: blue;
}
```