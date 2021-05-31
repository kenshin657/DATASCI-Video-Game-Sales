# Video Game Sales

![Image](games.jpg)

## Motivation

<div style="text-align: justify">
  
Video games has served the purpose as a way to escape the real world and into an imaginary world where people can focus on something they truly enjoy. It has become something allows us to de-stress and have fun while playing. It has also allowed friends and strangers to interact or play with each other creating stronger bonds no matter where you are in the world. This is more evident especially during these times of quarantine where people cannot simply meet each other. These video games gave a platform to people to continue to interact with each other and enjoy everyones presence even if it is just online. Video games has also lead to thousands of jobs around the world from game developers, to professional e-sport atheletes, and to livestreamers. Video games has opened countless opportunities for people to experience.
  
<br>
<br>

Over the past few decades, video games have slowly taken over the world by storm. From the introduction of the first commercially successful video game "Pong" to the present day cloud gaming services. The gaming industry has been alive for only around 49 years but it has become one of the largest profitable markets in the world. According to the Visual Capitalist, in 2020, the gaming industry was estimated to have earned a revenue of $165 billion. Gaming has become the biggest entertainment market by beating markets like television, film box office, and digital music. Through innovation and constant increase in popularity, it is said that its revenue forecast will hit $291 billion by 2027. It has been a couple of years now that the gaming industry has dominated the world market and has become a more accepted aspect of life for a majority of people around the world.

<br>
<br>
  
The visualization below (Made by Pelham Smithers) shows the rise of revenue earned by the gaming industry over the 49 year life span. It shows how different consoles affected the market by gaining pieces of it over the years. It also shows important releases made over the decades.
  
</div>

![Image](timeline.jpg)

<div style="text-align: justify">

The speed of how fast the gaming industry has grown has peaked the interest of our group hence we wanted to dwell deeper into the video game sales. We wanted to find out the different players or factors that come into play when it comes to high successful sales. We want to be able to find certain trends within the video game sales. We also want to find out who are the top conteders in their own category. Through this, we might be able to see what can make a successful game.
  
</div>


## Datasets Used

Before we dive into exploring the data regarding video game sales, we want to explain first the data set that we used. A data set is basically a file that contains thousands of information regarding a certain topic. For this research, we looked through a free public data set library website called Kaggle which allows people to download data sets provided by other people. After a bit of searching, we found a particularly good data set simply called Video Game Sales 2019. It contained all the information we needed. It had over 55,000+ games and had information like the game's genre, publisher, sales numbers, and esrb rating. 

![Image](2019.png)

The way the author (Abdulshaheed Alqunber) collected this data is through an automated trick called web scrapping wherein you write a certain script that will go through a specific website and collect information from it. The author based his web scrapping script of GregorUT's script which utilizes the Python library called "BeautifulSoup" which is a web scrapping library. They wanted to collect data from a verified source which is why they chose to scrape the data from VGChartz.com which is a public website that holds statistics on thousands of games from their release dates, to genres, and to their sales. So with that, they developed the script that went through the entire website and collected the data they needed. This is how the data that you will see later in the database was collected. This entire process may seem a bit sketchy but the authors made sure that what they are doing is legal and allowed by the website owners.

After getting the Video Game Sales 2019 dataset, we thought if we could possibly get a more updated database since the 2019 version is 2 years old already. The first thing that we did is to try to use the web scrapping script that the authors published in order to scrape the information ourselves. However, after thinkering and setting up the scripts, they didn't seem to run as intended. The script kept crashing and we noticed that the problem was related to the proxy server that we needed to use in order to connect to the site. After multiple failed attempts to find a working proxy, we decided to look for a more updated dataset in Kaggle. Thankfully, we were able to find a more recent version. 

The data set is called Video Game Sales 2020 which was based off the 2019 but was published by a different author. This version collected its data on July 7, 2020. We were happy with this update already. The biggest difference between the two datasets is that the 2020 version lacks the ESRB Ratings for the games. ESRB Ratings are essentially age-restriction labels placed by the ESRB Organization. This rating helps identify what age group can play said game. With this, we decided to just merge both the 2019 and the 2020 data sets together to create an updated complete dataset. Doing so allowed us to properly analyze and process the data easily. 

