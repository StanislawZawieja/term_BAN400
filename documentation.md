Group project BAN400: Exchange rate converter
---------------------------------------------

### Purpose
The purpose of this project is to create an application that interacts with a user to
convert exchange rates, and display visualize the comparison in different methods. The
user is free to choose between which two currencies within a time period they want to
compare.

### Packages
*Currency exchange rate converter* uses the *priceR* package to access currency exchange data which is necessary for its main functionality. *Tidyverse* packages make it convenient to build the app because of the ability to use pipes. The *Shiny* package is required to build the Shiny app, the *tidyr* package contains the *unite()* function which is useful for data wrangling. The *shinycssloaders* package contains *withSpinner()* which is used to produce a spinner while the plot is loading. The historical exchange rate data is displayed in a graph format using the *ggplot2* package. 

### Input
The user of *Currency exchange rate converter* can specify two different currencies and a range between two chosen dates. The three inputs, two strings with the currencies and one vector with two dates, are later used to generate outputs.

#### Currency inputs
The app uses *selectInput()* to prompt the user to input values for currency1 and currency2. The list of all available choices is supplied using *currencies()* from the *priceR* package. Default currencies are specified to be PLN and NOK. Because of the chosen input method the user is forced to make a selection only from the available currencies, so there is no need to test for correct inputs.

#### Date range input
The app uses *dateRangeInput()* to prompt the user to choose two dates which are the start and the end of the time period relevant for the user. The app will display historical currency data only for the chosen time period. The earliest and latest possible choices (01-01-2000 and the current date) correspond to the dates available in the *priceR* package. This is why there is no need to test whether the user entered a correct date. The input is formatted to have convenient default values, date display format, and week display format. The selection starts at the decade level which makes it easier to select a different year.

### Output
Our desired output for the Shiny App where to visualize the currency rates for the selected currency pair over the chosen time period. In addition, inform the user in text format about the current currency rate. However, if the user have chosen the same currency for both inputs, a warning message would pop up instead to notify the user.

First of all to get the desired text outputs, we must use *renderText()* from *shiny* package. This allow us to make a reactive version of the given function that also uses *base::cat()* to turn its result into a single-element character vector. Inside the first text output, the main function we use is *historical_exchange_rates()* which comes with the *priceR* package. It retrieves historical exchange rates between a currency pair in a given time period. However, this function can only take a currency code as its arguments, and therefore we use *sapply()* and *strsplit()* on the user inputs to extract only the three letter currency code. At last, when receiving the current rate of the currency pair, we use *paste()* function to paste it into a text.

In the other hand, to output the warning message we use a function based on an *if* statement to notify the user if the currency pair are alike. For better appearance, we uses *spans* from *tags* to visualize it in color red.  

#### Graph

When it comes to the plot output, we uses *renderPlot()* to render the reactive plot. The plot, in our case, is build with the *ggplot2* package using *ggplot()* function to graphically visualize it as mentioned above. Before writing the ggplot function, we must go through the similar steps as inside our first *renderText* function, to extract only the currency code. The difference this time is that the time period is not set on default as the current date, but instead it uses the users chosen date inputs.

To eliminate as much misunderstandings as possible, we uses *withSpinner()* function from *shinycssloaders* package as mentioned above to inform the user that the plot is loading when user changes the inputs. Note, that this is used in under the *mainPanel()* at the UI and not the server.  


Notes:
We considered displaying the historical exchange rates as a GIF, but it was impractical to do so due to a long rendering time of the plot.


