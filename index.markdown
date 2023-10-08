---
layout: default
---
<style>
h1 {
    color: darkorange;
}
.terminal {
    text-align: left;
    justify-content: center;
}
</style>

<div class="center">
<img src="{{ site.baseurl }} {% link /images/BurningMUD_ASCII_Logo.png %} " alt="Burning MUD">

<div id="terminal" class="terminal"></div>

<script>
body {
background-image: url('/images/BurningMUD_Orhan.jpg');
background-size: cover;
background-position: center;
transition: opacity 5s;
opacity: 0;
}

function fadeInBackground() {
    document.body.style.opacity = "1";
}
const terminal = document.getElementById("terminal");
const lines = [
    "Out of the burning ashes",
    "Rose a new life",
    "A new creature",
    "Born into the Burning world"
];
const typeSpeed = 50;

let currentLineIndex = 0;
let currentCharIndex = 0;

function typeLine() {
    if (currentCharIndex < lines[currentLineIndex].length) {
        terminal.innerHTML += lines[currentLineIndex].charAt(currentCharIndex);
        currentCharIndex++;
        setTimeout(typeLine, typeSpeed);
    } else {
        terminal.innerHTML += '<br>';
        currentCharIndex = 0;
        currentLineIndex++;
        if (currentLineIndex < lines.length) {
            setTimeout(typeLine, 500); // 500ms delay between lines
        }
    }
}
setTimeout(fadeInBackground, 2000); // 2 seconds delay before fade-in
typeLine();  // Start the typewriter effect
</script>

