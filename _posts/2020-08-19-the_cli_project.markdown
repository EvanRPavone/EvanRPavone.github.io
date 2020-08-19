---
layout: post
title:      "The CLI Project"
date:       2020-08-19 11:03:57 -0400
permalink:  the_cli_project
---


Sunday night I looked at the the first project, CLI Data Gem Portfolio Project, and I started to freak out because I had no idea where to begin and what to do the project on. What really helped me get out of this hole was the [CLI Gem Walkthrough](https://www.youtube.com/watch?v=_lDExWIhYKI) video which guided me through on what I needed to know.

# My Process
At first, I wanted to base my code off of videogames and scrape a website showing the genre of the videogame and the best videogame in that genre, but I was having a really difficult time with that so I decided to scrap that whole idea and go off something I know I can do.

My first ever job was in junior year of high school. It was with a company that built robots and I was the person to take the pictures the robots and put them on the website. I used HTML to organize and add the pictures to the pages. I knew the code so I knew that I could use the website for scraping data for my project. After I figured this out all of it blended together.

# My Code

In the CLI Gem Walkthrough video, it showed me how to setup all of my files to work together and what my files should be called.
The program that I created would scrape new robots that superdroid made by their category: Autonomous, robot kits, inspection, specialized, prebuilt, programmable, wifi and the new robot arms.
Once I figured out how to scrape one of the categories on the website in the Robots class (robots.rb), I was able to easily do it for rest of the categories.
```
    def self.scrape_autonomous
      doc = Nokogiri::HTML(open("https://www.superdroidrobots.com/shop/category.aspx/autonomous-robots/210/"))
      #binding.pry

      robot = self.new
      robot.category = "Autonomous Robots" 
      robot.name = doc.search("div.listname").first.text
      robot.desc = doc.search("div.listdesc").first.text
      robot.availability = doc.search("#ContentPlaceHolder1_columnrepeater div.messages").first.text
      robot.price = doc.search("#ContentPlaceHolder1_columnrepeater div.listprice").first.text
      robot.url = doc.search("div.listname a").first.attr("href")
      robot
    end
```

Once I got on the scraping to work, I was able to focus on how it would look in the terminal. To do this I would be coding in the cli.rb file for the CLI class.
```
    def list_robots 
      puts "Let's Take a Look at the new Superdroid Robots:"
      @robots = SuperDroidRobots::Robots.all 
      @robots.each.with_index(1) do |robot, i|
        puts "#{i}. "
        puts " - #{robot.category} -".strip 
		end
		
		def menu
      input = nil
      while input != "exit"
        puts "Enter the number of the robot to get more info or type list to see the robots again or type exit"
        input = gets.strip.downcase

        if input.to_i > 0 
          the_robot = @robots[input.to_i-1]
          puts "#{the_robot.name}".strip
          puts " - "
          puts "#{the_robot.availability}".strip
          puts " - "
          puts "#{the_robot.price}".strip
					
			 elsif input == "list" #If I put list it will then give me the list of robots from list_robots again
          list_robots
       elsif input == "exit"
          puts "I hope you found everything you were looking for!"
       else #if I put in a random input it will tell me to put a number associated to a robot, or put list, or exit
          puts "Did not understand. Please put the number related to the robot, type list to see the list again or type exit."
       end
		end
	end
```

After a lot of testing and binding.pry I was able to finally run the program with very small errors. The superdroid-env is the environment for the whole thing, this is what the user would use to start the CLI program by typing in the terminal ./bin/superdroid-env
Once the environment is put into the terminal the program would start and it would give out a list of all the robot categories with the newest robot.
```
Let's Take a Look at the new Superdroid Robots:
1. 
- Autonomous Robots -
VIPR - Configurable Compact Indoor Autonomous Platform
--------------
2.
- Robot Kits -
Configurable - IG52-SB4-T, Custom Size 4WD All Terrain Robot
--------------
- Inspection Robots -
Configurable - GPK-Zoom Wireless Tracked Inspection Robot with Zoom Camera
--------------
4.
- Specialized Robots -
Configurable - Lawn Mower Chassis Upfit Robot Package - WheelChair Motor System
--------------
5.
- Prebuilt Custom Robots -
NEW Prebuilt - 4WD IG42-SB-T Custom Size Robot
--------------
6.
- Programmable Robots -
Pololu Zumo Robot Kits
--------------
```

If the user wants to know more info about the robot they can put the number associated to the robot category they are interested in. This would return the name of the newest robot, the availability, price, the description and the URL to the robot.
```
Enter the number of the robot to get more info or type list to see the robots again or type exit
1 #My input
VIPR - Configurable Compact Indoor Autonomous Platform
 -
Built to Order: 10-16 weeks
 -
$16,900.00
 -
A compact autonomous robotic platform that's offers flexibility in both development and design. Capable of creating it's own path in both known and unknown areas. SLAM and other sensors allow for accurate obstacle avoidance!
```

They can repeat the list if they type list into terminal or they can put in another number associated to the robot. If they want to exit the program they can just type exit and it will say goodbye.
```
Enter the number of the robot to get more info or type list to see the robots again or type exit
exit #my input
I hope you found everything you were looking for!
Thank you for stopping by!
```

# What I Could Have Done Different
If I could have figured out the videogames program that I originally wanted to do, I would have stuck with that. The reason I say this is because I am a huge gamer and it would have been a lot of fun for me but I just couldnt figure out how to scrape the website because of how it was setup. 
The reason I chose to do superdroid instead was because I new the code of the website and I knew how it was setup making the scraping a little more easier. I also noticed that it takes a little bit of time to load the program once I call it in the terminal. If I could have found a way to shorten the load time, the program would be a lot better.


