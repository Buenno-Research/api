---
title: "Buenno MCP: connect Claude and ChatGPT to your customer feedback"

meta:
  - name: description
    content: Connect your AI client, such as Claude, to Buenno and ask about your customer feedback in plain language. NPS, CSAT, trends, stores, customer comments, themes and reports, read-only and with your own Buenno login.
  - property: og:title
    content: "Buenno MCP: connect Claude and ChatGPT to your customer feedback"
  - property: og:description
    content: Connect your AI client, such as Claude, to Buenno and ask about your customer feedback in plain language. NPS, CSAT, trends, stores, customer comments, themes and reports, read-only and with your own Buenno login.
  - property: og:type
    content: website
  - property: og:url
    content: https://docs.buenno.fi/mcp.html
  - name: twitter:card
    content: summary

toc_footers:
  - <a href='/'>Buenno API reference</a>
  - <a href='mailto:info@buenno.fi'>Contact us to enable the AI Suite</a>

search: true
code_clipboard: true
---

# Buenno MCP

Buenno MCP lets you ask about your Buenno customer feedback in plain language, right inside your AI client, and get answers based on the same numbers as your Buenno report.

It is a remote Model Context Protocol (MCP) server. The AI assistant calls it to read your results; you sign in with your own Buenno login, and you only see the surveys and stores your Buenno account has access to.

> Connector URL

```text
https://webreport.buenno.fi/mcp
```

## What you can ask

* NPS, CSAT and overall scores for any period, compared with the previous period
* Trends month by month or week by week
* Rankings and comparisons of stores, areas and countries
* Scores per survey question, how answers are distributed, and response rates
* Customer comments, recurring themes, and what drives satisfaction the most
* AI insights Buenno has spotted, such as a store that is dropping or a growing complaint
* Charts and a full report in Buenno's style, or a complete dataset for building your own slides, documents or dashboards

Every answer states the period and the number of responses it is based on, so you can check the numbers against the Buenno report.

## Example questions

* How did our NPS develop over the last 12 months, and how does last month compare to the month before?
* Which stores had the lowest customer satisfaction last quarter, and what did customers complain about there?
* What do customers say about waiting times in the Helsinki area?
* What explains the drop in NPS from September to October?
* Make a one-page summary of last month's customer feedback with the main numbers, a chart and the top themes from comments.

## Charts and reports

* **Charts in the chat:** the assistant adds a chart when it helps the answer, such as a trend, a store ranking or the main themes, and always in Buenno's style. Hover over a chart to see each value and the number of answers behind it. Clients that can't show Buenno charts draw their own from the same numbers, in Buenno's colours.
* **The full Buenno report inside the chat,** with summary, charts and filters.
* **Your own reports:** ask for a document, PDF, slides or a dashboard for a period, and the assistant builds it from the complete report data, in Buenno's look.

Try: *"Make slides of last quarter's results for our management meeting"* or *"Build a dashboard of our NPS by area."*

# Getting started

## Requirements

* A Buenno account with access to at least one survey.
* The Buenno AI Suite switched on for your organisation. <a href='mailto:info@buenno.fi'>Contact us to enable it</a>.
* An AI client that supports remote MCP connectors with OAuth sign-in, such as Claude.

## Connect in Claude

1. In Claude, open **Settings → Connectors**.
2. Find **Buenno** in the directory, or choose **Add custom connector** and enter the connector URL `https://webreport.buenno.fi/mcp`.
3. Click **Connect**. The Buenno sign-in page opens: sign in with your Buenno login, choose which surveys Claude may see, and allow access.
4. Start a new chat and ask a question about your customer feedback.

On some plans, an owner or admin may need to add the connector for the organisation first.

## Connect in ChatGPT

1. In ChatGPT, open **Settings → Apps** (called **Connectors** on some plans).
2. Find **Buenno**, or create a custom app or connector with the connector URL `https://webreport.buenno.fi/mcp` and OAuth as the authentication.
3. Click **Connect**. The Buenno sign-in page opens: sign in with your Buenno login, choose which surveys ChatGPT may see, and allow access.
4. Start a new chat, choose Buenno, and ask a question about your customer feedback.

On some plans, an admin needs to allow custom apps first, or turn on developer mode.

## Staying signed in

The connector keeps you signed in in the background, as long as your Buenno login is allowed to. When the sign-in expires, or when your Buenno password or access changes, your AI client asks you to connect again.

To disconnect, use **Connected apps** in Buenno (below), or remove the connector in your AI client's settings.

