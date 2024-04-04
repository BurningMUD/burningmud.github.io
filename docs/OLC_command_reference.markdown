If you are interested in building a new zone for Burning, please fill
out the web form located at: http://goo.gl/1JXT2a
```
            OLC QUICK COMMAND REFERENCE

ROOMS       MOBS        OBJECTS     ZONE RESETS
-----       -----       -----       -----
radd        madd        oadd        zadd
redit       medit       oedit       zedit
rcopy       mcopy       ocopy       contents
rremove     mremove     oremove     close/open/lock
rformat                             purge
                                    options
                                    equipment
                                    inventory


QUESTS      SHOPS       OTHER COMMANDS
-----       -----       -----
qadd        sadd        mobsnoop vnum/mobname
qedit       sedit       show room vnum (EX: show room 455)
qremove     sremove     show mob vnum
                        show obj vnum
                        goto vnum(room #)/mobname/playername
                        olc vnum(zone #)
                        mpstat vnum(mob #)
```
Questions? Need assistance? Email olc@burningmud.com and we can help.

## ENTER / EXIT OLC EDITING MODE
| COMMAND | ARGUMENT | DESCRIPTION |
|---------|----------|-------------|
|  olc    |zone number| Enter target OLC zone. Use without argument to leave OLC mode. |

## ROOMS
| COMMAND | ARGUMENT(S) | DESCRIPTION |
|---------|-------------|-------------|
| radd    | \<room vnum> | Creates a new room at vnum and opens it for edit. If no vnum provided, use lowest available. |
| redit | \<room vnum> | Edits the room you are standing in, or the room number you specify. |
| rcopy | \<source room vnum> \[target room vnum] | Copies the room to a new vnum. If no target vnum is provided, copies room to lowest available vnum. |
| rremove | \<room vnum> | Deletes room permanently. If vnum left blank it removes the current room. (Restricted to level 108+.) |
| rformat | None | Used to format the current room description to a standard 80 character per line limit. |

## MOBS
| COMMAND | ARGUMENT(S) | DESCRIPTION |
|---------|-------------|-------------|
| madd    | [mob vnum] | Creates a new mobile at vnum and opens it for edit. If vnum not provided, use lowest available. |
| medit   | \<mob vnum> | Edit target mobile. Cannot use keywords, only vnums, since editing mobile globally not per instance in zone. |
| mcopy   | \<mob vnum> \[new mob vnum] | Copies mobile to new vnum, including mobprogs. If second argument left blank, uses lowest available vnum. |
| mremove | \<mob vnum> | Deletes mob permanently. |

## OBJECTS
| COMMAND | ARGUMENT(S) | DESCRIPTION |
|---------|-------------|-------------|
| oadd    | \[obj vnum] | Creates a new object at vnum and opens it for edit. If vnum not provided, uses lowest available vnum. |
| oedit   | \<obj vnum>  | Edit target object.|
| ocopy   | \<source obj vnum> \[target obj vnum] | Copies object to the target vnum. If vnum not provided, use lowest available vnum. |
| oremove | \<obj vnum> | Deletes object permanently. |


## QUESTS
| COMMAND | ARGUMENT(S) | DESCRIPTION |
|---------|-------------|-------------|
| qadd    | \[quest vnum] | Creates a new quest at vnum. Without argument, uses lowest available vnum. |
| qedit   | \<quest vnum> | Edit a quest. |
| qremove | \<quest vnum> | Delete a quest permanently. |

## Zone Reset Commands
| COMMAND | ARGUMENT(S) | DESCRIPTION |
|---------|-------------|-------------|
| equipment | \<mobile keyword> | Edit the worn equipment of a mobile in the room. |
| inventory | \<mobile keyword> | Edit the inventory of a mobile in the room. |
| contains | \<container keyword> | Edit the contents of a container in the room. |
| zadd | \<mobile|object> | Zone Add. Remove resets for mobile or object in the room. |
| purge | \<mobile|object> | Remove resets for a mobile or object in the room. |

## Zone Configuration Options
| COMMAND | ARGUMENT(S) | DESCRIPTION |
|---------|-------------|-------------|
| options | None | Set default templates for rooms and mobs in your zone. |
| zedit | None | Set Zone information such as Name, Author, Description, Level Limits, Continent. |

## NPC Shops
| COMMAND | ARGUMENT(S) | DESCRIPTION |
|---------|-------------|-------------|
| sadd | \[shop vnum] | Create a new shop at target vnum. With no argument, uses lowest available vnum. |
| sedit | <shop vnum> | Edit shop contents. |
| sremove | <shop vnum> | Delete a shop permanently. |