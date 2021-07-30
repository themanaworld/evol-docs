# The Mana World Evolved
### Custom Functions

Last Update: 2021-07-30

## About custom functions
The bulk of functions used are NPC scripts.
They are loaded by npc/scripts.conf and divide in a few blocks:

- Critical Functions
- General Purpose Framework Functions
- Pre-Loading Functions
- Main Functions
- Item Functions
- Magic Functions
- GM Commands
- Events
- Post-Loading Functions
- NPC Functions

## Critical Functions
These functions are critical, and breaking them will break several other functions,
breaking in turn several NPCs, and will probably cause the server to crash.

In other words: They are nested by NPCs, scripts and functions.

### Main

#### menuimage ( image, string )

Formatting for select

#### dnext ( )
Same as next, but honors `GSET_LONGMENU_DENSITY`

#### menuaction ( str )
Returns `[str]`

#### setq1 ( quest, val )
Sets quest field 1.

#### setq2 ( quest, val )
Sets quest field 2.

#### setq3 ( quest, val )
Sets quest field 3.

#### setqtime ( quest, val )
Sets quest time field. Unused and does not work properly.

#### mesn ( {name} )
Header for NPC dialog. Use it before NPC start talking.

#### mesq ( message )
Sends a NPC message enclosed in quotes. You should give it an `l()` function.

#### g ( female, male )
Returns something variating with gender.
Is totally useless, difficult to translate, and its use is generally frowned upon.

#### b ( message )
Makes the message bold

#### col( message{, color} )
Send message in color. Defaults to color code 9.

#### adddefaultskills ( )
Ensure a player have the default skills (sit, walk, talk, resync, etc.)

#### addremovemapmask ( map, mask, mask )
Updates map mask. I'm not sure how it actually works.

#### mesc ( message, {color} )
Same as `mes(col(message{, color}))`

#### get_race ( {class} )
Returns the human readable form of your race (from `$@allraces$`)
Currently unused and broken.

#### tutmes ( message, {header=Tutorial, headerfirst=True} )
Sends the message if `TUTORIAL` is set.
Came with Moubootaur Legends and is unused.

#### narrator ( flag, str )
```
// Function to show narrator text. Accepts string args.
// If first arg is a number N, then it represents bit flags.
// Bit flags :
//   0x1 -- blank line at beginning
//   0x2 -- blank line at the end
//   0x4 -- use last "next;"
//   0x8 -- don't use first "mesn;"
```

Came with Evol and is unused.

#### speech ( flag, string )
See narrator, but for NPCs

#### npcdebug ( message )
Shows debug message on server console if `.debug` is set.

#### askyesno ( )
Ask players to select between YES and NO.

Returns the choice in `ASK_YES` or `ASK_NO` constants.

#### compareandsetq ( quest, current, next )
Checks if quest is current and updates to next if true.
Returns true if it updated the quest.

#### npctalkonce ( text{, delay=1{, function=npctalk3}} )
```
// Use a delay to prevent spams from NPC that display text without the
// use of (a) close/next function(s).
// Argument:
//  0 Text to display
//  1 Lock delay (default = 1)
//  2 Message function:  (default = 0)
//      0 = npctalk3
//      1 = npctalk
//      2 = message
// TODO: Use temp player var, because NPC var affect other players
```

#### rand2 ( min{, max} )
Same as `rand` but for small numbers. Increases entropy.

#### any( <arg>{, ...<arg>} )
returns one argument randomly

#### any_of( <array> )
returns any member of the array

#### die ( )
Kills the player. If `$HARDCORE` is true, it'll set `@grace` variable.
This allows hardcore servers to NOT send players to the abyss when they were
killed by script.

#### ispvpmap( {mapid} )
Returns true if the map has PVP enabled.

#### msObjective ( condition , message )
Function from Moubootaur Legends, colors `message` based if `condition` is true
or not.

#### getmap ( )
Same as `getmapname()` but using `getmapxy()` instead.
Performance was not measured.

#### isin ( map, x1, y1, {[x2, y2][radius]} )
Verifies if the player is in the specific rectangle (or square, if radius is
provided instead of a x2,y2 tuple)

#### isat ( map, x1, y1 )
Same as `isin` but only for the specific tile.

