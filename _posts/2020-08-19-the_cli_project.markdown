---
layout: post
title:      "The CLI Project"
date:       2020-08-19 15:03:56 +0000
permalink:  the_cli_project
---


Sunday night I looked at the the first project, CLI Data Gem Portfolio Project, and I started to freak out because I had no idea where to begin and what to do the project on. What really helped me get out of this hole was the [CLI Gem Walkthrough](https://www.youtube.com/watch?v=_lDExWIhYKI) video which guided me through on what I needed to know.

# My Process
At first, I wanted to base my code off of videogames and scrape a website showing the genre of the videogame and the best videogame in that genre, but I was having a really difficult time with that so I decided to scrap that whole idea and go off something I know I can do.

My first ever job was in junior year of high school. It was with a company that built robots and I was the person to take the pictures the robots and put them on the website. I used HTML to organize and add the pictures to the pages. I knew the code so I knew that I could use the website for scraping data for my project. After I figured this out all of it blended together.

# My Code

In the CLI Gem Walkthrough video, it showed me how to setup all of my files to work together and what my files should be called.
![My file layout](https://gyazo.com/51447d270a792290c20e1253b6f7e5e4)
The program that I created would scrape new robots that superdroid made by their category: Autonomous, robot kits, inspection, specialized, prebuilt, programmable, wifi and the new robot arms.
Once I figured out how to scrape one of the categories on the website in the Robots class (robots.rb), I was able to easily do it for rest of the categories.
![Autonomous Category](https://gyazo.com/55a313b458ccb60b3aaa3ee02a721d7b)
Once I got on the scraping to work, I was able to focus on how it would look in the terminal. To do this I would be coding in the cli.rb file for the CLI class.
![CLI class](https://gyazo.com/edf06adee9b69e6fad1d7a24b615bc9e)
After a lot of testing and binding.pry I was able to finally run the program with very small errors. The superdroid-env is the environment for the whole thing, this is what the user would use to start the CLI program by typing in the terminal ./bin/superdroid-env
![superdroid-env](https://gyazo.com/b2081fd3d27e71c690726688295a7080)
![Calling superdroid-env](https://gyazo.com/3e2bdc8edcdc0d5859e98af2f0c58e49)
Once the environment is put into the terminal the program would start and it would give out a list of all the robot categories with the newest robot.
![Program Starts](https://gyazo.com/49d7e6656198c62cdd45308235880ae4)
If the user wants to know more info about the robot they can put the number associated to the robot category they are interested in. This would return the name of the newest robot, the availability, price, the description and the URL to the robot.
![The Program](https://gyazo.com/a7f5d9892a6f6fd7b79f7e99876e2b48)
They can repeat the list if they type list into terminal or they can put in another number associated to the robot. If they want to exit the program they can just type exit and it will say goodbye.
![Exit](https://gyazo.com/8fdab5fee258ba6a1312ce0d9efd3c16)

# What I Could Have Done Different
If I could have figured out the videogames program that I originally wanted to do, I would have stuck with that. The reason I say this is because I am a huge gamer and it would have been a lot of fun for me but I just couldnt figure out how to scrape the website because of how it was setup. 
The reason I chose to do superdroid instead was because I new the code of the website and I knew how it was setup making the scraping a little more easier. I also noticed that it takes a little bit of time to load the program once I call it in the terminal. If I could have found a way to shorten the load time, the program would be a lot better.


