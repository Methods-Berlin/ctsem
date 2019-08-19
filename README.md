
<!-- README.md is generated from README.Rmd. Please edit that file -->

[![Build
Status](https://travis-ci.org/cdriveraus/ctsem.svg?branch=master)](https://travis-ci.org/cdriveraus/ctsem)

See the NEWS file for recent updates\!

ctsem allows for easy specification and fitting of a range of continuous
and discrete time dynamic models, including multiple indicators (dynamic
factor analysis), multiple, potentially higher order processes, and time
dependent (varying within subject) and time independent (not varying
within subject) covariates. Classic longitudinal models like latent
growth curves and latent change score models are also possible. Version
1 of ctsem provided SEM based functionality by linking to the OpenMx
software, allowing mixed effects models (random means but fixed
regression and variance parameters) for multiple subjects. For version 2
of the R package ctsem, we include a Bayesian specification and fitting
routine that uses the Stan probabilistic programming language, via the
rstan package in R. This allows for all parameters of the dynamic model
to individually vary, using an estimated population mean and variance,
and any time independent covariate effects, as a prior. ctsem is
documented in a JSS publication (Driver, Voelkle, Oud, 2017), and in R
vignette form at
<https://cran.r-project.org/package=ctsem/vignettes/ctsem.pdf> . The
Bayesian approach is outlined in Introduction to Hierarchical Continuous
Time Dynamic Modelling with ctsem, at
<https://github.com/cdriveraus/ctsem/raw/master/vignettes/hierarchicalmanual.pdf>
. To cite ctsem please use the citation(“ctsem”) command in R.

To install the github version, use:
remotes::install\_github(‘cdriveraus/ctsem’, INSTALL\_opts =
“–no-multiarch”, dependencies = c(“Depends”, “Imports”))

Troubleshooting Rstan / Rtools install for Windows:

Ensure recent version of R and Rtools is installed.

try including these lines in home/.R/makevars. :

CXX14 = g++ -std=c++1y

CXX14FLAGS = -O3 -Wno-unused-variable -Wno-unused-function

If makevars does not exist, run this code within R:

dotR \<- file.path(Sys.getenv(“HOME”), “.R”)

if (\!file.exists(dotR)) dir.create(dotR)

M \<- file.path(dotR, ifelse(.Platform$OS.type == “windows”,
“Makevars.win”, “Makevars”))

if (\!file.exists(M)) file.create(M)

cat(“14FLAGS=-O3 -march=native -mtune=native”, if( grepl(“^darwin”,
R.version\(os)) "CXX14FLAGS += -arch x86_64 -ftemplate-depth-256" else  if (.Platform\)OS.type
== “windows”) “CXX11FLAGS=-O3 -march=native -mtune=native” else
“CXX14FLAGS += -fPIC”, file = M, sep = “”, append = TRUE)

In case of compile errors like ‘g++ not found’, ensure the devtools
package is installed: install.packages(‘devtools’) and include the
following in your .Rprofile

library(devtools) Sys.setenv(PATH = paste(“C:/Rtools/bin”,
Sys.getenv(“PATH”), sep=“;”)) Sys.setenv(PATH =
paste(“C:\\Rtools\\mingw\_64\\bin”, Sys.getenv(“PATH”), sep=“;”))
Sys.setenv(BINPREF = “C:/Rtools/mingw\_$(WIN)/bin/”)