#### delinventorylist ( )
Clear output of getinventorylist()

#### gf_accid / gf_charnameid / gf_charname / gf_charid / validatepin
Moubootaur Legends functions. Should never be used.

####  Exception( Message, {Flags{, Return Code}} )
Error handling. See RB_ constants for flags which may be used.

#### mescordialog ( text, color, {dialog=1} )
If dialog is set, sends text as a mesc. Otherwise, sends it as a dispbottom.

#### itheal ( hp{, mp{, time}} )
// Delayed healing. Takes 3~5 seconds. Variates with Vit up to +100%.
// The vit can have an additional 20% bonus as well.
Mana regenerates instantly.

#### sqldate ( {day variation, month variation} )
Offsets and returns current date in SQL format

#### set_aggro( monster{, mode=MD_AGGRESSIVE} )
Makes a monster aggressive. Can set other monster mobs as well, such as MD_LOOTER
and MD_ASSIST.

#### numdate ( )
Special function which makes current date (ISO) a progressive number.
eg. `20210730`.

If `$@OVERRIDE_NUMDATE` is set, it'll return that instead.

#### json_encode ( {varname, varvalue}, {varname 2, varvalue 2}... )
Formats a dictionary in JSON format.

#### api_send ( code, data )
Dumps data into `api_export` table. Used by Mirror Lake.
Code is an integer and data is a JSON-string.

#### getquestlink ( quest )
Returns the quest link in M+

#### getmonsterlink ( mob )
Returns the mob link in M+

#### getpetlink ( pet )
Returns the pet link in M+

#### getmercenarylink ( merc )
Returns the merc link in M+

#### gethomunculuslink ( homun )
Returns the homun link in M+

#### mapexit ( )
:warning: Deprecated. Does nothing. Error message in console won't be decent.

#### destroy ( )
:warning: Deprecated. Disable the current NPC.

#### npcaction
Compatibility layer, do not use.

#### gmlog ( message )
Writes message to GM Log.

#### getx ( )
Returns X position

#### gety ( )
Returns Y position

#### getnpcx ( )
Returns .x variable

#### getnpcy ( )
Returns .y variable

#### title
Alias for `setnpcdialogtitle`

#### camera
Alias for `setcamnpc` (if argument provided) or `restorecam` (otherwise)

#### mapmask
Alias for `sendmapmask`

#### getmask
:warning: Deprecated. Always return 1

#### if_then_else
:warning: Deprecated. Alias for `(if ? then : else)` unary

#### misceffect ( eff{, target} )
Shows effect for everyone in area, centered in NPC or target if provided.

#### selfeffect ( eff{, target} )
Shows effect for yourself, centered in NPC or target if provided.

#### fakenpcname
Alias for `setnpcdisplay`

#### npcwarp ( x, y{, npcid} )
Warps a NPC without animations.

#### get
Alias for `getvariableofnpc`

#### sc_check
Alias for `getstatus`. If the second argument is not passed, defaults to `0`.

#### wgm
Sends a `@request`.

#### registercmd
Alias for `bindatcmd`.

#### iscollision
Alias for `checknpccell` (with `cell_chkpass`)

#### readparam2
Alias for `readbattleparam` but without asking for account ID.

#### updateskill
Alias for `skill` with flag 0.

#### npctalk2
Same as `npctalk` but with arguments swapped.

#### learnskill
Same as `updateskill`, but only runs if your skill level is less than provided.
If no skill level is given, defaults to 1.

#### spawndummy ( map, x, y, ID{, name{, event}} )
Creates a dummy monster for cutscenes. Returns the GID.

#### DelItemFromEveryPlayer( ID )
#### DelAccRegFromEveryPlayer( KEY )
#### DelChrRegFromEveryPlayer( KEY )
#### DelQuestFromEveryPlayer( ID )
#### ReplaceItemFromEveryPlayer( OldID, NewID )
#### ReplaceSkillFromEveryPlayer( OldID, NewID )

Functions for ServerUpdate().

### String
Safe string manipulation functions. Does not require PCRE.

#### str(<int>)
//     returns whatever is passed, converted to string

#### startswith("<string>", "<search>")
//     returns true if <string> begins with <search>

#### endswith("<string>", "<search>")
//     returns true if <string> ends with <search>

