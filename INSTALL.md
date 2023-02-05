# Installation

To toot your own Working Group's document changes, follow these steps:

## 1. Fork this Repo

This service isn't provided in a central repo because we don't want to have your credentials. Create a copy by forking it (so that you can pull updates later).

## 2. Create a Mastadon Application

Assume you have a Mastadon on a server, and BASE_API is said server.

1. Go to BASE_API/settings/applications/new

You will be given three items:

* `Client key`
* `Client secret`
* `Access token`

Currently only `Access token` is used.

## 3. Set Repository Secrets

These reside under https://github.com/ietf-wg-<wgname>/datatracker-toots/settings/secrets/actions

Click on `New Repository Secret` and add the following:

* `WORKING_GROUP` - the short identifier for the WG, e.g., `httpbis`, `tls`. Should be lowercase.
* `TOOT_API_BASE` - the Mastodon instance connected to
* `TOOT_TOKEN_KEY` - the Access Secret


## 4. Randomise the Cron Job

Go into [`.github/workflows/run.yml`](.github/workflows/run.yml) and change this line:

~~~ crontab
    - cron: "15 */4 * * *"
~~~

... to randomise the minute that the job runs at, so that the datatracker API isn't overwhelmed.


## 5. Configure Github Actions

1. If they aren't already, enable Actions under `Settings` -> `Actions`.
2. On the same page, make sure that `Workflow permissions` is set to `Read and write permissions` (so that `LAST_SEEN` can be saved to the repo).
3. Go to the `Actions` top-level tab and click `I understand my workflows, go ahead and enable them`.
4. Under `Workflows`, click on `Tweet Datatracker Events` and make sure it is enabled.


## 6. Update

Once in a while, you should update your copy of the repo, by pulling changes from upstream.

The easiest way to do this is to go to the GitHub home page of your fork of the repo, click 'Fetch upstream' near the top right, and confirm with 'Fetch and merge'.
