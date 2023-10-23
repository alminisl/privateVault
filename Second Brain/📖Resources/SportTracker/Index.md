> Write down more information about the project

SportTracker AKA Team Score Manager


Using the `t3` stack I started making a simple sport match tracker for our office games. It currently is made to support 1v1 and 2v2 matches. (the naming is a bit off in the app now especially in the DB as I was hacking things together withouth a concrete plan, probably will refactor in the future)

The basic idea is to have a ranking table using Elo rating for every player which adapts depending on the matches played and Win/Loss ratio.

The tables/Prisma schema in the app look like this

//TODO: Add excalidraw of the tables we have and how they are working



# Installation and configuration


The way the app is configured.. Vercel + Supabase and running. 

Elo Rating: https://ryanmadden.net/posts/Adapting-Elo
// TODO: add a excali draw


## Made as trello bugtracker

trello.com/b/jMcGdFnQ/tsm-bug-board
