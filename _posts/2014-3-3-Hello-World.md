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

Step 3: Visualize

Step 4: Problem Statement

Step 5: Approach

Step 7: What it means to have clean data
