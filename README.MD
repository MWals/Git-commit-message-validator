# Git Commit Message Hook Example
date: 2020-10-19
author: Markus Wals, es19m012

## TODO 
Validate commit messages on all branches with a simple regex

## Solution
to enforce that commit messages start with PJM- followed by a 4 digit number.

How does this regex work?

^             Beginning of the string (line anchor)
PJM-          The Letters PJM followed by a - symbol
[0-9]{4}      Issue ID, 4 Digits that can be numbers from 0 - 9
\b            Word boundry

## Examples for good commit messages:
PJM-0001 Anytext
PJM-9999 Some other text
