Group project BAN400: Exchange rate converter
---------------------------------------------
# Group 99

## Purpose of this project - Nina

## Packages - Stan

## Input - Stan

### Graphical user interface - Nina

## Output - Imran

Our desired purpose for the Shiny App where to visualize the currency rates for the chosen currencies over the chosen time period. In addition, message the user in text format about the current currency rate. However, if the user have chosen the same currency for both inputs, a warning message would pop up instead to notify the user.

First of all to get the desired text outputs, we must use renderText() from shiny package so that we can make a reactive version of the given function which also uses base::cat() to turn its result into a single-element character vector. Inside the first text output, the main function we use is historical_exchange_rates() which comes with the priceR package. It retrieves historical exchange rates between a currency pair in a given time period. However, this function can only take a currency code as arguments, and therefore we use sapply() and stringsplit() on the user inputs to extract only the currency code. At last, when receiving the current rate of the currency pair, we use paste() function to implement it into a text.

In the other hand, to output the warning message we use a function based on an if statement to notify the user if the currency pair are alike. For better appearance, we uses "spans" from "tags" to visualize it in color red.  

### Graph - Imran

When it comes to the plot output, we uses renderPlot() to render a reactive plot. The plot, in our case, is build with the ggplot2 package using ggplot() function to graphically visualize it. Before writing the ggplot function, we must go through the similar steps as inside our first renderText function, to extract only the currency code. The difference is that the time period is now not set by default as the current date, instead it uses the users chosen time period.

To eliminate as much misunderstandings as possible, we uses withSpinner() function from "shinycssloaders" to inform the user that the plot is loading after user changes the inputs. Note, that this is used in under the mainPanel() at the UI. 
