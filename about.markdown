---
layout: default
title: About
---
<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
.collapsible {
  cursor: pointer;
  padding: 18px;
  width: 100%;
  border: none;
  text-align: left;
  outline: none;
  font-size: 15px;
}
.active, .collapsible:hover {
  background-color: #555;
}
.collapsible:after {
  content: '\002B';
  font-weight: bold;
  float: right;
  margin-left: 5px;
}
.active:after {
  content: "\2212";
}
.content {
  padding: 0 18px;
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.2s ease-out;
  }
</style>
</head>
<body>
<button class="collapsible">History</button>
<div class="content">
    <p>Burning MUD was opened in its current form by Lorgalis, Alxar and Andraax, after an extended downtime from the first iteration of Burning MUD. Lorgalis had played Burning MUD since around 1990, and the game shut down around 1994. After entirely rebuilding the game, it was reopened publicly on the first of January, 1996.</p>
    <p>Burning MUD is a heavily modified Diku codebase with a mostly original medieval fantasy world that brings a unique flavor to the genre of text-based MMO games. Burning contains a massive planet spanning two continents separated by a deep ocean, and lurking beneath the bustling surface of the planet's crust lies an extensive expanse of procedurally generated underground caverns, called the Well.</p>
    <p> The Well, an expansive underground cave system, leading 20 levels deep with thousands of rooms, reaveals countless mythical creatures and deadly environmental traps as one ventures deeper underground. Each day, the caverns are reshaped by these environmental forces such as lava flows, bringing surprises and unending threats to the intrepid adventurers who dare to explore the perilous depths. But risk is not without reward, for one will find that the creatures are imbued with the magic of these baffling caverns, leaving behind fragments of elemental energy that grant unimaginable powers of an eternal and ancient race.</p>
</div>

<button class="collapsible">Multiclassing</button>
<div class="content">
    <p>Burning MUD has a unique multi-classing system where you select a second class after gaining mastery over the first class. Your character becomes a mix of the two classes, allowing interesting combinations of powerful abilities. Pick opposites like the Mage/Fighter to have a broad range of abilities, or narrow your focus instead and choose Mage/Mage to gain highly specialized spells and skills. There are over 64 different combinations, including classics such as the Fighter, Priest, Mage, and Rogue, as well as more exotic options Warlock, Nightblade, Animist, and Templar. Nearly any combination of two classes is possible, while the first class will weigh more heavily in defining your character.</p>
</div>

<script>
var coll = document.getElementsByClassName("collapsible");
var i;

for (i = 0; i < coll.length; i++) {
  coll[i].addEventListener("click", function() {
    this.classList.toggle("active");
    var content = this.nextElementSibling;
    if (content.style.maxHeight){
      content.style.maxHeight = null;
    } else {
      content.style.maxHeight = content.scrollHeight + "px";
    } 
  });
}
</script>

</body>