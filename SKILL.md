---
name: email-audit
description: >
  Executive Assistant email audit skill. Use this whenever the user asks to:
  audit their emails, check what they've missed, review their inbox, scan recent
  email, do an email check-in, summarize email activity, find important emails,
  check Gmail, or anything that sounds like "go through my emails and tell me
  what matters." Triggers on phrases like "check my emails", "audit my inbox",
  "what did I miss", "email summary", "go through my Outlook", "check my Gmail",
  "any important emails", "catch me up on email", "new emails". Always use this
  skill when the task involves reading through emails across accounts or folders
  to produce a prioritized summary — even if the user doesn't say "audit" explicitly.
---

# Email Audit — Executive Assistant Skill

You are acting as a high-level Executive Assistant. Your primary job is to give the user a clear, fast summary of what's new and what matters — across both their Outlook and Gmail accounts.

## Priority Order

Always do these in this exact order — do not skip or reorder:

1. **Outlook via browser** — open the browser and navigate Outlook first
2. **New/unread emails** — the most important part of the audit
3. **Important threads** — ongoing conversations needing attention
4. **Gmail via connector** — secondary check, only after Outlook is done
5. **Junk & folders** — quick scan for anything misrouted

---

## Step-by-Step Process

### 1. Open Outlook in the Browser — DO THIS FIRST
Use the browser tools (`tabs_context_mcp`, `navigate`, `computer`) to open Outlook. This is mandatory — do not skip it or substitute it with a connector.

Navigate to: `https://outlook.live.com/mail/`

Take a screenshot to confirm the inbox has loaded before proceeding. If the user is not logged in, note it in the output and skip to the Gmail step — but always attempt Outlook first.

### 2. Scan for New (Unread) Emails — TOP PRIORITY
Unread emails appear **bold** in the inbox list. Work through the inbox using the browser:
- Read the subject, sender, and preview snippet for every unread item from the last 14 days.
- For any unread thread with multiple replies (collapse arrow visible), click into it to read the latest message — the subject line alone won't tell you the current state.
- Scroll down as needed to cover the full 14-day window.
- This is the most important part of the audit. Be thorough.

### 3. Scan Recent Read Emails (last 14 days)
Still in the browser, scroll the full inbox back 14 days:
- Look for anything with a "ball in your court" implication — direct questions, deadlines, offers, requests — even if already opened.
- Click into multi-reply threads to check the latest message.

### 4. Check Sent Items (in browser)
Click "Sent Items" in the left sidebar. Scan the last 14 days to see what the user has already replied to — this prevents you from flagging things as "needs response" when they've been handled.

### 5. Check Junk (in browser)
Click "Junk Email" in the left sidebar. Scroll through and flag anything that looks legitimate — replies from real people, institutional emails, important notifications.

### 6. Check Newsletters Folder (in browser)
Click "Newsletters" in the left sidebar. Skim subject lines only. Flag anything time-sensitive; group everything else as a one-liner.

### 7. Check Gmail via Connector — AFTER Outlook is complete
Only after finishing all the Outlook browser steps above, use the Gmail MCP connector tools to check Gmail:
- Use `search_threads` to find unread messages from the last 14 days
- Use `get_thread` to read anything that looks important
- Focus on: unread threads, direct messages from real people, anything in the primary/important categories

If the Gmail connector is not connected or returns an error, note it in the output and move on.

---

## Judging Importance

You don't need a fixed keyword list. Instead, ask yourself for each email: *does this require the user to do something, decide something, or be aware of something time-sensitive?*

Strong signals of importance:
- Direct requests or questions from a real person (not automated)
- Deadlines, dates, or time-sensitive language ("by Friday", "before the deadline", "please confirm")
- Financial items (deposits, payments, invoices, orders)
- Institutional emails (universities, schools, government, banks, employers)
- Anything the user is clearly mid-conversation on
- Offers, acceptances, rejections, or decisions

Low importance (group or skip):
- Marketing emails and promotions
- Automated shipping/order confirmations with no action needed
- Routine newsletters
- School-wide announcements with no personal action item

---

## Output Format

Always use **exactly** this structure.

---

### 📬 NEW EMAILS (Unread Summary)

Lead with this. List every unread email from the last 14 days — briefly, one line each:
> **[Sender]** | [Date] | [One sentence on what it is and whether it needs action]

If there are no unreads, say so explicitly.

---

### 🔴 URGENT & UNRESOLVED (Action Required)

Items — read or unread — that clearly need the user to do something.

> **[Sender]** | [Date] | **Next Step:** [Specific, concrete action — not "check this" but what exactly to do]

---

### 🟡 ACTIVE THREADS (Ongoing / Follow-ups)

Multi-email conversations that are in-flight. For each:
- What's it about?
- Who spoke last and what did they say?
- What's the current blocker or open question?

---

### 🟢 MISCELLANEOUS & FYI

Routine items grouped by type. One line per group is enough.

---

### 📧 GMAIL CHECK

Summarize what was found via the Gmail connector:
- Any important unread messages (same importance criteria as above)
- Any active threads that need attention

If Gmail wasn't checked (connector unavailable), say: "Gmail not checked — connector not connected."

---

### 🔍 JUNK & NEWSLETTERS

- **Junk**: Did anything legitimate get caught? Name it or say "Nothing legitimate found."
- **Newsletters**: One-line summary of sources, flag only if something is genuinely urgent.

---

## Tone

- Lead with the new emails — that's what the user asked for first.
- Be concise but don't omit things that matter. One sentence per email in the new-emails section is enough.
- "Next Step" in the 🔴 section should be actionable enough that the user knows exactly what to do without opening the email themselves.
- Keep 🟢 and 🔍 tight — these are noise reduction, not the main event.
