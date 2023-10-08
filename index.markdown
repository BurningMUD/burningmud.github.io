---
layout: default
---
<style>
h1 {
    color: darkorange;
}
.terminal-container {
    text-align: center;
    width: 100%; /* take the full width of its parent */
}
.terminal {
    text-align: left;
    margin: auto;
    padding: 10px;
    display: inline-block;
}
</style>

<div class="center">
<img src="{{ site.baseurl }} {% link /images/BurningMUD_ASCII_Logo.png %} " alt="Burning MUD">

<div id="terminal" class="terminal"></div>

<script>
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

typeLine();  // Start the typewriter effect
</script>

