---
layout: post
title:      "My CLI Data Gem Portfolio Project"
date:       2020-10-20 21:42:54 +0000
permalink:  my_cli_data_gem_portfolio_project
---


Oh, what fun it has been!! Two weeks ago, i remember still being a little doubtful about this project and here i am at the end of it. It has been a great learning experience.
I made a CLI data gem that gives information about some of the best wineries in California. The scraping part was a little tricky for me. I was not able to find that many websites out there that provided somewhat decent data without being too verbose.

The site that had the information i wanted, did not have a very good html structure (not many css selectors targeting specific elements). However, i decided to take on the challenge. It was a little tricky and i had to come up with all sorts ideas to parse the data correctly but after i got a little hang of it, it all came together. Below is one of the parsing examples:
```
def self.winery_info_array
        array = @doc.css("div.entry-content p").map do |info|
            info.text
        end
				
        # remove '\n' from info and replace with ':'
        modified_array = array.map do |info|
            info.gsub("\n", ": ")
        end
        winery_info_array = []
        winery_info_array << modified_array[11..18] # Mendocino
        winery_info_array << modified_array[21..32] # Sonoma
        winery_info_array << modified_array[35..45] # Napa
        winery_info_array << modified_array[48..53] # East Bay
        winery_info_array << modified_array[56..60] # Monterey
        winery_info_array << modified_array[64..73] # Paso Robles 
       
        winery_info_array
    end
		```

I worked on the project bit by bit and that helped a lot. At the begining, trying to think through everything made it very complicated but with every progress made in the project, the next step revealed itself.

I followed the strategy from one of the example cli gem build videos and first focused on getting everything to working.
Then i started with my CLI controller file by slowly working to display the data the way i wanted to using just arrays that i had scraped and parsed. Then bit by bit,  i worked on building my wine region and winery classes; collaborating objects, initializing them, adding attributes and running my console and checking for return values numerous times. It was a tedious process, and took sometime to figure out, but I learnt a lot from it. It reminded me of one of my favorite quotes :-  "One must learn by doing the thing; for though you think you know it, you have no certainty until you try." - Sophocles

I am pretty happy with what i ended up with at the end, given that this is my first project ever building something from scratch. A simple step in the world of programming, but definitely a big and exciting one for myself!
Advice to my fellow students that are nearing this project or have started, go slow and work on your project with a clear mind. Be patient, it will all come together!







