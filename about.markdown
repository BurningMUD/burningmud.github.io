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
  font-weight: bold;
  background-color: #f0e7d5;
}
.active, .collapsible:hover {
  background-color: #CC6633;
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
Burning MUD is a completely free, text-based online multiplayer game. All players login and play together in the same world!

Burning is a cooperative PvE Hack n' Slash MUD, with optional PvP inside special arenas for fun. Play alone or with friends. An extensive channel system allows public and private chats, as well as a Mercenary Group system where you can build a home base for your group of friends that is entirely private.

Group focused and social at the core, with no limit to the size of a group, the nearly immortal creatures require that players band together in large numbers to defeat the greatest threats to the world, but the rewards may far outshine what you can achieve alone in a treacherous landscape. Come have some fun and play casually or dive deep into the depth of ancient medieval castles and caverns.

Burning is not a roleplaying MUD. Chat about whatever you want in-game, as long as it fits within the rules. Everyone is welcome on Burning!

To play the game use one of the various [MUD Clients](mud_clients.markdown) available, at your preference.

If you enjoy playing Burning, you can vote for us on a few MUD listing sites.

[Vote for Burning MUD](/vote.markdown)

{% from description in site.data.about_topics %}
  <div class="description">
  <p>{{ description.content | newline_to_br }}</p>
  </div>

{% for topic in site.data.about_topics %}
  <button class="collapsible">{{ topic.title }}</button>
  <div class="content">
    <p>{{ topic.content | newline_to_br }}</p>
  </div>
{% endfor %}

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
