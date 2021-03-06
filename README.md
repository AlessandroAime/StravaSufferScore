# Strava Suffer Score

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Decoding the Algorithm
Few months ago I purchased a [Suunto Ambit3 Peak](http://www.suunto.com/en-US/Products/Sports-Watches/Suunto-Ambit3-Peak/Suunto-Ambit3-Peak-Sapphire-HR/) after four years, and thousands of kilometres, with my faithful [Polar RC3](https://www.polar.com/us-en/products/improve_fitness/running_multisport/RC3_GPS). The fact anyone can build small apps for this device is one of the main reasons that made me opt for it instead of its competitors.

Being a big fan of Strava I had the idea of "reverse engineering" the Strava Suffer Score algorithm to make it an app for all the Suunto users out there.

At the end these are the results:

- Z1: 25 point/hour
- Z2: 60 point/hour
- Z3: 115 point/hour
- Z4: 250 point/hour
- Z5: 300 point/hour

## Making of the Suunto App
Here’s the [final code](http://www.movescount.com/apps/app10925786) from the Movescount App Zone editor:

```
RESULT = SCORE;
if(SUUNTO_HR >= SUUNTO_USER_REST_HR && SUUNTO_HR <= 60*SUUNTO_USER_MAX_HR/100) {
  SCORE = SCORE + 25/3600;
} else if(SUUNTO_HR > 60*SUUNTO_USER_MAX_HR/100 && SUUNTO_HR <= 70*SUUNTO_USER_MAX_HR/100) {
  SCORE = SCORE + 60/3600;
} else if(SUUNTO_HR > 70*SUUNTO_USER_MAX_HR/100 && SUUNTO_HR <= 80*SUUNTO_USER_MAX_HR/100) {
  SCORE = SCORE + 115/3600;
} else if(SUUNTO_HR > 80*SUUNTO_USER_MAX_HR/100 && SUUNTO_HR < 90*SUUNTO_USER_MAX_HR/100) {
  SCORE = SCORE + 250/3600;
} else {
  SCORE = SCORE + 300/3600;
}
```

A list of `case` would have been better, unfortunately the [available syntax](http://content.static.movescount.com/downloads/SuuntoAppZoneDeveloperManual.pdf) is really limited.

**Movescount doesn't let you edit the content of your app when this has been downloaded by more then one user, so the executable code won't look as "clean" as the one above.**
