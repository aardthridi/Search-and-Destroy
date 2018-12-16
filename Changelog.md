# Search and Destroy v2.0 (rel-1.0.7) — 15 Oct 2018
Good morning, this S&D update is mostly internal code changes, fixes, and things like that.  I'm too tired to think of anything witty to say at the moment, so here is what's different:

 - I rewrote the mob keyword guessing process from scratch, due to issues with it that I couldn't resolve simply by editing the existing code.  The new version should handle certain problem areas better than the old.  Hatchling Aerie is probably the most obvious example; pretty much every mob in the zone has "dragon whelp" in its keywords, which means hunt trick could take a while.  This and similar situations should be a lot better now.  Note that it's not perfect and won't correctly guess all keywords (it was never supposed to) but as before it will get most of them right, and the new process means I can add filtering that I couldn't before.  Also, as a 'bonus' the mob keywords will randomly vary in length, from 4 to 5 characters for double keywords, and somewhat more so for single-keyword mobs.  I was bored.

 - Mob keywords, mob link color, and similar things are determined during the cp target list build process, rather than after the fact.  This makes it easier for script functions to access them, and makes things like displaying the links faster.

 - Quick where has also been rewritten.  It was overly complicated and had some long-standing issues.  Most of the complexity came from the fact that quick where can be called manually or by script, and the approach that was taken to deal with that.  It was too convoluted and difficult to follow, so I fixed that.  Also, the new version sort-of checks to see if the 'where' output is just flat-out wrong.  For example, if I want to look for "a villager" I probably don't want info for "a confused shopper" but they both have villager as a keyword.  If the output is obviously wrong it will try 2.villager and so forth.  It can still get the wrong mob (e.g. "a confused villager" or similar) but if totally wrong it should be able to skip it and try the next.

 - Quick where will no longer guess mob keywords when called manually.

 - The glitchiness with moving and resizing the GUI window should be mostly fixed.  I'm sure I missed something and it's still possible to bug it out, but for the most part it moves and handles like other plugins, and should no longer "jump" when you grab the title bar.
 
 - There are improvements to the GUI window, mainly dealing with the cp level readout.  Red means you must level before taking a new cp, green means you can take a new cp at your current level, and blue means the plugin is installing or you are offline.  I also cleaned up a lot of its code in general and I think it works pretty well now.
 
 - The process used to determine when you have arrived in the correct zone (area cp's) has been revamped and is faster.
 
 - Improved output when using 'xq' to target your quest mob, and improved quest status tracking.
 
 - I adjusted the level filtering in room cp's again.  This is just something that can't be gotten perfect simply by using the game-defined area level limits.  For example, living wall is level 86, but it's in an area with a level max of 55, so it will show as "ignoring due to level".  The aim here is to reduce the number of links which can sometimes be excessive ("the kitchen" exists in more than a dozen areas) but for now it's a trade-off between having a sensible number of links and getting it right enough of the time.  In most room cp's it isn't a big problem, and there are few enough of these that I can probably do an area-specific filtering thing similar to that found in the keyword guesser.
 
 - On that topic, the "ignoring due to level" messages are in red so as to be more visible.
 
 - Also regarding room cp's, fixed a crash in the cp target builder involving 'noquest' areas.
 
 - I tightened up a lot of the regexp regarding trigger matches, avoiding some accidental triggering and issues arising if the trigger fires on text that is somehow toxic to the plugin.  It seldom happened anyway, and in general was a random fluke when it did, mainly being possible when reading notes and in similar situations.  It should be very unlikely now.

I'm a little nervous about this update due to the number of changes and won't be too surprised if there are error reports, but as usual just let me know about them and I'll fix them as soon as I can.  Thanks for all your ongoing support!

# Search and Destroy v2.0.0 — 19 Aug 2018
Good morning, it's time once again to turn the thermostat of awesome up a notch and so here we are.  Thanks to everyone for reporting issues with the beta and helping me find the root cause of those problems.  At this point the issues arising from the three-plugin system are basically gone.  Most of these came down to lots of duplicate (triplicate, really) code, issues with plugin broadcast and response, and issues when a change to one plugin breaks the others (which I must then fix).  The merge went a lot smoother than I expected and the number of problem reports dropped off fast as things were fixed.

The beta is therefore finished and v2.0.0 is officially live.  The main feature is the merge itself rather than any actual new things, but there are some other improvements as well:

 - Removing the plugin-broadcast system fixed all of the data sync issues and having to track a lot of changes across all three files.
 
 - Removing all the duplicate code makes it run smoother and without the laggy feel it used to have.
 
 - Everything in one file makes changes and whatnot much more predictable, avoiding problems and saving time.
 
 - At SH, the messages about being able to take a new campaign are different from when you are levelling.  This was overlooked in the original and I didn't catch it because I very seldom sit SH.  These messages should now be tracked correctly.  At SH auto-noexp is probably undesirable so you'd probably turn it off via 'xset noexp 0'.  This is now unnecessary – when you reach 200/201 noexp will be toggled off until you remort.  Your TNL set point remains unchanged and auto-noexp is technically still on, it is simply ignored while you are 200/SH.  You can still toggle noexp manually if you need to.
  
 - The window command buttons now 'light up' when clicked, which doesn't make anything happen faster, but I like how it looks.  The window plugin was always the last in line as far as getting updates because everything in it depended on the other two plugins, so its code will be getting a much-needed overhaul.
 
 - The GUI window also displays the cp level taken.  Red border means you can't take a cp at your current level, green border means you can.
 
It's a short list, but hopefully the differences are apparent.  If you encounter a problem, let me know.  Thanks for all of your support, reports, and advice that helped make the version 2 release successful in all respects!

# Search and Destroy v2.0 beta — 11 Aug 2018

- Beta revision 9 uploaded at 03:05 on 11 Aug 2018

Good morning ninjas and ninja fans, I have finally gotten around to merging the original three plugins (Mapper Extender, Search and Destroy, and Search and Destroy GUI) into a single plugin.  Version 2.0 should do everything that the originals did, while suffering none of the drawbacks.

As the beta release of version 2.0 there are no new features yet.  I expect this to have unresolved problems, but I've been doing campaigns with it over the last day and nothing's really caught fire.  Feel free to give it a try and let me know what you think!

Here is the outline of what's been done up to this point:

 - Removed the plugin-broadcast interface and its supporting code and replaced with conventional variable assignments and function calls.  Three separate plugins receiving mostly the same data made for a lot of redundant/triplicated code and CPU work.  All gone now.
 
 - Removed most of the redundant/duplicate code resulting from separate plugins having similar functions and utilities.  The    
   important ones are pretty much taken care of, but given time constraints and exhaustion from work I had to prioritize a bit
   and likely didn't get it all.  I'll clear up the rest in the next update.
   
 - Fixed duplicate alias/trigger names, of which there were a few.  Duplicate pattern matches should all be merged and the excess 
   removed.
   
 - The plugin help text is not working.  It took up a lot of space and was making it harder to browse the file so I cut it out and 
   put it in a text file for later.  Also removed the help button from the window because it wasn't really useful.  I'd like to 
   redesign the window layout and features but am not sure what to do yet.
   
 - Rearranged the XML code for aliases and triggers to be more compact, reducing file length by some 150 lines.  It makes it a lot 
   easier to find and fix things.
 
 - Default start rooms for Ooku and Arboretum have been added.
 
 - I reworked init_plugin and there shouldn't be any problems at the login screen or login process.  Let me know if there are.
 
 - Since version 2 is an entirely new plugin, it has a different plugin ID which means that user-set area start rooms and 
   similar saved things will not carry over.  It's not feasible to try combining three sets of saved settings and ensure there 
   are no problems.  The new version is basically incompatible with the old.  I regret any inconvenience arising from this.
   
That's pretty much it for now.  Please let me know when things break so I can get them handled, and keep in mind that this is indeed a beta version which might crash or glitch on you.  General comments, suggestions, and questions are also welcome, as always.  The beta will run for a couple of weeks to a month, depending on feedback and further testing.  Good luck, and thanks for all of your support and encouragement!

# Search and Destroy 1.3.5 - 7 April 2018
Happy new year, ninjas and other fans of mine!  I'm happy to report that 1.3.5 is a really nice update.  Without further ado, here's what's new:

 - The process for getting cp target data has been redesigned.  The cp type check is the primary
    director of process flow and occurs after cp check, rather than during.  The number of required
    mapper DB operations is reduced by roughly half and all of the post-process filtering has been
    eliminated, further improving performance and reducing ambiguity.  This should finally put an
    end to most of the display and link-related problems that have plagued S&D since the beginning.
    
    As of April 27 the recent crashes and a few other issues discovered during the investigation
    should be fixed.  I guess we'll find out.  Let me know if not.
  
  Additional process improvements, bug fixes, and other changes include:
 
 - Unknown target links were glitchier than expected but Mapper Extender and GUI should now handle them correctly.
 
 - Adjusted the room cp filtering parameters to deal with high-level mobs in low level areas.  For
    example, living wall in Descent to Hell would come up as unknown because it's a level 85 mob in
    a level 35 to 55 zone.  Most of these should now be handled correctly.  A side effect of this
    change is that you'll probably see more 'redundant' room cp links than before.  Unfortunately,
    using the area level ranges for filtering is sub-optimal and given the number of exceptions and
    overly broad (or just flat out wrong) level ranges, the only good way to filter would be to
    store data for every mob, but at that point you're looking at something way more involved.
	
 - Cp type check moved to Search and Destroy, using cp info to get the data.  This removes the 
    escalating probability of mis-identification, which can happen if cp check is used instead.
	The cp level taken is also recorded at this time.
   
 - Room names containing parentheses are now matched correctly.
  
 - Mapper Extender should no longer crash due to missing area or mapper data (e.g. as happens when new areas
    are added to the game).
 
 - The area indexing process is only allowed run when your character state is 3 (standing), 8 (fighting), 9 (asleep), or 11 (sitting or resting).  This solves any issues related to the process running at inappropriate times, e.g. while logging in, afk, or writing a note.

 - Cp check output for room cp's is now easier to read.
  
 - Dead targets on room cp's now display correctly.

 - Xcp with no argument would always target the first mob in the list, even if dead, which could
    prove unhelpful.  Xcp now targets the first mob that is alive.
    
 - Xcp also skips over targets whose locations are unknown.
	
 - Xcp can now be set to automatically hunt trick, quick where, or do nothing after running to
    the target area (on area cp's).  The syntax is 'xcp mode [ht|qw|off]'.  The default has always
    been hunt trick, but sometimes that's not ideal and this allows some flexibility.  Has no 
	effect on room cp's since they directly state the room name.

 - Improved quest handling.  S&D has always worked with quests, but 'xcp' would overwrite the quest
    info and cause it to be lost.  The command 'xq' has been added which re-targets your quest mob.
 
 - Auto noexp has been updated to use GMCP config, making it about as reliable as it can get.
  
 - Removed a lot of dead, orphaned, or otherwise obsolete code and triggers; improved regexp for
    various triggers, etc.; and other general cleanup.

# Search and Destroy 1.3.4 - 9 December 2017
Happy birthday, ninjas everywhere.  We have a new update, which is more of a bug fix update than a feature update.  But 
there are some new things, and hopefully some of the glitchiness in 1.3.3 has gone away and not been replaced.

Search and Destroy:
 - Settings like noexp, etc. will be saved between sessions/installations.

 - New feature: xwhere.  It lets you 'where' multiple mobs quickly, which can be useful
   in many different situations.  'xwhere 10 mob' does 'where' starting at 1.mob and
   counting to 10.  'xwhere 10 20 mob' does 'where' starting at 10 and counting to 20.
   Previously I would do this using a command-line "for" loop, but got tired of typing
   them out and just wrote it into an actual command.

Mapper Extender:
- "xrunto" only works with the area keyword.  It no longer tries to match the area long
   name, or to guess the start room.  It still does partial matches on the area keyword.
   If no match is found, it will pull up 'area keywords <your text>' and display any
   matches.

   The problem is that the area keywords and long names have too many words in common
   and with partial matches it gets even worse.  This is why 'xrt desert' or whatever
   would sometimes go to the wrong area.  The "runto roulette" / go to random room in
   area problem can range from annoying to deadly.  I don't have a better answer yet,
   but for now, limiting input to areaid/keyword eliminates the errors and gives
   consistent performance.
 
- Added default start rooms for open clan halls, manor areas, and some other areas.

- Room cp links to non-questable (clan, manor, etc.) areas are no longer displayed.

- Room links are now filtered according to the level the cp was taken, rather than the
   current player level.

- Fixed a bug which spammed GMCP requests and broke target detection upon plugin install.

- Fixed a bug where 'xcp' sometimes sends you to the wrong target while on a room cp.

Mapper Extender GUI:
- 'xset' and 'xgui' are equivalent for window settings and commands.

- Font size and line spacing are saved between sessions/installations.

- Much-improved window resizing and performance.  Special thanks to Ylar for this!
   It's a bit glitchy, probably because fiddled with the code to address some minor
   details, but most of the time it isn't apparent.  To resize the window, use the
   widgit thing in the lower right corner, as with the standard Aardmush plugins.

- Re-added maximize and minimize window functions as right-click menu options.

Once again, thanks to everyone who has given me your support in this project, I've
learned a lot in working on it and I hope you all enjoy the results.  Thanks for all
the ideas, contributions, and technical advice.

To those who haven't supported me (of which there are a few people) your criticism
is valuable because it keeps me evaluating, and helps me moderate my enthusiasm so
that I don't lose perspective or get too carried away.  Thanks for that.

Happy searching and destroying, ninjas of aard.


# Search and Destroy 1.3.3 - 22 October 2017
Good morning ninjas, we have a new update today.  As usual, if there are any problems, let me know and I'll do
what I can.  Here we go:

- The campaign type detect should correctly identify the cp type when a room and the area 
  it's in have the same name.

- The display glitch where targets don't show up should be fixed.  Let me know if not.

- The current 'xcp' target is now highlighted in the GUI window.

- Room cp targets are now sorted by area.  Special thanks to Fiendish for helping me with this.

- The font size and line spacing can now be changed in the GUI window.  The commands are 'xgui fontsize \<number>'
  and 'xgui linespace \<number>'.  Defaults are 8 and 15, respectively.

- The cp list font will change between Lucida Sans Unicode and Segoe depending on cp type.  Segoe is a bit
  narrower than Lucida and it might allow more room cp text to fit in the window.  Xgui fontsize works on
  both.  

- "nx" and "nx-" now do 'quick scan' after the run.

- Removed all but the "?" button from the window title bar.  I never used them, did anyone else?

- Added "send to front/back" to the window title bar as a right-click menu.  The title bar buttons (including
  'bring to front') usually got covered up when sending the window to back, making them un-clickable.  Not helpful.
  As long as you can right click the title bar, it's easy to bring the window to front again.

- Finally removed the 'reset gui' commands and related code.  Their only purpose was to bring the window back after it glitched out and left the screen, but since that bug no longer exists there is nothing to reset anymore.

- Removed much of the spam that happens on Mapper Extender install, and when you take a new cp.  Also removed some
  old debugging output as well as "cp ch" and other echoes when the plugin sends commands to the mud.  The output
  looks and feels a lot cleaner now.

- Continued the trend of more code clean-up, regexp simplification, neater output appearance, and all that.

That's all for now.  Happy searching and destroying, and thanks for all your support!


# Search and Destroy 1.3.2 - 22 September 2017
- Added 'xcp' as an alias for 'xcp 1'.

- 'xcp' will retry if it fails because of "no object or data busy".  

- If you hit 'nx' too many times, you can go back by using 'nx-' or right-clicking
  the 'nx' button.

- Enlarged GUI buttons to make them easier to click.

- S&D now detects which type of CP is active.

- Target list is now filtered according to cp type.  This removes most of the extra 
list items displayed (mostly in area cp's) when a target location is both a valid 
area and room name.  Room cp's can still generate multiple links per target (as they
should) if the same room name exists in different areas.

- Simplified 'xcp' and 'cp check' syntax in Mapper Extender.  I get what WinkleWinkle
was doing with these crazy regexp's, but most wind up being complexity for their 
own sake.  Fiendish certainly doesn't use them in his scripts, and I can see why.
Unless anyone actually requires the complex versions, I'm looking at gutting the 
command interface and making it simpler and more consistent.

- Removed a lot of spammy text output (old debugging messages, etc.) plus other 
general cleaning-up. 

Lastly, on short notice, I'm implementing a change to correct a glaring omission that was brought
to my attention.  A few other things I was working on also made it in.  Hopefully they
aren't horribly broken:

- Hunt trick should now work for Navigators hunting through portals.  Previously, 
it would break because the portal hunt message didn't match the regexp.  It looks
functional to me now, but I'm not a navigator so please let me know if and when this
breaks.  If it works, it should remove the need to patch it yourself.  

- Navigator auto-hunt will be trickier.  For now, when you try to hunt through a portal, you
will be prompted to enter the portal and then autohunt again.

- The autohunt command interface has been redone, in line with the general simplification
plan mentioned above.  If anything goes wrong with it, let me know.  This wasn't rushed,
exactly, it just hasn't had as long to be tested as other things, but I fixed all of the
issues that I was able to identify.  Type "search help" to see the new command syntax.

# Search and Destroy 1.3.1 - 14 June 2017
Bug fixes:
- hunt trick will now correctly terminate after trying to hunt something that doesn't exist.
- hunt trick will now correctly terminate if you try to do it while resting, sitting, or sleeping.
- hunt trick and quick-where will no longer use 1.mob for its first
try.  It will just do 'hunt mob' or 'where mob'.  I don't think it matters which is used,
it seems to target the same thing either way, I just didn't like 1.mob.  If problems with
it let me know and I can change it back.
- campaign target window will now populate when taking a CP from a questor.  Before, it would
only populate when requesting from Commander Barcett.
- the problem with 'xrunto' sometimes taking you to a random-ish room is mostly fixed. If 
xrunto takes you to the wrong area, e.g. Fantasy Fields instead of 'fields' (Killing Fields)
go to (in this case) Killing Fields and 'xset mark' the start room again and that should fix it.

New feature:
- Auto-noexp!  When you're at low TNL and you can take a campaign at your current level, 
 it will turn on noexp and prevent you from over-levelling and missing a campaign.

   When plugin is installed, it defaults to off.  To turn it on, do 'xset noexp (amount)'.
 If you're on a CP but can take a new one at your current level, noexp will kick on 
 when your TNL drops below the given amount.  Noexp will kick back off after you finish
 your current CP and then go and take another one.  You can also toggle noexp off 
 manually via 'noexp' as usual.  For low levels I suggest setting it at 1000 TNL or so,
 and around 500 when you get higher and mobs award less XP.  You may need to go higher
 if there's a lot of double stacking with your daily blessing bonus.
 
# Search and Destroy 1.3.0 - 31 May 2017
- Search and Destroy is once again being actively worked on, and this time I'm in charge!
Good times are ahead!
- The bug causing the GUI window to 'jump' and leave the screen when you try to move it has
been fixed.  It is no longer possible for the window to get lost, stuck, or otherwise go
beyond the edges of the screen.
   
  