Now that we have our complete data set, we will now try to clean, analyze, and process the data so that it can be more useful for us later down the line.

## Cleaning & Analyzing The Data

Aside from merging the two datasets together we had to do some cleaning in the data set since we noticed some weird things. The first thing that we did is to check the number of "null" or empty values there are for each column. We noticed that there are some columns that had a lot of missing data. We needed to fill in this data somehow in order to have more consistent data. We did two major things to change the data. 

First is that we created a new column called "Total Sales". It can be noticed that there are 6 different columns that have sales value. So we decided to combine them into one column to show the total sales for that specific game title. The columns are total_shipped, global_sales, na_sales, jp_sales, pal_sales, and other_sales. We noticed that if total_shipped exists, global_sales doesn't and vice versa. So if either of them exists, then that becomes the total sales value. However, if neither exist, we added the sales from the four regional sales to create the total sales. After that, we were able to get a better view of the sales for each game.

The second adjustment we did was regarding the ESRB Rating, we noticed that there is a gigantic percentage of it that is missing data and might skew the results later down the line. At first we tried to look for other data sets that we can use to merge with our complete data set but we were not able to find a data set that had a similar format to ours. Others had more complex rating systems, different game title formatting, or even just a lack of games in general. So what we decided to do is to manually find the ESRB Rating for each of the game that had a total sale that is not 0. This was a tedious process since there were thousands of data points that we had to fill in. What added to the trouble is that there were games with no official rating so we were forced to leave them empty. In the end, we were able to fill up a good chunk of the missing data which we think is enough for our analysis down the line. 

After dealing with the empty values, we then removed some useless columns that did not help our analysis. We dropped the "Unnamed: 0", "img", and "last_update" columns since we didn't need their data anyways. With that, we finished processing our data set. The next section will explain the contents of the final data set.

## Contents of the Data Set

The data set has the following features

- 55845 games (36808 unique game titles)
- 77 unique consoles
- 20 unique genres
- 8 unique ESRB Ratings
- 3141 unique publishers
- 8189 unique developers
- 17 different feature columns

Each column has its own definition which is listed below.

- title - Name of the game
- console - The specific console the game is running on (PC, PS4, XBox, etc.)
- genre - The specific genre of the game (Action, MMO, Adventure, etc.)
- publisher - The company that published/distributed the game
- developer - The company that developed the game
- vg_score - The game rating provided by VGChartz
- critic_score - The game rating provided by game critics
- user_score - The game rating provided by the players
- total_shipped - Total copies solid (in millions)
- global_sales - Total sales earned (in millions)
- na_sales - Sales from North America (in millions)
- jp_sales - Sales from Japan (in millions)
- pal_sales - Sales from PAL (Most of Europe, Asia, Oceania, etc.) (in millions)
- other_sales - Sales from the rest of the world (in millions)
- release_date - The date the game was released
- ESRB_Rating - The official ESRB rating provided (Age restriction) (Everyone, Teen, Mature, etc.)
- Total_Sales - The total amount of sales earned by the game

With all the data available, we can finally do some analysis

## Exploratory Data Analysis (EDA)

To guide our analysis we created 10 research questions that we wanted to answer by the end of this study. The questions are as follows:

- What genre of games have the highest sales?
- What kind of ESRB ratings do top selling games have?
- Which publishers have received the most sales?
- What are the sales trends of certain games in different regions?
- Do certain regions lean towards specific game genres?
- On what platform do games receive more sales?
- What is the relationship between the critic & user scores to the game’s sales?
- Are newer games able to compare against older games with sales?
- What is the trend of newer video game releases per console?
- What are the top genres for the ESRB Ratings

We will be going through each question one by one and showing different visuals and how we understood the data.

### What genre of games have the highest sales?

In this section we show the top 20 genre and their total sales. The top 3 genres are shooter, sports, and action. These results are not surprising since franchises such as Call of Duty series, FIFA/2K series, or the BioShock series have been popular titles in their own genres. They have been releasing multiple titles under the same name which has lead to a hardcore following where fans keep buying the next series. This further increases the popularity of the genre which leads to even more games being developed in order to lure these fans to other games of the same genre. 

![Image](11.png)



###  What kind of ESRB ratings do top selling games have?