#### capitalize("<string>")
//     returns <string> with its first letter capitalized

#### titlecase("<string>" {, "<delimiter>" {, <camel>}})
returns <string> with the first letter of each word capitalized.
if <camel> is true, the string is joined in a camelCase fashion

#### camelcase("<string" {, "<delimiter>"})
Alias for `titlecase` with camel set to True.

#### zfill("<string>" {, <width> {, "<padding>"}})
//     returns <string> padded to the left with <padding> up to width

#### format_number(<integer> {, "<separator>"})
//     formats a number properly

#### fnum
Alias for format_number

#### strip("<string>")
//     removes spaces at the start and end

#### reverse("<string>")
//     returns <string> reversed

#### repeat("<string>", <multiplier>)
//     repeats <string> many times and returns it

#### shuffle("<string>")
//     returns <string> shuffled

### Array
Deals with arrays.

#### array_pad ( array, size, value )
prepend or append <value> until the array is of <size> size
returns the amount added on success, or false (0) if nothing changed

#### array_replace ( <array>, <needle>, <replace>{, <neq>} )
replace every occurence of <needle> with <replace>
returns the number of replaced elements

#### array_find ( <array>, <needle>{, <neq>} )
return the index of the first occurence of <needle> in <array>
if not found it returns -1

#### array_rfind(<array>, <needle>{, <neq>})
return the index of the last occurence of <needle> in <array>
if not found it returns -1

#### array_exists(<array>, <needle>{, <neq>})
//     return true or false accordingly if <needle> is found in <array>

#### array_count(<array>, <needle>{, <neq>})
//     counts the number of occurrence of <needle> in the <array>

#### array_entries(<array>)
//     returns the number of non-empty entries

#### array_remove(<array>, <needle>{, <neq>})
//     removes every occurrence of <needle> in the <array> while shifting left

#### array_reverse(<array>)
//     reverses the array

#### array_sum(<array>)
//     return the sum of every element of the array

#### array_difference(<array>)
//     return the difference of every element of the array

#### array_shift(<array>)
//     returns the first element of the array and removes it, while shifting left

#### array_unshift(<array>, <value>)
adds <value> to the start of the array, while shifting right
returns the new size

#### array_pop(<array>)
//     returns the last element of the array and removes it

#### array_push(<array>, <value>)
adds <value> to the end of the array
returns the new size

#### array_shuffle(<array>)
//     shuffles the array

#### array_unique(<array>{, <threshold>})
//     allows entries to appear up to <threshold> in the array

#### array_diff(<array1>, <array2>{, <array>...}, <array>)
```
//     compares array1 against one or more other arrays and fills the last array
//     with the values in array1 that are not present in any of the other arrays
//     returns the number of entries not matching
```

#### array_filter(<array>, "<function>")
//     filters the array using a callback function

#### array_highest(<array>)
Returns the index of the highest value in <array>\
NOTE: Array must be an INT array!

#### relative_array_random(<array: 0, {[value, probability]..}>)
```
//     returns a random entry from the array, by relative probability
//     the first key of the array should be 0 and every entries are a tuple
//     of [value, probability]
```

### Math

#### abs(<int>)
//    returns the absolute value of the passed integer

#### lognbaselvl({<multiplicator>{, <min value>}})
//     returns BaseLevel * logn (BaseLevel * alpha).

#### log2(<int>)
//    returns the log base 2 of the passed integer, up to 20 (2**20=1.048.576) (round down always)

#### is_between ( lower, higher, target)
// result is: `lower < target <= higher`

#### limit ( lower, target, higher)
:warning: Deprecated. Use `cap_value` instead.

// forces the equation: `lower <= target <= higher`.
// Note it still works if higher and target values are swapped.

#### ponderate_avg ( arg1, sub1, arg2, sub2)
// result is the ponderate average.

### Bitwise

#### bitwise_get ( variable, mask, {shift} )
Gets a bitmasked value in from an integer. If the shift is omitted, it will be
deduced from the mask.

#### bitwise_set ( variable, mask, shift, new value )
Sets a bitmasked value in a variable.

Returns a reference to the variable.

#### bitwise_count ( int )
//    returns the number of bits set in <int>

#### get_nibble ( VAR, NIBBLEID )
Gets a nibble from a bitmasked variable.

