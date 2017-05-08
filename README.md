# Heroku Scaler - AWS Lambda Edition

## What is this?

An AWS Lambda function for applying batch updates to the formation used by
a Heroku application.

When coupled with [CloudWatch Schedule Events][], it provides a simple way to
implement time-based autoscaling for your dynos. This is ideal if you're
ineligible for Heroku's [Autoscaling][] offering but want to scale down during
times of reduced activity.

Personally, I wanted to...

* host a project that's only awake when I am
* be eligible for Heroku SSL and [Automated Certificate Management][] by using
  a paid tier
* spend less than I'd spend on an unmanaged setup on [DigitalOcean][]

[CloudWatch Schedule Events]: https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/ScheduledEvents.html
[Autoscaling]: https://devcenter.heroku.com/articles/scaling#autoscaling
[Automated Certificate Management]: https://devcenter.heroku.com/articles/automated-certificate-management
[DigitalOcean]: https://www.digitalocean.com/
