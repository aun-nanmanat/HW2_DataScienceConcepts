README
================

# Homework 02

‼️ **Update:** [Week 3 Exercises](Update_Week3.md)

Exercises instructions of Week 2 below.

**Data Visualization and Data Wrangling with `nycflights13`.** A data
set about flights departing from the three New York City airports in
2013. This is a common practice data collection in data science.

## General instructions

This repo contains starter documents.

- Clone this repository to your local machine

In **Week 2** do the in R with RStudio: - Do the exercises below in the
file **hw-02-R.qmd**. - In git, add your changes, commit, and push it
back to this GitHub repository.

You have learned how to do the *git-GitHub dance* in Homework 01.  
If you do not know how to do it, do Homework 01 before.

In **Week 3** do the same in Python in the file **hw-02-py.qmd**.

## Instructions for R

Work in the file **hw-02-R.qmd**.

### Warm up with the *git-GitHub dance*

Fill in your name in the YAML and render. Stage the modified .qmd files
and add the html-files in Git and make a commit with message “Rendering
to html works”. Push this commit to GitHub.

### Data overview

1.  Run the first chunk `packages-data` such that the lines are executed
    in the console to load the tidyverse functions and the ny3cflight13
    data. See which dataframes are available in the Environment tab. The
    environment should be empty, but you can select
    “package:nycflights13” instead of “Global Environment” and you see
    values markes as `<Promise>`. Once you click on one or call it in
    the Console you see basic information there.

2.  Replace the “??” in the text with the actual numbers. Don’t write
    the numbers your self, but write *inline code* in which you output
    the number of rows of each data frame. In the document this already
    done for the `airlines`. See how the backticks `` ` `` with a
    starting `r` specify something like a small inline chunk. Render the
    document to see if it works. More information
    <https://quarto.org/docs/get-started/computations/rstudio.html#inline-code>

3.  Explore the datasets. Write `View(flights)` in the Console to see
    the data as a spreadsheet. Write `glimpse(flight)` to see an
    overview of all variables, their types and first values. As these
    dataframes come from a package there is also a Help page for each
    dataframe which you access with `?flights`. There you find short
    descriptions about each variable.

Write a nicely formatted short description about the variables `origin`,
`arr_delay`, and `dep_delay` from `flights` and `engine` and `seat` from
`planes`. Read about some markdown basics in the quarto documentation
<https://quarto.org/docs/authoring/markdown-basics.html>

### Data visualization

1.  We first want to know the distribution of values of the categorical
    variable `origin` in `flights`. To that end, make a bar chart. Read
    the Help `?geom_bar` and decide if you need to use `geom_bar` or
    `geom_col`. You can use the template below. Write your solution in
    the chunk `flightsorigin`. Test your line by sending it to the
    Console (with Ctrl + Enter). Once you are satisfied, render the
    document, commit the changes with message “First Visualization!” and
    push it. In the following, you can commit and push when you want.
    (Note, that we can provide help directly in your repo when you
    commit and push before.) This is the template.

``` r
ggplot(data = __________, mapping = aes(x = ________)) + 
  geom_TOSELECT()
```

2.  Now, we want to know the distribution of values of the numerical
    variable `distance` in `flights`. A common visualization is a
    histogram. Use `geom-histogram` with the same template, write the
    solution in the chunk `flightsdistance`, and test it. Notice, the
    red comment in the console. It advises to specify a binwidth. Test
    `binwidth = 5`, `binwidth = 50`, and `binwidth = 500` in
    `geom_histogram`, notice the difference (consult `?geom_histogram`)
    for details, and decide which shows the distribution best.

3.  In chunk `distributions` you see two ways to visualize the
    distribution of the number of `seats` in `airplanes` - points for
    each observation and a boxplot. (Read `?geom_boxplot` for more
    information). Note, that there are three ggplot objects (`g1`, `g2`,
    `g3`) which are shown combined with `g1 + g2 + g3` (using the
    `patchwork` package). Make the empty `g3` into a vertical histogram
    for the same data following the exercise before. Hint: For the
    vertical histogram assign `distance` to the `y` aesthetic and leave
    out the `x` aesthetic. Think about the advantages and disadvantages
    of each visualization.

4.  Now, we make the first plot which visualizes two variables, the
    categorical variable `engine`, and the numerical variable `seats` in
    `planes`. Use the template with aesthetics `x` and `y` and
    `geom_boxplot`. Put the solution into the chunk `engine-seats`

5.  Two numerical variables can be visualized with a scatter plot using
    `geom_point` and the aesthetics `x` and `y`. Let us look at
    `dep_delay` and `arr_delay` of `flights`. Warning: `flights` is very
    large! So, do not use `flights` in `data = _____` but a random
    sample of 10,000 flights `sample_n(flights, 10000)`. Now, let us add
    information about the categorical variable `origin` and assign it to
    the `color` aesthetic. Put your solution into the chunk `delays`.
    Test your solution several times and observe the changes in the
    visualization because of the random sampling. (Side questions: In
    which region are the changes in the visualization most
    *substantial*?)

6.  Finally, let us visualize the location of `airports` as points at
    their *longitude* and *latitude* (look up the variable names) and
    color them with the timezone `tzone` they are in. Put the solution
    into the chunk `airportlocations`.

### Data wrangling, pipes, and visualization

In the following, you have to solve some data wrangling tasks. For data
wrangling, the usage of the **pipe**, or a chain of pipes, is
convenient. You can also use the pipe to finish with a visualization.

<div>

> **Note**
>
> Since R version 4.1 There is a pipe operator in base-R `|>`. In
> earlier versions there is none, but there was already the pipe
> operator `%>%` from the package `magrittr` which is part of the
> `tidyverse` though not in the tidyverse core. Code you find on the
> internet may often use `%>%` instead of `|>`. There are only minor
> differences between the two, so your default should be to replace
> `%>% with`\|\>\`.

</div>

1.  Put the code snippet below into the chunk `flightsaveragespeed` and
    test it. The `mutate` line makes a new variable called `speed` which
    is the distance of the flight divided by the time in the air. The
    `select` line selects variables from the dataset. In this case, it
    selects `air_time` as the first, `distance` as the second, and the
    new `speed` as the third variable. All other variables are
    dropped.  
    The values in the new speed variable do not look like speeds of
    airplanes in km/h. Why? Because they are in miles/minute which we
    know from the variable descriptions. Modify the equation in the
    mutate command such that the values are in km/h. To that end, you
    have to divide air time by 60 and multiply distance by a certain
    factor. Look up the factor. Be careful with the order of
    mathematical operations and maybe use brackets `()`. Test your
    computation. Are the speed values reasonable?  
    Now, make a histogram of speed. Add another pipe after the `select`
    statement and write `ggplot(mapping = aes())` in the next line.
    Note, that you should not put `data = flights` into the argument of
    `ggplot()` this time! It is the mission of the pipe to do this. Fill
    out the `aes()` command accordingly, and add the geom for a
    histogram.

``` r
flights |> 
  mutate(speed = distance / air_time ) |> 
  select(air_time, distance, speed)