// A Nibble can go up to 15. There are 7 nibbles.

#### get_byte ( VAR, BYTEID )
Gets a byte from a bitmasked variable.

// A Byte can go up to 255. There are 3 bytes, and a fourth going up to 127.

#### get_bitword ( VAR )
// A Bitword can go up to 65535 and is fixed in position to handle Soul EXP.

#### set_nibble ( VAR, NIBBLEID, VAL )
Returns bitwise_set

#### set_byte ( VAR, BYTEID, VAL )
Returns bitwise_set

#### set_bitword ( VAR, VAL )
Returns bitwise_set


### Permissions

#### is_admin ( {account ID} )
Returns true if is an admin, with all permissions

#### is_trusted ( {account ID} )
Returns true if is a staff member and receives ClientVersion

#### is_dev ( {account ID} )
Returns true if is a dev, and can listen to `@wgm`

#### is_evtc ( {account ID} )
Returns true if is an event coordinator, and can spawn

#### is_gm ( {account ID} )
Returns true if is a game master, and can jail

## General Purpose Framework Functions
These are tools used by NPCs and scripts; But generally not by other functions

### Input

#### menuint ( «struct» )
Composed by tuples of (string, int); Causes a menu to show up.
Will save the int from selected option in `@menuret` variable.
And then, return it.

#### menustr ( «struct» )
Same as menuint, but arguments are strings. Uses `@menuret$`.

#### menuint2 ( array )
Same as menuint but takes a single array and then extrapolates it.

### Time
Contains utilites related to time management

#### now ( )
Same as `gettimetick(2)`

#### santime ( )
Same as `gettimetick(2)`. Unused, from Moubootaur Legends.

#### time_from_ms ( )
Undocumented

#### time_from_seconds ( )
Undocumented

#### time_from_minutes ( )
Undocumented

#### time_from_hours ( )
Undocumented

#### time_from_days ( )
Undocumented

#### FuzzyTime(<unix timestamp>{, options=3{, precision=2}})
```
//     gives time in a human-readable  format
//
//     <options> is bitmasked:
//     1  do not show "ago" when in past
//     2  do not show "in" when in the future
//     4  show "from now" instead of "in" when in the future
//
//     <precision> is the number of units to show,
//     by default uses two (eg. 2m30s or 1h20m).
//     Use '99' for max precision
```

#### time_stamp ( )
Undocumented

#### HumanTime
:warning: Deprecated.
The old version of FuzzyTime.
DO NOT REUSE.

### Timer
Expands the powers of `addtimer`

#### areatimer("<map>", <x1>, <y1>, <x2>, <y2>, <tick>, "<npc>::<event>")
`addtimer` in area

#### areadeltimer("<map>", <x1>, <y1>, <x2>, <y2>, "<npc>::<event>")
`deltimer` in area

#### areatimer2
Same as `areatimer` but cancels running timers of same event

#### addtimer2
Same as addtimer but deletes any existing timer with same event

#### maptimer("<map>", <tick>, "<npc>::<event>")
`addtimer` in whole map

#### maptimer2
Same as `maptimer` but cancels running timers of same event

#### mapdeltimer("<map>", "<npc>::<event>")
Cancels a timer event in the whole map

####  partytimer("<map>", <tick>, "<npc>::<event>", partyid)
A map timer, but filters the party

### Goodbye

#### goodbye_msg ( )
Returns a random goodbye message.

#### cwarp ( {x,y}/{map, x, y} )
Closes the dialog, then warps the player.
- If map is not specified, will slide to coordinates.
- If no coordinates are passed, will warp randomly.

#### cshop ( {name} )
Closes the dialog, then opens a shop.
It is optimized for evol use, so {name} should always be supplied.

#### cstorage ( )
Closes the dialog, then opens storage.

#### bye ( {emote} )
//     closes the dialog without waiting for the player to press close
//     can also display an emote

#### goodbye ( {emote} )
//     same as bye, but also displays a canned message
//     can also display an emote

#### goodbye2 ( {emote} )
```
//     Waits for the player to press close, displays a canned message,
//     ends execution.
//     Can also display an emote
```

### Vault
Contains the core functions for the Vault.

#### getvaultid ( )
Returns your Vault ID, or zero, if not a Vault user.

