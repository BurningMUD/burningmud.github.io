<!doctype html>
<html lang="{{ site.lang | default: "en-US" }}">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <style>
      body {
        overflow-y: visible;
      }
      img {
        max-width: 1000px;
        max-height: 288px;
        width: 100%;
        height: 100%;
      }
    </style>
{% seo %}
    <link rel="stylesheet" href="{{ '/assets/css/style.css?v=' | append: site.github.build_revision | relative_url }}">
    <script src="https://code.jquery.com/jquery-1.12.4.min.js" integrity="sha256-ZosEbRLbNQzLpnKIkEdrPv7lOy9C27hHQ+Xp8a4MxAQ=" crossorigin="anonymous"></script>
    <script src="{{ '/assets/js/respond.js' | relative_url }}"></script>
    <!--[if lt IE 9]>
      <script src="//html5shiv.googlecode.com/svn/trunk/html5.js"></script>
    <![endif]-->
    <!--[if lt IE 8]>
    <link rel="stylesheet" href="{{ '/assets/css/ie.css' | relative_url }}">
    <![endif]-->
    <meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no">
    {% include head-custom.html %}
  </head>
  <body>
      <div id="header">
        <div style="text-align: center;>
          <br>
          <h1>{{ site.title | default: site.github.repository_name }}</h1>
        <br>
        <br>
        <center><img src="{{ site.baseurl }} {% link /images/burning.jpg %} " alt="Burning MUD"></center>
        Obvious Exits: [ <a href="/">Home</a> | <a href="/maps">Maps</a> | <a href="/mud_clients">MUD Clients</a> | <a href="/player_sites">Player Sites</a> | <a href="/about">About</a> | <a href="/documentation">Documentation</a> | <a href="/help">Help</a> ]
      </div><!-- end header -->

    <div class="wrapper">

      <section>

          {{ content }}

      </section>

    </div>
  </body>
</html>
