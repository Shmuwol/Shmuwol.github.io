---
layout: post
title: "Scoring My First ruby Gem"
categories: [ruby]
---


Before I get into the technical details, let me just jot down my initial idea and then I'll attempt to break down how it was done.

As part of [Flatiron School][6]'s [remote][7] Full Stack Development course, I was instructed to create a CLI scraper Ruby Gem As a solo challenge that will be reviewed upon completion by a senior instructor as an assessment.

***

### Gem Requirements

1. _Package as a gem_
2. _Provide a CLI on gem installation._
3. _CLI must provide data from an external source, whether scraped or via a public API._
4. _Data provided must go at least a level deep, generally by showing the user a list of available data and then being able to drill into a specific item._


### Coming up with with a Gem idea

This was the first time as a Web Development student that I had to come up with an idea for a project and code it on my own, so naturally I turned to my other love, Baseball, I was to create a CLI gem to give me the MLB scores with a focus on the Yankees.

I have to admit, I was pretty overwhelmed at first, I felt like a kid removing the training wheels from a bike while learning how to ride, I fell, _scraped_ (pun!) my knee and for a while I was kinda scared to ride my ruby bike again, and regretfully procrastinated a bit longer than I hoped I would, but after watching some Videos I got it done and I must say, the joy I got when it finally came together reminded me why I love code and why I'm doing this.

***

### MLB API

While looking for a data source for my gem I first tried scraping mlb.com and ESPN using Nokogiri, the problem I encountered was both sites were using some sort of page rendering and I wasn't getting any of the data I wanted, and then I found the holy grail, MLB API. my first impression was, SO MUCH DATA!

***
![][8]{: .img-responsive }

***

The good thing about a lot of data is that you have lot of data, the bad part of a lot of data is.. A _lot_ of data. It can be pretty overwhelming for a newbie to work with API's, especially a data heavy API like MLB, baseball after all, is a game of numbers.

While I was trying to make sense of the copious amount of data thrown at me I was hoping there would be some sort of documentation for the MLB API but I couldn't find anything useful so I'll try my best to document the data I used and how to find it and some perhaps some code examples.

***

### Where to begin

MLB's API can be found at [http://gd2.mlb.com/components/][1] and it looks like this:



![][9]{: .img-responsive }



***

The url can be broken down in 3 parts as follows;

1. [http://gd2.mlb.com/components/game/mlb/][10]
2. [year_2009/month_11/day_04][11]
3. [/master_scoreboerd.json][12]

***

This first part of the URL will get you to the index of all the way back to 1927, there are some earlier indices but 1927 is the first year with a scoreboard.

The second part selects the year and month and day, this gives you yet another index with 'stuff', but still no Json, this json dude is really playing hard to get… but we're almost there.

Finally we have [/master_scoreboerd.json][12], the elusive json we've been looking for, we finally have the json we need!

***

![][13]{: .img-responsive }

***



### My Gem

To conclude this post I'll try to sum up a few of the interesting stuff I learned in the process of this project.

1. [Ordinalize][14] numbers with the `num.ordinalize` method can be done by including the [activesupport][15] gem that is built in to Rails, it allows you to correctly ordinalize numbers, like 1st, 2nd and 3rd. I used it in my gem to ordinalize the innings.
2. Json is pretty much a giant hash, so knowing your way around hashes is pretty useful
3. The [Date][16] module that comes with ruby is pretty cool, you get access to all the awesomeness by requiring the module.

Check out my gem on [GitHub][17] or on [RubyGems.org][18] or reach out to me on [Twitter][19]

***
![yankee_score][2]{: .img-responsive }

***







[1]: http://gd2.mlb.com/components/
[2]: /static/img/gem_gif.gif
[6]: http://flatironschool.com/
[7]: http://learn.co
[8]: /static/img/data.gif
[9]: https://cdn-images-1.medium.com/max/800/1*BNdJcxTgkUSDx5REkGfmig.png
[10]: http://gd2.mlb.com/components/game/mlb/year_2016/month_04/day_09/master_scoreboard.json
[11]: http://gd2.mlb.com/components/game/mlb/year_2009/month_11/day_04/
[12]: http://gd2.mlb.com/components/game/mlb/year_2009/month_11/day_04/master_scoreboard.json
[13]: https://cdn-images-1.medium.com/max/800/1*M9PG9p0H23dd8sZjee-MRg.jpeg
[14]: http://www.merriam-webster.com/dictionary/ordinal%20number
[15]: https://rubygems.org/gems/activesupport
[16]: http://robdodson.me/playing-with-ruby-dates/
[17]: https://github.com/Shmuwol/yankee_score
[18]: https://rubygems.org/gems/yankee_score
[19]: https://twitter.com/ShmullyWolfson
