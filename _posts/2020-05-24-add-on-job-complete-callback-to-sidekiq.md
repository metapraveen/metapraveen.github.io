---
title: 'Adding on job complete callback to sidekiq'
author: Praveen
layout: post
permalink: /add-on-complete-done-callback-to-sidekiq/
---

Came across a use case at work where I wanted record the status of the job I schedule ( enqueued, failed, success ).
On failure sidekiq calls `sidekiq_retries_exhausted` callback. But there is no callback when job is completed successfully. Lets implement this as a sidekiq middleware.

- Write a middleware for sidekiq which calls the on job complete on the job instance if the method is present
<script src="https://gist.github.com/metapraveen/e93c723d54efeb3f8687bcdc56648bab.js"></script>

You can keep this in under configs

- Register this middleware in sidekiq configuration
<script src="https://gist.github.com/metapraveen/1fd24374afe906b4a6bbe7455198847d.js"></script>

- Now you can use this hook in your sidekiq jobs, for e.g. I have a job which gets some data from a url and write to cache
<script src="https://gist.github.com/metapraveen/c3055b93c23a4d9d2f2292e0df688908.js"></script>


