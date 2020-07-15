---
published: true
---
![]({{site.baseurl}}/https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcT1pPDwi6zv_R26-FSx3OQFNishFvyl3KGcug&usqp=CAU)

I wanted to take a peak at contracts moving forward through seasons as NBA players transition from rookie to seasoned vets.  

Here is my viz looking at [win share-based net value](https://adamagovino.github.io/Net-Value/) based on season number:

<div class='tableauPlaceholder' id='viz1594733897187' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;NB&#47;NBA2_0_15940685245360&#47;DraftPickValue&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='NBA2_0_15940685245360&#47;DraftPickValue' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;NB&#47;NBA2_0_15940685245360&#47;DraftPickValue&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1594733897187');                    var vizElement = divElement.getElementsByTagName('object')[0];                    vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px';                    var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>

Looking at this, it seems as though seasons 1-4 for a player trend upward in terms of value, while experiencing a decline following this. Since net value is based on what a player earns, this makes sense considering that players are generally signed under rookie contracts for years 1-4, meaning that GMs are __bound__ to sign players for specific amounts (there is a range, but in the scope of all NBA contracts it is a small window).  There are some exceptions in years 3 and 4 due to team options, but teams would generally not flinch on giving that option to any player that is above average. 

The NBA is a soft-cap league, and other than veteran minimums and max contracts, GMs are really free to spend what they would like on any free agent.  Therefore, post-year 4 salaries are based on market value within the league.  

Remember that [net value](https://adamagovino.github.io/Net-Value/) is based upon a ****league**** - wide "win share-worth" (aka the league-wide mean of how much a GM pays per win share).  This number changes each year (as new contracts are given out and as the salary cap changes) - they are as follows:

2018-19: 2892980.5323072015
2017-18: 2672176.2756527993
2016-17: 2374298.4274322162
2015-16: 1920468.3199235233
2014-15: 1668303.8220311997
2013-14: 1586231.6678608393
2012-13: 1497732.327359618
2011-12: 1478518.6007905134

However, looking at these season-based quartiles, it may not be accurate to include the rookie-scale players in this mean, as these are fixed contracts that are pre-determined.  Let's look at what these numbers come out to if we exclude rookies:

2018-19: 3626033.342042756
2017-18: 3366121.8944471045
2016-17: 2908138.2932804488
2015-16: 2246251.8696787367
2014-15: 2009908.4301636228
2013-14: 1881308.8099097009
2012-13: 1787643.2533803645
2011-12: 1862600.726403454

Just as you probably would have guessed, win shares become more expensive once you exclude the limit of rookie salaries.
