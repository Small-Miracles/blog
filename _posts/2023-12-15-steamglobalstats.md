---
title: "Steam Global Stats for in-game analytics"
date: 2023-12-15
---

For the [demo](https://store.steampowered.com/app/2428520/Quest_for_Gold/) of my game I was interested in seeing how many players would actually play through each of the levels. In this post I will showcase how Steam's [Global Stats](https://partner.steamgames.com/doc/features/achievements) can be used as a quick and easy way to add analytics to your game. These stats can be used for example to figure out how often each level of your game was won/lost, how many points were collected, which upgrades players love or what the average playtime for a level is. You could use this information to figure out which levels are too difficult for players, where they quit the game and so on. 

Steam Stats are similar to achievements but by default they do not seem to be visible to players. Usually, stats are tracked per player. Steam also has "Global Stats" which are aggregated stats. They are still tracked per user but Steam keeps a global total of all users' values for the stat. Global stats can be easily retrieved (as opposed to stats from every user that played your game). So they can be used to do easy analytics. 

Example: Keep track of the unique player count that beat a level in your game. Want to know how many players beat level one, two and so on in your game? Add a stat in the Steamworks App-Admin page to your demo/game for each level you want to track. Use INT as the type, called "level_1_won" and min/max value are 0/1. Set to increment only (if a player beat a level, they can't "unbeat" it) and Aggregated (important, this tells steam to keep a global total of this stat). Then, use the Steamworks SDK in your game code whenever a player beats a level to store this stat for the player with a value of 1 (SteamUserStats.SetStat("level_1_won", 1); SteamUserStats.StoreStats();). Steam will then keep a global total for that value which increases by one every time anyone beats a level for the first time. 

The cool thing about global stats is that you as the developer can retrieve the value. With SteamUserStats.RequestGlobalStats(1) and SteamUserStats.GetGlobalStat("level_1_won", out level1WonTotal); and Debug.Log(level1WonTotal) will show how many unique players beat that level.

Will this help in making your game better? I added it out of curiosity and to learn the Steamworks SDK for stats. Also, there are obviously more sophisticated analytics tools out there to use.

Further examples for analytics are total money or total kills. Average length of playtime per level would also work by dividing global total playtime for a level by total playercount that beat the level. 

For reference, here's a full example using Unity: {% gist 06673ae23cc0f61ecd8bac9ec44b8994 SteamScript.cs %}
