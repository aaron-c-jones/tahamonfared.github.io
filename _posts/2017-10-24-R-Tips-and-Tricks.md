---
excerpt: "R Tips and Tricks"
---

Taha Monfared
October 24, 2017

There are some tricky stuff in R you need to remember. I will need to update this post as these stuff come up.

If you want to pass on a text to be converted to a function in R you will need to do so in this way:

``` r
eval(parse(text = paste0(...)))
```

This is an example of it.

``` r
library(scales)
ECDF<-function(dist, params){
  plot(ecdf(eval(parse(text = paste0("r", dist, "(1000 ,",params,")")))),
       main = "Empirical CDF", col = alpha("blue",.5), lwd = 3)
}

ECDF("norm","mean = 5, sd = 1")
```

![](/assets/images/2017-10-24-R-Tricks_files/figure-markdown_github/unnamed-chunk-1-1.png)

Seems easy here, since you basically didn't need it. But sometimes in a function you'll need to do this. I'm going to provide an exmaple in Shiny later.

But since we are on the shiny front let's just have an example here. [BNLearn](https://tahamonfared.shinyapps.io/Bayesian_Network/?lipi=urn%3Ali%3Apage%3Ad_flagship3_profile_view_base_treasury%3Br6XWYE10SDahuZR4AACxxA%3D%3D)

This is a Bayesian network app to estimate probabilities on adult dataset from UCI repository...
