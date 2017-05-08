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

## Event Format

For consistency, the event format is equivalent to the payload specified in
Heroku's [Formation Batch Update][] documentation.

  ```javascript
  {
    "updates": [
      {
        "type": "web",
        "quantity": 1
      }
    ]
  }
  ```

## Getting Started

1. **Setup [apex](https://github.com/apex/apex) for deploying to AWS.** This is
   optional but simplifies provisioning and environment configuration.

1. **Install npm packages for the function.**

    ```bash
    $ pushd functions/scale-dyno
    $ npm install
    $ popd
    ```

1. **Copy the configuration template and add your Heroku API token and
   application name.**

    ```bash
    $ cp env.json.example env.json
    ```

1. **Build and deploy the function to AWS.**

    ```bash
    $ apex build scale-dynos > /tmp/scale-dynos.zip
    $ apex deploy scale-dynos --zip /tmp/scale-dynos.zip --env-file env.json
    ```

1. **Test a scaling event by invoking the function.** This will change the
   formation, so be sure you're ready to do this!

    ```bash
    $ echo -n '{ "updates": [{ "type": "web", "quantity": 1 }] }' | apex invoke scale-dynos
    ```

[CloudWatch Schedule Events]: https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/ScheduledEvents.html
[Autoscaling]: https://devcenter.heroku.com/articles/scaling#autoscaling
[Automated Certificate Management]: https://devcenter.heroku.com/articles/automated-certificate-management
[DigitalOcean]: https://www.digitalocean.com/
[Formation Batch Update]: https://devcenter.heroku.com/articles/platform-api-reference#formation-batch-update
