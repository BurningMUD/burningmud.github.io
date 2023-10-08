---
layout: default
---
<style>
h1 {
    color: darkorange;
}
</style>
<div class="center">
<img src="{{ site.baseurl }} {% link /images/BurningMUD_ASCII_Logo.png %} " alt="Burning MUD">

<script src="https://cdn.jsdelivr.net/npm/typed.js@2.0.12"></script>

<div id="typed-output">
var options = {
    strings: [
        "<h1>Out of the burning ashes</h1>",
        "<h1>Rose a new life</h1>",
        "<h1>A new creature</h1>",
        "<h1>Born into the Burning World</h1>"
    ],
    typeSpeed: 50,  // typing speed
    backSpeed: 25,  // backspacing speed
    backDelay: 1000,  // delay before starting to backspace
    startDelay: 500,  // start delay time
    showCursor: true,  // show cursor
    cursorChar: '|',  // character for cursor
    loop: false,  // loop the animation
    fadeOut: false,  // fade out instead of backspace
    smartBackspace: true,  // only backspace what doesn't match the previous string
    appendTo: '#typed-output'  // the element to append typed strings to
};

var typed = new Typed("#typed-output", options);
</div>
