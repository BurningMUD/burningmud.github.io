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

<div class="terminal">
    <div id="typed-output"></div>
</div>

<script>
var options = {
    strings: ["<h1>Out of the burning ashes</h1>", "<h1>Rose a new life</h1>", "<h1>A new creature</h1>", "<h1>Born into the Burning World</h1>"],
    typeSpeed: 50,
    backSpeed: 0,
    showCursor: true,
    loop: false,
    onComplete: function(self) {
        if (self.arrayPos < self.strings.length - 1) { // make sure we don't go beyond our string array
            var newPrompt = document.createElement("div");
            document.querySelector('.terminal').appendChild(newPrompt);
            var newId = "typed-" + new Date().getTime();
            newPrompt.id = newId;
            new Typed("#" + newId, options);
        }
    }
};

var typed = new Typed("#typed-output", options);
</script>