---
title: 'Github PR review, commitwise vs whole diff'
author: Praveen
layout: post
permalink: /pr-review-commitwise-vs-whole-diff/
---

This topic came up while discussing a big pull request with the team and what is the best way to review it. So thought of writing about it.

Basically, you can review a PR in 2 ways, one by checking the whole diff, and try to understand what is the change and why its made without reading any commit messages and another one is reading commit by commit. Below are the pros and cons of both according to me.

## reviewing commit by commit
pros
- You can follow the PR author's mental model 
- commit messages gives you a lot of contexts
- Every change you see, you relate to a message, so everyone tries to add a clear message, so no more commit messages saying "some fixes", "prod fixes" etc.

cons
- the code in one commit may change in the other one, so you can't make a review comment easily ( or you can make and amend it later )
- If you find code itself is self-explanatory reading commit by commit is time-consuming

## reviewing the whole diff of the PR
pros
- If you have complete context of the codebase this review can be faster
- you will see the code in the final form which wants to go to a stable branch 

cons
- not reading commit message may lead to a difference (e.g. as an author I write a message explaining a workaround from breaking a corner case, as a reviewer you miss the message and find that change is bad )
- For some, it is hard to see the complete change in one go and relate to the codebase

I feel commit messages acts as documentation for your future self and others. Reviewing commit by commit and at the end seeing the whole diff would give you more context and that should lead to faster PR reviews. 

Feel free to leave a comment about what your team follows and how effective it is.  