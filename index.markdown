---
layout: default
---
<style>
h1 {
    color: darkorange;
}

.terminal {
    background-color: black;
    color: limegreen;
    padding: 10px;
    max-width: 600px;
    border-radius: 5px;
    font-family: monospace;
    font-size: 16px;
}

.terminal-prompt {
    display: inline-block;
    color: white;
    vertical-align: top;
}

#typed-output, #typed {
    display: inline-block;
}
</style>
<div class="center">
<img src="{{ site.baseurl }} {% link /images/BurningMUD_ASCII_Logo.png %} " alt="Burning MUD">

<script src="https://cdn.jsdelivr.net/npm/typed.js@2.0.12"></script>
<div class="terminal">
    <div>
        <span class="terminal-prompt">$</span> <span id="typed"></span>
    </div>
</div>


<script>
var options = {
    strings: ["<h1>Out of the burning ashes</h1>", "<h1>Rose a new life</h1>", "<h1>A new creature</h1>", "<h1>Born into the Burning World</h1>"],
    typeSpeed: 50,
    showCursor: true,
    loop: false,
    onComplete: function() {
        document.querySelector('.terminal').innerHTML += '<div><span class="terminal-prompt">$</span> <span id="typed' + new Date().getTime() + '"></span></div>';
        this.strings.push("");
        this.start();
    }
};

var typed = new Typed("#typed", options);

</script>