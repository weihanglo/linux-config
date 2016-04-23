#------------------------------------------------------------------------------#
#                                   Rprofile                                   #
#                                                                              #
#            Modified at Fri Feb 26 13:33:03 CST 2016 by Weihang Lo            #
#------------------------------------------------------------------------------#

#################################################################
#interactive load .Rprofile START
if (interactive()) {

#-----------------------------
# Autoload packages
#-----------------------------
if (library(colorout, logical.return = TRUE)) {
    message(base::sprintf("colorout %s loaded",
        as.character(utils::packageVersion("colorout"))))
}

if (Sys.getenv("NVIMR_TMPDIR") != "") {
    options(nvimcom.verbose = 1)
    library(nvimcom)
}

#-----------------------------
# Autoload functions
#-----------------------------
autoload("%>>%", "pipeR")
autoload("data.table", "data.table")
autoload("fread", "data.table")
autoload("microbenchmark", "microbenchmark")
autoload("ggplot", "ggplot2")
message("\nAutoloaded Functions...\n", paste("\n--", ls("Autoloads")))


#-----------------------------
# Useful packages list
#-----------------------------

#---Prerequisite---
# devtools
# colorout
# vimcom or nvimcom
#install.packages("devtools")
#devtools::install_github("jalvesaq/colorout")
#devtools::install_github("jalvesaq/VimCom")
#devtools::install_github("jalvesaq/nvimcom")

#---General---
# doParallel
# data.table
# microbenchmark
# rmarkdown ---> require: pandoc
#install.packages(c("doParallel", "data.table", "microbenchmark", "rmarkdown"))

#---Plot---
# rgl ---> require: freeglut-devel
# plotly
# ggplot2
# gridExtra
# animation ---> require: ImageMagick
#install.packages(c("rgl", "plotly", "ggplot2", "gridExtra", "animation"))

#---Spatial analysis---
# spatstat
# raster
# rgeos
# rgdal ---> require: gdal, gdal-devel, proj...
# ggmap
# leaflet
#install.packages(c("spatstat", "raster", "rgeos", "rgdal", "ggmap", "leaflet"))

#---Data I/O---
# RMySQL
# RSQLite
# RPostgreSQL
# rmongodb
# readxl
#install.packages(c("RMySQL", "RSQLite", "RPostgreSQL", "rmongodb", "readxl"))

#---Ecology---
# vegan

#---Web related---
# XML
# RCurl
# rvest
# selectr
# jsonlite
#install.packages(c("rvest", "RCurl", "XML", "selectr", "jsonlite"))

#---Machine learning---
# rpart
# party
# randomForest
# e1071
#install.packages(c("rpart", "party", "randomForest", "e1071"))

#---Text mining---
# tm
# tmcn --> on R-forge
# jiebaR
# wordcloud
# SnowballC
# LSAfun
#install.packages(c("tm", "tmcn", "jiebaR", "wordcloud", "SnowballC", "LSAfun"))

#---Scientific computing---
# rootSolve
# deSolve
#install.packages(c("rootSolve", "deSolve"))


#-----------------------------
# Set options
#-----------------------------

#---Set CRAN mirror---
local({
        r <- getOption("repos")
        r["CRAN"] <- "http://cran.csie.ntu.edu.tw/"
        options(repos = r)
})

#---Set prompt---
options(continue = ". ")


#-----------------------------
# Convenient function
#-----------------------------

#---rm all---
.rm <- function(...) rm(list=ls(1), pos=1, ...)

#---Improved ls---
.ls <- function (pos = 1, pattern, order.by, decreasing=FALSE) {
    if(length(ls(pos = pos, pattern = pattern))==0) stop("Nothing found.")
    nply <- function(names, fn) sapply(names, function(x) fn(get(x, pos)))
    names <- ls(pos = pos, pattern = pattern)

    obj.class <- nply(names, function(x) as.character(class(x))[1])
    obj.mode <- nply(names, mode)
    obj.type <- ifelse(is.na(obj.class), obj.mode, obj.class)
    obj.size <- nply(names,
        function(x) format(utils::object.size(x), units = "auto")
    )

    obj.dim <- t(nply(names, function(x) as.numeric(dim(x))[1:2]))
    vec <- is.na(obj.dim)[, 1] & (obj.type != "function")
    obj.dim[vec, 1] <- nply(names, length)[vec]

    out <- data.frame(obj.type, obj.size, obj.dim)
    names(out) <- c("Type", "Size", "Rows", "Columns")

    if (!missing(order.by)) out <- out[order(out[[order.by]]), ]
    out
}


#-----------------------------
# Start & Exit
#-----------------------------

.First <- function() {
    try(utils::loadhistory("~/.Rhistory"))
    message("\n\nSuccessfully loaded .Rprofile at ", date())
}

.Last <- function() {
    try(utils::savehistory("~/.Rhistory"))
    message("\nExit R session at ", date())
}

#interactive load .Rprofile END
}
