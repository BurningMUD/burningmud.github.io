---
layout: default
title: Maps
---
## Graphical Maps
### Continents

* [Ohran](../images/BurningMUD_Orhan.jpg)<br>
* [Ashinara](../images/BurningMUD_Ashinara.jpg)

## Karandras Home Town Map
Karandras is the default starting point for all players, and remains the most popular city in the game and acts as a central hub for grouping up. The maps here are from the in-game map, which is given to all new characters upon creation. If you need help navigating or have any questions, the gossip channel is a good place to ask other players for some advice, or just contact an immortal directly in-game, as the immortals are here to help.
* [Karandras - Side A](../images/karandras_map_side_a.png)
* [Karandras - Side B](../images/karandras_map_side_b.png)

## Text Maps
A cartographer in each Temple City such as Karandras or Sundhaven can sell you maps for the city itself and the surrounding areas. Make sure to visit them on your travels! A Temple City is any city that contains a temple which may be used as a starting point when you login to the game or after you die. Learn more about [Temple Cities](../help.markdown).

Check [Player Sites](../player_sites.markdown) for extensive text maps created by the players.

* * *

<table>
  <thead>
    <tr>
      <th>Text Maps</th>
    </tr>
  </thead>
  <tbody>
    {% for file in site.static_files %}
      {% if file.path contains '/maps/files/' %}
        {% assign base_name = file.name | remove: file.extname %}
        {% assign display_name = base_name | replace: '_', ' ' %}
        <tr>
          <td><a href="{{ site.baseurl }}{{ file.path }}">{{ display_name | capitalize }}</a></td>
        </tr>
      {% endif %}
    {% endfor %}
  </tbody>
</table>