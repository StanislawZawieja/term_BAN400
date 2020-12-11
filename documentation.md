Group project BAN400: Exchange rate converter
---------------------------------------------

## Purpose
The purpose of this project is to create an application that interacts with a user to
convert exchange rates, and display visualize the comparison in different methods. The
user is free to choose between which two currencies within a time period they want to
compare.

## Packages
*Currency exchange rate converter* uses the *priceR* package to access currency exchange data which is necessary for its main functionality. *Tidyverse* packages make it convenient to build the app because of the ability to use pipes. The *Shiny* package is required to build the Shiny app, the *tidyr* package contains the *unite()* function which is useful for data wrangling. The *shinycssloaders* package contains *withSpinner()* which is used to produce a spinner while the plot is loading. The historical exchange rate data is displayed in a graph format using the *ggplot2* package. 

## Input
The user of *Currency exchange rate converter* can specify two different currencies and a range between two chosen dates. The three inputs, two strings with the currencies and one vector with two dates, are later used to generate outputs.

### Currency inputs
The app uses *selectInput()* to prompt the user to input values for currency1 and currency2. The list of all available choices is supplied using *currencies()* from the *priceR* package. Default currencies are specified to be PLN and NOK. Because of the chosen input method the user is forced to make a selection only from the available currencies, so there is no need to test for correct inputs.

### Date range input
The app uses *dateRangeInput()* to prompt the user to choose two dates which are the start and the end of the time period relevant for the user. The app will display historical currency data only for the chosen time period. The earliest and latest possible choices (01-01-2000 and the current date) correspond to the dates available in the *priceR* package. This is why there is no need to test whether the user entered a correct date. The input is formatted to have convenient default values, date display format, and week display format. The selection starts at the decade level which makes it easier to select a different year.

## Output - Imran

### Graph - Imran

Notes:
We considered displaying the historical exchange rates as a gif, but it was impractical to do so due to a long rendering time