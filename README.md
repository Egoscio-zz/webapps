# How to make a WebApp

## Introduction:

After the recent advancements in HTML5, CSS3 and ECMAScript 6 (Javascript), as well as a handful of powerful libraries and frameworks such as jQuery, AngularJS, and RiotJS, Developers began working on implementing said technologies in the domain of mobile applications. By following this philosophy, one is able to write his or her code once and deploy it on multiple platforms with the click of a button. This tutorial will show you how to make web apps using your existing knowledge of making websites.

## Step 1: The Basics

First, if you are doing this locally, make a folder to contain your project files. This can be named whatever you want.

Fire up your preferred code editor, be it [Atom](https://atom.io), Notepad++, [Codepen](https://codepen.io), or whatever it may be (not MS Word or Google Docs!), and make a new HTML document named `index.html`.

Paste in this snippet of HTML to get you started:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" type="text/css" href="style.css">
  <title>My WebApp</title>
</head>
<body>
  <!-- Your code starts here -->

  <!-- and ends here -->
  <script type="application/javascript" src="https://code.jquery.com/jquery-latest.min.js"></script>
  <script type="application/javascript" src="script.js"></script>
</body>
</html>
```

In the same folder, make a new file named `style.css` and paste in this snippet of CSS:

```css
/* style.css */

*, *:before, *:after {
  box-sizing: border-box;
}

* {
  margin: 0;
  padding: 0;
}

html, body {
  height: 100%;
  width: 100%;
}

/* Your code goes below here */
```

Finally, in the same folder, make a new file named `script.js` and paste in this snippet of JS:

```js
// script.js

$(document).ready(function () {
  // Your code goes in here
})
```

These snippets of code form the foundation of your application, yet they don't do much just yet. That's for step 2!

## Step 2: Let's make something!

Now that we have the base of our app, lets make something simple... a tap race game!

Add the following snippets in the respective files:

HTML: Add two buttons to the page with classes so that they are distinguishable in code.
```html
<div class="tap red">Tap to play</div>
<div class="tap blue">Tap to play</div>
```
CSS: Defines how the two buttons should look, gives them respective colors, and flips one of them.
```css
.tap {
  height: 50%;
  width: 100%;
  font-size: 3em;
  font-family: Arial;
  text-align: center;
  padding-top: 100px;
}

.red {
  background-color: red;
  transform: rotate(180deg);
}

.blue {
  background-color: blue;
}
```
JS: On touch, increment the score of the button presser by 1.
```js
// Contains score data:
var scores = {
  red: 0,
  blue: 0
}
var won = false
var $taps = $('.tap')

// When someone taps an element with the class "tap", run the function.
$taps.on('touchstart mousedown', function (e) {
  if (!won) {
    // The element that was clicked:
    var $this = $(this)
    // Grabs the second item of the class attribute, which is red or blue respectively.
    var type = $this.attr('class').split(' ')[1]
    // Increments the score
    scores[type] += 1
    // Change the text.
    $this.text('Your score is ' + scores[type])
    // Add condition for finishing the game.
    if (scores[type] >== 100) {
      won = true
      // Reward the winner.
      $taps.text(type + ' won the game!')
      setTimeout(function () {
        // Reset scores
        scores = {
          red: 0,
          blue: 0
        }
        // Add it back.
        $taps.text('Tap to play')
        won = false
      }, 3000)
    }
  }
  // Stop it from doing generic actions like selecting text.
  return false
})
```

Now you can run your app depending on your editor (IE: Double click the index.html if you did this locally, or Codepen will auto-reload when you're done typing) and play against a friend!

More steps to come. If you have any questions or suggestions, file an [issue](https://github.com/Egoscio/webapps/issues/new)!
