---
title: Benchmarking R, Python, and Julia
layout: post
comments: true
---

The folks at [Simply Statistics](http://simplystatistics.org/2016/01/21/parallel-blas-in-r/) recently emphasized the performance benefits of alternative R builds. The bottom line is, you should not use the default binaries provided by [base R from CRAN](http://cran.us.r-project.org/) but instead consider either the [Microsoft R binary](https://mran.revolutionanalytics.com/) or build R from source yourself. This last option is made easier on Mac OS X by using [Homebrew](http://brew.sh/). Do one of these things, and your R programs will run much faster. 

Out of curiosity, I replicated the profiling used by Simply Statistics on my computer for Microsoft R, Homebrew R, Python, and Julia. The specs are found either from *About This Mac* or by running `sessionInfo()` in R.

* macbook air 8Gb memory
* 2.2GHz processor, 4 cores
* R version 3.2.3 (2015-12-10)
* Platform: x86_64-apple-darwin14.5.0 (64-bit)
* Running under: OS X 10.10.5 (Yosemite)

The code to be run in R is: 

    system.time({ x <- replicate(5e3, rnorm(5e3)); tcrossprod(x) }) 

The equivalent in python (running on the ipython interactive command line) is:

    from numpy import random
    %timeit n = int(5e3); x = random.randn(n,n); x.dot(x.T)

And in Julia,

    tic(); n = round(Int,5e3); x=randn(n,n); x*x'; toc()

Here are the results:

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;margin:0px auto;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg .tg-yw4l{vertical-align:top}
@media screen and (max-width: 767px) {.tg {width: auto !important;}.tg col {width: auto !important;}.tg-wrap {overflow-x: auto;-webkit-overflow-scrolling: touch;margin: auto 0px;}}</style>
<div class="tg-wrap"><table class="tg" style="undefined;table-layout: fixed; width: 272px">
<colgroup>
<col style="width: 109px">
<col style="width: 163px">
</colgroup>
  <tr>
    <th class="tg-yw4l">Platform</th>
    <th class="tg-yw4l">Elapsed Time (seconds)<br></th>
  </tr>
  <tr>
    <td class="tg-yw4l">Microsoft R<br></td>
    <td class="tg-yw4l">5.3</td>
  </tr>
  <tr>
    <td class="tg-yw4l">Homebrew R<br></td>
    <td class="tg-yw4l">5.3</td>
  </tr>
  <tr>
    <td class="tg-yw4l">Python (2.7.10)<br></td>
    <td class="tg-yw4l">3.4</td>
  </tr>
  <tr>
    <td class="tg-yw4l">Julia (0.4)<br></td>
    <td class="tg-yw4l">2.6</td>
  </tr>
</table></div>

----------

As noted by [Yihui Xie](http://yihui.name/en/), the source-built R from Homebrew performs equivalently to the Microsoft version of R. Julia is the fastest, and Python is intermediate between R and Julia. 

Another (subjective) benchmark is how much time it took me to figure out the code for timing things in each language. R was the fastest because I could copy and paste from the blog post. Python took a little longer because I couldn't remember the syntax of the `%timeit` macro. Finally, it took me a good 20 minutes to work out the Julia syntax. Of course this is biased due to my heavier use of R and Python compared to Julia, but I think it illustrates that in small applications, the free performance improvements of using a faster version of R might outweight the even greater performance improvements of switching to a newer language, because of the increased human time needed to learn the language. Of course, for those of us needing to run many computationally intensive simulations, languages like Julia have a major appeal!