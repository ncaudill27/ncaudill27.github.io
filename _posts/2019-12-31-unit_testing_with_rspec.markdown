---
layout: post
title:      "Unit Testing With RSpec"
date:       2019-12-31 14:36:25 -0500
permalink:  unit_testing_with_rspec
---

Throughout the Flatiron curriculum we are pushed to work using Test Driven Developmet (TDD). Using RSpec test suites to check against the code we write ensuring we achieve the desired output. Learning to understand these tests has been a huge benefit to me personally. Once realizing work could be done literally side by side with the specs I saw a new breakthrough in production. Being able to see interpret the specs, and predict exactly how the code needs to be structured allows for proper planning. As opposed to constantly running tests as you make adjustments.

While working on my CLI project something that really stood out to me was how time consuming lack of tests can be. Having to manually walk through your code on the console, even with tactful `binding.pry`, feels painfully sluggish. It was then I realized learning to write my own tests was something that would be much more than merely convienient. It scares me to think of the total time spent navigating menus during that CLI project, especially considering it was not a big application. Imagine something larger!

Coming from a non-professional background, I was of the mindset my experience would hold me back in the tech world. But, while repeating the same actions time and time again I began to hear a familiar voice in my head. One that was fine tuned to pick up on missed opportunities for higher efficiency.

"Wasted trip."

"Wasted trip."

"Wasted trip."

The service industry has left me with a more complete toobox than I realized. When you repeat the same few actions thousands of times a week efficiency becomes your best friend. Behind the bar, moving faster for the sake of speed usually tends to produce the opposite results. Before even getting halfway with the CLI project it really felt like I had been moving faster, rather than smarter. By the end of it learning to write my own tests became high priority.

Like with anything new. The first step proved to be the hardest. Wait, nevermind, `rspec --init` does that for you. Well, that was easy, but writing the tests is definitely going to be more complicated right? [Less than 3 minutes of video](https://rspec.info/) prove otherwise. As with anything practice makes perfect. However, one thing we Flatiron students don't have to worry about is having to find a variety of specs to refer to.

As mentioned `rspec --init` does a lot of the work for you. The rest is simply requiring the files needed with is easily done through an `environment.rb` file. Maybe with a require_all gem if needed. So, slowly but surely I began to put together some unit tests and have them run against code I had built. Doing my best to think about possible edge cases and boundaries.

Structuring the specs and adding context is as simple as keeping track of different levels of nesting. With your inner-most blocks doing the bulk of the work. While I'm sure specs can become quite nuanced, the work we've been shown at Flatiron shows that basic funtionality is easily reached. Referencing old labs and some [documentation](https://rubydoc.info/gems/rspec-expectations/RSpec/Matchers) relieved a lot of my uncertainty.

Probably the most intimidating part is all of the possible configuration options, but thankfully nothing more than the basic setup is needed to actually get started. That being said, being introduced to Sinatra has shown me that unit testing is just one piece of the puzzle. A very important corner piece though.

For the time being I feel confident about having taken this step in the hopes of increasing future production. Getting off to a basic start and having the next steps (configuration, integration tests) laid out feels comfortable.  Knowingly having added more depth to planning sessions.
