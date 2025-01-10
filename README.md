# Enhanced Match Timer
 The Enhanced Match Timer, formerly "Progressive Ruleset Timer Plugins", is a SourceMod plugin that modifies the behavior of the match and round timer in competitive 5CP matches.

# Plugin History
 Originally, this plugin set out to simply reduce the length of the round timer, and remove the match timer once said timer had expired while also reducing the score required to win.

 The goal of that iteration of the plugin was to impove competitive integrity by eliminating timer based strategies such as parking the bus (that is, running down the clock once a team has a lead) and to make every match end in a last point capture.

 However, the plugin failed to account for tournament structures where the overall match time has a significant impact on subsequent games played (such as LANs and One Night Cups), and additionally the plugin was susceptible to abuse by teams who would intentionally run up the score gap to a large number, and then park the bus into overtime to force the underdog team to make an impossible comeback over an unreasonably long period of time.

# How we've fixed this
 First off, when I chose to work on this plugin, I wanted to make sure that the plugin followed a simple rule: **Any new features of the plugin should be opt-in, not opt-out**. This means that if a league admin does not update their configs, but does update this plugin, the behaviour of the plugin should not change.

 With that said, we've implemented the following features:

## Win Difference Threshold
 Enabled with `mp_winlimit_improved_threshold <score>`, this feature will prevent the plugin from activating if the score difference between the two teams is greater than the threshold. This can be a little confusing, so let me explain

 When you take the score of the two teams (red and blue), and subtract the lower score from the higher score, you get the win difference. If this win difference is __*greater than*__ the threshold, the plugin will not start overtime, and the match will end as normal. This is handy for leagues that only wish to use the plugin as an automatic golden cap, or for leagues that wish to end a game early if it's clear that one team is significantly in the lead with next to no chance of being beaten.

 In case that still isn't clear, here's a practical example:

 Let's say we set the threshold to 1. Red team has scored 4 points, and Blue team has scored 1. At the end of the timer, the plugin will see that the win difference is 3, but we've set the threshold to 1. The game will now end.

 Inversely, let's say the threshold is 1, Red team has scored 2 points, and Blue team has scored 1. The win difference is 1, and so is the threshold. The game will now go into overtime, and the winlimit will be reduced to 3, meaning that which ever team gets to 3 points in overtime will be declared the winner.

 Lastly, if you simply want it to go into overtime no matter what, set the threshold to -1, and the plugin will ignore the win difference.

## Maximum Overtime Length
 Enabled with `mp_timelimit_improved_timelimit <minutes>`, this feature will set a maximum time limit for the match timer in overtime. This is useful for leagues that wish to have a hard time limit on matches, but still want to use the plugin for its other features.

 Once the match timer has expired, if the game were to go to overtime, the match timer will be increased by the value of `mp_timelimit_improved_timelimit <minutes>`. For instance, if the match timer is set to 25 minutes, and `mp_timelimit_improved_timelimit <minutes>` is set to 5 minutes, the match will go to overtime with a 30 minute timer (which TF2 will interpret as adding 5 minutes to the current timer).

 This also adheres to the Win Difference Threshold, so if the win difference is greater than the threshold, the match will end as normal.

## Tiebreaker
 Enabled with the Maximum Overtime Length and `mp_timelimit_improved_tiebreaker <0/1>`, this feature will resolve ties at the end of overtime. If both teams are tied for rounds, the winning team will be determined by the number of points captured (or, in simpler terms, whoever has captured mid). The winning team will receive 1 additional round point and the game will then be immediately ended. If the mid point is not captured, the game will end in a tie still, as it is not possible to determine a winner.

 This feature is useful for leagues that wish to have a clear winner at the end of a match, and especially useeful for LANs.

# Why Use This Plugin instead of the Original?
 As mentioned earlier, the original plugin had a number of flaws for tournament structures that weren't a traditional 5CP Scrim or Official, however the maintainers of that plugin do not seem to see these issues as a problem. At the bequest of several league admins, I have taken it upon myself to fix these issues and provide a more robust plugin that can be used in a wider variety of settings.

 Naturally as the original plugin would conflict with this one, I've also chosen to add functionality to disable the original plugin should this one be running in the same environment. This is to prevent any conflicts that may arise from having two plugins that modify the same cvars or interact with the same timers.

# How to Install
 You'll need SourceMod installed on your server before installing Enhanced Match Timer.

 Place the addons folder into the tf directory.

# Commands
 `end_match`: Ends the match immediately, can be used without RCON. Players should use this instead of re-executing, as it will not cause logs to be lost.

# Options
 `mp_timelimit_improved`: Enables the plugin's match timer related behaviors. 0 off (default), 1 on.

 `mp_timelimit_improved_visibility`: Hides the match timer when a team reaches 4 rounds won. 0 off (default), 1 on.

 `mp_roundtime` / `round_time_override`: Changes the length (in seconds) of the round timer in 5CP and KOTH. -1 for default gametype behavior (default).

 `sm_improvedtimers_chat`: If 1 (default), prints timer related notifications to chat.

 `mp_timelimit_improved_threshold`: The win difference threshold for activating the Enhanced Match Timer features. Anything above this number of rounds between the teams will end the match at the end of the timer.  Set to -1 to disable (default)

 `mp_timelimit_improved_timelimit`: The time limit (in minutes) for the match timer in overtime. 0 for no time limit (default).

 `mp_timelimit_improved_tiebreaker`: If 1, the match will resolve ties at the end of overtime (if mp_timelimit_improved_timelimit is greater than 0). In the event that both teams are tied for rounds, the winning team will be determined by the number of points captured (or, in simpler terms, whoever has captured mid). The winning team will receive 1 additional round point and the game will then be immediately ended.

# Credits

- [Dewbsku](https://github.com/dewbsku) and [b4nny](https://github.com/b4nnyBot) - Original authors of the plugin

- [Ozfortress](https://ozfortress.com) - For their support, feedback, and testing of the plugin

- [CappingTV](https://twitch.tv/cappingtv) - For letting Summer Brawl 2025 be the guinnea pig for the tiebreaker feature.
