---
published: true
---
![ballmoney.jpeg]({{site.baseurl}}/_posts/ballmoney.jpeg)





I wanted to take a peak at contracts moving forward through seasons as NBA players transition from rookie to seasoned vets.  

Here is my interactive viz looking at [win share-based net value](https://adamagovino.github.io/Net-Value/) based on season number:
<div class='tableauPlaceholder' id='viz1595164759345' style='position: relative'><noscript><a href='#'>
  <img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;NB&#47;NBAPlayerNetValue&#47;SeasonValue&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'>
  <param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> 
  <param name='embed_code_version' value='3' />
  <param name='site_root' value='' />
  <param name='name' value='NBAPlayerNetValue&#47;SeasonValue' />
  <param name='tabs' value='no' />
  <param name='toolbar' value='yes' />
  <param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;NB&#47;NBAPlayerNetValue&#47;SeasonValue&#47;1.png' /> 
  <param name='animate_transition' value='yes' />
  <param name='display_static_image' value='yes' />
  <param name='display_spinner' value='yes' />
  <param name='display_overlay' value='yes' /><param name='display_count' value='yes' />
  <param name='language' value='en' />
  </object></div>                
  <script type='text/javascript'>                    var divElement = document.getElementById('viz1595164759345');                    var vizElement = divElement.getElementsByTagName('object')[0];                    vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px';                    var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>


Looking at this, it seems as though seasons 1-4 for a player trend upward in terms of value, while experiencing a decline following this. Since net value is based on what a player earns, this makes sense considering that players are generally signed under rookie contracts for years 1-4, meaning that GMs are __bound__ to sign players for specific amounts (there is a range, but in the scope of all NBA contracts it is a small window).  There are some exceptions in years 3 and 4 due to team options, but teams would generally not flinch on giving that option to any player that is above average. 

The NBA is a soft-cap league, and other than veteran minimums and max contracts, GMs are really free to spend what they would like on any free agent.  Therefore, post-year 4 salaries are based on market value within the league.  

Remember that [net value](https://adamagovino.github.io/Net-Value/) is based upon a __league__ -  wide  "win share-worth" (aka the league-wide mean of how much a GM pays per win share).  This number changes each year (as new contracts are given out and as the salary cap changes) - they are as follows:

2018-19: $2,892,980.5323072015<br>
2017-18: $2,672,176.2756527993<br>
2016-17: $2,374,298.4274322162<br>
2015-16: $1,920,468.3199235233<br>
2014-15: $1,668,303.8220311997<br>
2013-14: $1,586,231.6678608393<br>
2012-13: $1,497,732.327359618<br>
2011-12: $1,478,518.6007905134<br><br>

However, looking at these season-based quartiles, it may not be accurate to include the rookie-scale players in this mean, as these are fixed contracts that are pre-determined.  Let's look at what these numbers come out to if we exclude rookies:

2018-19: $3,626,033.342042756<br>
2017-18: $3,366,121.8944471045<br>
2016-17: $2,908,138.2932804488<br>
2015-16: $2,246,251.8696787367<br>
2014-15: $2,009,908.4301636228<br>
2013-14: $1,881,308.8099097009<br>
2012-13: $1,787,643.2533803645<br>
2011-12: $1,862,600.726403454<br><br>

Just as you probably would have guessed, win shares become more expensive once you exclude the limit of rookie salaries - lets see how this changes the outlook of net value once we adjust for this:

<div class='tableauPlaceholder' id='viz1595164893706' style='position: relative'>
  <noscript>
  <a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;NB&#47;NBAPlayerNetValue&#47;NetValuevs_AmendedNetValue&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'>
  <param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> 
  <param name='embed_code_version' value='3' /> 
  <param name='site_root' value='' />
  <param name='name' value='NBAPlayerNetValue&#47;NetValuevs_AmendedNetValue' />
  <param name='tabs' value='no' /><param name='toolbar' value='yes' />
  <param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;NB&#47;NBAPlayerNetValue&#47;NetValuevs_AmendedNetValue&#47;1.png' /> 
  <param name='animate_transition' value='yes' />
  <param name='display_static_image' value='yes' />
  <param name='display_spinner' value='yes' />
  <param name='display_overlay' value='yes' />
  <param name='display_count' value='yes' />
  <param name='language' value='en' />
  </object></div>                
  <script type='text/javascript'>                    var divElement = document.getElementById('viz1595164893706');                    var vizElement = divElement.getElementsByTagName('object')[0];                    vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px';                    var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>
  
  ..

The new value - amended net value - is now shown in red vs the original value in orange.  It's easy to see how the net value has now increased across the board.  We can now measure players more accurately by season. 

Interestingly, one additional takeaway that I had from this data is how imperative the contract/extension is following the rookie contract towards getting the best possible net value per season.  Which, considering the rate at which rookies stay with their drafting teams, places an even greater premium on drafting - we'll look at this soon.  And down the rabbit hole we go... thanks for reading!
