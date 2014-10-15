---
layout: default
title: Examples
permalink: examples/
---

# Examples

## Accessing time range properties

~~~php
use League\Period\Period;

$period = Period::createFromDuration('2014-10-03 08:12:37', 3600);
$start = $period->getStart(); //return the following DateTime: DateTime('2014-10-03 08:12:37');
$end   = $period->getEnd(); //return the following DateTime: DateTime('2014-10-03 09:12:37');
$duration  = $period->getDuration(); //return a DateInterval object
$duration2 = $period->getDuration(true); //return the same interval expressed in seconds.
~~~

Learn more about how this all works in the [Overview](/overview/).

## Iterate over a time range

A simple example on how to get all the days from a selected month.

~~~php
use League\Period\Period;

$period = Period::createFromMonth(2014, 10);
foreach ($period->getRange('1 DAY') as $day) {
    $day->format('Y-m-d');
}
~~~

The `Period` object comes with many [named constructors](/instantiation/) to help instantiate easily your time range.

## Comparing time ranges

~~~php
use League\Period\Period;

$period    = Period::createFromDuration('2014-01-01', '1 WEEK');
$altPeriod = Period::createFromWeek(2014, 3);
$period->sameDurationAs($altPeriod); //will return true because the duration are equals
$period->sameValueAs($altPeriod); //will return false because the endpoints differ
~~~

The class comes with other way to [compare time ranges](/comparing/) based on their duration and or their endpoints.

## Modifying time ranges

~~~php
use League\Period\Period;

$period    = Period::createFromDuration('2014-01-01', '1 WEEK');
$altPeriod = $period->endingOn('2014-02-03');
$period->contains($altPeriod); //return false;
$altPeriod->durationGreaterThan($period); //return true;
~~~

`Period` is an immutable value object. Any changes to the object returns a new object. The class has more [modifying methods](/modifying/)