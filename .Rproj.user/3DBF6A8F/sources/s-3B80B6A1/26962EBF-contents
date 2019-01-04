
list.of.packages <- c("flexdashboard", "httr", "highcharter", "shiny", "tidyverse")
new.packages <- list.of.packages[!(list.of.packages %in% installed.packages()[,"Package"])]
if(length(new.packages)) install.packages(new.packages)

library(flexdashboard)
library(httr)
library(highcharter)
library(shiny)
library(tidyverse)




# Data IN tildelinger

tilsagn_url <- "https://data.innovasjonnorge.no/api/files?filename=Tildelinger.csv&container=innovasjonnorge&subfolder=tildelinger/csv"
eos_url <- "https://data.innovasjonnorge.no/api/files?filename=TildelingerEOS.csv&container=innovasjonnorge&subfolder=tildelinger/csv"
rentestotte_url <- "https://data.innovasjonnorge.no/api/files?filename=TildelingerRS.csv&container=innovasjonnorge&subfolder=tildelinger/csv"

tilsagn <- read.csv(tilsagn_url, sep = ";", stringsAsFactors = FALSE)
eos <- read.csv(eos_url, sep = ";", stringsAsFactors = FALSE)
rentestotte <- read.csv(rentestotte_url, sep = ";", stringsAsFactors = FALSE)

tilsagn %>%
    count(`Næringshovedområde`) %>%
    arrange(n) %>%
    hchart(type = "treemap", hcaes(x = `Næringshovedområde`, value = n, color = n))

mapdata <- get_data_from_map(download_map_data("https://code.highcharts.com/mapdata/countries/no/no-all.js"))
hcmap("https://code.highcharts.com/mapdata/countries/no/no-all.js") %>%
    hc_title(text = "Norge")


hcmap("https://code.highcharts.com/mapdata/countries/no/no-all.js", data = eos, value = "Innvilget.beløp",
      joinBy = c("name", "Fylkesnavn"), name = "Tildelt", # @todo: lage variabel i tilsagn som tilsvarer hc-a2
                 dataLabels = list(enabled = TRUE, format = "{point.name}"),
                 borderColor = "#FAFAFA", borderwidth = 0.1,
                 tooltip = list(valueDecimals = 0))
