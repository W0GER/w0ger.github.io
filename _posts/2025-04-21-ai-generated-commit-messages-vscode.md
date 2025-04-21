---
title: "✨ How to Generate Commit Messages with AI in Visual Studio Code"
comments: true
tags:
  - Tools
  - AI
  - Development
  - Git
  - VS Code
date: 2025-04-21 00:00:00.000000000 -05:00
excerpt: "Learn how to save time and write better commit messages using AI tools in VS Code"
header:
  teaser: images/growtika-FQ3lFA4Zi58-unsplash.jpg
  overlay_image: images/growtika-FQ3lFA4Zi58-unsplash.jpg
  overlay_filter: 0.5
  caption: "Photo by [**Growtika**](https://unsplash.com/@growtika?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [**Unsplash**](https://unsplash.com/photos/a-computer-on-a-desk-FQ3lFA4Zi58?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)"
categories:
  - Technology
  - Development
---      

Let's face it - writing good commit messages can be a chore! 📝 But what if AI
could do the heavy lifting for you? Today, I'm sharing how you can use AI to
generate meaningful commit messages right in VS Code. This small change to your
workflow can save time while improving your commit history quality!

## 🤔 Why Good Commit Messages Matter

Before diving into the AI tools, let's remember why we care about commit
messages:

- They provide context for future you (and your teammates)
- They make debugging and code archaeology much easier
- They help with generating changelogs
- They create a useful history of your project's evolution

The problem? Writing good ones takes time and mental energy that could be spent
solving actual problems!

## 🛠️ AI-Powered Solution in VS Code

Using VS Code's message generator is as simple as 1-2-3:

1. Open the Source Control view.
2. Click the star icon next to the message input field.
3. Voila! A pre-populated message summarizing your changes appears, ready to be
   tweaked and approved.

![Screenshot of VSCode highlighting the AI commit button]({{site.post-images}}/Screenshot-ai-commit.png)

## Combining with Conventional Commits

I like using [Conventional Commits](https://www.conventionalcommits.org).
You can provide an instruction to VS Code by adding the following in your
settings.json file:

{{< mdl-disable "<!-- markdownlint-disable MD013 -->" >}}

```json
"github.copilot.chat.commitMessageGeneration.instructions": [
  {
    "text": "Follow the Conventional Commits format strictly for commit messages. Use the structure below:\n\n```\n<type>[optional scope]: <gitmoji> <description>\n\n[optional body]\n```\n\nGuidelines:\n\n1. **Type and Scope**: Choose an appropriate type (e.g., `feat`, `fix`) and optional scope to describe the affected module or feature.\n\n2. **Gitmoji**: Include a relevant `gitmoji` that best represents the nature of the change.\n\n3. **Description**: Write a concise, informative description in the header; use backticks if referencing code or specific terms.\n\n4. **Body**: For additional details, use a well-structured body section:\n   - Use bullet points (`*`) for clarity.\n   - Clearly describe the motivation, context, or technical details behind the change, if applicable.\n\nCommit messages should be clear, informative, and professional, aiding readability and project tracking."
  }
]
```

## 💡 Tips for Better AI-Generated Commit Messages

Even with AI help, here are some tips to get the best results:

- **Review before committing**: Always check what the AI generated - it's not
  perfect!
- **Make atomic commits**: Smaller, focused changes lead to better AI-generated
  messages
- **Add custom context**: Some extensions let you add notes to guide the AI
- **Customize templates**: Adjust the AI's output style to match your team's
  conventions

## 🚀 My Experience

I've been using AI-generated commit messages for the past month, and it's been
a game-changer! Not only does it save me time, but the quality of my commit
history has actually improved. The AI tends to be more thorough and consistent
than my manual messages, especially for small routine changes where I might
have just written "fix bug" or "update styles" 😅.

My team has also noticed the improvement in our repository's commit history.
Finding specific changes is easier, and our changelogs practically write
themselves now!

## 🔮 The Future of Development

This is just one example of how AI is transforming little parts of the
development workflow. While not revolutionary on its own, these small
improvements add up to significant productivity gains.

What's your favorite AI-powered development tool? Have you tried generating
commit messages with AI? Let me know in the comments below! 👇

Happy coding (and committing)! ✨
