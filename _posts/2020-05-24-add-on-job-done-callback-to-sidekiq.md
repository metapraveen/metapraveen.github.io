---
title: 'Adding on job done callback to sidekiq'
author: Praveen
layout: post
permalink: /add-on-job-done-callback-to-sidekiq/
---

Came across a use case at work where I wanted record the status of the job I schedule ( enqueued, failed, success ).
On failure sidekiq calls `sidekiq_retries_exhausted` callback. But there is no callback when job is completed successfully. Lets implement this as a sidekiq middleware.

- Write a middleware for sidekiq which calls the method if present

```ruby
module Middleware::Server
  class JobDone
    def call(worker, msg, queue)
      yield
      args_to_job = msg["args"]
      worker.on_job_done(args_to_job) if worker.respond_to?(:on_job_done)
    end
  end
end
```
You can keep this in under configs

- Register this middleware in sidekiq configuration

```ruby
Sidekiq.configure_server do |config|
  ...
  config.server_middleware do |chain|
    chain.add Middleware::Server::JobDone
  end
end
```

- Now you can use this hook in your sidekiq jobs, for e.g. I have a job which gets some data from a url and write to cache

```ruby
class DownloadAndWriteToCache
  include Sidekiq::Worker

  def perform(url, cache_id, name, meta)
    ...
  end

  def on_job_done(args)
    url = args[0]
    cache_id = args[1]
    name = args[2]
    meta = args[3]
    ...
  end
end
```



