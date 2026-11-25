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
    content: https://buenno-research.github.io/api/mcp.html
  - name: twitter:card
    content: summary

toc_footers:
  - <a href='/api/'>Buenno API reference</a>
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

* **Charts in the chat:** ask for a chart and the assistant shows one in Buenno's style, such as a trend, a store ranking or the main themes. Clients that can't show Buenno charts draw their own from the same numbers.
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
3. Click **Connect**. The Buenno sign-in page opens: sign in with your Buenno login and allow access.
4. Start a new chat and ask a question about your customer feedback.

On some plans, an owner or admin may need to add the connector for the organisation first.

## Connect in ChatGPT

1. In ChatGPT, open **Settings → Apps** (called **Connectors** on some plans).
2. Find **Buenno**, or create a custom app or connector with the connector URL `https://webreport.buenno.fi/mcp` and OAuth as the authentication.
3. Click **Connect**. The Buenno sign-in page opens: sign in with your Buenno login and allow access.
4. Start a new chat, choose Buenno, and ask a question about your customer feedback.

On some plans, an admin needs to allow custom apps first, or turn on developer mode.

## Staying signed in

The connector keeps you signed in in the background, as long as your Buenno login is allowed to. When the sign-in expires, or when your Buenno password or access changes, your AI client asks you to connect again.

To disconnect, remove the connector in your AI client's settings.

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
* **Your own access.** You sign in with your Buenno login (OAuth 2.0). Every answer is limited to the surveys and stores your account can see in Buenno.
* **No conversation data.** Buenno does not receive your chat with the assistant, only the tool calls it makes, such as "NPS for survey X in October".
* **Audit log.** For security and support, Buenno logs each tool call: who made it, which tool, its arguments, the result status and how long it took.
* **Customer comments** are returned as data. The assistant is told never to follow instructions written in a comment.

# Troubleshooting

Problem | What to do
---- | ----
The sign-in page does not open, or shows an error | Remove the connector in your AI client and add it again. Check that you use `https://webreport.buenno.fi/mcp` exactly.
Sign-in is refused, or no surveys are listed | The Buenno AI Suite is not switched on for your organisation, or your account has no survey access. Ask your Buenno contact person.
A survey or store is missing | The connector shows what your Buenno account can see.
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
