---
layout: default
title: Mobprogs Document
---
<style>
h1 {
    color: green;
}

h2 {
    color: green;
}
code {
    color: lightgreen;
}
</style>


# MOBprograms
MOBprograms are a way to make your mobiles more interesting. This
basic version has enough to get things going, and should be quite readable and
understandable and more to the point, extendable. The remainder of this document describes MOBprograms and gives a couple trivial examples.

# Table of Contents
- [The Basic Idea](#the-basic-idea)
- [MOBprogram Syntax](#mobprogram-syntax)
- [Trigger Types](#trigger-types)
- [Variables](#variables)
- [Control Flow Syntax](#control-flow-syntax)
- [Operators](#operators)
- [If Checks In Control Flow](#if-checks-in-control-flow)
- [MOBcommands Of Interest](#mobcommands-of-interest)
- [Quick Reference Guide](#quick-reference-guide)
- [Mobprog Usage Complexities](#mobprog-usage-complexities)
- [MOBprogram Example](#mobprogram-example)
- [Regarding CPU Slowdown](#regarding-cpu-slowdown)
- [Miscellaneous Information](#miscellaneous-information)
- [Adding New Triggers](#adding-new-triggers)
- [Associating MOBprograms With A Mobile](#associating-mobprograms-with-a-mobile)
- [MOBprogram Files](#mobprogram-files)
- [Credits](#credits-&-history)

## The Basic Idea
Ever wonder why most muds either seem dead or overcrowded? The answer
is probably partially due to the fact that the mobiles never do anything
but wait to be slaughtered. Unless someone has gone to great lengths
and added many special procedures, most mobiles have no idea you are in
the room with them and rarely listen to what you say. The typical Midgaard
mayor wanders happily along even when the populace pokes him, waves his
City Key about, unlocks his gates, or frenchs his secretary, etc. So a way to
give the mobiles a bit more spirit would be neat. Enter the MOBprograms.

The backbone of the MOBprograms shall be called triggers from this
point on. Essentially, they are procedure calls placed in sneaky places in
the mud code which provide the context for what is going on around the
mobile. So, if something happens in the mobile's room and a trigger is
activated, then a list of commands is sent to the interpreter in the
mobile's name, thus making her/it/him do an appropriate something.

Since knowing the appropriate response for every mobile to every
possible trigger is not easy, this command list shouldnt be a rigid script, but
needs to be somehow unique for the mobile and the situation. However, in
order to know the situation, a mobile needs to know more about the trigger
than if it just happened. So, we have to include some sort of variables
as well to set the context appropriately.

As most Implementors know, most area creators are not versed in
coding, but usually have great ideas. Therefore, whatever system is used needs
to be quite simple. This is not to demean creators in any way. Simply, it is
useless to have a powerful system, if the only person able to write anything
is someone who finds C coding in general to be exciting and non frustrating.
If that is going to be the case, then stick to the special procedures, since
there is no bound to what a complex special procedure can accomplish. Yet,
from experience working on several muds, most admins and Implementors prefer
not to be writing one shot spec_procs to satisfy the needs of their creators.

Thus, the basic idea: let mobiles react to a myriad of mud
events/situations by having them perform a list of commands which can be
tailored to the moment through a simple and unintimidating scheme usable by
any creator.
#### [&#x2191; Back to ToC](#table-of-contents)


## MOBprogram Syntax

The simplest way to describe any syntax is by example, so here goes.
First, define the notation: anything contained in braces {} is required,
anything in brackets [] is optional, anything in quotes "" is a case
insensitive literal, NL refers to a required new-line. The meanings of
the labels used will be described following the syntax diagram.

```
`">" {trigger_type} " " {argument_list} "~" NL
{program_command_1} NL
{program_command_2} NL
{program_command_3} NL
. . .
{program_command_N} NL
"~" NL`

Explanations:
A TRIGGER_TYPE is one of the available triggers.
A PROGRAM_COMMAND can be any legal mud command, or a control flow command.
The ARGUMENT_LIST depends upon the trigger, but it is always parsed into the
system as a character string.

This is an example of ONE MOBProgram block for a mob.
```
#### [&#x2191; Back to ToC](#table-of-contents)

## Trigger Types

Triggers are fairly easy to add, but this basic list should hold for
most needs. Their names, argument list syntaxes, and translation into
more articulate english are given below:

### `in_file_prog <ARGUMENT>`
```
The argument is a single word which is the location of the stored file
as referenced from the running directory (MOBProgs).

NOTE: Dummy trigger. Not valid in any file, only for use in loading
files from the method described above.
```

### `act_prog [p] <ARGUMENT>`
```
The argument is a list of keywords separated by spaces. If the first
word is the character 'p' by itself then the rest of the word list is
considered to be a phrase. The trigger is activated whenver a keyword
(or the phrase) is contained in the act() message. Both the phrase and
keywords are case insensitive.

NOTE: Most general trigger. Applies to almost every event which happens
in the mud. Anytime the function act() is called with a message to be
delivered TO_CHAR,TO_VICT,TO_ROOM,etc. the act can be triggered.
Basically this will trigger on almost everything you'll ever want (and
some things you wont as well).

For example:
MOBprogram: >act_prog p pokes you in the ribs.~

This trigger will only be activated if a mobile receives a message in
which the above five words are found in the exact order and spacing given.
Note that the period is needed because the words must be found on their
own. This eliminates confusion when the keyword is 'hi' and a message
with the word 'this' is being checked. In CircleMud2.20 with these
patches, neither emote nor say can trigger and act_prog, so it can
ONLY be triggered by socials (and possibly by an IMPs echo ;)
```

### `speech_prog [p] <ARGUMENT>`
```
The argument is the same as for an act_prog.

NOTE: This is only triggered when the keyword or phrase is contained
in a message which has been said by a PC in the same room as the mob.
The PC restriction is not necessary, but makes infinite loops between
two talking mobiles impossible. It also makes it impossible for two
NPC's to stand and discuss the weather however.
```

### `rand_prog <NUMBER>`
```
The argument is a number betweeen 1 and 100 inclusive.

NOTE: This trigger is checked at each PULSE_MOBILE and if the argument
is greater than a percentage roll the trigger is activated. This will
happen even if there is no PC in the room with the mob, but there must
be players in the same area.

It is useful to give mobiles a bit of a personality. For instance a
janitor who stops to spit tobacco, or complain about the hours, or
wonder why there are no woman janitors on muds, or a fido which
barks or growls or pees on the curb is much more alive than one
which just sits there scavenging.

This trigger will even be checked when the mobile is fighting, so
can provide some confusion if you don't expect it (for instance an
mpecho about a fido peeing on the curb can happy during a fight or
even while the mobile is lying mortally wounded!)
```

### `fight_prog <NUMBER>`
```
The argument is a percentage like in rand_prog.

NOTE: Useful for giving mobiles combat attitude. It is checked every
PULSE_VIOLENCE when the mobile is fighting. Can be used to cast
spells, curse at the opponent, or whatever. Only the first successful
one will be processed to save time. Also, this means that the mobile
wont get lucky and 1. curse, cast a fireball and 2. spit on the
player, cast another fireball in the same pulse.
```

### `hitprcnt_prog <NUMBER>`
```
The argument is a percentage.

NOTE: Is activated at each PULSE_VIOLENCE when the mobile is fighting.
It checks to see if the hitpoints of the mobile are below the given
percentage. Multiple hitprcnt_progs should be listed in increasing
order of percent since a 40% will always be activated before a 20%
and, only the first successful hitprcnt trigger is performed.
```

### `greet_prog <NUMBER>`
```
Again a percentage argument.

NOTE: Whenever someone enters the room with the mobile, and the mobile
saw the person enter, this is checked. Good for shopkeepers who want
to welcome customers, or for pseudo-aggressive mobiles which need to
discriminate on who they attack.
```

### `all_greet_prog <NUMBER>`
```
Again a percentage argument.

NOTE: Like greet_prog, but it can be triggered even if the mobile didnt
see the arrival (i.e. sneak, invis, etc). Most useful for faking teleport
rooms (if your mobiles can transfer) or for impassable guardians.

**NOTE: neither greet_prog is activated if the mobile is fighting.**
```

### `entry_prog <NUMBER>`
```
Again a percentage argument.

NOTE: The opposite of a greet_prog. Whenever the mobile itself enters
a new room, this can be triggered. Useful for looking around, or
waving or other things that real PCs do when they arrive at a crowded
room. Only the first successful one of these is done so the mobile
doesn’t look stupid by repeating commands resulting from multiple
MOBprograms.
```

### `leave_prog <NUMBER>`
```
Again a percentage argument.

NOTE: Whenever someone leaves a room with the mobile, and the mobile
saw the person leave, this is checked. Good for shopkeepers who want
to wave goodbye to customers, or for pseudo-aggressive mobiles which
need to stop people from leaving etc. If the person leaving the room
is attacked in the trigger, he/she can't leave the room as intended.
```
### `all_leave_prog <NUMBER> ??`
```
Again a percentage argument.

NOTE: This is just like leave_prog, except it will trigger even if
the mobile cannot see the character leaving.
```

### `give_prog <ARGUMENT>`
```
The argument is either the complete name of an object, or the word
'all'. A complete name is like: "sword shiny magic" vs "sword". It
is whatever is on the line of the object section following the VNUM.

NOTE: This is triggered whenever something is given to the mobile.
Best used for quests. Since the first successful trigger is the only
one of this type which is processed, having an "all" argument
give_prog at the end of the MOBprogram list is essentially a default
response.
```

### `bribe_prog <NUMBER>`
```
The argument is any positive integer number.

NOTE: This trigger is activated whenever money is given to the mobile.
If the amount given exceeds the number, then process the commands.
Note again, that an argument of '1' would act as a default response.
If money is given to a mobile with this trigger type, instead of the
cash being added to mob->gold, the mobile is instead given a pile of
coins in the proper amount. In this way, the mobile can drop the
coins or refer to the object by "amount" (short description:"%d gold
coins").

This surely has some drawbacks, but it lets the mobile do something
with the bribe (NOTE: dropping it and getting it turns it into cash).
This can be done sneakily if a NPC-only "at" command exists.
```

### `hour_prog <1-24>`
```
The argument is the clock when the trigger shall activate.

NOTE: When the mudhour strikes X (1-24), this trigger is activated.
```

### `ferry_prog <PERCENT>`
```
The argument is a percentage.

NOTE: This trigger is activated when a ferry reaches its new
destination but before the captain exits the ferry. It is the
captain who will act in this prog, not the vessel!
```

### `page_prog <id> <PERCENT>`
```
<id> is a number to identify the page_prog and percent is the
chance it is activated when triggered by mppage.

NOTE: This trigger is activated when another mobile uses
mppage to trigger it with the same id. See mppage for its
syntax.
```

### `death_prog <NUMBER>`
```
The argument is a percent once again.

NOTE: When the mobile dies, if the random percentage is less than
the argument the mobile performs the MOBprogram commands rather
than the usual death_cry sequence. This is done before the corpse
is made, so the commands can be considered the mobiles last gasp.
It could perhaps destroy the items it was holding, or create some,
or cast a spell on the killer and the room, or even goto a new
location and die there (with a text message, the corpse would seem
to vanish) The position of the mobile is set to STANDING, and so it
can do all the normal commands, without worrying about being DEAD.
However, even if the mobile restores itself to full hitpoints, it
will still die.

This is not a way to immortal mobiles. However, the last thing this
mobile does could be to goto some vacant room, load a fresh version
of itself, drop all its items, force the new mobile to get all the
items and wear them, send the new mobile back to the character who
killed it and force the new mobile to attack that character. Along
with a text message which said the mobile restored itself, this might
be a convincing effect. (Note that your kitten could turn into a dragon
this way too). Of course this assumes that some NPC commands have been
implemented.

In the original code, it was impossible to do the 'restoration' trick
above, however, in this code, it is in fact possible. Try it ;)
```

### `command_word_prog <COMMAND>`
```
This mobprog will trigger on the command specified in <command>

Syntax: command_phrase_prog <command> <args>

This mobprog will trigger on the command specified in <command> if the
argument is the same as specified in <args>.

IE: command_phrase_prog open door~

Note that the first successful bribe_prog, give_prog, hitprcnt_prog,
death_prog, fight_prog, rand_prog and entry_prog is the only one which
is executed. All the successful greet(_all)_progs, speech_progs, and
act_progs will be done. This is the best arrangement we found for
handling situations where you imported several MOBprogram files for a
mobile. If you are going to write lots of little files and piece them
together to create the effect you want, it is advisible to not mix
things together all that much, otherwise you have to pay close attention
to the order in which the programs are added to the link list.

Also, no MOBprograms will be successful when the mobile is charmed (since
it has no self violition, it should act like it has none) to protect
mobiles which are given special powers from being implemented by a player.
One bug we had in early testing was a player who charmed a mobile and then
used its aggressive greet_prog to attack other players.
```
#### [&#x2191; Back to ToC](#table-of-contents)

## Variables

To make things come alive, variables are needed. These are represented in the
MOBprograms by using a dollar sign convention as in the socials. When the mud
command is processed, these variables are expanded into the values shown
below. Usually, it is best to use the short descriptions of mobiles and the
names of players when speaking them, but if you are performing an action to
someone almost always you want the name. The title field for players is an
extra that probably wont often be used. Without further hesitation... the
variables:

```
$i the first of the names of the mobile itself.
$I the short description of the mobile itself.
$n the name of whomever caused the trigger to happen.
$N the name and title of whomever caused the trigger to happen.
$t the name of a secondary character target (i.e A smiles at B)
$T the short description, or name and title of target (NPC vs PC)
$r the name of a random char in the room with the mobile (never == $i)
$R the short description, or name and title of the random char

$j he,she,it based on sex of $i.
$e he,she,it based on sex of $n.
$E he,she,it based on sex of $t.
$J he,she,it based on sex of $r.

$k him,her,it based on sex of $i.
$m him,her,it based on sex of $n.
$M him,her,it based on sex of $t.
$K him,her,it based on sex of $r.

$l his,hers,its based on sex of $i.
$s his,hers,its based on sex of $n.
$S his,hers,its based on sex of $t.
$L his,hers,its based on sex of $r.

$o the first of the names of the primary object (i.e A drops B)
$O the short description of the primary object
$p the first of the names of the secondary object (i.e A puts B in C)
$P the short description of the secondary object

$a a,an based on first character of $o
$A a,an based on first character of $p
```

Also, in if_checks, the accepted variables are the basic ones (i,n,t,r,o,p). If a variable is referenced that doesn’t exist, then the value is simply left blank. (i.e referring to $o when the trigger is: A kisses B)

The only problem with the variables is that the secondary object and the secondary target are passed by act() in the same location. This means that if you reference $t in an A puts B in C situation, the result will probably be a happy mud crash or some weird side effect, especially if $t is used in an if_check (i.e. if isnpc($t) in the above situation) The basic fix for this is to change everyone who calls the act() procedure to specify a secondary object and a secondary character. But that is a fairly comprehensive trivial twiddle, so we left it the way it is so that, you aren’t forced to make all those twiddles to use the MOBprograms.
#### [&#x2191; Back to ToC](#table-of-contents)

## Control Flow Syntax

In place of any legal mud command in a MOBprogram, one can substitute a flow of control command. Here is the syntax for a flow of control command.

```
"if" " " {if_check_1} "(" {argument} ")" [ {operator} {value} ] NL
[ "or" " " {if_check_2} "(" {argument} ")" [ {operator} {value} ] NL ]
. . .
[ "or" " " {if_check_N} "(" {argument} ")" [ {operator} {value} ] NL ]

[ {program_command_1} NL ]
[ {program_command_2} NL ]
. . .
[ "break" NL ]
. . .
[ {program_command_N} NL ]

[ "else" NL ]

[ {program_command_1} NL ]
[ {program_command_2} NL ]
. . .
[ "break" NL ]
. . .
[ {program_command_N} NL ]

"endif" NL
```

Basically, it is: an 'if' line, followed by zero or more 'or' lines, followed by zero or more legal mud commands, which may contain a 'break' line, possibly followed by an 'else' line , followed by zero or more legal mud commands, which may contain a 'break' line, followed by an 'endif' line.

The only new syntax labels are all in the IF line:

Explanations:
An IF_CHECK is a string which describes under what context to compare things. The ARGUMENT is the reference point from which the LHS of an expression comes. The OPERATOR indicates how the LHS and RHS are going to be compared. The VALUE is the RHS of the expression to be compared by the operator.

The BREAK command bails out of the entire MOBprogram regardless of the level if nesting.

If that looks confusing, skip to the end of the document and review the Example. Hopefully that should clear things, otherwise you'll probably have to give us a mail since examples are the best way we know to explain syntax.
#### [&#x2191; Back to ToC](#table-of-contents)

## Operators

Most of the basic numeric operators are legal and perform the same function as in C. The string operators are a bit more confusing. There are negative versions of some of the operators. These are not strictly needed, since the if/else construct of Control Flow commands can handle either case.

| Numeric Operators | Description |
|-------------------|-------------|
| == | equal to |
| != | not equal to |
| > | greater than |
| < | less than |
| >= | greater than or equal to |
| <= | less than or equal to |
| & | and |
| \| | or |

| String Operators  | Description |
|-------------------|-------------|
| == | equal to |
| != | not equal to |
| / | is contained in |
| !/ | is not contained in |

NOTE: For strings, == and != check for exact match between the two strings and the other two, / and !/ check to see if the second string is contained in the first one. This is so things like: if name($n) / guard will respond true to "cityguard" "guard" "guardian" etc. Using == on a name implies that you are matching the complete name "cityguard guard" or whatever. The string operators are case SENSITIVE.
#### [&#x2191; Back to ToC](#table-of-contents)

## If Checks In Control Flow

The provided list of if_checks and their arguments are below. They should all be fairly obvious in what they do, but some of the more obtuse deserve a slight explanation. Any '==' operator can be replaced with any of the available ones described above. The argument ($*) refers to any of the variables which make sense for that if_check (i.e. for an if_check which is referencing a person the only valid variables would be $i, $n, $t or $r) A value type of string is a sequence of characters. It does not need to be included in quotes or anything like that (i.e. name($n)== orc large brown)

| Command | Description |
|---------|-------------|
| `rand(num)` | Is random percentage less than or equal to num |
| `isnpc($*)` | Is $* an NPC |
| `ispc($*)` | Is $* a PC |
| `isgood($*)` | Does $* have a good alignment (also works for isevil and isneutral) |
| `isfight($*)` | Is $* fighting |
| `ishunt($*)` | Is $* hunting |
| `isimmort($*)` | Is the level of $* greater than max_mortal |
| `ischarmed($*)` | Is $* affected by charm |
| `isfollow($*)` | Is $* a follower with their master in the room |
| `isaffected($*) & integer` | Is ($*->affected_by & integer) true (person only) |
| `isleader($*)` | Is $* the leader or soloing (no master) |
| `isgrouped($*)` | Is $* grouped (regardless of where group is) |
| `inquest($*) == <num>` | Is $* in quest <num> |
| `inmerc($*) == <num>` | Is $* in team <num> |
| `exit(north\|east\|south\|west\|up\|down) == integer` | Is there exit to room integer |
| `hitprcnt($*) == percent` | Is the hit/max_hit of $* equal to percent |
| `inroom($*) == [integer \| $i \| $n \| $t \| $r]` | Is the room of $* equal to integer or other person. (person only) |
| `sex($*) == integer` | Is the sex of $* equal to integer |
| `position ($*) == integer` | Is the position of $* equal to integer (1 dead, 2 morted, 3 incap, 4 stunned, 5 sleep, 6 rest, 7 sitting, 8 fighting, 9 standing, 10 flying) |
| `level($*) == integer` | Is the level of $* equal to integer |
| `class($*) == integer` | Is the class of $* equal to integer (1 mage, 2 priest, 3 rogue, 4 fighter, 5 warlock, 6 animist, 7 nightblade, 8 templar) |
| `goldamt($*) == integer` | Does $* have a gold total equal to integer |
| `objtype($*) == integer` | Is the type of $* equal to integer (armor, boat, etc) |
| `objval#($*) == integer` | Is $*->value[#] equal to integer (# from 0-3) |
| `number($*) == integer` | Is the vnum of $* equal to integer |
| `name($*) == string` | Is the name of $* equal to string |
| `iswearing($*) == integer` | Is $* wearing item equal to integer |
| `str($*) == integer` | Is the strength of $* equal to integer |
| `int($*) == integer` | Is the intelligence of $* equal to integer |
| `wis($*) == integer` | Is the wisdom of $* equal to integer |
| `dex($*) == integer` | Is the dexterity of $* equal to integer |
| `con($*) == integer` | Is the constitution of $* equal to integer |

#### [&#x2191; Back to ToC](#table-of-contents)

## MOBCommands Of Interest

These are fairly basic things, most of them are wiz commands which have been changed to allow for mobiles to perform the commands. If you have the problem of immortals abusing these powers on your mud either ditch the immortals, or add a check in all of them to only let NPC's with null descriptors do the commands. (However, you lose a little debugging help that way). MERC 2.2 has provided a little security feature against this but it is by no means comprehensive. Please check yourself if you are concerned.

Here are the basic MOBcommands that we found to be enticing:

### `MPSTAT <mobile>`
```
Shows the MOBprograms which are set on the mob of the given name or vnum
and some basic stats for the mobile
```

### `MPJUNK <object>`
```
Destroys the object refered to in the mobiles inventory. It prints no message
to the world and you can do things like junk all.bread or junk all. This
is nice for having janitor mobiles clean out their inventory if they are
carrying too much (have a MOBprogram trigger on the 'full inventory')
```

### `MPECHO <text_string> / MPECHOAT <target> <text_string> / MPECHOAROUND <target> <text_string>` / `MPASOUND <text_string>`

```
Prints a text string.

MPECHO - Everyone in the room sees this message.
MPECHOAT - Only the target sees this message.
MPECHOAROUND - The target DOES NOT see this message, but everyone else in
the room does.
MPASOUND - Only individuals in adjacent rooms will see this message.

Builders may use this to craft custom messages for all points of view
during a custom action, such as a special attack in combat, or any message
that might "look" different from different perspectives, such as the below
messages involving being swallowed by a giant slime. At the end, if it
successfully "absorbs" a player, it will heal itself with a Miracle spell.
We don't need to add an mpasound message for when it absorbs the player,
as adjacent rooms already see death cry messages.

if rand(50)
  @emote chirps!
  @mpasound You hear something chirping nearby.
  @mpecho $I suddenly EXPANDS, attempting to absorb!
  if rand(10)
    @mpechoat $n You weren't fast enough to get away!
    @mpechoaround $n You jump back just in time.
    @mpechoat $n $I absorbs you into itself. Your body is dissolved instantly by the boiling acid.
    @mpechoaround $n $n SCREAMS as $I absorbs $m into itself! $I looks healthier.
    @mpinfo $N was violently absorbed and dissolved by $n.
    @mpdamage $n 5000d500+10000 constitution 3 10
    @mpcast 'miracle' self
  break
  endif
  @mpecho You jump back just in time.
break
endif

To extend what these commands are capable of, combine it with MPAT, such as:

MPAT $r MPECHO The wind rustles the leaves at your feet.

This message will reach the player regardless of what room or zone they are in.
```

### `MPMLOAD <vnum> / MPOLOAD <vnum>`
```
Loads the obj/mobile into the inven/room of the mobile. Even if the item
is non-takable, the mobile will receive it in the inventory. This lets a
mobile distribute a quest item or load a key or something.
```


### `MPKILL <victim>`
```
Lets a mobile kill a player without having to murder and be fifth level.
Lots of MOBprograms end up with mpkill $n commands floating around. It
works on both mobiles and players.
```


### `MPPURGE [argument]`
```
Destroys the argument from the room of the mobile. Without an argument the
result is the cleansing of all NPC's and items from the room with the
exception of the mobile itself. However, mppurge $i will indeed purge the
mobile, but it MUST be the last command the mobile tries to do, otherwise
the mud cant reference the acting mobile trying to do the commands and bad
things happen.
```


### `MPGOTO <dest>`
```
Moves the mobile to the room or mobile or object requested. It makes no
message of its departure or of its entrance, so these must be supplied with
mpecho commands if they are desired.
```


###  `MPAT <dest> <command>`
```
Perfoms the command at the designated location. Very useful for doing magic
slight of hand tricks that leave players dumbfounded.. such as metamorphing
mobiles, or guard summoning, or corpse vanishing.
```


### `MPTRANSFER <victim> [dest]`
```
Sends the victim to the destination or to the room of the mobile as a default.
if the victim is "all" then all the characters in the room of the mobile are
transfered to the destination. Good for starting quests or things like that.
There is no message given to the player that it has been transfered and the
player doesnt do a look at the new room unless the mob forces them to.
Immortals cannot be tranfered.
```


### `MPFORCE <victim> <command>`
```
Forces the victim to do the designated command. The victim is not told that
they are forced, they just do the command so usually some mpecho message is
nice. You can force players to remove belongings and give them to you, etc.
The player sees the normal command messages (such as removing the item and
giving it away in the above example) Again, if the victim is "all" then
everyone in the mobiles room does the command. This cannot be used on immortals.
```

Here are the extra Burning mobile commands:

### `MPPAUSE <how many ticks to pause>`
```
Burning has added the fourth dimension 'time' to the original mobprog code.
As a result of this, on Burning each mob command is performed once per mob
tick, whereas on standard mobprog muds all commands are performed instantly.
If you want the mobile to pause while performing its commands, you can use
the mppause command to specify how many mob-ticks the mobile should pause
before performing the next command in the list.
```


### `MPHOUR <hour to wait for>`
```
Burning has added the fourth dimension 'time' to the original mobprog code.
As a result of this, on Burning each mob command is performed once per mob
tick, whereas on standard mobprog muds all commands are performed instantly.
If you want the mobile to wait for a certain hour before resuming the
commands, you can use mphour with the hour to wait for.
```


### `MPDAY <day to wait for>`
```
This command works like mphour with the difference that the mobile waits for
a certain day before resuming the commands.
```


### `MPFLUSH`
```
This command is very useful when writing complex mobprogs that allows the mob
to change its course of action. When executing mpflush, the mobile throws
away any pending commands. You can then add new commands that will be
executed next. It is perfectly ok to call mpflush on a mobile that does not
have any pending commands just to make sure it doesn't.
```

### `MPWALK <virtual room number of desired destination>`
```
This very powerful command is used to have the mobile walking around in the
mud without any prior knowledge of its whereabouts or the path to a specific
room. By simply adding a mpwalk command followed by a virtual room number,
the mobile will try to walk to that room always choosing the shortest path.
The next command will not be executed until the mobile has reached its
desired destination.
```


### `MPSTOP`
```
This command clears the hunt list, i.e. the mob will no longer hunt for
a certain room or player.
```

### `MPZIP`
```

Do nothing. This command is use to simulate the NOT command, e.g.:
if(ishunt($i))
mpzip
else
sing
endif
```


### `MPWAIT <victim> <duration>`
```
Causes the victim of the mpwait command to suffer a waitstate before any further
action is carried out. Duration is in combat pulses and is of the xDy+z variety.
```

### `MPPAGE <room number> <mobile name | virtual number> <id>`

```
room number can be:
    0 - activate mobs in this room only.
    -1 - activate mobs in any room (the world)
    <room> - activate mobs in <room> only.
    mobile name | num - x.guard, guard, or virtual number.
    id - an integer matching the page_prog id.

If the second argument, mobile name or number, is a number then all mobiles with
that virtual number in the 'room' are paged. If a mobile has a page_prog with an
<id> that matches the mppage, that mobprog is activated.

Examples:
mppage -1 3067 1 - activate all mobs with vnum 3067 in the world that have a
page_prog with id 1.
mppage 0 3067 1 - activate all mobs in this room only with vnum3067 and id 1.
mppage 0 2.guard 1 - only activate 2.guard in this room if he has id 1.
mppage 3046 guard 2 - activate the first guard in room 3046 with id 2.
```


### `@ <original command>`
```
Sometimes one wants the mobile to perform commands faster than one command per
tick. This is possible by adding the @ character in front of the normal command.
When using the @ character in front of a command, the next one will be performed
instantly (just like on the original mobprog).

Example:
@smile
say Hi, welcome to my humble place!

Will cause the mobile to smile followed by an instant 'say'. You can call any
command after the @ sign, including mobprog commands.
```



### `MPWEAR <victim> <subcmd> <object> ...`
```
Victim will switch equipment, old equipment gets autoremoved.
(except NOREMOVE items)

Example:
@mpwear $n wield sword
or @mpwear $n wear helm
or @mpwear $n wear helm head
```


### `MPBOND <victim> <object>`
```
Set unique_id number for item with bond flag.

Example:

@mpbond $n sword

- Object gets victim's unique_id only if mob can_see object in victim's inventory.
```

### `MPADDREP <victim> <value> <group| > <silent| >`
```

Victim gets <value> rep points. Argument 'group' affects all group members; silent
is without info.

Example:
@mpaddrep $n 20
- Victim gets 20 rep points.
@mpaddrep $n 20 group
- All members in victim’s group get 20 rep points.

```
### `MPCAST <spell> <victim>`
```
Cast any spell in the game on target.z
```

### `MPDAMAGE <target OR target-type> <damdice> [damtype] [damflags] [savemod]`
```
This is a mobprog command used to cause damage to a player.

It takes at least 2 arguments, with an optional 3 more.

Usage:
mpdamage <target OR target-type> <damdice> [damtype] [damflags] [savemod]

Argument description:
<target OR target-type> is either the name of a player/mob ($n usually) or one of
the following: "all" will damage everyone in room, "allm" will damage all mobiles
in room, and "allp" will damage all players.

<damdice> is a standard damage dice format, such as 5d200.

[damtype] is optional and is any standard MUD damage type, such as crush, slash,
spell, etc.

[damflags] is optional and is a bitvector field, which can take the following
flags: Negate Sanctuary (1), No Maxdam (2). As it is a bitvector, to get multiple
flags, you add the number of each flag together. So a mpdamage command which has
negate sanctuary and no max damage would have a damflag value of 3.

[savemod] is the modifier to saving throws that the target receives.

Example:
mpdamage allp 5d200 spell 1 0

This would damage all players in the room with a dice of 5d200, the damage would
negate sanctuary, and be of a 'spell' damage type.
```

### `MPINFO <message> - send a custom info kill message`

```
note: mpinfo only works in combination with mpdamage, and must be placed BEFORE
the mpdamage command.
```

### `MPEXIT <north|east|south|west|up|down> <target room> [flags] [exit descr]`
```
Where <target room> is the target room's vnum, [flags] are optional exit flags,
and [exit descr] is an optional exit description.
    
Example: MPEXIT north 50001 SECRET ANTI-GOOD This is a secret anti-good exit.
Note: Previous exit will be replaced. Use <target room> -1 to remove exit.
```


### `MPAFFECT <target> <spell> <duration> - add spell affect to target mob/player`
```
Can remove spell effects by setting duration to 0.
```
### `MPHEAL <target> XdY+Z - heals target for XdY+Z hitpoints`
```
Heal any target for any amount. Is not affected by saving throws or any other
system.
```

### `MPVAR <variable> <integer(0-100)>`
```
In the game, each mobile can use two special variables, $1 and $2, that
initialize at 0 but can be changed to anything between 0 and 100. The
builder changes these numbers with a command called MPVAR, like
"MPVAR $1 0" to set $1 to 0, or with MPADD to increment or decrement in the
amount desired, such as "MPADD $2 15", which adds 15 to the current value.

These numbers help builders make the mobs act in different ways
based on conditions they set, like "if var($2) >= 50", to control how a mob
reacts or behaves. Essentially, this gives mobs a way to "remember" up to 101
different situations or actions.

A mobile for instance, could count the number of players entering his zone,
and warn other mobiles accordingly. If the number grows over 10 (that he is
aware of), page the boss of the zone to prepare himself, which triggers the
king to call for his guards. If the mob, a gatekeep perhaps, checks again
and there are no players in his vicinity for a period of time, the extra
guards return to their normal positions after the king is notified that the
threat level has reduced.

This system introduces a form of memory for mobs, allowing them to keep track
of past events and adding more depth to the game. It's a tool for builders to
craft more complex and interactive game experiences
```

### `MPADD <variable> <+/- integer>`
```
Add or subtract, from an VAR variable. For use with MPVAR command. Variable
range is limited to 0-100.
```
#### [&#x2191; Back to ToC](#table-of-contents)

## Quick Reference Guide
```
trigger argument and what must happen to activate trigger
-----------------------------------------------------------------------------
act_prog       WORDLIST or P WORD_PHRASE to match from act() to mobile
bribe_prog     INTEGER amount of minimum gold amount given to mobile
entry_prog     PERCENT chance to check when mobile moves to a new room
give_prog      FULL OBJECT NAME or ALL to match when obj given to mobile
greet_prog     PERCENT chance to check if visible char enters mobile's room
all_greet_prog PERCENT chance to check when any char enters mobile's room
fight_prog     PERCENT chance to check at fight_pulse if mobile is fighting
hitprcnt_prog  PERCENT lower than mobiles hit/max_hit if mobile is fighting
death_prog     PERCENT chance to check after mobile has been slain
rand_prog      PERCENT chance to check whenever a PC is in the mobiles zone
speech_prog    WORDLIST or P WORD_PHRASE to match in dialogue to mobile

variable            mobile  actor  victim  random  object  2nd_object
-----------------------------------------------------------------------------
name                  $i      $n     $t      $r      $o      $p
shrt_desc/title       $I      $N     $T      $R      $O      $P
he/she/it             $j      $e     $E      $J      --      -- 
him/her/it            $l      $m     $M      $L      --      --
his/hers/its          $k      $s     $S      $K      --      --
a/an                  --      --     --      --      $a      $A

'$'symbol=$$


ifcheck & argument          meaning
-----------------------------------------------------------------------------
rand(num)                   Is a random percentage less than or equal to num
isnpc($*)                   Is $* an NPC
ispc($*)                    Is $* a PC
isgood($*)                  Does $* have a good alignment
isfight($*)                 Is $* fighting
ishunt($*)                  Is $* hunting
isimmort($*)                Is the level of $* greater than max_mortal
ischarmed($*)               Is $* affected by charm
isfollow($*)                Is $* a follower with their master in the room
isleader($*)                Is $* a leader with followers in the room?
isaffected($*) == integer   Is ($*->affected_by integer) true (person only)
iswearing($*) == integer    Is $* equal to object vnum.
hitprcnt($*) == percent     Is the hit/max_hit of $* equal to percent
inroom($*) == [integer | $i | $n | $t | $r] Is the room of $* equal to integer
    or other person. (person only)
sex($*) == integer          Is the sex of $* equal to integer
position($*) == integer     Is the position of $* equal to integer
level($*) == integer        Is the level of $* equal to integer
class($*) == integer        Is the class of $* equal to integer
goldamt($*) == integer      Does $* have a gold total equal to integer
objtype($*) == integer      Is the type of $* equal to integer (armor,boat,etc)
objval#($*) == integer      Is $*->value[#] equal to integer (# from 0-3)
number($*) == integer       Is the vnum of $* equal to integer
name($*) == string          Is the name of $* equal to string
var($*) == integer          Is the number of $* ($1 or $2) equal to integer.

MOBcommand argument_list MOBcommand argument_list
-----------------------------------------------------------------------------
MPSTAT <mobile>
MPJUNK <object>
MPECHO <text_string>
MPECHOAT <victim> <text_string>
MPECHOAROUND <victim> <text_string>
MPASOUND <text_string>
MPMLOAD <mobile
MPOLOAD <object> <level>
MPKILL <victim>
MPPURGE [argument]
MPGOTO <dest>
MPAT <dest> <command>
MPTRANSFER <dest> [location]
MPFORCE <victim> <command>

+++ Additional Burning mobprog commands +++

MPPAUSE <ticks>
MPWALK <virtual room number> - let mobile walk to <room>.
MPHOUR <hours>  - let mobile pause until the hour is <hours>.
MPDAY <days> - let mobile pause until the day is <days>.
MPFLUSH - cancel all buffered mob commands.
MPSTOP - stop all hunting (including pending mpwalk commands).
MPZIP - do nothing.
MPWAIT <victim> <duration> - give victim <duration> rounds of waitstate.
MPPAGE <room> <victim> <id> - trigger another mobile page_trigger with <id>.
MPWEAR <victim> <subcmd> <object> - wear an item.
MPBOND <victim> <object> - bond an item to a victim.
MPADDREP <victim> <value> <group| > <silent| > - add reputation to victim.
MPCAST 'spellname' <victim> - cast a spell 'spellname' on <victim>.
MPQUEST <victim> <quest num> - make <victim> join quest <quest num>.
MPCOMPQUEST <victim> - make victim complete current quest.
MPDAMAGE XdY+Z <save_type> <dam_flags=1|2|4> <save modifier>
MPINFO <message> - send a custom info kill message
 note: mpinfo only works in combination with mpdamage
MPEXIT <north|east|south|west|up|down> <target room> [flags] [exit descr]
where <target room> is the target room's vnum, [flags] are optional exit
 flags, and [exit descr] is an optional exit description.
 Example: MPEXIT north 50001 SECRET ANTI-GOOD This is a secret anti-good exit.
 Note: Previous exit will be replaced. Use <target room> -1 to remove exit.
MPAFFECT <target> <spell> <duration> - add a spell affect on target
MPHEAL <target> XdY+Z - heals target for XdY+Z hitpoints
MPVAR <variable> <integer> - Range from 0-100. Variables $1 and $2 avaialble to set.
MPADD <varable> <-/+ int> - Add or subtract desired amount from variable.
```

EXAMPLE Referenced from above in the Control Flow section
```
>act_prog p pokes you in the~
if isnpc($n)
    chuckle
    poke $n
else
if level($n) <= 5 or isgood($n)
    tell $n I would rather you didnt poke me.
else
    if level($n)>15
    scream
    say Ya know $n. I hate being poked!!!
    kill $n
break
endif
slap $n
shout MOMMY!!! $N is poking me.
endif
endif
~
```
Ok.. time to translate.. the trigger will only happen when the mobile
gets the message "... pokes you in the ..." If the offender (recall
the $n and $N refer to the char who did the poking...) is an NPC, then
the mobile merely chuckles and pokes back. If the offender was a PC
then good and low level characters get a warning, high level chars
get attacked, and midlevel chars get slapped and whined at.

Note that two of these mobiles could easily get into an infinite poke
war which slows down (or frequently crashes) the mud just a bit :(
Be very careful about things like that if you can. (i.e dont respond
to a poke with a poke, and try not to let heavily programmed robot mobiles
wander around together. More on that is given above.)

Also, it is clear that the 'order' command could get confused with the 'or'
control flow. However, this is only the case when 'order' is abbreviated to
its two letter form, and placed immediately following an 'if' line. Thus,
if you want to be that malicious in trying to break the MOBprogram code,
noone is going to stand in your way (However, the result of this would be
a bug message and a bail out from the ifcheck so things dont really break)
#### [&#x2191; Back to ToC](#table-of-contents)

## Mobprog Usage Complexities

Some truths or limitations of mobprogs, some of which might feel unexpected from a builder's point of view, especially if they don't have a coding background.

*  The entirety of a mobprog is processed at the same time, regardless of whether the mobprog involves time or takes time to execute. If a mob has a prog that waits for 10 mob ticks, then waves to a player in the room, it will have decided which player it is waving to as soon as the mobprog is triggered. The entire mobprog is processed when triggered. If the player happens to wander off during this time, the mobile will attempt to wave to a player who is already gone.

* $r is always the same target, within the same triggered event. In a mobprog where $r is used multiple time, perhaps to cast multiple spells, $r will be the same individual for each spell. $r, the variable, is only determined once, at the beginning of the execution of the mobprog. For each run of the mobprog, $r may be different, but within the same event, $r is always the same target. In this sense, sometimes it might feel like $n, but it can still be useful if you understand this is not random, at every single instance of $r, but only at mobprog execution time. This allows you to cast a spell on a random target, and then keep track of that random target for the rest of the mobprog to do anything else.

* MPAT can be combined with many other mobprog commands. This allows the mobile to act upon rooms and players who are not in the vicinity.

* As noted above, the BREAK command will exit out of a mobprog entirely, regardless of nested level of BREAK.

* The flow of mobprogs is dictated naturally by mob-ticks unless you control the timing yourself with @. A mobprog containing multiple lines of mobprogs without any flow control, will execute each command at one mob-tick intervals. This adds a small pause between each action that gives it a more realistic feeling, rather than processing all lines at once.
    * Mob ticks are a little shorter than a second. If you are not directly controlling the flow with @, then commands happen about every .75 seconds.
    * A Tick, that players may be more familiar with, is about 75 seconds of real time, which corresponds to 1 hour of game time.
    * @ command prefix allows the specified command to execute immediately after the previous command without time between.
    * As time may pass, during the time it takes for the mobprog sequence to run, sometimes mobprogs will attempt to target victims which are no longer present. MPAT command allows you to act upon any room in the game as if they mobile is in the target room during the MPAT command.

* If-statements are not required in basic progs, but as the mud may drop some mobprog commands if too much CPU usage occurs, it seems that through testing, the best way to ensure that a mobprog always triggers, is to wrap an if-statement around the mobprog logic. This can often simply be an if rand(100) statement, which just means that 100% of the time, this event will trigger, when the mobprog itself is activated. Without this if-statement, it seems the mud may process the command more lazily or not at all in rare instances.

*  "0." always matches against players. Sometimes, a player and an NPC may share the same name or keywords, and might even be standing in the same room. So, in the case of a mobprog, use "0." prefix to match with only player names, and not NPC. If there is no player in the game matching, it will not look for the next match. This is also the case for gameplay, with spells such as summon, where to target the player named Orc, versus one of the many orcs in the game, they must use "0.Orc".

* Individual mobprogs are limited to 120 lines.



## Regarding CPU Slowdown

We have no real idea how slow this makes a mud. However, you will find
that if you are judicious with your use of MOBprograms, you can either do
little damage, or even reduce the effort on your server! This means that
mobile polling (including the rand_progs) need only be checked when players
are around. This reduces computation of random_stuff a little, but it is
still a polling method, and subject to a basic inefficiency there. However,
aside from the rand_progs, the only additional slowdowns will be when the
mobile is responding to the situation, and you would get that from a special
procedure as well (although MOBprograms are surely not as efficient as
compiled C code)

For those who are afraid that MOBprograms will drown their CPU, here is a
brazen suggestion which could put you a bit more at ease. Instead of having
aggressive mobiles, try the following MOBprogram block on all would be
aggressives.
```
>greet_prog 100~
if ispc($n)
if isimmort($n)
bow $n
else
mkill $n
endif
endif
~
```
This has the effect of making the mobile attack the FIRST visable
mortal player who walks into the room.

What this should allow, is to comment out the aggressive mobile check
section of the code and thus reduce computation by a bunch. There is no
continuous polling through all the mobiles in occupied zones and checking to
see if there is an NPC aggressor and a PC victim. There is also no need to
worry about players skipping through aggressives, since the trigger catches
folk as soon as they enter the room.

Note that the price paid for this, was that if a second player
walked in during the combat, and the first character fled, the mobile won't
realize that there is a new target. So, a compromise would be adding a
rand_prog which had the mobile appear to peer around the room and then do an
mkill $r.
AHA! you say, we are back to polling. Well true, but since mobile_update
is called anyway (at 1/16 the frequency of aggr_update in default Merc 2.0)
and we only add an if check, a walk of a short link_list and the MOBprogram
execution itself, we have still reduced the aggr_update stuff by major amounts.
#### [&#x2191; Back to ToC](#table-of-contents)

## Miscellaneous Information

There is really no limit to the number of MOBprograms a given mobile
can have. However, the length of a single command block is limited by the
value of MAX_STRING_LENGTH. In my version it was around 4k, so that is
probably about 100 lines. The indentation spaces shown in the example
above are NOT required, but do make it easier to read (and debug)

The MOBprogram stuff runs totally without anything in the
mob_commands.c file, but letting mobiles be a bit more godlike has allowed
us to do what we consider to be wonderful things. The replicant and
polymorphing mobiles described above as well as some nifty mob helping mob
interactions are an example.

It IS possible to accidentally make mobiles which can trigger in
loops. As mentioned in the example at the end of this document, the result is
usually a mud crash or major CPU dent. We dont know any way to prevent this
from happening, other than careful coding and a restriction of mobile travel
from zones of one creator to another (another good reason to not have charmed
mobiles do anything). Tracking down the culprit mobile is not always easy.
The only thing we have found which always works, is to add a log statement
into the MOBprogram driver and fill some disk space until it becomes apparent
what commands are repetitively issued. Also, most infinite loops are flukes
where the situation just happens to be right and usually it never happens
again.

The list of variables and triggers and if_checks will grow
continuously as our creators demand the ability to do certain things. If you
have a request or if you have a new one, we don't mind hearing about them,
and if you find bugs, we shall gladly attempt to squash them for you. As
additions or fixes are made, the code will occasionally be redistributed.
However, if you want a current version, please feel free to ask. When the
code is redistributed, a file containing the change history from the original
release will be provided (when possible) to allow you to patch in the changes
with low grief.

I will be glad to lend advice to someone who is trying to install this for
a modified version of Circle 2.20 and if something develops I will be glad to
make that public as well.
#### [&#x2191; Back to ToC](#table-of-contents)

## Associating MOBprograms With A Mobile

There is one only way for the mud to associate the program with the
mobile. In either case, the result is a link list of mob_programs which are
attached to the mobile_prototype. This is done at boot time, and so only one
copy is kept, regardless of how many instances of the mobile are running
about. This also means that there is no dynamic way to edit or modify the
MOBprograms.

Back to how to associate...
The method involves a simple in-file approach. In your mobile file
in your world directory, at the end of the mobile's block (i.e. on the line
following the typical position/default position/sex line), append any number
of MOBprogram blocks (using the syntax above) followed by a line starting
with one '|' (pipe).

```
#3062
fido dog~
the beastly fido~
A beastly fido is mucking through the garbage looking for food here.
~
The fido is a small dog that has a foul smell and pieces of rotted meat hanging
around his teeth.
~
161 0 -200 S
0 20 10 1d6+4 1d4+0
0 25
8 8 1
>greet_prog 60~
if isgood($n)
if rand(30)
mpechoat $n $I wags $l tail at you.
mpechoaround $n $I wags $l tail at $n.
endif
else
growl $n
endif~
|

Explanations
Since it is often useful to have the same MOBprograms affecting several
different mobiles, referencing MOBprograms stored in an external file
is needed. Using the method above, in place of a true MOBprogram block, one
can place the dummy line in the mob file in place of the MOBProgram block(s).
CircleMud 2.20 with these modifications expects these programs to be
stored under the lib/world/prg directory.
```

```
">" "in_file_prog" {MOBprogram_filename} "~" NL

#3062
fido dog~
the beastly fido~
A beastly fido is mucking through the garbage looking for food here.
~
The fido is a small dog that has a foul smell and pieces of rotted meat hanging
around his teeth.
~
161 0 -200 S
0 20 10 1d6+4 1d4+0
0 25
8 8 1
>in_file_prog greet.prg~
|
```
```
Note there is no list of program_commands as well as no second tilde ~.
You can in fact have multiple >in_file_prog blocks, as well as mixing
them with in line MOBProg blocks.

In a file, the syntax is exactly the same as it is for a in_file
approach:

A list of MOBprogram (NOT including any dummy in_file_prog
lines, sorry but recursion was outlawed for simplicity)
blocks followed by a line starting with one '|' (pipe).

More than one mobile can use the same file and one mobile can call more
than one file. Files referenced using the dummy in_file_prog line are
placed in the MOBprogram list at the point where the dummy line exists.
```
#### [&#x2191; Back to ToC](#table-of-contents)

## Adding New Triggers

This section explains how to add new triggers.

All you have to do is to follow these simple steps...

1. Add the appropriate #define XXXXX_PROG to structs.h
2. Write a trigger procedure at the end of mob_prog.c
3. Add the new case in *mprog_type_to_name(...) in mob_cmd.c
4. Add a new if statement in mprog_name_to_type(..) in db.c

There you have it, a new trigger for your MOBProgram system.
#### [&#x2191; Back to ToC](#table-of-contents)

## Credits & History
```
The reason this code was written was to enhance the playing
experience at ThePrincedom (a Merc 2.0 based world scheduled to open in
October 1993)

The original idea for this type of MOBprogram came from playing on:
WORLDS of CARNAGE, a dikumud implemented by Robbie Roberts and Aaron Buhr.
Aaron (known as Dimwit Flathead the First) was the original author from what
I have been told, and I hope he will not be totally offended and angered
by my coding and sharing a mimicked version with the world. This version
is probably not as good as the original and I do feel remorse for publishing
the idea. However, since Carnage has been down for months without a word of
information regarding its return, I am glad to let one of the best features
live on in future generations of MUDs.

There are no objections to this code being shared, since, aside from
a nuclear destruction of all the Temples of Midgaard (excepting the original
one!!), bland mobiles are the greatest bane of Dikumuds today. It would be
nice to get a message saying you are using the code just for our references.
We shant answer questions from anyone until told where they are using the
code. *grin* Since this code is not copyrighted, you of course dont have to
do anything we say, but it would be nice of you to put the mobprog help
screen into your database. and have mobinfo show up somewhere on a more
visable help screen (possibly tagged onto the bottom of credits as a see
also...)

I acknowledge all the work done by the original Diku authors as well as
those at Merc Industries and appreciate their willingness to share code.
Also, quick thanks to Wraith for doing a little beta-installation testing.

N'Atas-Ha June, 1993
murph@ri.cmu.edu

In addition to this DOC file credit section, I'd like to add
a thank you to Yaz, Mahatma, Zelda, and the rest of the Marble Mud crew for
extensively testing MOBProgram 2.1 for me. You may see MOBPrograms in
action as well as their own "flavor" of mud at marble.bu.edu 4000.

Kahn Oct 28th, 1993
MERC Industries

I have ported this code to CircleMud 2.20 and this DOC file was
modified slightly to include information correct with regards to that version
of the code. A lot of the references to Merc Specific features or internals
were removed. I am indebted however to the MERC Industries folks for
providing it in the first place.

Moonchilde Jun 14th, 1994
jtraub@zso.dec.com

Ported to BurningMUD and expanded by Lorgalis
Expanded further by Ninian
```

Further questions about mobprogs on Burning specifically, can be sent to olc@burningmud.com.
#### [&#x2191; Back to ToC](#table-of-contents)
