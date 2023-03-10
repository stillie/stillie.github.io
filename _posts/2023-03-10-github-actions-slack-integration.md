---
title: How to Integrate GitHub Actions with Slack Bots
date: 2023-04-10
categories: [Development,Slack,Github-Actions]
tags: [github-actions,slack-bot,integration]
---

# How to Integrate GitHub Actions with Slack Bots

GitHub Actions is a powerful automation tool that allows you to build, test, and deploy your code directly from GitHub. Slack, on the other hand, is a popular collaboration tool that many teams use to communicate and stay organized. Integrating GitHub Actions with Slack bots can be a useful way to keep your team informed when a certain event occurs in your GitHub repository. In this tutorial, we'll show you how to set up this integration step-by-step.

## Step 1: Create a new Slack bot

1. Navigate to the [Slack API page](https://api.slack.com/apps) and create a new bot user.
2. Take note of the bot token as you'll need it later in the process.

## Step 2: Configure the Slack bot settings

1. Configure the bot's settings, including setting up permissions and adding the bot to the appropriate Slack channels.
2. Follow the instructions provided by Slack to complete this step.

## Step 3: Create a new GitHub action

1. Create a new YAML file in your repository under the `.github/workflows` directory.
2. Add the following code to the YAML file:

```yaml
name: Slack Notification
on:
  push:
    branches:
      - main
jobs:
  slack_notification:
    runs-on: ubuntu-latest
    steps:
      - name: Notify Slack
        uses: rtCamp/action-slack-notify@v2.2
        env:
          SLACK_WEBHOOK: ${{ secrets.SLACK_WEBHOOK }}
        with:
          status: ${{ job.status }}
          text: 'A push event occurred in the main branch'

```

## Step 4: Add secrets to your repository

1. Go to your repository's settings and click on "Secrets".
2. Add a new secret with the name `SLACK_WEBHOOK` and the value set to your Slack webhook URL.

## Step 5: Test the integration

1. Make a push to the main branch of your repository.
2. If everything is set up correctly, you should receive a message in your Slack channel indicating that a push event occurred.

## Conclusion

Integrating GitHub Actions with Slack bots can be a powerful way to keep your team informed when important events occur in your GitHub repository. By following the steps outlined in this tutorial, you'll be able to set up this integration in no time. Keep in mind that this is just one example of how you can use GitHub Actions and Slack bots together, so feel free to customize and experiment with this setup to fit your specific needs.