###  Which publishers have received the most sales? (Ky)
![Image](https://github.com/kenshin657/DATASCI-Video-Game-Sales/blob/main/images/topPubs.png)

###  What are the sales trends of certain games in different regions?

This section shows the top 10 games according to their total sales per region. For the NA graph, the games that showed up are understandable since NA is more into the shooter, action, adventure genre of games such as Grand Theft Auto and Call of Duty. These game titles have been popular in NA for quite some time now. For the JP graph, these are games mostly developed and released in Japan hence it has more japanese sales. Grand Theft Auto can be seen within the chart but the other Japanese games are still dominating the region. For PAL on the other hand, it is similar to the interests of the NA region except for the dominance of the sports genre, especially FIFA. FIFA holds a big portion of sales within the PAL region. The sports genre is famous around the European, South American, and South African areas, hence the growth of the sports genre in the region. Lastly, for the other regions, it is similar to the trends for the NA region with shooters and action games taking a big portion of the top 10. 

Overall, titles such as Grand Theft Auto and Call of Duty have been consistent in the 4 provided regions. Which can also explain the amount of sales genres like shooters and action are getting. These games have a big following all throughout the world. 

![Image](41.png)

![Image](42.png)

![Image](43.png)

![Image](44.png)

###  Do certain regions lean towards specific game genres?

In terms of game sales, there are 4 "regions" namely Japan(JP), North America(NA), Phase Alternate Line or PAL, and other regions not included in the first 3. In the first graph seen, all 4 regions highly gravite towards Sports Genre. This is understandable because Sports video games like NBA and FIFA release games every year and also on special events.

![Image](genre_region_melt.png)

Upon closer inspection, the top genre for each region slightly differs. For JP, the top genre would be Role-Playing while Sports in only second. For PAL, Action is the top genre while Sports is also only second. For both NA and other regions, Sports is the top while Action places second. Action being one of the top selling genres makes sense as it also has the most number of games in the dataset.

![Image](genre_region_indiv.png)

###  On what platform do games receive more sales? (Ky)
![Image](https://github.com/kenshin657/DATASCI-Video-Game-Sales/blob/main/images/top%2010%20game%20consoles.png)

###  What is the relationship between the critic & user scores to the game’s sales?

With this, there is not enough data to create a solid analysis on the relationship of critic/user score towards game sales since the ratings vary even with high/low selling games. One observation is that on average, users score games higher compared to critic scores. This is evident in the games above the top 50. The games in the top 50 seem to have higher critic scores than user scores. Though the scores for some games may be high, they do not show a lot of game sales. This needs to be validated by seeing how many critics or users scored that specific game to see how the scale is tipped.

As it can be seen in the scatterplot, the trends of the critic and user scores are similar to each other from the entire range of sales, may it be low or high sales.

![Image](7.png)

###  Are newer games able to compare against older games with sales?

###  What is the trend of newer video game releases per console? (Ky)
![Image](https://github.com/kenshin657/DATASCI-Video-Game-Sales/blob/main/images/trend.png)

###  What are the top genres for the ESRB Ratings?

This section shows the genmre of games popular for the top 3 ESRB ratings (Mature, Teen, and Everyone). For the everyone rating, famous genres are sports, miscellanous, puzzle, and racing games. These kinds of games are definitely for any age since they do not contain much violence, gore, or suggestive themes. These kinds of games stay true to their genre and replicate what they are trying to copy. Sports games like FIFA and 2K stay true to the rules of the sport. Racing games are focused on the racing aspect of the game, while puzzles are focused on the thinking aspect of games. For Teen and Mature, they have similar Top 3 genres which are role-playing, action, and shooter. These games now tend to have violence and sensitive themes within the game hence for such rating. The difference between the two are in the top 4 and 5. Teen has more fighting and strategy games. These games have mild violence only. Fighting games are just people punching or hurting one another while strategy games are mostly destruction based objectives. 

![Image](101.png)

![Image](102.png)

![Image](103.png)


## Concluding Remarks

## References
https://www.grandviewresearch.com/industry-analysis/video-game-market
https://www.reuters.com/article/sponsored/popularity-of-gaming
https://www.visualcapitalist.com/50-years-gaming-history-revenue-stream/
