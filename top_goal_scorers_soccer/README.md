# Top International Goal Scorers in Men's Soccer: Pull from Wikipedia

Inspired by [this](https://github.com/tashapiro/tanya-data-viz/blob/main/tennis/womens-tennis.png) and [this](https://www.liamdbailey.com/post/making-beautiful-tables-with-gt/), I wanted to revisit building tables in R, specifically with the `gt::` package. I scraped data on top all-time international goal scorers in men's soccer from Wikipedia for the data.

## Notes  

I leaned heavily on this [example](https://www.liamdbailey.com/post/making-beautiful-tables-with-gt/) to build two tables -- one of top scorers, and one of top scorers grouped by confederation.

Some highlights:

*  Building clean tables with `gt::` is really fun, and putting the country flags on it was a nice polish.

To-do:

[] I'd like to fix the flag issue for the Hungarian player (haven't figured out why `recode()` isn't working)
[x] I should add in the periods that they played.
[] I should try to get the country label centered over the flags.
[] I could experiment with adding player images in the table.
[] UEFA only showing four scorers, which I should fix
[] I think a table or graphic on goals per match would be really cool

## Visualization  

![](https://github.com/mrafa3/viz_experiments/blob/main/top_goal_scorers_soccer/graphics/tbl_top_scorers.png)

![](https://github.com/mrafa3/viz_experiments/blob/main/top_goal_scorers_soccer/graphics/tbl_scorers_by_confed.png)
