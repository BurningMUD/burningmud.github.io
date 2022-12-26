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
  background-color: #FF6633;
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

<button class="collapsible">What is a MUD?</button>
<div class="content">
  <p>A MUD is a Multi-User Dungeon, as it was originally coined. It is generally considered an open-world online game with other players that is text-based, or an MMO. A MUD is really just a text MMO? Yes, and many players are already familiar with this term, although when MUDs released, this was not yet a term. The MMO genre started its life in the form of MUDs, and there were very many MUDs based on open source codebasese like Diku, Smaug, RoM, CircleMUD, and many others.</p>
</div>

<button class="collapsible">Why should I play a MUD?</button>
<div class="content">
  <p>We all like to have a game that we can play anytime, and not worry that it might be gone tomorrow or bought by a larger company and totally changed out from under us. It's nice to not have a paid subscription fee. It's nice to know that regardless of how long it has been since you played, your characters are still saved and waiting for you.</p>
  <p>One might feel that a text-only game has many weaknesses when compared to a modern MMO or action game, but some people say the book is always better than the movie. Graphics can help visualize your environment in a fun and meaninful ways, and 3D environments and worlds provide interesting emergent behaviors that add complexity to even simple systems, but the strengths of modern MMOs can also expose their weaknesses in turn. Displaying 3D graphics can consume a lot of computing power, and this limits the scope, scale, performance and fidelity of any graphical game, which in the long run, can affect the longevity of your game as it ages and loses the technical edge that it had upon release.</p>
  <p>Problems that affect longevity of MMOs, can be issues like:</p>
  <p> * Costs associated with architecting and hosting, which trickle down to monthly subscriptions or other fees for players. Once this money stops rolling in, it's likely the game will shut down. MUDs are cheap to host, and building content is as simple as writing a paragraph.</p>
  <p> * "Sharding" required with most graphical MMOs ends up splitting the playerbase into small chunks in order to avoid lag. On a MUD, everyone exists and plays together in the same world.</p>
  <p> * New content is difficult, costly and time consuming to create. To create content on a MUD you just need to use your imagination, and any computer will work.</p>
  <p> * Graphics age and become outdated. MUDs only limitation graphically is your imagination, and they never age visually.</p>
</div>

<button class="collapsible">Why should I play Burning MUD?</button>
<div class="content">
<p>Burning is a unuiqely fast-paced cooperative action game. It might sound like an oxymoron to say that a text game is fast-paced, but combat can be intense and satisfying in Burning, and split second decisions can mean life or death!</p>
</div>

<button class="collapsible">Features</button>
<div class="content">
    <p>Burning MUD has a unique multi-classing system where you select a second class after gaining mastery over the first class. Your character becomes a mix of the two classes, allowing interesting combinations of powerful abilities. Pick opposites like the Mage/Fighter to have a broad range of abilities, or narrow your focus instead and choose Mage/Mage to gain highly specialized spells and skills. There are over 64 different combinations, including classics such as the Fighter, Priest, Mage, and Rogue, as well as more exotic options Warlock, Nightblade, Animist, and Templar. Nearly any combination of two classes is possible, while the first class will weigh more heavily in defining your character.</p>
    <p>Burning MUD is a heavily modified Diku codebase with a mostly original medieval fantasy world that brings a unique flavor to the genre of text-based MMO games. Burning contains a massive planet spanning two continents separated by a deep ocean, and lurking beneath the bustling surface of the planet's crust lies an extensive expanse of procedurally generated underground caverns, called the Well.</p>
    <p>The Well, an expansive underground cave system, leading 20 levels deep with thousands of rooms, reaveals countless mythical creatures and deadly environmental traps as one ventures deeper underground. Each day, the caverns are reshaped by these environmental forces such as lava flows, bringing surprises and unending threats to the intrepid adventurers who dare to explore the perilous depths. But risk is not without reward, for one will find that the creatures are imbued with the magic of these baffling caverns, leaving behind fragments of elemental energy that grant unimaginable powers of an eternal and ancient race.</p>
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