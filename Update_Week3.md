Update: Week 3 Exercises
================

These are a additional exercises to practice more data wrangling on New
York City Flights 2013. Solve them in R first and then solve them in
python.

1.  Extend the file **hw-02-R.qmd** (respectively **hw-02-R.qmd**) on
    your own. Render it and make sure that headlines and text are
    formatted correctly.

    1.  Make a new headline “More data visualization”.
    2.  Write as plain text “In the following we provide some more
        information about the flights of different airlines, about the
        age or planes departing for the three New York airports and the
        weekly percipation on the three airports.”
    3.  For all following graphs use human readable axis labels and an
        informative title. (Hint for R: use `+ labs()`).

2.  **Graphs about airlines**

    1.  Create a chunk in which you visualize the following: On the
        y-axis you provide the names of all airlines. On the x-axis you
        provide bars which show the number of flights this airline
        operated. Order the airlines by the number of flights. Use the
        names of the airport in the graphic, not the carrier ID! Write a
        decriptive label for the x-axis and remove the label “Airline”
        on the y-axis. (Hints for R: You need to join data here! Avoid
        that text like “Joining with `by = join_by(carrier)`” appears in
        the html output. To that end, copy the join specification into
        the join command. There are different ways to construct the
        graphic either using `geom_bar` or first summarizing the data
        frame and then using `geom_col`. Use the second way. An easy way
        to summarize for this case is to use `count`. Use `fct_reorder`
        to order the airport names by the number of fights. Use
        `+ labs(...)` for customization of the axis labels.)
    2.  Create another chunk and visualize the mean departure delay by
        airline similarily. (Hints for R: Create the new variable for
        the mean departure delay with `summarize`.)  
    3.  (BONUS) Visualize the mean departure delay and the mean arrival
        delay with two bars (departure and arrival delay) for each
        airline side by side. (Hints for R: Use `pivot_longer` to create
        a column `delay_type` and `mean_delay`. Then assign `delay_type`
        to the `fill` aesthetic in the plot. Use `position = "dodge"` to
        make the bars side-by-side. Optional: Use `fct_reorder2` to
        create your order across `delay_type` and `mean_delay`).

3.  Graph the the **number of departing planes** by the **year they were
    manufactured** facetted by the three origin airports using the full
    airport names. (Hints for R: You have to join data here twice
    (planes and aiports to flights). Warning: There maybe a complication
    with variables names in planes. You could solve it by using
    `rename`. Further on, you have to check on which variables to join
    the airports. When you have the joined data frame, you can
    `group_by` the year manufactured and the airports from which they
    departed. `summarize` by counting the number of flights using the
    convenience function `n()`. Alternatively you could also use
    `count`. Make a ggplot using the count on the y-axis and the
    manufactured year on the x-axis. `facet_wrap` by the name of the
    airport of departure. With `facet_wrap` you can change the graph
    such that the facets are in one row or in one column. Try both and
    select the one, in which you can compare the distributions best.)

4.  Graph the total **weekly percipation** at the three airports with a
    line plot with lines of different color for each airport. (Hints for
    R: Practice string and date manipulations in the following way.
    Create a new variable `date` for which you first create a string
    which concatenates the variables `year`, `month`, and `day` into a
    string of the format “YYYY-M-D” using the function `paste` with a
    custom separator `sep = "-"`. Then apply the function `as.Date` to
    create the date variable in the `<date>` format. (Ignore the
    existing time_hour variable here to practice.) Now, use the function
    `week` to create a variables with the week number. Group by the week
    and the airport and sum the percipation of the week. Make a line
    plot using the week for x and the total percipation for y and the
    airport for color.)
