---
title       : Pizza Ordering
subtitle    : Reproducible Pitch Presentation
author      : Tommy Ho
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [bootstrap]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Pizza Ordering, a Shiny App (Slide 1)

For a copy of the Shiny App
- URL: *https://tommyho.shinyapps.io/devdataprod-002/*
- Hosted by **shinyapps.io**
- GitHub: *https://github.com/tommykho/devdataprod-002/*
- ShinyApp that calculates the order amount from number of pizza and their size
- Download code:

```
git clone https://github.com/tommykho/devdataprod-002.git
```

--- .class #id 

## ui.R (Slide 2)

```
library(shiny)
library(shinyapps)

shinyUI(pageWithSidebar(
  headerPanel("Pizza Ordering"),
  sidebarPanel(
    numericInput('mQty', 'Quantity', 1, min = 1, max = 10, step = 1),
    radioButtons("mSize", "Size",
                 c("6' Personal ($5)" = 5,
                   "8' Small ($8)" = 8,
                   "10' Medium ($12)" = 12,
                   "12' Large ($18)" = 18,
                   "14' Extra Large ($24)" = 24),
                 selected = 12),
    checkboxGroupInput("mToppings", "Toppings",
          c("Pepperoni, Classic" = "P",
          "Sausage, Italian" = "S",
          "Ham" = "H",
          "Chicken, Grilled" = "GC",
          "Bacon, Pieces" = "BP",
          "Olives, Black" = "BO",
          "Peppers, Green" = "GP",
          "Pineapple" = "PA")),
    dateInput("mDate", "Pickup Date:"),
    sliderInput("mTime", "Pickup Time (1 - 9 PM):", 1, 9, 1, step = 1,
                round = FALSE, format = "#,##0", locale = "us",
                ticks = TRUE, animate = FALSE),
    actionButton("mPrint", label = "Print")
  ),
```

--- .class #id 

## server.R (Slide 3)

```
shinyServer(
  function(input, output) {
    output$odate <- reactive({paste(input$mDate,"(",input$mTime,"PM )")})    
    output$oqty <- reactive({input$mQty})
    output$otoppings <- reactive({input$mToppings})
    output$osauce <- reactive({input$mSauce})
    output$osize <- reactive({input$mSize})
    output$oprint <- reactive({as.numeric(input$mPrint)})
    output$oamount <- reactive({paste("$", input$mQty * as.numeric(input$mSize), 
                                      "for", {input$mQty}, "pizza(s)")})
  }
)
```

--- .class #id 

## R in action within Slidify (Slide 4)

R calculates Medium Pizza Price as table

```r
mQty <- 1:10
oAmount <- 12 * x
df <- data.frame(mQty, oAmount)
df
```

```
##    mQty oAmount
## 1     1      12
## 2     2      24
## 3     3      36
## 4     4      48
## 5     5      60
## 6     6      72
## 7     7      84
## 8     8      96
## 9     9     108
## 10   10     120
```

--- .class #id 

## R in action within Slidify (Slide 5)

R plots Medium Pizza Price as graph


```r
mQty <- 1:10
oAmount <- 12 * mQty
plot(mQty, oAmount)
```

![plot of chunk simpleplot](assets/fig/simpleplot.png) 

