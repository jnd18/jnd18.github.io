---
layout: post
title: Visualizing Name Popularity Over Time With Tableau
---

I've heard a lot of praise for Tableau, but in general I'm pretty turned off by point-and-click interfaces,
especially when there are excellent code-based alternatives, such ggplot2 for R and Seaborn for Python, not to mention the plethora of JavaScript plotting libraries.
But I figured I might as well give it a try, so I made a basic dashboard that you can find [here](https://public.tableau.com/profile/jonathan.dorsey#!/vizhome/babynames-dashboard/NamePopularityDashboard?publish=yes).
I'll give a short overview of the dashboard below the break,
but first let me say that I'm pleasantly surprised by how generally intuitive it is to create polished interactive plots in Tableau.

So, as the title of this post says, I decided to visualize name popularity over time using one my favorite datasets,
Hadley Wickham's [babynames](https://github.com/hadley/babynames).
The data is from the US Social Security Administration, and it contains the number of childen of each sex given each name, for each year from 1880 to 2017.

The dashboard is pretty self-explanatory, but I'll give a brief description here.
On the top half, we have a line graph of the popularity of names over time,
where the popularity of a name in a given year is the percentage of children who were given that name.
The way I set it up, you can type names into the `Name` selection box (near the bottom of the line graph) and select which ones you want by ticking the boxes.
The graph only displays one sex at a time, which you can select using the `Sex` selection box in the top right corner.
In the middle is the color key, which shows which names are selected and what colors are being used to plot those names.
The `Name` box is a little awkward down near the bottom, but I put it there so that you can easily see which sex and names are already selected while typing in the box.
The bottom two graphs show the top ten names for each sex in a given year.
You can select a year by typing or clicking in the `Year` box.

I'll conclude by saying again that I am quite pleased with Tableau.
It has that same kind of "linguistic" or "grammatical" flavor as the nice code-based plotting libraries like ggplot2,
and you can really tell that a lot of thought went into its design.
I'm looking forward to getting to know this tool better.

