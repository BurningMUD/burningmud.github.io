---
layout: default
title: About
permalink: /about/
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
<p>History</p>
<button class="collapsible">History</button>
<div class="content">
  <p>Burning MUD was opened in its current form by Lorgalis, Alxar and Andraax on the first of January 1996.

Burning MUD is a fast-paced team-oriented PvE hack'n slash online text-based game. Each character class plays a unique role in and outside of combat. Explore the vast world through your own ingenuity, or group up with any number of other players to defeat legendary creatures that hold immensely powerful artifacts and other bountiful treasures. Join or create a mercenary group of like-minded individuals and gain access to a member-built lodge. Share loot and strategize on your next targets in a private members-only channel. Be careful and be warned, adventurer! Combat is furious and deadly, and you will need to think quickly to survive, but the brave shall be rewarded! Burning MUD is not a roleplay oriented game.

Burning MUD is a heavily modified Diku MUD with a mostly original medieval fantasy world that brings a unique flavor to the genre of text-based MMO games. Burning contains a massive planet spanning two continents separated by a deep ocean, and lurking beneath the bustling surface of the planet's crust lies an extensive expanse of procedurally generated underground caverns, revealing countless mythical creatures and deadly environmental traps as one ventures deeper underground. Each day, the caverns are reshaped by these environmental forces such as lava flows, bringing surprise and unending threats to the intrepid adventurers who dare to explore the perilous depths. But risk is not without reward, for one will find that the creatures are imbued with the magic of these baffling caverns, leaving behind fragments of elemental energy that grant unimaginable powers of an eternal and ancient race.

Up for over 20 years with one single continuous world, and all characters saved forever, come settle in for awhile and make yourself at home! Stop in for a chat, and stick around for the fun! We look forward to seeing you there. Our staff is always available to answer questions, and can be reached with a "tell" in-game anytime, or just "pray" at the temple altar where all new players start the game. If you would like to request help outside of the game, or for general inquiries, concerns, thoughts about mud-life, please email us at support@burningmud.com.

Burning MUD is a 100% free game. There is no cost to join, no subscription fees, and no in-game purchases. Donations are not accepted. The Burning MUD staff is committed to fair play.</p>
</div>

<p>Features</p>
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
</html>