#### getvaultexp ( exp )
Grants Mirror Lake EXP points if you have a Vault ID.

#### vaultOnLogin ( )
Handles login for players using the Mirror Lake.

#### vaultOnLogout ( )
Flushes mirror lake data to TMW Vault.

#### MirrorLakeSendTo ( World, Lake )
Sends a signal to the Mana Launcher to move you to a different world.

This signal is sent to ManaPlus and then relayed to the Launcher.

## Pre-Loading Functions
Most of these are scripts, with some exceptions. They are pre-loading because they
may be needed by other scripts.

### clear_vars

#### ClearVariables ( )
Post-login updater for players

#### ServerUpdate ( )
Post-Init updater for server

### asklanguage

#### languagecode()
Returns the string language code of user's language.

#### asklanguage()
Allows player to change their game language.

### inventoryplace

#### inventoryplace ( {item, number, item, number, item, number...} )
Checks if player have enough space for the items.
Closes dialog if false.

### random-talk
Random dialog for various random NPCs.

They take no arguments.

#### Functions:
-  hello
-  moubootalk
-  villagertalk
-  sailortalk
-  legiontalk
-  asleep
-  studenttalk


### inc_sc_bonus

#### SC_Bonus ( delay, SC, min{, max} )
```
//    Applies effects for INC_* (STR doesn't exist)
//    Valid values: INCAGI INCVIT INCINT INCDEX INCLUK INCHIT INCFLEE SC_FURY
//    Doesn't works: SC_STRUP
//    Works if .@min == .@max: INCMHP INCMHPRATE INCMSP INCMSPRATE
///   Untested Values: WALKSPEED (reverse logic) INVINCIBLE (broken)
//    PS. SC_FURY causes crit rate to increase
//
// Variables:
//    .@delay    Second of buffing
//    .@type     SC_*
//    .@min      Min amount of type
//    .@max      Max amount of type (optional)
```

#### SC_Bonus2(delay, SC1, val1, val2)
Same as SC_Bonus, but when the SC takes two values.

### commands/kami

### filters

Filters for array_filter and other callbacks.

#### filter_always( id )
Always return true.

#### filter_onlyme( id )
Returns true if id is your account id.

#### filter_notme( id )
Returns true if id is not your account id.

#### filter_sameguild( id )
Returns true if id is in the same guild as you, incl. yourself.

#### filter_sameguildnotyou( id )
Returns true if id is in the same guild as you, excl. yourself.

#### filter_sameparty( id )
Returns true if id is in the same party as you, incl. yourself.

#### filter_sameguildorparty( id )
Returns true if id is in the same guild or party as you, incl. yourself.

#### filter_sameguildorpartynotyou( id )
See above. Excludes yourself.

#### filter_hostile( id )
Returns true if id is:
- An hostile player in a PvP map, honoring noparty and noguild subrules
- A monster
- An hostile homunculus
- A hostile pet
- A hostile mercenary
- A hostile elemental
- A player/slave not in same guild or party.

Always return false for npcs.

#### filter_friendly( id )
Returns true if id is not hostile (See above)

#### filter_notboss( id )
Returns true if id is not a boss monster.

### quests

Contains quest handles, such as `QuestSagatha`; `elanore_exp`; `Valon`; etc.

## Main Functions
These are functions and scripts used largely by NPCs.

### alchemy
Handles **all** alchemy tables in the world.

#### AlchemySystem ( )
Invokes Alchemy system, even without a table.
Returns `true` if concatenation was successful.

### banker

#### Banking ( )
Handles GP operations

#### Banker ( )
Handles a Bank - Complete: GP, storage, mail, quests if any.

### barber

#### BarberSayStyle ( {what} )
// what: 1 = Style; 2 = Color; 3 = Style + Color in dialog

#### BarberChangeStyle ( )
Private function

#### BarberChangeColor ( )
Private function

#### BarberChangeBodyType ( )
Private function

#### BarberChangeRace ( )
Private function

#### Barber ( {intro=True} )
A barber NPC. If intro is not set, can be used by dialogs.

### dailyquest

:warning: Deprecated.
Requires a full rewrite.
DO NOT REUSE.

### ferry

Configures ferries.

### travelers
Could use a rewrite.

#### Traveler ( )
The traveler NPC