## Choose what each app sees

When you connect, the Buenno sign-in page lists your surveys, grouped by organisation. All are ticked; untick the ones the app shouldn't see. Keep **Also new surveys I get access to** ticked to include surveys you get later.

To change this later, open **Account settings → Connected apps** in Buenno. For each app you see when it was connected, when it was last used and how many questions it asked. **Change surveys** updates the choice from the app's next question. **Disconnect** ends the app's access at once; it then has to ask you to connect again.

Your choice can only narrow what the app sees: never more than you see in the Buenno report.

# For admins

Organisation admins manage AI apps in the **Control Center → AI assistants**. The menu item appears once Buenno has switched AI assistants on for your organisation.

## Settings

* **Let people connect AI apps.** Off blocks every AI app at once; switching it on again restores the existing connections.
* **Surveys open to AI apps.** Close a survey to keep it away from every AI app, for example an employee survey. **New surveys are open to AI apps** decides for surveys created later.
* **What AI apps may read.** Scores, trends and rankings are always included. Open comments and themes, and individual answers, can each be switched off.
* **Who may connect.** Limit connecting to certain roles. No role ticked means every role may connect.
* **Which AI apps.** Allow only apps that prove where they come from, such as Claude and ChatGPT, or any app that supports Buenno sign-in. Apps that registered themselves lose access at once when you switch to the first option.

These settings only narrow access. A person never sees more than their own access in the Buenno report allows.

## Connections

The **Connections** tab shows who in your organisation has connected which AI app, how many of your surveys each connection can read, when it was last used and how many questions it asked about your surveys in the last 30 days. Admins see usage, not the questions themselves.

**Disconnect** ends one person's app; **Disconnect all** ends every AI app of everyone listed. A disconnect ends the app in every Buenno organisation the person belongs to. They can connect again at any time.

# Tools

The connector gives the AI assistant these read-only tools. You don't call them yourself: the assistant picks the right ones for your question.

Tool | What it does
---- | ----
List surveys | The customer feedback surveys you can report on and the metrics available for each.
Find stores and areas | The stores, areas and countries you can see in a survey.
Score overview | Headline NPS, CSAT or overall score for a period, with the number of responses and the change from an earlier period.
Score trend | NPS, CSAT or overall score month by month or week by week.
Scores by store, area and more | Ranks stores, areas, countries, sellers, product categories or weekdays by score.
Question scores | Average score per survey question, for the whole chain or per store.
Answer distribution | How often each answer option was chosen.
Response rate | Responses compared with invitations sent.
Customer comments | Customers' open comments, filtered by sentiment, keyword, store or area.
Individual responses | Individual survey responses with their scores and comments.
Comment themes | The main themes in open comments and how often each is mentioned positively or negatively.
Key drivers | What drives the score up or down, and what explains a change between two periods.
AI insights | Patterns Buenno's AI has spotted in the results.
Buenno chart | A chart of a result inside the chat, in Buenno's style.
Buenno report | The interactive Buenno report inside the chat.
Buenno report dataset | All the numbers for a period report in one call, for building documents, slides or dashboards.

The connector also offers ready-made prompts: **Monday summary**, **Period report**, **Explain a change** and **Store check**.

# Security and privacy

* **Read-only.** The connector never changes your Buenno data.
* **Your own access.** You sign in with your Buenno login (OAuth 2.0). Every answer is limited to the surveys and stores your account can see in Buenno, and to the surveys you chose for the app.
* **Your organisation decides.** Admins choose which surveys and data AI apps may read, who may connect and which apps are allowed.
* **No conversation data.** Buenno does not receive your chat with the assistant, only the tool calls it makes, such as "NPS for survey X in October".
* **Audit log.** For security and support, Buenno logs each tool call: who made it, which tool, its arguments, the result status and how long it took.
* **Customer comments** are returned as data. The assistant is told never to follow instructions written in a comment.

# Troubleshooting

Problem | What to do
---- | ----
The sign-in page does not open, or shows an error | Remove the connector in your AI client and add it again. Check that you use `https://webreport.buenno.fi/mcp` exactly.
Sign-in is refused, or no surveys are listed | The Buenno AI Suite is not switched on for your organisation, or your account has no survey access. Ask your Buenno contact person.
A survey or store is missing | The connector shows what your Buenno account can see, limited to the surveys you chose for the app (**Account settings → Connected apps**) and the surveys your organisation opens to AI apps.
The assistant says the data is being prepared | Buenno is preparing the numbers for that period. The assistant tries again after a few seconds; ask again if it doesn't.
The assistant says there were too many requests | Wait a minute and ask again.
Your AI client asks you to connect again | Your sign-in expired. Click **Connect** and sign in.
A number differs from the Buenno report | Check that the period, survey and store filters match. The answer states them.

