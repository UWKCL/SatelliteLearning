SatelliteLearning
==================

This repository contains R functions and scripts that are intended for use with data from the Satellite Learning task (ver3.8.5). These functions are bound to be version specific, and so we will want to tag them at some point.

Loading Data
-------------

Loading data involves specifying the path to the directory where all of the data are stored. For example, the data are currently stored at:

```
RogersLab/Experiments/Behavioral/satelliteLearning/Spring2015/data
├── pilot
│   ├── 001PILOT_data.txt
│   └── 001PILOT_session.txt
└── round01
    ├── 1006_data.txt
    ├── 1006_session.txt
    ├── 1007_data.txt
    ├── 1007_session.txt
    ├── 1008_data.txt
    ├── 1008_session.txt
    ├── s1001_data.txt
    ├── s1001_session.txt
    ├── s1002_data.txt
    ├── s1002_session.txt
    ├── s1003_data.txt
    ├── s1003_session.txt
    ├── s1004_data.txt
    ├── s1004_session.txt
    ├── s1005_data.txt
    └── s1005_session.txt
```

You may need to adjust your path to this data, depending on what computer you are using. The way to do that would be to create a variable `STUDY_INFO` that contains a field called `datadir`. For example: 

```{R}
STUDY_INFO = list(
  datadir="/mnt/RogersLab/Experiments/Behavioral/satelliteLearning/Spring2015/data"
)
save(STUDY_INFO, file='STUDY_INFO.Rdata')
```

The functions `load_session_data` and `load_response_data` currently take two arguments, `round` and `STUDY_INFO`. For example:

```{R}
load_session_data <- function(round,STUDY_INFO) { ... }
```

After you set up your `STUDY_INFO` variable, you will load the data in using a series of commands like the following:

```{R}
SessionData <- load_session_data(round=1, STUDY_INFO)
ResponseData <- load_response_data(round=1, STUDY_INFO)
```

Which will create `data frames` that looks something like:

```{R}
library(dplyr) # This is just for the as.tbl() function
as.tbl(SessionData)
Source: local data frame [71 x 6]

   subject session  task               start                 end  accuracy
1     1006       1 study 2015-02-19 20:16:09 2015-02-19 20:30:13        NA
2     1006       1 train 2015-02-19 20:30:13 2015-02-19 20:38:27 0.1250000
3     1006       1 train 2015-02-19 20:38:36 2015-02-19 20:45:31 0.3750000
4     1006       1 train 2015-02-19 20:45:40 2015-02-19 20:52:36 0.2187500
5     1006       1 train 2015-02-19 20:52:42 2015-02-19 20:58:55 0.3125000
6     1006       1 train 2015-02-19 20:59:02 2015-02-19 21:05:59 0.2812500
7     1006       1 train 2015-02-19 21:06:04 2015-02-19 21:13:08 0.3125000
8     1006       2  test 2015-02-19 21:14:51 2015-02-19 21:21:19 0.1372549
9     1006       3  test 2015-02-20 09:02:32 2015-02-20 09:10:41 0.2156863
10    1007       1 study 2015-02-19 20:16:33 2015-02-19 20:31:43        NA
...

as.tbl(ResponseData)
Source: local data frame [3,431 x 30]

   subject session  task round trial itemnumber TP1 TP2 TP3 TP4 TP5   TCl   TCd RP1 RP2 RP3 RP4 RP5   RCl   RCd O1 O2 O3 O4 O5 O6
2     1006       1 study     1     1         15   2   3   1   2   6 Gamma Nivex   2   3   3   2   4 Gamma Nivex NA NA NA NA NA NA
3     1006       1 study     2     1         15   2   3   1   2   6 Gamma Nivex   2   3   3   2   4 Gamma Nivex NA NA NA NA NA NA
4     1006       1 study     3     1         15   2   3   1   2   6 Gamma Nivex   2   3   3   2   1 Gamma Nivex NA NA NA NA NA NA
5     1006       1 study     4     1         15   2   3   1   2   6 Gamma Nivex   2   3   3   2   5 Gamma Nivex NA NA NA NA NA NA
6     1006       1 study     5     1         15   2   3   1   2   6 Gamma Nivex   2   3   3   2   6 Gamma Nivex NA NA NA NA NA NA
7     1006       1 study     5     1         NA   6   5   5   5   5 Alpha Nodon   2   3   3   2   6 Gamma Nivex NA NA NA NA NA NA
8     1006       1 study     1     2          1   6   5   5   5   5 Alpha Nodon   6   5   3   5   5 Alpha Nodon NA NA NA NA NA NA
9     1006       1 study     2     2          1   6   5   5   5   5 Alpha Nodon   6   5   3   5   6 Alpha Nodon NA NA NA NA NA NA
10    1006       1 study     3     2          1   6   5   5   5   5 Alpha Nodon   6   5   4   5   5 Alpha Nodon NA NA NA NA NA NA
11    1006       1 study     3     2         NA   6   6   5   5   5 Alpha Sorex   6   5   5   5   5 Alpha Nodon NA NA NA NA NA NA
..     ...     ...   ...   ...   ...        ... ... ... ... ... ...   ...   ... ... ... ... ... ...   ...   ... .. .. .. .. .. ..
Variables not shown: O7 (lgl), Time (dbl), Acc (int), CumPCorr (dbl)
```

The notion of a *round* is employed just to clearly separate different data collection efforts. In the event that more data need to be collected after this *round*, we would create a new folder and save data into that one. The folder would need to be called `round02`, or whatever the next value would be. A current limitation of the existing code is that there is no way to load in the pilot data, but this could be easily addressed. 

Analysis
---------

Analysis functions are not written yet.
