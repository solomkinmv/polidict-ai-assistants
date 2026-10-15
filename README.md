# Polidict

Polidict is a vocabulary app for language learners. This plugin connects your Polidict account to Claude, ChatGPT and other AI assistants, so you can build and practise your vocabulary in conversation. What you save syncs with the Polidict website, mobile apps and browser extension.

## What you can do

- Look up words and save them with meanings, translations, examples and notes
- Find and edit your saved words without losing existing meanings or progress
- Organize words into groups
- Pick a credited photo for a word from image search results
- Practise meaning, writing, listening and speaking with words that are due for review
- See your progress with a word and your plan's remaining capacity

Try asking:

- "What does resilient mean? Add it to my English words with two examples."
- "Help me practise five of my English words, one question at a time."
- "Create a Weekend Trips group and add bridge and forest to it."

## What's included

| Component | Purpose |
|---|---|
| MCP server `https://api.polidict.com/mcp` | 13 tools for words, groups, images, progress and practice |
| Skill `manage-vocabulary` | How to add, edit and organize words, images and groups safely |
| Skill `practice-vocabulary` | How to run exercises, grade attempts and save only confirmed results |

## Install

In Claude Code:

```text
/plugin install polidict --marketplace solomkinmv/polidict-ai-assistants
```

In Claude, ChatGPT and other apps, install Polidict from the app's plugin or connector directory, or add the MCP server URL `https://api.polidict.com/mcp` as a custom connector.

## Requirements

A Polidict account (free plan available) from [polidict.com](https://polidict.com) or the Polidict mobile app. The first tool call opens Polidict's sign-in and consent page (OAuth); you choose what to allow. Disconnect at any time from Polidict's connected-apps settings.

## Data and privacy

The plugin runs no local code. It only connects to Polidict's MCP server at `api.polidict.com` over HTTPS.

- **Sent to Polidict:** tool requests such as search terms, words and groups you add or edit, image selections, and practice results you confirm. Not your whole conversation.
- **Returned to the assistant:** your profile, plan and capacity, learning languages, saved words, groups and progress.
- **Third parties:** image search queries go to stock photo providers (Unsplash, Pexels). Saved word text may be sent to text-to-speech providers to create pronunciation audio.
- **Practice:** exercises stay in the conversation. Polidict stores only the outcome you approve for each answer, never your answer text or audio.

Read the full [privacy policy](https://polidict.com/privacy-policy) and [terms of service](https://polidict.com/terms-of-service).

## Support

Email [support@polidict.com](mailto:support@polidict.com) or see the [setup guide](https://polidict.com/en/ai/mcp).

## License

[PolyForm Noncommercial 1.0.0](LICENSE): you may use, modify and share this plugin for noncommercial purposes. Anyone may install and use the unmodified plugin with their Polidict account, including at work. Other commercial use needs permission from [support@polidict.com](mailto:support@polidict.com).
