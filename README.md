
<!-- README.md is generated from README.Rmd. Please edit that file -->

![logo](logo.svg)

# **DeepG4**: A deep learning approach to predict active G-quadruplexes

<!-- badges: start -->

[![Codecov test
coverage](https://codecov.io/gh/morphos30/DeepG4/branch/master/graph/badge.svg)](https://codecov.io/gh/morphos30/DeepG4?branch=master)
<!-- badges: end -->

**DeepG4** is a deep learning model build in keras+tensorflow who aims
to predict the probability of DNA sequences to form G-Guadruplexes
secondary structures. **DeepG4** is wrapped in a R package, but can work
with any langage that has implemented keras and tensorflow (see below).

## Abstract

DNA is a complex molecule carrying the instructions an organism needs to
develop, live and reproduce. In 1953, Watson and Crick discovered that
DNA is composed of two chains forming a double-helix. Later on, other
structures of DNA were discovered and shown to play important roles in
the cell, in particular G-quadruplex (G4). Following genome sequencing,
several bioinformatic algorithms were developed to map G4s in vitro
based on a canonical sequence motif, G-richness and G-skewness or
alternatively sequence features including k-mers. Here, we propose
instead a convolutional neural network (DeepG4) to map active G4s
(forming both in vitro and in vivo). DeepG4 is very accurate to predict
active G4s, while state-of-the-art algorithms fail. Moreover, DeepG4
identifies key DNA motifs that are predictive of G4 activity. We found
that active G4 motifs do not follow a very flexible sequence pattern as
current algorithms seek for. Instead, active G4s are determined by
numerous specific motifs. Moreover, among those motifs, we identified
known transcription factors which could play important roles in G4
activity by either directly contributing to G4 structure themselves or
by participating in G4 formation in the vicinity. Lastly, variant
analysis suggests that SNPs altering predicted G4 activity could affect
transcription and chromatin, e.g. gene expression, H3K4me3 mark and DNA
methylation. Thus, DeepG4 paves the way for future studies assessing the
impact of known disease-associated variants on DNA secondary structure
and provides a mechanistic interpretation of SNP impact on transcription
and chromatin.

## Requirements

DeepG4 has been built with `Keras 2.3.1` and `tensorflow 2.1.0` but
should work with any version of theses tools.

A very convenient way to install it is within `R`, using `keras` R
package : <https://keras.rstudio.com/>.

``` r
install.packages("keras")
library(keras)
install_keras()
```

This will provide you with default CPU installations of Keras and
TensorFlow.

## Installation

You can install the development version from
[GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("morphos30/DeepG4")
```

## Usage with DeepG4 R package

``` r
library(Biostrings)
library(DeepG4)

sequences <- system.file("extdata", "test_G4_data.fa", package = "DeepG4")
sequences <- readDNAStringSet(sequences)

predictions <- DeepG4(sequences)
head(predictions)
```

## Using our model directly with keras in R

Using our model with keras is very simple, the code is very similar, but
you have to convert youre sequence in one-hot first. To help you, our
function `DNAToNumerical` help you to do it.

``` r

library(Biostrings)
library(DeepG4)
library(keras)

sequences <- system.file("extdata", "test_G4_data.fa", package = "DeepG4")
sequences <- readDNAStringSet(sequences)

model <- system.file("extdata", "model.hdf5", package = "DeepG4")
model <- load_model_hdf5(model)

sequences <- DNAToNumerical(sequences)

predictions <- predict(model,sequences)
```
