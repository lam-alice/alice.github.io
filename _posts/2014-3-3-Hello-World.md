---
layout: post
title: Data Science is a-w-e-s-o-m-e!!
published: true
---


## Alice Lam's GA Project 2 - Billboard data

### Step 1: Explore and describe data

Step 1 & 2: describe data, interesting observation; clean data along the way
- Total 317 entries, info shows that year, artist, track, time, genre, date entered, date peaked, 1st week, all have data and non-null.
- For wk2 to wk76, there are cells with empty data - indicated that some songs did not get ranked on BB100 during week 2 to 76
- Two songs on BB share the same name, but belong to different artist. These songs are renamed¶
- Some songs fall in and out of the chart throughout its lifespan, it is due to Billboard's certain policy to help promote new songs. Hence the song's final BB appearance might be on week 63, but has only been on BB for 57 wks.
- Many so-so songs fall out of the chart after week 20. Further investigation shows it's also BB's policy
- Songs that can make it past week 28 tend to have hit top 20, and have much longer lifespan on BB (up to 50-60 weeks)
- Song lengths fall closely in 3.5 to 4.5 mins range: average 4 min 2 secs, 25th to 75th percentile of songs range from 3 min 39 sec to 4 min 17 sec
- Number of weeks to peak: average 7 weeks, 25th to 75th percentile range from 3 wk to 10 wk. longest is 45 weeks (song: Higher, by Creed)
- Number of weeks on BB: average 16.7 weeks, 25th to 75th percentile range from 10 wk to 20 wk, max 57 wks.
- Some data appear missing. While sorting according to time, at any given date, there is less than 100 ranked song

