**Table des matières**
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [A propos](#a-propos)
- [Principes de base](#principes-de-base)
  - [``ui.R``](#uir)
  - [``server.R``](#serverr)
  - [Déploiement de l'application](#d%C3%A9ploiement-de-lapplication)
- [Intégration d'une carte Leaflet au sein d'une application Shiny](#int%C3%A9gration-dune-carte-leaflet-au-sein-dune-application-shiny)
  - [``ui.R``](#uir-1)
  - [``server.R``](#serverr-1)
- [Informations supplémentaires](#informations-suppl%C3%A9mentaires)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## A propos

Shiny est un outil développé par R Studio qui permet de réaliser des web app intéractives.
Un exemple du potentiel de Shiny est visible ici : [Statistiques descriptives du jeu de données *Iris* avec **Shiny**](http://iris.axelbellec.fr).
La documentation officielle de Shiny est disponible [ici](http://shiny.rstudio.com/tutorial/).

![Exemple de réalisation possible avec Shiny](http://i.imgur.com/RhESmuC.png?1)

## Principes de base 
Shiny est disponible sous la forme d'un package R. 
```r
# Installation et chargement du package Shiny
install.packages('shiny')
library(shiny)
```

Afin d'appréhender son fonctionnement, je vous conseille de regarder le simple exemple suivant. Tapez dans la console R : 
```r
runExample("01_hello")
```

Afin de créer un web app avec R, il est nécessaire de comprendre le fonctionnement de Shiny. 
On dispose de 2 scripts, un script nommé ``ui.R``(user-interface) qui permet de contrôler l'apparence et la mise en page de l'application. Le script ``server.R`` contient les instruction qui seront interprétées par le serveur.

Vous trouverez ci-dessous le code nécessaire pour bâtir l'application [Iris-Shiny](http://iris.axelbellec.fr). J'ai utilisé la majeure partie des fonctionnalités proposées par Shiny.
### ``ui.R`` 
```r
library(shiny)

# Define UI for dataset viewer application
shinyUI(fluidPage(
  
  # Application title
  titlePanel("Descriptive statistics of Iris dataset with R and Shiny Apps"),
  
  # Sidebar with controls 
  sidebarLayout(
    sidebarPanel(
      h3("Filtering data"),
      selectInput("dataset", "Choose a dataset (or a subset) :", 
                  choices = c("all iris data", "setosa", "versicolor", "virginica")),
      selectInput("Xvar", "X variable", 
                  choices = c("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width")),
      selectInput("Yvar", "Y variable", 
                  choices = c("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"), selected = "Sepal.Width"),
      numericInput("obs", "Number of observations to view on table:", 10),
      h3("K-Means"),
      numericInput("clusters", "Cluster count", 3, min = 1, max = 9),
      h3("DBSCAN"),
      sliderInput("eps", "Radius of neighborhood of each point", min = 0.0, max = 1.0, value = 0.2),
      sliderInput("minPoints", "Number of neighbors within the eps radius", min = 0, max = 10, value = 3),
      h3("Iris Data"),
      downloadButton("downloadData", "Download 'Iris.csv'", class = NULL)
    ),
    
    # MainPanel divided into many tabPanel
    mainPanel(
      tabsetPanel(
        tabPanel("Plot", h1("Scatterplot"), plotOutput("simplePlot"), h1("Boxplot"), plotOutput("boxPlot")),
        tabPanel("Descriptive statistics", h1("Descriptive statistics"),verbatimTextOutput("summary")),
        tabPanel("Table", h1("Table"), textOutput("NbRows"), tableOutput("view")),
        tabPanel("Clustering", h1("K-Means"), textOutput("NbClust"), plotOutput("kmeansPlot"), 
                 h1("Density-based cluster (DBSCAN)"), textOutput("dbscan_Param"), plotOutput("dbscanPlot"),
                 h1("Decision tree"), plotOutput("treePlot"))
      ) 
    )
  )
))
```

### ``server.R``
```r
library(shiny)
# Other useful packages
library(datasets)
library(rpart)
library(party)
library(fpc)

# Define colors
palette(c("#E73032", "#377EB8", "#4DAF4A", "#984EA3",
          "#FF7F00", "#FFDD33", "#A65628", "#F781BF", "#999999"))

# Define server logic 
shinyServer(function(input, output) {
  
  datasetInput <- reactive({
    switch(input$dataset,
           "all iris data" = iris,
           "setosa" = subset(iris, iris$Species == "setosa"),
           "versicolor" = subset(iris, iris$Species == "versicolor"),
           "virginica" = subset(iris, iris$Species == "virginica"))
  })
  
  colX <- reactive({
    switch(input$Xvar,
           "Sepal.Length" = iris$Sepal.Length,
           "Sepal.Width" = iris$Sepal.Width,
           "Petal.Length" = iris$Petal.Length,
           "Petal.Width" = iris$Petal.Width)
  })
  
  colY <- reactive({
    switch(input$Yvar,
           "Sepal.Length" = iris$Sepal.Length,
           "Sepal.Width" = iris$Sepal.Width,
           "Petal.Length" = iris$Petal.Length,
           "Petal.Width" = iris$Petal.Width)
  })
  
  clusters <- reactive({
    kmeans(iris[,1:4], input$clusters)
  })
  
  myColors <- reactive({
    switch(input$dataset,
    "all iris data" = c(palette()[1],palette()[2],palette()[3]),
    "setosa" = palette()[1],
    "versicolor" = palette()[2],
    "virginica" = palette()[3])
  })

  # Generate a summary of the dataset (or subset by Iris.Species)
  output$summary <- renderPrint({
    dataset <- datasetInput()
    summary(dataset)
  })
  
  # Show the first n observations
  output$view <- renderTable({
    head(datasetInput(), n = input$obs)
  })
  output$NbRows <- renderText({ 
    paste("You have selected to show ", input$obs," lines.")
  })
  
  
  # Show a simple x,y plot
  output$simplePlot <- renderPlot({
    
    df_iris <- datasetInput()
    plot(df_iris[,c(input$Xvar,input$Yvar)], xlab = input$Xvar, ylab = input$Yvar,
         main=toupper(ifelse(input$dataset == "all iris data", "iris", input$dataset)), pch=16, cex = 2,
         col = ifelse(df_iris$Species == "setosa", palette()[1], 
                ifelse(df_iris$Species == "versicolor", palette()[2], palette()[3])) )
    
    legend("bottomright", legend = unique(df_iris[,5]), 
           col = myColors(), title = expression(bold("Iris.Species")),
           pch = 16, bty = "n", pt.cex = 2, 
           cex = 0.8, text.col = "black", horiz = FALSE, inset = c(0.05, 0.05))
  })
  
  # Show boxplot
  output$boxPlot <- renderPlot({
    df_iris <- datasetInput()
    
    if (input$dataset == "all iris data") {
      boxplot(df_iris[,c(input$Yvar)] ~ df_iris[,5], xlab = "Species", ylab = input$Yvar, main = "IRIS", 
              border = "black", col = myColors())
    }
    else {
      boxplot(df_iris[,c(input$Yvar)], xlab = "Species", ylab = input$Yvar, main = toupper(input$dataset),
              border = "black", col = myColors())
    }
  })
  
  # K-Means Plot
  output$NbClust <- renderText({ 
    paste("K-means clustering performed with ", input$clusters," clusters.")
  })
  output$kmeansPlot <- renderPlot({
    plot(iris[,c(input$Xvar,input$Yvar)],
         col = clusters()$cluster,
         pch = 20, cex = 2)
    points(clusters()$centers, pch = 4, cex = 4, lwd = 4)
  })
  
  # Density-based cluster
  output$dbscan_Param <- renderText({ 
    paste("DBSCAN clustering performed with eps = ", input$eps," and minPts = ", input$minPoints,".")
  })
  output$dbscanPlot <- renderPlot({
    cluster <- dbscan(iris[,-5], eps = input$eps, MinPts = input$minPoints)
    plot(cluster, iris[,c(input$Xvar, input$Yvar)])
  })
  
  # Decision Tree
  output$treePlot <- renderPlot({
    ctree <- ctree(Species ~ ., data = iris)
    plot(ctree, type="simple")
  })
  
  # Create a .csv file with dataframe inside
  output$downloadData <- downloadHandler(
    filename = function() {
      paste('data-Iris-', Sys.Date(), '.csv', sep='')
    },
    content = function(con) {
      write.csv(iris, con)
    }
    )
  
})
```

### Déploiement de l'application
Avant de déployer l'application sur le web, vous devez vous enregistrer [ici](https://www.shinyapps.io/admin/#/signup). Il est aussi possible de créer un compte rapidement grâce à GitHub ou Google. Vous devez récupérer votre clés d'authentification [ici](https://www.shinyapps.io/admin/#/dashboard) (*step 3*) : appuyez sur le bouton ``{ secretButtonText }``.

![Bouton affichage clé](http://i.imgur.com/NujfAZt.png?1)

Déployez ensuite votre application à l'aide du code R suivant :    
```r
# Installation et chargement du package devtools
install.packages('devtools')
library(devtools)
# Install et chargement des packages shinyapps et packrat
devtools::install_github('rstudio/packrat')
devtools::install_github('rstudio/shinyapps')
library(packrat)
library(shinyapps)
# Autorisation d'accès à l'API
shinyapps::setAccountInfo(name='votre username shiny', 
                          token='votre clé token', 
                          secret='votre clé secrète')
# Déploiment
shinyapps::deployApp('/repertoire/vers/votre/dossier/') # répertoire du dossier contenant les script ui.R et server.R
```
Afin de vérifier que l'application a bien été déployée vous pouvez de nouveau vous rendre sur le [dashboard de Shiny](https://www.shinyapps.io/admin/#/dashboard), vous devrez voir apparaître le nom de votre application suivi de son état (*running*).
![Déploiement réussi](http://i.imgur.com/mZVoaKh.png?2)

## Intégration d'une carte Leaflet au sein d'une application Shiny
Il pourrait être utile durant le projet de savoir afficher des objets ayant des coordonnées `lat`/`lon`. On peut par exemple penser à afficher la position d'un chauffeur de taxi sur une carte. Au cas où cette éventualité se présenterait, voici un exemple de code `R` permettant d'intégrer au sein d'une Web App Shiny, une carte dynamique générée par Leaflet.

![Leaflet output with RShiny](http://i.imgur.com/xsYdtsX.png)

L'exemple intéractif est disponible ici : [Shiny - French Largest Cities](https://axelbellec.shinyapps.io/Shiny-FrenchCities)

### ``ui.R``
```r
library(shiny)
library(leaflet)
library(magrittr)

# Define UI for dataset viewer application
shinyUI(fluidPage(
  
  # Application title
  titlePanel("France - Largest Cities"),
  
  # Sidebar with controls 
  sidebarLayout(
    sidebarPanel(
      h3("Filtering data"),
      selectInput("dataset", "Choose a dataset (or a subset) :", 
                  choices = sort(c("all biggest cities", "Ile-de-France", "Provence-Alpes-Cote d'Azur", "Rhone-Alpes", 
                              "Midi-Pyrenees", "Pays de la Loire", "Alsace", "Languedoc-Roussillon", "Aquitaine", "Nord-Pas-de-Calais")))
    ), 

    # MainPanel divided into 2 tabPanels
    mainPanel(
      tabsetPanel(
        tabPanel("Plot", h1("Leaflet Map"), leafletOutput("leafletMap", width = "100%", height="700")),
        tabPanel("Table", h1("Data"), tableOutput("table"))
      ) 
    )
  )
))
```
### ``server.R``
```r
# Useful packages
library(shiny)
library(leaflet)
library(magrittr)

## Read our .csv data
df <- read.csv("www/french_cities.csv", sep=";")

## Formatting PopUps
df = within(df, {
  PopUp = paste("<b>",df$City, "</b>")
  PopUp = paste(PopUp, df$Region, df$Population, sep="<br>")
})

## Define a new icon 
cityLeafIcon <- makeIcon(
  iconUrl = "www/city.png",
  iconAnchorX = 10, iconAnchorY = 10,
  shadowUrl = "www/city.png"
)

# Define server logic 
shinyServer(function(input, output) {
  datasetInput <- reactive({
    switch(input$dataset,
           "all biggest cities" = df,
           "Ile-de-France" = subset(df, df$Region == "Ile-de-France"),
           "Provence-Alpes-Cote d'Azur" = subset(df, df$Region == "Provence-Alpes-Cote d'Azur"),
           "Rhone-Alpes"  = subset(df, df$Region == "Rhone-Alpes"),
           "Midi-Pyrenees" = subset(df, df$Region == "Midi-Pyrenees"),
           "Pays de la Loire" = subset(df, df$Region == "Pays de la Loire"),
           "Alsace" = subset(df, df$Region == "Alsace"),
           "Languedoc-Roussillon" = subset(df, df$Region == "Languedoc-Roussillon"),
           "Aquitaine" = subset(df, df$Region == "Aquitaine"),
           "Nord-Pas-de-Calais" = subset(df, df$Region == "Nord-Pas-de-Calais"))
  })
  
  ## Show the entire table of our dataset
  output$table <- renderTable({
    datasetInput()[1:5]
  })
  
  ## Create and show our Leaflet Map
  output$leafletMap <- renderLeaflet({
    df <- datasetInput()
    map <- leaflet() %>% 
      addTiles() %>% 
      setView(1.846033, 46.97068, zoom = 6) %>% 
      addMarkers(data = df, lng = ~ Longitude, lat = ~ Latitude, popup = df$PopUp, icon = cityLeafIcon)
    map
  })
  
})
```
## Informations supplémentaires

Si vous faite un ``commit`` de votre projet sur **GitHub**, il devient possible de partager facilement votre application. Par exemple si vous voulez montrer vos travaux à un autre groupe, ils pourront juste exécuter cette commande dans ``R`` : 
```r
runGitHub("nom du dépôt sur GitHub", "pseudo GitHub")
```
Exemple avec l'application Shiny-Iris : 
```r
runGitHub("Shiny-Iris", "belekkk")
```

Si vous avez des questions sur le fonctionnement de `Shiny`, vous pouvez me les poser à l'adresse mail suivante : [axel.bellec@outlook.fr](mailto:axel.bellec@outlook.fr).