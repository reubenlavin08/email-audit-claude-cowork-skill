\# Multi-Channel Email Audit Skill for Claude Cowork



A hybrid automation skill for Claude Cowork that aggregates communications from Outlook and Gmail into a single, prioritized action list.



\## Overview

This skill solves the split-inbox problem by using a dual-fetch strategy:

1\. Outlook: Utilizes browser-based automation to navigate and parse the web interface.

2\. Gmail: Utilizes the native Claude Google Workspace Connector for high-speed, structured data retrieval.



Running this skill returns a unified summary of your recent emails and outlines urgent action items that require immediate attention.



\## Prerequisites

To use this skill successfully, you must ensure the following:



\* Active Outlook Session: You must be logged into Outlook in a browser tab that Claude Cowork can access.

\* Gmail Connector (Required): You must enable the native Gmail connector in Claude. 

&#x20;   \* How to enable: Click the + icon in the chat interface -> Hover over Connectors -> Toggle Gmail to ON.

&#x20;   \* Note: You may be prompted to complete a Google OAuth sign-in to authorize Claude's read-only access.



\## Installation

1\. Create a folder in your Claude Cowork workspace named email-audit-skill.

2\. Place the skill.md file inside this folder.

3\. Refresh your Claude Cowork session to allow the agent to index the new skill.



\## Usage

Trigger the skill by asking Claude:

"Run my email audit skill" or "Check my Outlook and Gmail for urgent items."



\## Security and Privacy

\* No Credential Storage: This skill does not store passwords or API keys. It relies on your active browser session and official OAuth tokens.

\* Local Processing: All email data is processed within the context of your Claude session and is not transmitted to third-party databases.

\* Read-Only: By design, this skill is configured to read and summarize, not to send or delete emails.

