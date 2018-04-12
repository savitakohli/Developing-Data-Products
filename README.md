---
title: "Leaflet in R Markdown"
author: "Savita Kohli"
date: "April 11, 2018"
output:
  html_document: default
  
type: shiny
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
###Map plotted using leaflet and shiny packages.

```{r, eval=TRUE, echo=TRUE, warning=FALSE}
library(leaflet)
library(shiny)
ui <- fluidPage(
  dateInput(inputId = "n_date", label="Date: ", value = Sys.Date(),
            format = "dd-mm-yyyy", startview = "month",
            language = "en", width = NULL),
  leafletOutput("map")

)

server <- function(input, output, session) {

  dailyData <- reactive(cleanData[cleanData$Date == format(input$n_date, '%d/%m/%y')] )

  output$map <- renderLeaflet({  leaflet(dailyData) %>% addTiles() %>% 
     addMarkers(lat = 43.4804401, lng = -79.7111994, popup = "My Home in Oakville, Ontario, Canada")  })
}

shinyApp(ui, server)

```


