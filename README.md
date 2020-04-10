# R-OSISoft
R Package to retrieve data from PI historian

This code is from the [OSIsoft forums](https://pisquare.osisoft.com/blogs/holgeramort/2018/02/19/rosisoft-osisoft-pi-and-r-version-2). I've also added the latest version of [rClr](https://github.com/rdotnet/rClr).

OSISoft have a history of deleting code previously made available and I'm taking a copy here. I could not find a license in the original code.

## Getting started

* Installation is done manually. In RStudio select Tools\Install packages … and when the open dialog opens, change the option “Install from:” to “Packaged Archive File”
* After the installation the library is loaded with: `library(ROSIsoft)`
* To connect to AF and PI server use first: AFSetup() this will install dependencies such as rClr
  * If this doesn't work install the latest version [manually](https://github.com/rdotnet/rClr)
* To connect to the PI server use the following:
`connector<-ConnectToPIWithPrompt("<PI Server>")`  and `connector<-ConnectToAFWithPrompt("<AF Server>","AFDatabase")`

## Get data

```r
AFSetup()
con <- ConnectToDefaultPI()
con <- ConnectToDefaultAF()
```

### Get a value

```r
GetPointValue('sinusoid', '*-1h', 'interpolated', 'exact')
            TimeStamp    Values
1 2020-04-10 07:49:56 0.1922331
```

### Get values

```r
GetPointValues('sinusoid','*-2h', '*-1h', 'interpolated', 300)
             TimeStamp    Values
1  2020-04-10 06:51:15 8.7309960
2  2020-04-10 06:56:15 7.5389580
3  2020-04-10 07:01:15 6.4277470
4  2020-04-10 07:06:15 5.3994780
5  2020-04-10 07:11:15 4.4561090
6  2020-04-10 07:16:15 3.5994350
7  2020-04-10 07:21:15 2.8310870
8  2020-04-10 07:26:15 2.1525280
9  2020-04-10 07:31:15 1.5650480
10 2020-04-10 07:36:15 1.0697670
11 2020-04-10 07:41:15 0.6676277
12 2020-04-10 07:46:15 0.3593950
13 2020-04-10 07:51:15 0.1456558
```

### Summary data

```r
GetPointSummary('sinusoid', '*-2h', '*-1h', 'all', 'exact')
            TimeStamp Count  Average  Maximum    Minimum PercentGood
1 2020-04-10 06:53:48  3600 3.014178 8.112095 0.07305427         100
  PopulationStdDev    Range   StdDev     Total
1         2.380907 8.039041 2.380907 0.1255908
```

```r
GetPointSummaries('sinusoid', '*-2h', '*-1h', 'all', 'interpolated', 300)
             TimeStamp Count   Average   Maximum    Minimum PercentGood
1  2020-04-10 06:54:39   300 7.3350827 7.9104991 6.77327083         100
2  2020-04-10 06:59:39   300 6.2388221 6.7732708 5.71832714         100
3  2020-04-10 07:04:39   300 5.2258632 5.7183271 4.74767618         100
4  2020-04-10 07:09:39   300 4.2981343 4.7476762 3.86316528         100
5  2020-04-10 07:14:39   300 3.4574014 3.8631653 3.06647832         100
6  2020-04-10 07:19:39   300 2.7052647 3.0664783 2.35913183         100
7  2020-04-10 07:24:39   300 2.0431561 2.3591318 1.74247219         100
8  2020-04-10 07:29:39   300 1.4723359 1.7424722 1.21767346         100
9  2020-04-10 07:34:39   300 0.9938908 1.2176735 0.78573441         100
10 2020-04-10 07:39:39   300 0.6087313 0.7857344 0.44747741         100
11 2020-04-10 07:44:39   300 0.3175909 0.4474774 0.20354627         100
12 2020-04-10 07:49:39   300 0.1210235 0.2035463 0.05440535         100
   PopulationStdDev     Range     StdDev        Total
1        0.32831463 1.1372282 0.32831463 0.0254690372
2        0.30456221 1.0549437 0.30456221 0.0216625766
3        0.28023047 0.9706510 0.28023047 0.0181453583
4        0.25536577 0.8845109 0.25536577 0.0149240776
5        0.23001550 0.7966870 0.23001550 0.0120048659
6        0.20422818 0.7073465 0.20422818 0.0093932802
7        0.17805323 0.6166596 0.17805323 0.0070942921
8        0.15154102 0.5247987 0.15154102 0.0051122775
9        0.12474322 0.4319391 0.12474322 0.0034510095
10       0.09771308 0.3382570 0.09771308 0.0021136505
11       0.07050797 0.2439311 0.07050797 0.0011027460
12       0.04320056 0.1491409 0.04320056 0.0004202204
```

### Calculation bases

Applies to `GetPointSummary`, `GetPointSummaries`, `GetAttributeSummary`, and `GetAttributeSummaries`.

```r
GetAFCalculationBasis()
                               Values
1                        TimeWeighted
2                       EventWeighted
3              TimeWeightedContinuous
4                TimeWeightedDiscrete
5 EventWeightedExcludeMostRecentEvent
6   EventWeightedExcludeEarliestEvent
7        EventWeightedIncludeBothEnds
```

### Get Point Attributes

```r
GetPointAttributes('sinusoid', c('step', 'creationdate'))
          Name               Value
1         step                   0
2 creationdate 06/10/2005 13:38:18
```
## Support

Contact the original author in the [PI Square thread]((https://pisquare.osisoft.com/blogs/holgeramort/2018/02/19/rosisoft-osisoft-pi-and-r-version-2).
