---
title: "Migrating My Outsell Rules to Gmail Filters"
comments: true
tags:
  - Outlook
  - Exchange
  - Gmail
  - Email Rules
date: 2025-02-10 15:00:00.000000000 -05:00
excerpt: "5 Filters to Rule Them All."
header:
  teaser: images/stephen-phillips-hostreviews-co-uk-3Mhgvrk4tjM-unsplash-2.jpg
  overlay_image: images/stephen-phillips-hostreviews-co-uk-3Mhgvrk4tjM-unsplash-2.jpg
  overlay_filter: 0.25
  caption: Photo by [**Stephen Phillips** on Unsplash](https://unsplash.com/photos/black-laptop-computer-3Mhgvrk4tjM?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)
categories:
  - Technology
---

I tend to use a few rules to help make email easier to process.
 Yes, I'm one of those guys who has implemented [Getting Things Done](http://www.43folders.com/2004/09/08/getting-started-with-getting-things-done/).

I also try to get to ZEB (Zero Email Bound) every day or so.
 Essentially this is when you "bounce" up against zero emails in your inbox.
  This doesn't mean you've **done** all your tasks, instead you know what
   your **tasks are**.

To help me with this I use a system of rules. Essentially, as email shows up I
 need to process it, but not all emails are created equal. So I segment the
  emails in to the following types:

* **Most Important**: Emails sent directly to me, where my email address is on
 the **To** line.
* **Kind of Important**: Emails where I'm carbon copied (cc'd or bcc'd),
 these are usually a "Heads Up" type of email.
* **External Email**: Mail that was sent to me from **outside** my company.
* **Azure DevOps**: Emails generated from Azure DevOps (Work Item updates,
 Pull requests, etc.)
* **Meeting Invites**: My calendar accepts most invites unless there is a
 conflict. But I review these in case I need to prep for a meeting.

Scott Hanselman has a great write-up on how to implement these rules in
 Microsoft Outlook [The Three Most Important Outlook Rules for Processing Mail](https://www.hanselman.com/blog/the-three-most-important-outlook-rules-for-processing-mail)

However, my company just migrated from Microsoft 365 to Google Workspaces.
 So my challenge is re-creating these events as Gmail Filters.

In Gmail there are no "Folders", instead Gmail uses "Tags" to organize email.
 Before starting with the Filters, create the Tags you need
  (eg Inbox - Azure DevOps, Inbox - External, Inbox - CC, Inbox - Invites")

Gmail uses "Filters", instead of "Rules", you can find these under
 Settings > See all settings, then select the **Filters and Blocked Addresses**
 tab.

Here's how I setup my filters:

* **Most Important**: No filter, this is just what remains in my Inbox

* **Kind of Important**: Matches: `To: -email@company.com`, the dash at the
 beginning means NOT, then `Do this: Skip Inbox, Apply label "Inbox - CC"`

* **External Email**: Matches: `From: -@company.com`, so not to my company,
 then `Do this: Skip Inbox, Apply label "Inbox - External"`

* **Azure DevOps**: Matches: `From: azuredevops@microsoft.com`, then
 `Do this: Skip Inbox, Apply label "Inbox - Azure DevOps"`

* **Meeting Invites**: This is the one I haven't quite figured out yet.
 Outlook had a way to identify the email as an Invite, but Google doesn't seem
  to have a similar criteria filter.
  So for now, these are ending up in my Inbox.
  If you know a Filter to do this, please share it in the comments.
