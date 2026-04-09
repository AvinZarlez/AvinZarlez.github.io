---
title: "Pen the Pet: Building a Daily Puzzle Game"
categories:
  - Blog
tags:
  - Games
  - JavaScript
  - Puzzle
  - Open Source
---

In my off time I built a game recently called [Pen the Pet](https://www.avinzarlez.com/penthepet/), and it has gotten polished to the point that I am actually kind of proud of it now.

It is a free browser game. Every day there is a new puzzle. Your job is to place a limited number of walls and "pen your pet" in by cutting off every path to the edge of the map. The catch is that you are not just trying to solve the problem, you are trying to find the *best* possible answer.

If you like short daily puzzle games that reward a little thinking, this game is for you.

## What the game is

Each puzzle gives you a grid with terrain and a fixed wall budget. Water acts as a natural barrier. Sometimes there are "Holes" that can be filled by spending a wall there. Stars add points to your score, and Bees subtract points. Your pet starts at the home tile, and your goal is to trap it inside the largest, highest-value area you can create.

That means the puzzle is part path-blocking problem, part score optimization problem. Sometimes the obvious enclosure is not the best one. Often the best move uses the terrain in a way that allows you to reduce the amount of walls in one area in order to have extra to get something more valuable in another part of the map.

Be careful though, you only get to submit an answer once for each puzzle! You can take as long as you want, but there is just enough pressure to make the final submission feel meaningful.

## Why I made it

I ran into another browser puzzle with a similar premise that had the seed of a great idea. I didn't like some design choices made there, and had some issues with the person who made it. A friend of mine and I had gotten into the puzzle concept though, so I decided to build for us a version of the game I wanted to play.

I wanted something lightweight, easy to play, and easy to open from any device. No install. No account required. No app-store friction. In fact, the project is entirely a static webpage hosted on GitHub. Just load a URL and start playing.

That constraint shaped almost everything about the project.

I haven't made a proper game in a while. I've done plenty of software projects, web apps, tools, and other types of prototype and production code the last couple of years. But games have a different feel to them, it was nice to get back into that mindset again. There's something satisfying about a system where all the rules interact in interesting ways and you get to watch someone figure it out.

## A few details I especially like

There is a new puzzle every day, but you can go back and play older puzzles with the level selector.

You can change what type of pet you have via your choice of emoji, letting you customize the game for your favorite animal or mythical creature. I added multiple language support, currently just English and Spanish but happy to add more as people desire. There is also a hint system that will let you know if you want if you found the optimal answer already or not, or what exactly the optimal answer is to aspire to. The game is also designed to work well on mobile and desktop, and even in theory should work entirely via keyboard navigation.

These kinds of tweaks mattered to me a lot, not treating this game like a quick throwaway side project but something that could be played and supported for years to come.

It also has optional cloud sync if you want to carry your progress across devices, but the core game works perfectly fine without signing in.

## Technical challenges

Every map is generated offline and solved before it ever shows up in the browser. Since I wanted the game to be a static webpage, I couldn't use any dynamic code to solve levels in the backend. There is no backend for the game. The browser loads the map, renders the board, checks the penning logic, and calculates your score on the client side. Hosting is simple, deployment is simple, and the whole thing is easy to inspect because the source is public.

I deliberately kept the stack simple: vanilla HTML, CSS, and JavaScript. That said, I had to cheat a little for level generation. The game uses a Python solver based on Mixed Integer Linear Programming. In practice, that means each puzzle is turned into a math problem with explicit constraints and an objective function, and the solver computes the best possible result for that map. When the game tells you the optimal target, it is not making an educated guess. It is the proven optimum for that puzzle.

That was one of the biggest design goals for me. I did not want a puzzle game where the goal is to find the "best" answer if the "best" answer is fuzzy or not fully knowable. In order to generate levels, I created a GitHub Actions pipeline that runs the javascript and python code to generate maps, then it validates them before they get saved and published. The project checks for things like whether the pet can initially reach the edge, whether the puzzle is too trivial, and whether certain tile placements create uninteresting choices. The validation checks ended up being just as if not more important as the puzzle solver itself.

I also have extensive linting and testing that I am able to run as GitHub Actions pipelines, so no code needs to execute for the user at runtime but I still get the benefits of modern coding tools as part of the build and test process.

It takes a few seconds to make each level, a little longer than would be best for real time level generation. But I didn't want to make endless scrolling puzzles, I wanted a shared experience where every player sees the same level every day. The game is inherently social in that way, you are meant to share your results with your friends and compare your time and percentage.

As a side effect, this project became a pretty nice example of how far you can get with straightforward web tech if your scope is clear.

## Built with AI, but not on autopilot

I used AI coding agents heavily while building this project.

That helped a lot, but not in the magical "describe a game and receive a finished game" sense that people sometimes imply. The useful workflow was much closer to agent iteration with constant supervision and direction.

The agents were good at accelerating implementation. I was able to get a lot more done than I would have had time for otherwise. They were not good at knowing when a seemingly reasonable approach would create long-term problems. Architecture, edge cases, validation rules, and game-specific behavior still needed careful review. If I had just given it vague instructions, it would make trash.

However, I know how to develop a game, and I was able to describe to the agents section by section the kind of architecture needed to make something stable and maintainable. I still had to review every line of code the agent generated, and often had to send it back to fix the errors it had made or systems it over or under engineered.

Still I had some issues, some bugs were introduced that slipped past me. I was able to track them, fix them, and continue to make what ended up being well over 1,000 unit tests to ensure regressions are minimized in the future. All this ended up reinforcing something I already believed: AI can speed up development, but it does not replace the engineering judgment needed to turn working code into [stable software](https://www.avinzarlez.com/blog/code-vs-software/).

Oh and in case you are wondering, my kid made the art!

## It is open source for a reason

The whole project is up on GitHub:

- Game: [www.avinzarlez.com/penthepet](https://www.avinzarlez.com/penthepet/)
- Source: [github.com/AvinZarlez/penthepet](https://github.com/AvinZarlez/penthepet)

The repository includes the game, map data, generation scripts, tests, documentation, and a local level editor if you want to make custom levels. The tile system is structured so new tile types can be added from a single data definition, and the scoring logic is separated cleanly enough that the project could be adapted into other grid-based puzzle ideas.

I like side projects more when they are able to be inspected, see what is going on "under the hood" so to speak. If someone wants to see how the game works, or wants to copy an aspect they like such as the level generation tools or GitHub Actions pipelines, they can fork the code and do it themselves! I would encourage you to build any kind of daily puzzle game you want on top of the structure I have built here.

## What I want from people who try it

Mostly, I want to know whether it is fun.

Play a few daily puzzles. See if the puzzle feels fair. Try it on desktop or mobile. Make sure cloud sync is working for you. Use the hints, or ignore them. Tell me where the game gets confusing, what parts it gets interesting, and anywhere it breaks.

If you run into a bug or have a feature request, please let me know. Feedback like that is exactly what helps a project like this get better. Make an issue directly in the GitHub repo, I will review every single one.

Thank you for checking it out, I hope you join me and my friends in trying out the puzzle every day!
-Avin

```markdown
Pen The Pet 🐕‍🦺
Day 41 - Iron - Apr 9, 2026
Score: 100% - Time: 01:46
Hints used: checked for optimal
Play: https://www.avinzarlez.com/penthepet/?date=2026-04-09
```
