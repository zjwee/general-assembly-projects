# Project 1: SAT & ACT Analysis

## Problem Statement

Given 2017 and 2018 SAT and ACT aggregate data, identify trends in participation rates and scores across various states in the USA.

Identify possible factors affecting SAT participation rates, and recommend how the College Board may increase SAT participation rates.


## Executive Summary

SAT and ACT participation rates, individual subject scores and total/comopsite scores for each state were analyzed.

SAT and ACT participation rates were found to be negatively correlated. There is an overall preference for taking the ACT over the SAT. Central states tend to prefer the ACT, whereas coastal states prefer the SAT.

SAT and ACT scores were found to be negatively correlated to their respective participation rates. The more people taking the test, the lower the average scores for that test.

There is positive correlation between individual subject scores within the same test. Performance in an individual subject of a particular test indicates performance in the other subjects.

SAT and ACT participation rates and scores do not experience large changes year on year, with the exception of states that introduce new state-wide testing policies.

States that do not have an existing SAT or ACT testing programme could be targeted by the College Board to introduce state-wide SAT testing. More research on the demographics and education policies of these states could inform how the College Board can successfully implement SAT testing in targeted states.


## Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|state|object|ACT/SAT|State of origin of ACT/SAT scores|
|sat_participation|int|SAT|SAT participation rate in % for each state|
|sat_ebraw|int|SAT|Average SAT Evidence Based Reading and Writing scores for each state|
|sat_math|int|SAT|Average SAT Math scores for each state|
|sat_total|int|SAT|Average SAT Total scores for each state|
|act_participation|int|ACT|ACT participation rate in % for each state|
|act_english|float|ACT|Average ACT English scores for each state|
|act_math|float|ACT|Average ACT Math scores for each state|
|act_reading|float|ACT|Average ACT Reading scores for each state|
|act_science|float|ACT|Average ACT Science scores for each state|
|act_composite|float|ACT|Average ACT composite scores for each state|