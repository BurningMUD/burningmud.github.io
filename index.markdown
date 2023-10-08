---
layout: default
---
<style>
h1 {
    color: darkorange;
}
/* Style the cursor as a block */
.typed-cursor {
    opacity: 1;
    animation: blink 0.7s infinite;
    /* background-color: #fff; */
    width: 10px;
    display: inline-block;
}

@keyframes blink {
    50% {
        opacity: 0;
    }
}

/* Ensure the line and its content are aligned to the left */
.terminal {
    text-align: left;
    font-family: 'Courier New', Courier, monospace; /* this makes it look more terminal-like, optional */
}

.line {
    display: flex;
    align-items: center;
}

.prompt {
    margin-right: 10px; /* slight space between the prompt and the typed text */
}


</style>
<div class="center">
<img src="{{ site.baseurl }} {% link /images/BurningMUD_ASCII_Logo.png %} " alt="Burning MUD">

<script src="https://cdn.jsdelivr.net/npm/typed.js@2.0.12"></script>

<div class="terminal">
    <div class="line">
        <span id="typed-output"></span>
    </div>
</div>


<div id="terminal" class="terminal"></div>

<script>
var options = {
    strings: ["<h1>Out of the burning ashes</h1>", "<h1>Rose a new life</h1>", "<h1>A new creature</h1>", "<h1>Born into the Burning World</h1>"],
    typeSpeed: 50,
    backSpeed: 0,
    showCursor: true,
    loop: false,
    onStart: function() {
        // Before typing each string, add a new line
        var newLine = document.createElement("div");
        newLine.className = "line";
        newLine.innerHTML = '<span id="typed-' + this.sequence + '"></span>';
        document.querySelector('.terminal').appendChild(newLine);
        this.el = document.querySelector("#typed-" + this.sequence);  // Update the element to type into
    }
};

var typed = new Typed("#typed-0", options);
</script>

