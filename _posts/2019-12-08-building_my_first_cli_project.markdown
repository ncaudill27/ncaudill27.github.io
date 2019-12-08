---
layout: post
title:      "Building my first CLI project"
date:       2019-12-08 00:51:20 -0500
permalink:  building_my_first_cli_project
---

______________________________________________________________________________


# HollyPop the Hollywood Celebrity quiz game

For my initial project I wanted to build a CLI that was something a little with a little more flavor than your typical terminal experience. The idea for a game came from feeling the need to build something with "replay value". It's possible I got carried away with adding flair.

# Languages or Skills Implemented
* Language: Ruby
* Gems: Bundler, Nokogiri, tty-prompt, paint
* Tools: Trello, VS Code, GitHub
* Implementation: Module for output decorating (including a monkey patch), error handling
# Main features
* Colorful, dynamic UI, (driven by a module)
* Intuitive, flexible menus
* Quiz game, (high score functionality)
* Explore option, navigation of all possible celebrities and movies included in-game
* Multiple "Exit" points

### How you jumped the hurdles
This project began a little backwards. I knew I wanted something in a quiz format but had no idea what source material to choose. Being Thanksgiving time, and having a roadtrip coming up I saved various pages to have some material to read offline. So, facing limited internet hours, and figuring eventually I was going to scrape information. I made my way to a site I had seen scraped before just to play with Nokogiri, IMDB. What began as practice turned into an idea: "People like movies right?" Why make a boring quiz game on academic material, when I can use something more relatable in pop culture? There the project began to take life.

Equipped with my laptop, noise cancelling headphones, documentation for git and bundler, and a series of videos from Avi  I was prepared to face the void of 8 hours without internet. Most of that time was spent reading and note taking. Some, trying to wrap my head around using internet-dependant tools without being able to practice with them. Minimal time was spent coding, but the zero-level code I was able to ideate became my blueprint to build. It enabled me to have three vital components:
1. A little bit of the beginning, (bundler knowledge, notes)
2. A little bit of the middle, (pseudocode object interaction)
3. A little bit of the end, (data scraped and ready to be implemented)

It was hard not to think about getting my project started throughout Thanksgiving.

Once I began, it was easy to notice the advantages the prep-work gave me. Once I had a console up, piece after piece quickly came together. Having a blueprint made it easy to prioritize seperation of respobilities. Ensuring each file accomplished one task. It was exciting to see everything coming together so smoothly. Then, I came across my first big obstacle. Having the game interpret “loss” conditions on an incorrect answer proved a little more complicated than I anticipated. It became something much wordier than I cared for.

Enter error handling.

Having a wrong answer meant needing to deal with an integer zero, adding flow control...twice, once in Game, and again in Question. What if, when a question was answered incorrectly, if it returned a nil value instead of an integer zero? It could raise a TypeError. Rescuing it proved to be much more efficient. Allowing to succinctly break the game loop, and return the current accumulated points of a Game instance back to the main menu to record a possible high score.

```
begin
    # #new_question return nil on incorrect answers.
    @points += new_question
rescue TypeError
    # Allowing easy access to end game.
    puts "You lose."
    return @points
end
```
Having a wrong answer meant needing to deal with an integer zero, adding flow control...twice, once in Game, and again in Question. What if, when a question was answered incorrectly, if it returned a nil value instead of an integer zero? It could raise a TypeError. Rescuing it proved to be much more efficient. Allowing to succinctly break the game loop, and return the current accumulated points of a Game instance back to the main menu to record a possible high score.

Once I had the core functionality in place it was just a matter of replacing my "fake" objects with scraped data. By the end of day three I had my MVP! All because of the one day of planning and going over good resources (that I probably would not have done without the roadtrip).

Now it was time to add features. Which meant finding gems to accomplish my primary goal going into the project: provide a fun and easy to use interface. Of the two gems I added to enhance UX (one for color, one for menu control) each had their own learning curves. Experimenting with them was enjoyable and helped inspire confidence in my ability to involve outside code and adapt it to my needs.

### Refactoring
After adding various features the codebase began to grow. Writing clean, DRY code was top priority and it was about time to reassess. To keep up with that endeavor I found that adding the use of a module best suited to apply use of output altering methods throughout the application. Any menu that contained a loop was stripped down to point mostly at method calls.

While working on the module one method (changing the rate at which texts ouputs by character) proved difficult. Unable to find a way to work around the TypeError I was receiving when trying to call it on the string it should be affecting. Remembering a previous lesson that mentioned Ruby allowing changes to built in classes. I decided to include the module into the String class. Allowing the functionality desired.



### What's next?

My next goal with this project is using Bundler to release version 0.1.0 to RubyGems.org for others to install. My current idea for adding changes to the game is to add more focus to the quiz. In other words, add the options of either quizzing by movie era, or possibly, genres.

In addition, having audio cues for correct answers or "game over's" would be really exciting. Currently, I'm not sure how to handle having to require different commands for iOS vs. Windows. The only ruby rem I found to handle this sort of resposibility was Audio Playback. However, it required dependency packages, so it felt too high demand for users of this application.
