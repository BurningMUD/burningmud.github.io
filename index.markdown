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

</style>
<div class="center">
<img src="{{ site.baseurl }} {% link /images/BurningMUD_ASCII_Logo.png %} " alt="Burning MUD">

<script src="https://cdn.jsdelivr.net/npm/typed.js@2.0.12"></script>

<div class="terminal">
    <div class="line">
        <span class="prompt">100(100)H 100(100)M 100(100)V ></span>
        <span id="typed-output"></span>
    </div>
</div>


<script>
var options = {
    strings: ["Out of the burning ashes", "Rose a new life", "A new creature", "Born into the Burning World"],
    typeSpeed: 50,
    backSpeed: 0,
    showCursor: true,
    cursorChar: "",
    loop: false,
    onComplete: function(self) {
        if (self.arrayPos < self.strings.length - 1) {
            var newLine = document.createElement("div");
            newLine.className = 'line';
            var newPrompt = document.createElement("span");
            newPrompt.className = 'prompt';
            newPrompt.innerText = '100(100)H 100(100)M 100(100)V >';
            newLine.appendChild(newPrompt);
            var newSpan = document.createElement("span");
            var newId = "typed-" + new Date().getTime();
            newSpan.id = newId;
            newLine.appendChild(newSpan);
            document.querySelector('.terminal').appendChild(newLine);
            new Typed("#" + newId, options);
        }
    }
};

var typed = new Typed("#typed-output", options);

</script>