### game_rules

#### GameRules ( )
Show the rules for the player.

### inn

#### Inn ({price})

:warning: Deprecated. And old function for inns; Should not be used.
Needs a rewrite.

### magic

:warning: Deprecated. Contains the old functions for magic NPCs.

### mob_points

#### fix_mobkill(mobID)
Manual fix for scripted mobs

#### MobPoints ( )
Core function, for monster points and monster-killing quests where map is ignored.

### process_equip

:warning: Deprecated.
Documentation does not exist.

Seems to be a feeble attempt to extract dye colors for Inspector Quest.

### slot_machine

#### SlotMachine ( )
A Slot machine

#### SlotMachineSymbol ( )
Private.

### soul_menhir

#### SoulMenhir ( )
:warning: Deprecated.
A Soul Menhir. Require `@Xs`, `@Ys` and `@map$`.

It is affected by the weird TMWA mess regarding save positions and is not working
fully. Touching it should set both respawn point as location system of 000-0.

### water_bottle

#### WaterBottle ( )
Tool for filling water bottles (wells, water pumps, etc)

### evil_obelisk

:warning: Deprecated.
Used solely for Hurnscald Evil Obelisk.
Requires hidden, undocumented PC variables.
DO NOT USE.

### lockpicking

#### LockPicking ( )

:warning: Deprecated.
This is the original Iilia's lockpicking function, not Moubootaur Legends version.
Therefore, it is not flexible and not fit for reuse.

### default_npc_checks

#### PCtoNPCRange ( {distance=4} )
Same as setting `.distance` OnInit, but warn players they need to move closer.

#### CheckInventory

:warning: Deprecated.
Used solely for Trick'n'Treat.
DO NOT USE.

### undead_debug
Contains the NPC for Crypt debug.

#### UndeadDebug ( )
Function to obtain the items for the crpyt boss fights.

### headstyles

Creates a few variables:
- `setarray $@hairstyle$`
- `setarray $@haircolor$`
- `setarray $@REFEXP`

### stat_reset

#### StatReset ( )
A stat reset NPC

### quiz

:warning: :x: Deprecated.
The old Riddle System from TMWA.

Must be replaced.

### dynamic_menu

:warning: Deprecated.
Use menuint and rif instead.
DO NOT REUSE.

### DyeConfig

Creates a few variables:
- `setarray $@DYE_color_names$`
- `setarray $@DYE_colors$`
- `setarray $@DYE_items$`
- `setarray $@DYE_item_names$`

### motd

:warning: :x: Deprecated.
Contains the old MOTD configuration which is not flexible.

It needs to be replaced.

### motdconfig

:warning: :x: Deprecated.
Contains the old MOTD configuration which is not flexible.

It needs to be replaced.

### miriam

Private functions

### ghost

Private functions

### location

Coordinates location system, including respawns.
Sets a few arrays:
- `$@LOCMASTER_TP`
- `$@LOCMASTER_LOC$`
- `$@LOCMASTER_MAP$`
- `$@LOCMASTER_X`
- `$@LOCMASTER_Y`

#### ResaveRespawn ( )
Resaves your respawn point

#### ReturnTown ( )
Warps you to the town saved in `LOCATION$`

#### LocToMap ( LocName )
Retrieves map name from location name

#### MapToLoc ( MapName )
Retrieves location name from map name

#### TPToLoc ( TPCode )
Retrieves map name from TP constant

#### POL_LocToTP ( TOWNCODE )
Actually, a manual conversion from location name to its TP code.

#### EnterTown( LocName )
Updates `LOCATION$` variable

#### teleporthome ( )
Warps home and updates LOCATION$

### weather
Controls world seasons. But they are disabled in TMW.
Therefore, it controls weather magic.

A few commands are defined:
- `@wsnow`
- `@wrain`
- `@wsand`
- `@wevil`
- `@wnight`
- `@wclear`
- `@wreset`
- `@wset`

#### "#WeatherCore"::climate(mapid)
Returns the climate setting

#### "#WeatherCore"::weather(weather{, mapid})
Returns true if weather is present in map

#### "#WeatherCore"::weather_override(weather, duration{, mapid, override=false})
Modifies the weather on mapid for duration.
If override is set, disregard climate restrictions.

