---
published: true
---
## Do NBA GMs mostly fail when spending capital on new talent? 


How many times have you read about a transaction that your favorite team just made, or saw a Woj bomb and thought "Man, if only I ran the team!"  Maybe you've had the feeling that a talented team fell on some bad luck or that a particular team was full of overpaid players.  How a GM pays for talent is behing every team's success or lack thereof.  

Think their job is easy? I decided to take a look at the numbers and dissect contract data in order to compare it to a player's performance, in order to find out quantitatively which GMs were making "smart" moves and which ones fans could be justified in calling for their jobs.

The two main data points that I hoped to look at here was 1) each team's yearly cash expenditure on every player they employed, and 2) the stats that those players accumulated while receiving that cash.  

I decided to look back starting with the 2011-12 season, as that season was the start of a new collective bargaining agreement which had some significant contractual changes.  

I looked for a table that had player's advanced stats, draft position, and contract info all in once place.  This proved impossible (surprisingly, given the data world's passion for all things roundball-related), so I decided to make gather and wrangle my own data.  

I gathered and scraped data from both basketballreference.com and spotrac.com.  These both involved quite amount of cleaning (BR had inconsistent salaries and spotrac had inconsistent player cash take-homes prior to 2015-16, just to name a few).  Traded players also required cash adjustments. A minor note: player performance (and thus GM performance) was based on a player's _cash_ take home (what a GM spent on a player) and not necessarily their _cap hit_, which is the traditional measure of a team's spend.  A player traded mid season would not have a cap hit for their initial team, but obviously they accumulate stats and receive a salary - which for purposes of this analysis, should be the basis of their value.  Also noted in the scrape was any outcome/note for a particular contract - this included ten-day, waived, two-way, and amnestied contracts. 

Here is the code for determing the cash output for traded players that spotrac missed:

    cols = ['Player','Year','Team','Pos','Cap Hit','Cap Amend','Perc Cap','Cash','Cash Amend','Age','G','WS','VORP','PER','Signing Note','Cap Notes','Cash Notes','GM Name','Draft Year','Draft Pick','First Year']

    nba2 = pd.DataFrame(columns=cols)

	newish_nba['Money Spent'] = 0

    players = list(set(newish_nba['Player']))

    dfs = []

    #years spotrac doesnt adjust cash with trades
    syrs = [2012,2013,2014,2015]

	# Types of contracts which would not be traded (Dead=waived, Two=two-way, Ten=10-Day)
    ng = ['Dead','Two','Ten']

        for p in players:
            a = newish_nba[newish_nba['Player']==p]

          dr = max(a['Draft Year'])
          drp = max(a['Draft Pick'])
        pos = a['Pos'].values[0]

        max_age = max(a['Age'])
        max_age_year = a.loc[a['Age'] == max_age, 'Year'].iloc[0]

        years = list(set(a['Year']))
        for y in years:
            b = a[a['Year']==y]
            s = list(set(b['Team']))
            u = list(set(b['Cash']))

            mo = 0
            for i,row in b.iterrows():  
                if (y in syrs) and (row['Cap Notes'] in ng):
                    mo+=0
                else:
                    mo+=row['Cap Amend']
                if (y in syrs) and (len(b)>1) and (len(s)>1) and (0 in u):

                    if mo == 0:
                        b['Cash Amend'] = b['Cash']
                    else:
                        g = b['G'].sum()
                        new_cash = []

                        for i,row in b.iterrows():
                            if row['Cap Notes'] in ng:
                                new_cash.append(row['Cash Amend'])
                            else:
                                d = (row['G']/g)*mo
                                new_cash.append(d)
                        b['Cash Amend'] = new_cash
                else:
                    b['Cash Amend'] = b['Cash']
            teams = list(set(b['Team']))
            for t in teams:
                c = b[b['Team']==t]

                cap = c['Cap Hit'].sum()
                capa = c['Cap Amend'].sum()
                perc = c['Perc Cap'].sum()
                g = c['G'].values[0]
                ws = c['WS'].values[0]
                vorp = c['VORP'].values[0]
                per = c['PER'].values[0]
                mon = c['Cash'].sum()
                new = c['Cash Amend'].sum()       
                sig = c['Signed'].values[0]
                capn = c['Cap Notes'].values[0]
                cashn = c['Cash Notes'].values[0]
                gm = c['GM Name'].values[0]
                fy = max(c['First Year'])

                age_one = max(c['Age'])
                if age_one == 0:
                    diff = y - max_age_year
                    age = max_age + diff
                else:
                    age = age_one

                dff = pd.DataFrame(np.array([[p],[y],[t],[pos],[cap],[capa],[perc],[mon],[new],[age],[g],[ws],[vorp],[per],[sign],[capn],[cashn],[gm],[dr],[drp],[fy]]).T,columns=cols) 
                dfs.append(dff)

    nba2 = pd.concat(dfs)


Side note: I learned a hard-fought lesson with this project, the one thing that data experts always warn about: 80% of your time is spent filtering out crap data and wrangling it together, and that supposed sexiness of 'big data' is immediately sobered by the reality of the data wrangle.  Players had different spellings depending on the sources (some had nicknames ie Mo Bamba is Mohamed Bamba depending on who you ask, others had "Jr" or "II," etc), draft years were wrong or appropriated to older players with the same name, etc.  However, despite the tedious nature of data cleaning, it did allow me to cultivate and gain expertise on the subject matter.   

Once scraped, I combined the advanced stats from basketball reference with the contract data (both the cap hit and the cash expenditure) scraped from spotrac (in which the cash expenditure data needed to be adjusted for trades prior to 2016).  I then attached the GM associated with each player's season to each row.  Also calculated was the season number for each player year in order to see trends related to player age and season number (a topic I'll dive into during another post).  Finally, seasons were condensed by player and team, i.e. a player with three ten-day contracts would have all three combined into one row in order to align with their one row of advanced stats.

The main purpose of this analysis was to find the 'value' that each player brought during a particular season, in order to find out if the money spent of them was justified based on their production.  Were they overvalued or undervalued?  

The calculation for that was simple:

Player Net Value = ((Average $ spent per win share, league-wide) * win shares) - Cash expenditure

Here is the code: 

    # Creating a dictionary, based on year, for dollars spent per win share

    years = list(range(2012, 2021))

    WS_dict = {}

    for year in years:
        filt_nba = nba[nba['Year']==year]
        dollars_per_WS = ((filt_nba['Cash Amend'].sum() / filt_nba['WS'].sum()))
        WS_dict[year] = dollars_per_WS
    
    #determining what a player should be worth based on win shares
    
    player_win_share_worth = []
    for i,row in nba.iterrows():
        ww = row['WS'] * WS_dict[row['Year']]
        player_win_share_worth.append(ww)

    nba['WS Worth'] = player_win_share_worth

    nba['WS Worth'] = nba['WS Worth'].fillna(0)

    nba['Net Value'] = nba['WS Worth'] - nba['Cash Amend']

Here is what the final table looked like: 


 
Please contact me if you would like access to the .csv I put together with this data
    
REFERENCE MATERIAL:

[Basketball Reference](basketballreference.com)

[Larry Coon's Salary Cap FAQ](http://www.cbafaq.com/salarycap.htm)

[Spotrac](spotrac.com)


