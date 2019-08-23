# FantasyNBATools
A collection of all of my Fantasy Basketball related tools.

## Summary
These are different tools that I have created over the years which I use for my fantasy basketball league. Originally they were all in R, but as I learned more Python, and the internet has evolved, they have been moving to Python. All of these scripts are meant to help you collect data from various places to augment your fantasy basketball knowledge, be it of the NBA, or of your own league. I have built the following tools:

TODO: Include instructions for running scripts
TODO: Fix README

### Schedule Scraper
In 2015 I built a metric based on NBA schedules for fantasy basketball. The base concept is that, on a given night, you have a limited number of roster spots available to you to slot players into. Since there are 7.5 games a night, on an average night 15 teams are playing. That means that, even if every member of your roster is on a different team, it's probable that you could have all 15 players on your roster playing in a single night. The goal of the metric, and the charts that come with it, is to reduce the amount of conflicting players on your roster. Since each fantasy team  will have more than that same 7.5 games per night (obviously with add/dropping the figure becomes much larger), it behooves you to optimze which nights your roster favors.

Generally, Tuesdays and Thursdays have 2 to 6 games (with 6 being a rarity) each night. Mondays and Fridays tend to be around 8, Wednesdays 10, and weekends are very variable, due to the seasonal scheduling. However, since the National TV games are (a) relegated to specific timeslots and (b) relegated to specific teams, certain teams tend to play on certain nights more often than others. The Lakers, who probably will have a national game a week in 19-20, will play a lot of Tuesday and Friday nights, with fewer Saturdays and Mondays.

This script lines up all of the team schedules, then creates a chart of each team's conflicts with other teams, and calculates their total conflicts divided by the mean as each team's score.

I want to refine this metric to factor in the importance of late season games. I think applying some sort of decay would help. But that's another show.

Initially this was all in R, using the libxml package. It used the package to grab the HTML table from each team's page, and then used R's native dataframe structures to run through the calculations and spit out the final product.

However, E!SPN re-wrote their site over the course of the last season, so I had to rewrite the scraper in Python using Selenium. I then use Pandas to process.

### Yahoo! Scraper + Elo Calculator
I built this tool to calculate the Elos of different players in my fantasy league. [The Elo rating system was created by Arpad Elo as a way to guage the skill levels of opponents in chess matches.](https://en.wikipedia.org/wiki/Elo_rating_system). This system has been adapted over the years, even appearing in [The Social Network](https://www.youtube.com/watch?v=OLnd6-thEHM) in reference to it's use in FACEMASH.com. I adapted this slightly for fantasy. Since H2H is scored out of 9, and the formula predicts the probability of each side winning, I opted to use the scores, rather than a boolean, and used a slightly higher *k*. I feel like the volatility is about where I want it to be. Overwhelming victory through score matters more than rating when it comes to determining the delta. I like this because a 5-4 win is pretty common, and if the players are even, it shouldn't change much in either of their ratings.

I use Selenium to scrape Yahoo!'s site, and then Pandas to manage the data, with numpy to speed up the calculations. Very basic scripts. You can also get a dump of everyone's statistics if you want. Maybe it can come in handy ;)

TODO: There is something wrong with how the script functions over the playoffs. Will need to troubleshoot HARD this year.

### Fantasy Draft Lottery
I wanted to do a fantasy draft lottery the same way that the NBA does, or at least the way the NBA emulates. There are *n* lottery balls in play (determined by league rules, so go hog wild with your own stuff), each with a manager's name on it. Balls are randomly drawn until the first 6 choices are made, and then the rest are handed out in order of placement in the playoffs.

I also built a quick Average Draft Position calculator so I could test out different odds rollouts.

### SQL Tools
I wanted to try to build some tools to deploy the data from my Elo Calculator to a PostgreSQL database. Currently have not done much work on this.
