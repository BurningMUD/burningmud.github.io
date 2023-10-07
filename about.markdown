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

<div class="description">
  <p>{{ site.data.about_topics.description.content | newline_to_br }}</p>
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