# FAQ

## What is Buenno MCP?

Buenno MCP connects AI assistants such as Claude and ChatGPT to Buenno, so you can ask about your customer feedback in plain language: NPS, CSAT, trends, stores, customer comments and themes. Answers are based on the same numbers as your Buenno report.

## Can I use Buenno MCP with ChatGPT?

Yes. Buenno MCP works with AI clients that support remote MCP connectors with OAuth sign-in, such as Claude and ChatGPT.

## Does Buenno MCP change my data?

No. Buenno MCP is read-only. It never changes your Buenno data.

## Who can see what?

You see the same as in the Buenno webreport. You sign in with your own Buenno login, and every answer is limited to the surveys and stores your account can see there. Colleagues with different access see different results.

## Can I limit what an AI app sees?

Yes. When you connect, you choose which surveys the app may see, and you can change that later in **Account settings → Connected apps**. Your organisation's admins can also close surveys, comments or individual answers to all AI apps.

## Does Buenno receive my conversation with the AI assistant?

No. Buenno only receives the tool calls the assistant makes, such as a request for NPS for one survey in October, not your chat.

## Can it make charts, slides or reports?

Yes. Ask for a chart, the full Buenno report, or a document, PDF, slides or dashboard for a period, and the assistant builds it from your Buenno numbers in Buenno's look.

## Do I need technical skills?

No. Once the connector is added, you just ask questions in the chat. The assistant picks the right data itself.

<script type="application/ld+json">
{
 "@context": "https://schema.org",
 "@type": "FAQPage",
 "mainEntity": [
  {
   "@type": "Question",
   "name": "What is Buenno MCP?",
   "acceptedAnswer": {
    "@type": "Answer",
    "text": "Buenno MCP connects AI assistants such as Claude and ChatGPT to Buenno, so you can ask about your customer feedback in plain language: NPS, CSAT, trends, stores, customer comments and themes. Answers are based on the same numbers as your Buenno report."
   }
  },
  {
   "@type": "Question",
   "name": "Can I use Buenno MCP with ChatGPT?",
   "acceptedAnswer": {
    "@type": "Answer",
    "text": "Yes. Buenno MCP works with AI clients that support remote MCP connectors with OAuth sign-in, such as Claude and ChatGPT."
   }
  },
  {
   "@type": "Question",
   "name": "Does Buenno MCP change my data?",
   "acceptedAnswer": {
    "@type": "Answer",
    "text": "No. Buenno MCP is read-only. It never changes your Buenno data."
   }
  },
  {
   "@type": "Question",
   "name": "Who can see what?",
   "acceptedAnswer": {
    "@type": "Answer",
    "text": "You see the same as in the Buenno webreport. You sign in with your own Buenno login, and every answer is limited to the surveys and stores your account can see there. Colleagues with different access see different results."
   }
  },
  {
   "@type": "Question",
   "name": "Can I limit what an AI app sees?",
   "acceptedAnswer": {
    "@type": "Answer",
    "text": "Yes. When you connect, you choose which surveys the app may see, and you can change that later in Account settings → Connected apps. Your organisation's admins can also close surveys, comments or individual answers to all AI apps."
   }
  },
  {
   "@type": "Question",
   "name": "Does Buenno receive my conversation with the AI assistant?",
   "acceptedAnswer": {
    "@type": "Answer",
    "text": "No. Buenno only receives the tool calls the assistant makes, such as a request for NPS for one survey in October, not your chat."
   }
  },
  {
   "@type": "Question",
   "name": "Can it make charts, slides or reports?",
   "acceptedAnswer": {
    "@type": "Answer",
    "text": "Yes. Ask for a chart, the full Buenno report, or a document, PDF, slides or dashboard for a period, and the assistant builds it from your Buenno numbers in Buenno's look."
   }
  },
  {
   "@type": "Question",
   "name": "Do I need technical skills?",
   "acceptedAnswer": {
    "@type": "Answer",
    "text": "No. Once the connector is added, you just ask questions in the chat. The assistant picks the right data itself."
   }
  }
 ]
}
</script>

# Support

For questions or problems, contact your Buenno contact person.
