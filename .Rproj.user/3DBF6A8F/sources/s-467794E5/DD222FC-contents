#
# This is a Shiny web application. You can run the application by clicking
# the 'Run App' button above.
#
# Find out more about building applications with Shiny here:
#
#    http://shiny.rstudio.com/
#

library(shiny)

# Define UI for application that draws a histogram
ui <- fluidPage(
   
   # Application title
   titlePanel("Tildelinger Innovasjon Norge"),
   
   # Sidebar with a slider input for number of bins 
   sidebarLayout(
      sidebarPanel(
        selectInput("Næringshovedområde", label = "Velg næring:",
                    choices = c("X - Uspesifisert",
                                "A1 - Jordbruk/Skogbruk",
                                "S - Annen tjenesteyting"),
                    multiple = TRUE),
        
        selectInput("Fylke", label = "Velg fylke:",
                    choices = c("Oslo", "Akershus"), multiple = TRUE),
        
        dateRangeInput("Innvilget.dato",
                       label = "Velg dato:", 
                       start = min("Innvilget.dato"),
                       end = max("Innvilget.dato"),
                       separator = " - ", 
                       format = "yyyy-mm-dd",
                       startview = "year",
                       weekstart = 1),
        
        selectInput("Virkemiddelgruppe", label = "Velg Virkemiddelgruppe:", choices = c("Fylkesvise BU-midler", "Landsdekkende programmer"), multiple = TRUE)   
      ),
      
      # Show a plot of the generated distribution
      mainPanel(
         plotOutput("Treemap")
      )
   )
)

# Define server logic required to draw a histogram
server <- function(input, output) {
   
   output$distPlot <- renderPlot({
      tilsagn %>%
        count(`Næringshovedområde`) %>%
        arrange(n) %>%
        hchart(type = "treemap", hcaes(x = `Næringshovedområde`, value = n, color = n))
   })
}

# Run the application 
shinyApp(ui = ui, server = server)

