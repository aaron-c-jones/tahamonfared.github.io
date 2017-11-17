---
excerpt: "R Tips and Tricks"
---

Taha Monfared
October 24, 2017

There are some tricky stuff in R you need to remember. I will update this post.

**Passing text to functions as variables**

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

**Shiny app for Bayesian Network**

But since we are on the shiny front let's just have an example here. [BNLearn](https://tahamonfared.shinyapps.io/Bayesian_Network/?lipi=urn%3Ali%3Apage%3Ad_flagship3_profile_view_base_treasury%3Br6XWYE10SDahuZR4AACxxA%3D%3D){: .btn .btn--info}

This is a Bayesian network app to estimate probabilities on adult dataset from UCI repository...

**You want legend but it's in your way. Rbase.**

Rbase has a lot of advantages. you can use the Rbase legend as so, so that it does not get in the way.

``` r
legend("topright", ....,box.col = "transparent", bg = "transparent")
```

If you want the axes to look nicer.

``` r
plot(...,axes = FALSE)
axis(side =1 , labels=..., at =...)
```

**Shiny, how to add action item for Enter press?**

After struggling with the concept of adding the added ability of pressing Enter on the keyboard instead of clicking on the update button here is the way I found. It has problems but it serves it's purpose. As it keeps the value of last pressed key, so whenever you press Enter then everything gets updated until you press some other key afterwards. Then it waits for you to fill in the required fields before updating.

``` r
js <- '$(document).on("keyup", function(e) {
              Shiny.onInputChange("Enter", e.keyCode);
          });
      '
```

Then add this in the UI:

``` r
tags$script(js)
```

And, add this is the server:

``` r
if(!is.null(input$Enter) && input$Enter==13){...}
```
