
[![Build Status](https://travis-ci.org/jzeiders/gps-filter.svg?branch=master)](https://travis-ci.org/jzeiders/gps-filter)[![Coverage Status](https://coveralls.io/repos/github/jzeiders/gps-filter/badge.svg)](https://coveralls.io/github/jzeiders/gps-filter)

# gps-filter

Tool set for filtering and cleaning-up gps data. Remodels the data set as vectors in order to accomplish this.

## Installation

Download node at [nodejs.org](http://nodejs.org) and install it, if you haven't already.

```sh
npm install gps-filter --save
```
## Use
```sh
# Points is expected to be an array of GPS points with a latitude, longitude, and timestamp;
# Valid formats: Latitude: [lat, latitude, y]
#                Longitude[lng,longitude,x] 
#                Timestamp[time, timestamp, startime]
                
#Coordinate data in decimal, timestamp can be in any format momentjs can handle
#ALL SPEEDS ARE IN M/S
var gps-filter = require('gps-filter')

.positionFilter(points,min,max)
  #Removes points where the change in position is outside the bounds
  returns arrayOfFilteredPoints
  
.velocityFilter(points,min,max)
  #Removes points where the velocity is outside the bounds
  returns arrayOfFilteredPoints

.accelerationFilter(points,min,max)
  #Removes points where the acceleration is outside the bounds
  returns arrayOfFilteredPoints

.removeSpikes(points,sharpness,iterations)
  #Remove points where the angle between the vector that starts there and ends there is greater than the sharpness
  #E.g _/\_ ->  _ _ 
  #Sharpness: 0-Removes all points, 180-Removes None
  
  #Iterations: defines the number of passes
  returns arrayOfFilteredPoints

.smoothLine(points, threshold)
  #Removes points by assuming that if the sum of two vectors is ~parallel to the one
  #before it they should be combined
  #E.G. __/\ -> ___ 
  #~parallel is defined by threshold
  #Threshold: 0-Vectors must be perfectly parallel 180-Every vector considered parallel (will delete everything!)
  returns arrayOfFilteredPoints

```

## Tests

```sh
npm install
npm test
```

## Dependencies

- [vectorize](git+https://github.com/jzeiders/gps-filter.git): Converts gps points to motion vectors

## Dev Dependencies

- [chai](https://github.com/chaijs/chai): BDD/TDD assertion library for node.js and the browser. Test framework agnostic.
- [coveralls](https://github.com/nickmerwin/node-coveralls): takes json-cov output into stdin and POSTs to coveralls.io
- [istanbul](https://github.com/gotwarlost/istanbul): Yet another JS code coverage tool that computes statement, line, function and branch coverage with module loader hooks to transparently add coverage when running tests. Supports all JS coverage use cases including unit tests, server side functional tests
- [mocha-lcov-reporter](https://github.com/StevenLooman/mocha-lcov-reporter): LCOV reporter for Mocha
- [victor](https://github.com/maxkueng/victor): A JavaScript 2D vector class with methods for common vector operations


## License

MIT

_Generated by [package-json-to-readme](https://github.com/zeke/package-json-to-readme)_