#### Qualitative description of the data
Ranking factors: (airplay by ~1000 stations: approx. by # of gross audience impressions, cross-reference exact times of radio airplay), (physical sales), (digital sales), (top streamed songs on radio, on-demand, videos on leading online music services)
intention:
aid the industry to know the popularity of the “product” and to track the trends of the buying public
Billboard has adjusted the sale/airplay ratio many times to more accurately reflect the true popularity of songs.
Recurrents:
“in an effort to allow the chart to remain as current as possible and to give proper representation to new and developing artists and tracks, has (since 1991) removed titles that met “recurrent status”. - spent 20 weeks on Hot 100 but fell below 50
descending songs are removed from the chart if rank below number 25 after 52 weeks
exceptions made to re-releases, sudden resurgence in popularity of tracks that have taken a very long time to gain mainstream success. These are rare and handled on case-by-case basis

Step 1 - 1

      df.info()

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 317 entries, 0 to 316
Data columns (total 83 columns):
year               317 non-null int64
artist.inverted    317 non-null object
track              317 non-null object
time               317 non-null object
genre              317 non-null object
date.entered       317 non-null object
date.peaked        317 non-null object
x1st.week          317 non-null int64
x2nd.week          312 non-null float64
x3rd.week          307 non-null float64
x4th.week          300 non-null float64
x5th.week          292 non-null float64
x6th.week          280 non-null float64
x7th.week          269 non-null float64
x8th.week          260 non-null float64
x9th.week          253 non-null float64
x10th.week         244 non-null float64
x11th.week         236 non-null float64
x12th.week         222 non-null float64
x13th.week         210 non-null float64
x14th.week         204 non-null float64
x15th.week         197 non-null float64
x16th.week         182 non-null float64
x17th.week         177 non-null float64
x18th.week         166 non-null float64
x19th.week         156 non-null float64
x20th.week         146 non-null float64
x21st.week         65 non-null float64
x22nd.week         55 non-null float64
x23rd.week         48 non-null float64
x24th.week         46 non-null float64
x25th.week         38 non-null float64
x26th.week         36 non-null float64
x27th.week         29 non-null float64
x28th.week         24 non-null float64
x29th.week         20 non-null float64
x30th.week         20 non-null float64
x31st.week         19 non-null float64
x32nd.week         18 non-null float64
x33rd.week         12 non-null float64
x34th.week         10 non-null float64
x35th.week         9 non-null float64
x36th.week         9 non-null float64
x37th.week         9 non-null float64
x38th.week         8 non-null float64
x39th.week         8 non-null float64
x40th.week         7 non-null float64
x41st.week         7 non-null float64
x42nd.week         6 non-null float64
x43rd.week         6 non-null float64
x44th.week         6 non-null float64
x45th.week         5 non-null float64
x46th.week         5 non-null float64
x47th.week         5 non-null float64
x48th.week         4 non-null float64
x49th.week         4 non-null float64
x50th.week         4 non-null float64
x51st.week         4 non-null float64
x52nd.week         4 non-null float64
x53rd.week         4 non-null float64
x54th.week         2 non-null float64
x55th.week         2 non-null float64
x56th.week         2 non-null float64
x57th.week         2 non-null float64
x58th.week         2 non-null float64
x59th.week         2 non-null float64
x60th.week         2 non-null float64
x61st.week         2 non-null float64
x62nd.week         2 non-null float64
x63rd.week         2 non-null float64
x64th.week         2 non-null float64
x65th.week         1 non-null float64
x66th.week         0 non-null float64
x67th.week         0 non-null float64
x68th.week         0 non-null float64
x69th.week         0 non-null float64
x70th.week         0 non-null float64
x71st.week         0 non-null float64
x72nd.week         0 non-null float64
x73rd.week         0 non-null float64
x74th.week         0 non-null float64
x75th.week         0 non-null float64
x76th.week         0 non-null float64
dtypes: float64(75), int64(2), object(6)
memory usage: 205.6+ KB

Step 1 - 2: rename columns

Step 1 - 3: check data in key columns
artist and genre data are fine, but there's a duplicate songs by two different artist. we rename the songs to differentiate the two.

## Step 2: Modify data for analysis

Step 2 - 1: calculate length of track in seconds

Step 2 - 2: calculate time it takes to peak and to fade
Code:

convert to datetime type

      df_ed.date_entered = pd.to_datetime(df.date_entered)
      df_ed.date_peaked = pd.to_datetime(df.date_peaked)

calculate number of weeks to peak
timedelta in unit of microseconds

      days_to_peak = pd.to_numeric((df_ed.date_peaked - df_ed.date_entered)/60/60/24/1000000000)
      weeks_to_peak = pd.DataFrame((days_to_peak) / 7)
      weeks_to_peak.columns = ['wks_to_peak']
      df_ed = pd.concat([df_ed,weeks_to_peak], axis=1)
      df_ed.head()

Step 2 - 3: create week/rank only data frame to calculate number of weeks on billbaords, the week it last show up on BB

Step 2 - 4: find the best and worst ranking per track

Step 2 - 5: melt the week rank data

      df_week_melt = pd.melt(df_ed, 
                             id_vars = ['artist','track','genre','date_entered','date_peaked',
                                        'track_len','wks_to_peak','wk_last_appeared','wks_on_bb',
                                        'miss_wk','wks_peak_to_out','bb_best_rank','bb_worst_rank'], 
                             var_name = ['wk'],
                             value_vars = ['w01','w02','w03','w04','w05','w06','w07','w08','w09',
                                           'w10','w11','w12','w13','w14','w15','w16','w17','w18',
                                           'w19','w20','w21','w22','w23','w24','w25','w26','w27',
                                            'w28','w29','w30','w31','w32','w33','w34','w35','w36',
                                           'w37','w38','w39','w40','w41','w42','w43','w44','w45',
                                           'w46','w47','w48','w49','w50','w51','w52','w53','w54',
                                           'w55','w56','w57','w58','w59','w60','w61','w62','w63',
                                           'w64','w65','w66','w67','w68','w69','w70','w71','w72',
                                           'w73','w74','w75','w76'],
                            value_name = 'rank')
                      
                      

Step 2 - 6: Calculate the date for each rank
                  df_week_melt['date'] = 
                  (df_week_melt['wk_num']-1) * 7 * 60 * 60 * 24 * 1000000000 + df_week_melt['date_entered']
                  # week number need to minus 1, as week 1 = date_entered

## Step 3: Visualize

## Step 4: Problem Statement

From the perspective of a record company, with the goal of producing more BillBoard hit songs:

How to deepen understanding on what drives a song to be popular, and the trends of the drivers?

What type of songs should we produce more?

When should the song be released?

For how long should we market heavily on the song?

Where should we market the song?

Are there popular and very popular songs that would be overlooked by this billboard?

## Step 5: Approach for problem statement

Track longer time period, observe longer time trend

Observe seasonality over multiple years, e.g. is the rising % of Reggae in Oct - Dec 2000 a Q4 seasonality thing?

Gather more descriptive data on the songs, e.g.
* gender of artist
* race of artist
*group vs solo
*theme
*tempo (speed)
*mood (quantifiable: major vs minor tune, music range (highest minus lowest pitch) and frequency)
*song writer
*lyricist
*record company
*marketing budget per song
*is it a theme song for a major event / hot movie
*split in revenue from online purchase vs offline purchase
*split in radio airtime vs online streaming/youtube viewing (Should be able to purchase from Nielsen SoundScan, or cross reference BillBoard's "On-demand Songs" chart)

With more descriptive data and over longer time horizon, we can produce more and also spend more marketing dollars on songs that share those hit characteristics.

We should also repeat the study of week to peak, peak to last, and billboard duration, to further our statistical studies on how long it takes for each type of songs to ramp up the rank and stay on the chart. We should focus on our marketing dollar during those weeks.

Knowing where certain types of songs are more popular on which channel, helps us to do target advertising. If certain type of song by certain artists are mostly getting "airplay" online, marketing dollar should be spend online, e.g. buying more ad on itunes. Certain songs might still be a "radio" type of songs, then more effort should be put on marketing to DJs.

##### Caveat while doing time-series analysis on Billboard Hot 100
Weighting methodology had been changing over time to adapt to new environment in music industry, e.g. inclusion of various online channels
The chart is subjective: BillBoard has adjusted the sales/airtime ratio many times to more accurately reflect "the true popularity of songs"
The Chart had been subject to manipulation, e.g. 1991 SoundScan scandal.
High ranking does not necessarily means high revenue.

##### Side Note - methodology changes
pre 1995: singles were allowed to chart in the week they first went on sale, and chart based on airplay points alone
post 1995: only allow a single to debut after a full week of sales on combined sales and airplay points
1998: allow tracks to chart on the basis of airplay alone without commercial release
2005: include paid digital downloads tracked by Nielson SoundScan
2007: include digital streams
2012: add on-demand songs services (Spotify)
