# Calculating the age-stratified infection fatality ratio (IFR) of COVID-19

*Updated: 10 June 2020*

Author: Marc Bevand

The largest serological prevalence survey of COVID-19 was conducted by Spain
during the second round of a study that analyzed 63 564 samples between 18 May
2020 and 01 June 2020. We used its [provisional results][sero] published on 03
June to calculate the overall and age-stratified IFR of COVID-19 with the
Python script `calc_ifr.py`:

```
$ ./calc_ifr.py
Ages  0 to   9:  115013 infected,     4 deaths,  0.003% IFR
Ages 10 to  19:  177929 infected,     7 deaths,  0.004% IFR
Ages 20 to  29:  212099 infected,    32 deaths,  0.015% IFR
Ages 30 to  39:  281290 infected,    86 deaths,  0.030% IFR
Ages 40 to  49:  447942 infected,   287 deaths,  0.064% IFR
Ages 50 to  59:  410213 infected,   874 deaths,  0.213% IFR
Ages 60 to  69:  334709 infected,  2404 deaths,  0.718% IFR
Ages 70 to  79:  270572 infected,  6451 deaths,  2.384% IFR
Ages 80 to  89:  131703 infected, 11150 deaths,  8.466% IFR
Ages 90 to 199:   46631 infected,  5827 deaths, 12.497% IFR
Ages  0 to 199: 2428102 infected, 27121 deaths,  1.117% IFR
```

The average IFR for Spain is **1.117%**. However the true IFR may be higher due
to right-censoring and under-reporting of deaths.

The Spanish serological study remains the largest published study available to
this day. The age-stratified IFR was calculated from three sources:

1. Detailed *prevalence data for age brackets*, from the [serosurvey][sero] (table 1)
1. *Total deaths* and *deaths per age bracket* from the [Ministry of Health's daily report for 29 May][daily] (table 2 and table 3)
1. *Population pyramid* for Spain, from [worldpopulationreview.com][wpop]

In order to minimize right-censoring, the parameters *total deaths* and *deaths
per age bracket* should be obtained from a point in time as close as possible
to when the serosurvey was conducted (18 May to 01 June.) We found only two
Ministry of Health reports in this time period that document deaths per age
brackets: [18 May][dailyalt], [29 May][daily]. However the Ministry of Health
has made significant corrections to deaths statistics on 25 May by subtracting
approximately 2 000 deaths. Therefore we trusted the statistics from 29 May over
those of 18 May.

Important detail to note: there were 26 744 total deaths, however age information
was only available for 18 722 deaths, and was missing for 8 022 deaths.
We assume that these 8 022 deaths were distributed proportionally—not equally—among age
brackets, which seems to be a reasonable assumption.

# Applying the age-stratified IFR to other countries

The script `calc_ifr.py` is also able to apply the age-stratified IFR to
another population pyramid, thus calculating the expected average IFR for other
countries.

In the second half of the script, edit `pyramid_target` with the demographics data.
As an example, we supply pyramid data for the United States and calculate an IFR of **0.658%**:

```
$ ./calc_ifr.py
[...]
IFR on target country assuming disease prevalence equal among ages:  0.658%
```

However IFR is highly dependent on factors other than age: availability
of healthcare, population health, etc, so this estimate should be interpreted
with caution.

[sero]: https://portalcne.isciii.es/enecovid19/ene_covid19_inf_pre2.pdf
[daily]: https://www.mscbs.gob.es/profesionales/saludPublica/ccayes/alertasActual/nCov-China/documentos/Actualizacion_120_COVID-19.pdf
[dailyalt]: https://www.mscbs.gob.es/profesionales/saludPublica/ccayes/alertasActual/nCov-China/documentos/Actualizacion_109_COVID-19.pdf
[wpop]: https://worldpopulationreview.com/countries/spain-population/
