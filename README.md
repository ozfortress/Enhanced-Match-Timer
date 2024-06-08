# [TF2] Progressive Ruleset Timer Plugins
The Progressive Ruleset ("Pro Ruleset" for short) incorporates this plugin that creates a dynamic win condition. 5CP round win limit gets reduced to the current highest score +1 when the match timer runs out.  For example, if the score is 1 - 2 when the map timer runs out, the win limit will be set to 3 and round continues.

# Why Use This Plugin?
 All current competitive rulesets for the 5CP gametype include a timer that sets a hard time limit on matches. Match timers reduce competitive integrity in the 5CP gametype. In its current form, the timer kills comebacks, causes anticlimactic endings, and encourages teams to run down the clock.

 Enhanced Match Timer reduces the length of matches without encouraging timer related strategies. It allows for exciting comebacks, makes every match end in a last capture, and discourages running down the clock.

# How to Install
 You'll need SourceMod installed on your server before installing Enhanced Match Timer.

 Place the addons folder into the tf directory.

 # How to Use
 Enhanced Match Timer creates a new cvar named "mp_timelimit_improved" which is by default 0. This means that the plugin by default does nothing. I recommend that you change this cvar only through ruleset related configs. I've provided a modified rgl_6s_5cp_scrim config that contains "mp_timelimit_improved 1" as an example.

 The plugin is only active on cp_ maps when mp_timelimit is above 0 and mp_timelimit_improved is set to 1. These conditions must be met before the match begins. If the plugin is active, you should see the phrase "Running Enhanced Match Timer..." in chat after the match starts. If you need to toggle the plugin, simply exec a config with mp_timelimit_improved changed before readying up.

 Additionally, the plugin will not activate if the score difference is greater than the threshold defined by mp_timelimit_improved_threshold. For instance, if this convar is set to 1, then the win difference between both teams must be 1 or lower in order to activate the plugin. If the timer expires with a win difference of 2 or more, the match would end as normal.

# Options
 mp_timelimit_improved: Enables the plugin's match timer related behaviors. 0 off (default), 1 on.

 mp_timelimit_improved_visibility: Hides the match timer when a team reaches 4 rounds won. 0 off (default), 1 on.

 mp_roundtime / round_time_override: Changes the length (in seconds) of the round timer in 5CP and KOTH. -1 for default gametype behavior (default).

 sm_improvedtimers_chat: If 1 (default), prints timer related notifications to chat.

 mp_timelimit_improved_threshold: The win difference threshold for activating the Enhanced Match Timer features. Anything above this number of rounds between the teams will end the match at the end of the timer.  Set to -1 to disable (default)

# Credits

- [Dewbsku](https://github.com/dewbsku) and [b4nny](https://github.com/b4nnyBot) - Original authors of the plugin