### marriage
Contain private functions for marriage.

// to use, create a duplicate:
```c
001-1,30,31,0 duplicate(marriage)     name#x1,y1,x2,y2        NPCID
001-1,30,31,0 duplicate(marriage)     name#range      NPCID
```

### npcmovegraph
Contains the needed utilities for walking NPCs.

#### initmovegraph ( )
Initializes a walking NPC

#### setmovegraphcmd ( fromPositionLabel, toPositionLabel [,moveChanceWeight [,moveFlags]], postCommand, ...);
```
 * This function manipulates NPC moving graph. Before calling it, make sure
 * `initmovegraph' was called. The function accepts 3-5 parameters (many times):
 * fromPositionLabel, toPositionLabel -- starting and ending position of NPC move
 * moveChanceWeight -- positive integer, represents the chance of moving in given direction. (optional)
 * moveFlags -- if .mg_flags & moveFlags != 0, move is possible. (optional)
 * postCommand -- either "moveon" (start moving to next location straight after arriving from
 *                fromPositionLabel to toPositionLabel) or a semicolon-separated set of commands
 *                ("wait 3", "emote 5" etc, see `execmovecmd') that will be executed after arrival.
 *                The commands don't have to end with ";moveon", it's executed in the end by default.
```

#### execmovecmd
Private? Commands are:
- moveon
- dir
- sit
- stand
- wait
- emote
- class
- warp
- call
  - calls a function
- speed
- say
- debugmes
- flags
- flags_0
- flags_1

#### firstmove
```
// initial actions for npc when using move graphs.
// function can accept 2 arguments:
//    1: action sequence, for example "speed 200; dir 4". Default is "moveon"
//    2: start point label. Default is #0 from move graph labels
```

#### dographmovestep
???

#### npc_pausemove
Pauses NPC move

#### npc_resumemove
Resumes NPC move

#### npc_turntoxy (X, Y)
Turn NPC towards an object at position (X,Y)

#### getnextmovecmd
Private?

#### getrandompoint(x1,y1,x2,y2)
Private?
```
//    -- Get a random walkable point within a map rectangle
//    x1, y1 -- top-left corner of rectangle
//    x2, y2 -- bottom-right corner of rectangle
//  Returns 0 on success and -1 on error;
//  Since we cannot return multiple values, the random
//  coordinates are stored in NPC variables .move__rand_x, .move__rand_y
```

#### findmovegraphlabel
Private?

#### mg_npcwalkto
Private?
```
// wrapper function for npcwalkto. It can accept 4 parameters.
// If #3 and #4 params are set, the walkto location is chosen
//   from rectangle (x1,y1,x2,y2).
// It sets the npc variables .move_target_x, .move_target_y
//   that are used to resume NPC walking
// Returns 1 if walking is possible, 0 otherwise;
```

#### movetonextpoint
Private?

### npcmove
Contains the needed utilities for walking NPCs.

#### initpath
No documentation available

#### domoveaction
No documentation available
Internal commands exist.

- move
- dir
- wait
- emote
- class
- warp
- goto
- rmove
- speed
- sit
- stand

#### movetonextpos
No documentation available

#### initialmove
No documentation available

#### getmovecmd
No documentation available

#### domovestep
No documentation available


## Items Functions
used with callfunc(), when it was quite too much script code to be added on
item_db.conf directly. One file per item, and should be used only for the item.

## Magic Functions
The post-loader (`global_event_handler`) will load magic spells from here.
Each file is a magic spell of its own, with a couple exceptions:

### magic/config
Loaded before all magic spells.

### magic/final
Loaded after all magic spells.

## Commands
These define GM Commands.

## Events
These define annual and repeatable events. Mostly.

## Post-Loading Functions
These are mostly NPCs responsible for cleaning up the whole script and functions
interface so NPCs can be loaded after.

### Scoreboards

Contains the Leaderboards and is one of the most expensive components.

- HallOfGuild
- HallOfFortune
- HallOfLevel
- HallOfJob
- HallOfAcorns (not used)
- HallOfLethality (removed)
- HallOfAlmanach
- HallOfGame

Command: `@scoreboard` and `@scoreboards`

### Global Event Handler

Handles login events, logout events, death, assassinate, server init, clear logs,
and also handles the backbone of die() function.





