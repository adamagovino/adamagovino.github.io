---
published: true
---
## Do NBA GMs mostly fail when spending capital on new talent? 

How many times have you read about a transaction that your favorite team just made, or saw a Woj bomb and thought "Man, if only I ran the team!"

Think their job is easy? I decided to take a look at the numbers and dissect contract data in order to compare it to a player's performance. 

    cols = ['Player','Year','Team','Pos','Cap Hit','Cap Amend','Perc Cap','Cash','Cash Amend','Age','G','WS','VORP','PER','Signing Note','Cap Notes','Cash Notes','GM Name','Draft Year','Draft Pick','First Year']

    nba2 = pd.DataFrame(columns=cols)

	newish_nba['Money Spent'] = 0

    players = list(set(newish_nba['Player']))

    dfs = []

    #years spotrac doesnt adjust cash with trades
    syrs = [2012,2013,2014,2015]

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

    print(datetime.now() - startTime)

    nba2.head()




