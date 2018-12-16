# Search and Destroy v2.0 instruction manual

### Auto-hunt
- '**ah** \<**mob**\>' starts autohunt, which will hunt your mob and move you to the next room until you reach your mob.  Navigators can autohunt through portals.  It does not work with mapper cexits - autohunt uses the output of the hunt skill which is limited to cardinal directions only (and portals, for navigators).
- '**aha**' and '**ah0**' will cancel an auto-hunt in progress.
- Autohunt is very useful for navigating mazes, but may put you at risk of aggressive monsters.
- Autohunt requires you to practice up your hunt for it to work.  If your skill is too low, autohunt will not work (it would be pointless as all the directions would be wrong).  Note that this has no effect on the hunt trick (see "ht" hunt trick below).

### campaign: "xcp" command - target a mob on your 'cp check' list and get location
- '**xcp**' targets the first available mob on your cp list and gets possible locations. "Available" means living and location is known.  E.g. the first four mobs on your list are all dead, unknown, and/or both, "xcp" will ignore all of those and target the 5th mob.
- '**xcp** \<*n*\>' targets the *n*th target on your cp list, dead or alive.  If dead, the MUD only ever gives the area name, even if the cp is room, so dead mobs are always handled as if the cp were area.
- '**xcp 0**' clears the current target and its room search results.
- '**xcp mode** \<**ht**\|**qw**\|**off**\>' determines what xcp does after running to an area — "ht", "qw", nothing (area cp's only).  In most cases, setting it to "qw" (quick-where) will find the right mob without having to hunt trick, which is faster.  
- For area cp's, "xcp" first runs to target area.  Upon arrival, it does hunt trick (default) to pick out your cp mob, then does quick-where to get room(s).  If the area has duplicate roomnames, your mob could be in any of them, use 'nx' to check through them.
- For room cp's, "xcp" gets the room and area info from mapper and generates a direct run to that room.  If the same roomname exists in multiple areas, the cp target list builder will generate a list index for each of them, which can be barely noticeable, or flood the whole list with 12 links for one mob.  This is on the list of current problem-solve items and sooner or later will probably be fixed.
- Unknown mobs can't be targeted because the location isn't in your mapper db.  For area cp's, this means you've never been to the area at all.  For room cp's it means you haven't mapped any rooms with that name in any area — in most of these cases you'll have been to the area before, but haven't explored (i.e. mapped) every room.

### "goto" command — run to room within area after getting search results
- '**go**' runs to first room on the list returned by hunt trick / quick where.
- '**go** \<*n*\>' runs to the *n*th room on the list.
- '**go 0**' runs to the area start room (see 'xset mark').  This is useful for areas like Nenukon and similar maze, etc. situations where 'mapper goto' is unable to find a path.

### "ht" (hunt trick) command — leverage cp hunt mechanics to find target mob and location
- '**ht**' runs the hunt trick (ingame: **'help hunt trick'**) on your currently-targeted cp mob.
- '**ht** \<**mobname**\>' runs hunt trick on mobname, 2.mobname, 3.mobname, etc. until it finds the target or fails to do so after testing all instances.
- '**ht** \<*n*.**mobname**\>' runs hunt trick starting with *n*.mob Useful for skipping past no-hunt or similar mobs — these will interrupt hunt trick and cause it to time out or simply fail to locate.  "No-hunt" means hunt returns a "No one by that name" message as if the mob doesn't exist in the area.  Normally-huntable mobs return "You seem unable to hunt that target for some reason" when you get it as a cp (or gq) target.
- '**ht abort**', '**hta**', and '**ht0**' all cancel a hunt trick in progress without returning any results.
- Hunt trick does *not* require you to practice (or even have) the hunt skill.  If you don't actually have the skill, hunt will return random directions and also give the "unable to hunt" message for cp/gq mobs.

### "kk" (quick kill) command:
- '**kk**' tries to kill the current target
- '**xset kk** \<**command**\>' sets quick-kill to attack with the given skill or spell, e.g. , 'xset kk bs', 'xset kk c 541'

### "nx" and "nx-" commands — run to next or previous room in list of results
- '**nx**' runs to the next room in the list of results, after doing 'go'
- '**nx-**' runs to previous room.
- If you don't use 'go' first, 'nx' and 'nx-' will both run to the first room on the list (same as 'go')

### "qw" (quick where) command:
- '**qw**' gets results for your currently-targeted cp mob.
- '**qw** \<**mobname**\>' gets results for given mobname.  Use this when the auto-guesser fails.
- '**qw** \<*n*.**mobname**\>' gets results for *n*.mobname (e.g. 3.fido).
- Note that "qw" searches only one target, unlike hunt trick (whose input looks similar).  Use "xwhere" to 'where' multiple mobname instances.
- "qw" will fail if the mob is flagged no-where, or in a dark room.  It works intermittently on hidden mobs due to your detect roll vs hidden.

### Vidblain navigation
- '**xset vidblain**' turns on Vidblain navigation, which allows one to quickly and easily cross the dark portal into Vidblain.  It also compensates for the portal's reality-distortion and uncertain transit vector and landing room, enabling straightforward travel to Vidblain destinations which would otherwise be tedious at best.
- '**xset vidblain** \<*level*\>' turns off Vidblain navigation when you reach the desired level, typically that of your lowest-level Vidblain area portal.  It does take tier into account, as well.  This is useful because it's always faster to use an area portal to get to Vidblain than to run via the dark portal.

### Window commands - change font size, line spacing, etc.
- The window can be dragged to a new location via the title bar, and resized via the widget at bottom right.  Right-clicking the title bar brings up a menu with collapse, expand, and send to front/back.
- '**xset fontsize** \<*n*\>' changes target list font size.  Default is 8.
- '**xset linespace** \<*n*\>' changes target list line spacing.  Default is 14.
- '**xset** \<**off**\|**hide**\|**0**\>' turns the window off and removes it from view.
- '**xset** \<**on**\|**show**\|**1**\>' turns the window on and displays it.

### Xmapper commands
- '**xm** \<**room name**\>' generates 'goto' links for matching rooms in the current area.
- '**xm** \<**room name**\>**|**\<**area id**\>' generates 'goto' links for matching rooms in the given area id, e.g. 'xm along the sea floor|wooble'
- '**xm** \<**room name**\>**|all**' generates 'goto' links for all matching rooms in your database.  Note, there is no limit on how many results it can return, other than the size of your db — it will spam your screen with hundreds or thousands of results if you let it.
