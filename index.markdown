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

<div id="typed-output"></div>
<script>
    var options = {
        strings: [
            "<h1>Out of the burning ashes</h1>",
            "<h1>Rose a new life</h1>",
            "<h1>A new creature</h1>",
            "<h1>Born into the Burning World</h1>"
        ],
        //... (other options as I previously described)
    };

    var typed = new Typed("#typed-output", options);
</script>