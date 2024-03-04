---
title: "Lessons Learnt during the developtmen of `corssfire` Python package"
summary: Few thoughts and notes about the lessons I learnt while being mentored by Cuducos.
tags:
  - Python
  - En
date: "2023-03-04T00:00:00Z"

image:
  caption:
  focal_point: center
---

## Debuging in test
I already knew about the importance of debugging. Althought I never used it. But something that I didn't know is that I could debug the test, also.
This can be done by importing `pytest` to the source code, and adding `pytest.set_trace()` before the line that I want to debug. Then, I can run the test with the `-k` parameter, which will run only the test that I want to debug. 
tHE `set_trace` makes the test stop and leave the terminal so we can call the objects and functions to confirm it they are as expected.
[here (in Pt-Br)](https://github.com/FelipeSBarros/crossfire/pull/74#discussion_r1407879899)

## TDD is about exploring issues rather than a solution
At some point during the package development, I was facing an issue when trying to set a return value for a mocked function. After a long time analysing my code and not identifying the issue, I found in *Stack Over Flow* (yes, I still using it :) a suggestion of setting the `autospec` parameter to `True`. Of course I looked up at the `pytest` documentation to [try to] understand what does it do, but all I got was some glue about it. I decided, anyway, to use it and commit the code beliving I have solved [apparently] the issue. So, then, Cuducos adviced me:  

> Ok, so never add code you don't understand. Never. You can use it to ask: hey, I noticed that when I add that, it works for you. But this is a way to explore the issue rather than a solution. ([@cuducos](cuducos.me))
[here](https://github.com/FelipeSBarros/crossfire/pull/103#discussion_r1509013934)

