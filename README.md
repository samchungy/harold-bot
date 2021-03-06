<!--
title: Harold The Question Bot
layout: Doc
-->

# Project Board
https://trello.com/b/iAvdXVNU/harold-bot

# harold-question-bot

A simple slack bot which will ask a random member of the #under30s channel a random question

## Cron Schedule
Runs Monday to Friday at 10.15am AEDT

## About
Project is deployed using the serverless framework.

Harold runs as a nodeJS Lambda which is triggered on a Cron Schedule. He uses the `groups.info` Slack API to retrieve a list of user's for a channel and then sends a question to the channel via a webhook. You can access Harold's slack integration options from here: https://api.slack.com/apps/A81E1D9U1 If you do not have access PM @sean on Slack to be added as a contributor.

The list of questions is provided as a separate text file resource to the main application logic.

## Blacklisting Users

Since the `groups.info` returns all members of a group, it will also return inactive users and bots. Harold has a simple blacklist mechanism which takes an array of userID's and reselects a user if a blacklisted user is chosen. To blacklist a user, simply add their userID to the memberBlacklist array in `handler.js`.

## Deploy

To deploy harold, configure serverless credentials locally and then run:

`sls deploy --aws-profile default --verbose`

## Run Locally

To run it locally:

1. Comment out `- schedule: cron(15 23 ? * SUN-THU *)`
2. Uncomment the `- httpApi: 'GET /handler'` line.
3. run `sls offline`


## Secrets

Create an .env file with the following content:

```
OAUTH_TOKEN=X
ENVIRONMENT=prod
U30_SLACK_CHANNEL_ID=X
U30_WEBHOOK_URL=X
```

## Notes
TOKEN constant is the Oauth token
