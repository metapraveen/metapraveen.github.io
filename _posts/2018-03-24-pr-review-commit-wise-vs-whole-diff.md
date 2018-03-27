---
title: 'Github PR review, commitwise vs whole diff'
author: Praveen
layout: post
permalink: /pr-review-commitwise-vs-whole-diff/
---

This topic came up while discussing a big pull request with the team and what is the best way to reivew it. So thought of writing about it.

Basically you can review a PR in 2 ways, one by checking the whole diff, and trying to understand what is the change and why its made without reading any commit messages and other one is reading commit by commit. Below are the pros and cons of both according to me.

## reviwing commit by commit
pros
- You can follow the PR author's mental model 
- commit messages gives you a lot of context
- This leads to avoiding commit messages saying "prod fixes", "tests update" etc.

cons
- code in one commit may change in the other one, so you can't make a review comment easily ( or you can make and ammend it later )

## reviwing the whole diff of the PR
pros
- If you have complete context of the codebase this review can be faster
- you will see the code in final form which want to go to stable branch 

cons
- not reading commit message may lead to difference from the author
- commit messages gets ignored while doing any changes

I feel commit messages acts as documentation for your future self and others. Reviewing commit by commit and at the end seeing the whole diff would give you more context and that should lead to faster PR reviews. 
