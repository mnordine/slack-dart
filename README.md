# slack_notifier

Dart wrapper for posting messages to Slack using Incoming Webhooks.

[![Build Status](https://github.com/javoeria/slack-dart/actions/workflows/dart.yml/badge.svg?branch=master)](https://github.com/javoeria/slack-dart/actions/workflows/dart.yml)
[![pub package](https://img.shields.io/pub/v/slack_notifier.svg)](https://pub.dev/packages/slack_notifier)

## Getting Started

Incoming Webhooks are a simple way to post messages from apps into Slack. Creating an Incoming Webhook gives you a unique URL to which you send a JSON payload with the message text and some options. You can use all the usual [formatting](https://api.slack.com/reference/surfaces/formatting) and [layout blocks](https://api.slack.com/messaging/composing/layouts) with Incoming Webhooks to make the messages stand out.

To get the WEBHOOK_URL you need:

1. Create a Slack app (if you don't have one already)
2. Enable Incoming Webhooks
3. Create an Incoming Webhook
4. Use your Incoming Webhook URL to post a message

Read more about webhooks [here](https://api.slack.com/messaging/webhooks).

## Usage

This method posts a message to a public channel, private channel, or direct message/IM channel.

```dart
final slack = SlackNotifier('WEBHOOK_URL');
slack.send(
  'Hello world',
  channel: 'general',
  iconEmoji: ':chart_with_upwards_trend:',
  iconUrl: 'https://picsum.photos/48/48',
  username: 'My Bot',
  blocks: [SectionBlock(text: 'Hello world')],
  attachments: [Attachment(pretext: 'pre-hello', text: 'text-world')],
);
```

The usage of the `text` field changes depending on whether you're using `blocks`. If you are using `blocks`, this is used as a fallback string to display in notifications. If you aren't, this is the main body text of the message. It can be formatted as plain text, or with `mrkdwn`.

## Blocks

Blocks are a series of components that can be combined to create visually rich and compellingly interactive messages. [Block Kit](https://api.slack.com/reference/block-kit) can make your app's communication clearer while also giving you consistent opportunity to interact with and assist users.

- `ActionsBlock` A block that is used to hold multiple interactive elements.
- `ContextBlock` Used for contextual info, which can include both images and text.
- `DividerBlock` A content divider used to visually separate pieces of info inside of a message.
- `FileBlock` Used with remote files to display info about the attached files.
- `HeaderBlock` A larger-sized text block used as a header.
- `ImageBlock` A simple image block, designed to make those cat photos really pop.
- `InputBlock` A block that collects information from users in a multitude of ways.
- `SectionBlock` Display text or combine text with interactive elements and images.
- `VideoBlock` A block designed to display those cool cat videos.

Individual blocks can be stacked together to create complex visual layouts.

```dart
var blocks = [
  HeaderBlock(text: 'Onboarding'),
  SectionBlock(text: 'Example message for engaging new users.'),
  DividerBlock(),
  SectionBlock(text: "Hey there :wave: I'm *TaskBot*. I'm here to help you create and manage tasks in Slack."),
  ImageBlock(
    imageUrl: 'https://api.slack.com/img/blocks/bkb_template_images/onboardingComplex.jpg',
    altText: 'image1',
    title: 'image1',
  ),
];
slack.send('Onboarding', channel: 'general', blocks: blocks);
```
