---
date: 2012-11-19
title: "The Whiley Project on Ohloh"
draft: false
---

Just yesterday, I came across the [ohloh](https://www.ohloh.net) website for the first time and was surprised to find [the Whiley project already listed there](http://www.ohloh.net/p/whiley).  If you haven't seen it before, Ohloh is a site that attempts to gather stats and other information on open source projects such as: who the developers are, how many commits there are and how the line count has changed over time.  For example, the Whiley project currently has 64,375 LOC made up from 3,535 commits over the last 3 years.  Here's a snapshot of how the LOC count has changed over time:

{{<img class="text-center" width="50%" src="/images/2012/WhileyLOCGraph.png">}}

Here, blue gives the proportion of actual code, red gives the proportion of comments and green the proportion of blank lines.

Another interesting aspect of Ohloh is that, for each project, a high-level summary in plain English is given.  Here's what it says about Whiley:

{{<img class="text-center" width="50%" src="/images/2012/nutshell.png">}} 

It looks like I need to work harder on my code commenting!  Using the [COCOMO](http://en.wikipedia.org/wiki/COCOMO) model, the website also tries to come up with a cost estimate.  For Whiley, the estimated cost is $870,115 --- which seems a bit light to me ;)

The other interesting thing you can do is compare your project with other projects.  For example, here's a comparison with the Whiley project (left) and the Scala Project (right):

{{<img class="text-center" width="50%" src="/images/2012/WhileyComparison.png">}}

From this, it looks like my 12 month activity is pretty competitive!  Anyway, Ohloh is quite an interesting idea and it would be great to see different kinds of analysis being performed.

Finally, a similar website is [MasterBranch](http://masterbranch.com) and I added the [Whiley project to the list there as well](https://masterbranch.com/whiley-project/919904).  However, after a few hours looking around both websites, I seem to be preferring Ohloh ... but I guess time will tell!
