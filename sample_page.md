# Kawhi T-Shirt Reselling

## Background
I was in Rittenhouse Square, Philadelphia, with a few minutes to kill, and I came across a New Balance store. I went in (with zero intention to buy anything) and saw that they were selling shirts with Kawhi slogans on them.

I absolutely love Kawhi as a player, despite the protest from the most bitter aspects of my Sixers fandom.
<br>
<img src="images/tenor.gif?raw=true"/>
<br>
<img src="images/shirt_gallery.png?raw=true"/>
<br>

For $30, I had to snag one. I chose a black “Fun guy” shirt. That evening, I googled the shirt, and discovered that they were going for more on StockX. I knew right away that there was an opportunity to resell the shirts and turn a profit.

<img src="images/stockx_shirt.png?raw=true"/>

## Getting data and some basic graphs

StockX makes selling data available, so I copied it into RStudio, adding columns for color and slogan (“Fun guy” or “Board man gets paid”). My goal was to see what was the optimal shirt for reselling.

<img src="images/stockx_graph.png?raw=true"/>

I made a simple bar graph to see how often each slogan, shirt size, and color was selling. If I were to resell the shirts, I would not want to take on too much inventory risk, so I should probably choose a shirt that sells the most often. It appears that the “board man” slogan, medium, large, and extra large sizes, and black shirts sell the most frequently.

<img src="images/slogan_bar.png?raw=true"/>
<img src="images/size_bar.png?raw=true"/>
<img src="images/color_bar.png?raw=true"/>

I then wanted to see how each combination of slogan and size compared to each other in terms of price.

<img src="images/facet_box.png?raw=true"/>

Although the range of the “board man” shirts’ prices is much smaller due to their larger sample size, “fun guy” shirts have fetched a much larger sum. I created the same sort of graph again, but instead substituted color in for slogan.

<img src="images/color_facet_box.png?raw=true"/>

It appears that the prices for “black” vs. “white” are similar, with black shirts maybe going for a little more amongst the “M”, “L”, and “XL” sizes.

<br>

Before I modeled anything out, I wanted to see how the prices have been trending over time, because I didn’t want to take my sweet time only to discover that my window of opportunity had vanished.

<img src="images/time_price_point_all.png?raw=true"/>

Yikes! I better get to work because the longer I wait, the less I’ll make.

<img src="images/facet_point.png?raw=true"/>

It looks like this downward trend holds true across all shirts as well. Ok, enough talk. Let’s make a model.

## Modeling shirt price

My goal is to predict the price of a shirt using slogan, size, color, and time as predicting variables. The time variable is not for choosing which shirt to buy, because I would sell every shirt at the same time (as soon as I can), but it is helpful in predicting how much the shirts will go for. Using multiple linear regression, I made a model using these variables.

<img src="images/model_summary.png?raw=true"/>

Using the model, I add predictions to the data, then calculating each row’s residual and the overall RMSE, which was 27.4. Not so good, but should still give us some interesting insights.

## Choosing shirts

I made a table with every combination of slogan, size, and color, as well as a date of July 1, 2019 for every row. Using this table, I added predictions with the model, and sorted by prediction.

<img src="images/prediction_tibble.png?raw=true"/>

Surprisingly, when I checked StockX, the black “board man” combination were receiving substantially larger bids than white or “fun guy” shirts. Not so coincidentally, the New Balance store was all sold out of them when I went back. I’m not quite sure why my model did not predict this. Kawhi wore the black “board man” shirt to the parade, so maybe that had something to do with it.

<div style="width:image width px; font-size:80%; text-align:center;"><img src="images/kawhi_parade.jpg?raw=true"/>Pictured: a fun guy having a fun time about to get paid.</div>

At the New Balance store I picked up 2 large “fun guy” shirts in black (the model’s top choice) and one in white (all they had left). I immediately flipped them on StockX to avoid depreciation. The shirts sold for $45, $45, and $46 dollars, and after StockX’s fee (14%!), I ended up profiting $26.92. I guess it’s not just the board man who gets paid, huh. I probably could have flipped a couple more shirts, but it wouldn’t have been worth the risk of getting stuck with them, and the point of all this was to demonstrate a cool use of modeling, rather than making a few bucks.

<br>

Thanks for reading, and of course, if you have questions, suggestions, or want to share something similar that you’ve been working on, don’t hesitate to email me at leojacoby@gmail.com or tweet at me at @leotheprocess21.