```

2.  Practice `filter` operations, which subsets certain observations of
    a dataframe. Write a line which filters the flights which
    1.  had an arrival delay of two or more hours
    2.  flew to Houston (IAH or HOU)
    3.  arrived more than two hours late, but didn’t leave late
    4.  started with a delay of at least an hour, but made up over 30
        minutes in flight. Put all four lines into the chunk
        `filtering`.
3.  Another common operation is summarizing data. Put the code below
    into the chunk `summarizing` and test it. You see the average delay
    at departure. (See `?mean` to learn what `na.rm = TRUE` is doing).
    Now, we want to know the average delay at departure for each of the
    three airports of `origin`. This can be done by adding the variable
    in a `.by = VARNAME` argument to the `summarize` command.

``` r
flights |> 
  summarize(mean_dep_deplay = mean(dep_delay, na.rm = TRUE))
```

<div>

> **Note**
>
> Grouping for a categorical variable before summarizing or mutating
> other variables is a very important tool and a very common operation.
> Another version of doing this is to add a line with
> `group_by(VARNAME) |>` before `summarize`. `group_by` adds some
> grouping information to the data frame which will then be taken into
> account by later operations. Older tidyverse code examples will use
> this operation. The results is the same. Having grouping information
> (unconsciously) in a dataframe objects can be a source of confusion.
> Therefore, the `.by = VARNAME` is now the default in tidyverse.

</div>

### Data Audit

Finally, you do a typical data audit task starting with the plot of
`airportlocations`. The airport locations show the shape of the United
States of America. (Do you recognize the shape, maybe distorted? You see
Alaska?) There are four airports on the right hand side which do not fit
that pattern. Filter `airports` such that you only see these four
airport. Write your solution into the chunk `stangeairportlocations`.
Check with internet research where these airports are located. Why are
the locations from the data as they are? Write your hypotheses for each
airport under the chunk in plain text.

### Ne

## Instructions for python

Work in the file **hw-02-py.qmd**.

### Warm up with rendering and the *git-GitHub dance*

Fill in your name in the YAML and render.

<div>

> **Note**
>
> - Find out your prefered way of rendering to html with quarto for
>   python and Visual Studio Code. As Visual Studio Code is multi
>   language it might not be easiest to customize a click and point
>   solution.
> - You can also render from a bash-Terminal with
>   `quarto render FILE_TO_RENDER.qmd`
> - Learn how to check the working directory (the folder where to
>   execute the command) and how to set it correctly.
> - Maybe also the quarto `.qmd` files work not well with code
>   highlighting and autocompletion out-of-the-box. If you are used to
>   Jupyter notebooks (.ipynb files), e.g. with JupyterLab (a
>   browser-based IDE) you may also work with these. quarto can also
>   render .ipynb files with `quarto render hello.ipynb --to html`. Read
>   more about the IDE you select at
>   <https://quarto.org/docs/get-started/hello/vscode.html> and
>   <https://quarto.org/docs/get-started/hello/jupyter.html>.

</div>

Stage the modified source files and add the html-files in Git and make a
commit with message “Rendering to html works”. Push this commit to
GitHub.

### Exercises

Follow the same instructions as for R, except for the code. You find
coding pointers in comments in **hw-02-py.qmd**. Note: Some more textual
questions can be omitted.
