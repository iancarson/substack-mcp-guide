# Substack MCP Workflow Prompts

Ready-to-use Claude prompts for common Substack tasks via MCP. Copy, paste, and adapt.

---

## Drafting & Publishing

### Draft a newsletter issue

```
Using the Substack MCP, create a new draft with the following:
- Title: [your title]
- Subtitle: [your subtitle]
- Body: [paste your content or describe what to write]
- Section: [if you use sections]

Save as a draft, do not publish.
```

### Write and publish a Note

```
Write a Substack Note about [topic]. Keep it under 300 characters.
Make the first line a strong hook.
End with: "I cover this weekly — subscribe at [your URL]"

Post it now using the Substack MCP.
```

### Convert newsletter to 5 Notes

```
I'm going to paste my newsletter issue below.
Read it and write 5 Substack Notes based on the key ideas.

Rules:
- Each Note should be a standalone insight (no "this week I wrote about...")
- First line of each Note must work as a hook
- Vary the formats: mix insights, lists, and questions
- Under 400 characters each

After writing all 5, ask me which ones to post and which to save as drafts.

[Paste newsletter below]
```

---

## Archive & Research

### Summarize recent newsletters

```
Using the Substack research MCP, download my last 10 newsletter issues from [your Substack URL].

Then:
1. List the main topic of each issue
2. Identify the 3 most common themes across all 10
3. Identify any topics I haven't covered that would fit my niche
```

### Analyze a competitor newsletter

```
Using the Substack MCP, download the last 20 issues of [newsletter URL].

Analyze:
1. What topics do they cover most often?
2. What's their average post length?
3. What formats do they use (listicle, essay, interview, etc.)?
4. What questions do their readers ask in comments?

Give me a 1-page summary I can use to identify gaps in their coverage.
```

### Find my best-performing content

```
List my last 30 Substack posts using the MCP.
For each, show: title, publish date, and any available engagement data.

Rank them by engagement (restacks, likes, comments).
What do the top 5 have in common?
What should I write more of?
```

---

## Batch Operations

### Schedule Notes for the week

```
I'm going to give you 5 Note drafts. For each one:
1. Review and improve the first line to make it a stronger hook
2. Check it fits under 400 characters
3. Save it as a Substack draft

Then list all 5 with their draft titles so I can schedule them manually.

Notes:
1. [Note 1 text]
2. [Note 2 text]
3. [Note 3 text]
4. [Note 4 text]
5. [Note 5 text]
```

### Audit existing drafts

```
Using the Substack MCP, list all my current drafts.

For each draft:
1. Show the title and creation date
2. Flag any that are over 30 days old
3. Suggest which ones are ready to publish vs. need more work

Show me a prioritized list of what to publish first.
```

---

## Content Repurposing

### Turn a newsletter into a LinkedIn post

```
Read my latest Substack newsletter using the MCP.

Then write a LinkedIn post based on the main insight:
- 400–800 characters
- First line must be a standalone hook (no "this week I wrote about...")
- Professional tone (LinkedIn readers don't know my Substack world)
- End with: "I cover this in [Newsletter Name] every [day]. Subscribe at [URL]"
- No external links in the body (I'll add the link in the first comment)
```

### Generate tweet thread from newsletter

```
Read my latest Substack newsletter using the MCP.

Write a Twitter/X thread:
- Tweet 1: Most contrarian or surprising claim from the newsletter (under 280 chars)
- Tweets 2-6: One supporting point each (under 280 chars, numbered "2/7" etc.)
- Tweet 7: Synthesis + link to the full newsletter

Format each tweet on its own line.
```

---

## Automation Workflow (Advanced)

### Full Sunday batch workflow

```
Today is Sunday. Help me prepare the coming week's Substack content.

Step 1: Read my last newsletter issue using the Substack MCP to understand this week's theme.

Step 2: Write 5 Substack Notes based on that theme.
- Mix formats: 2 insights, 1 list, 1 question, 1 behind-the-scenes
- Under 400 characters each
- Strong first lines

Step 3: For Notes 1 and 4, also write LinkedIn-adapted versions (standalone, professional tone, under 800 chars).

Step 4: Save all 5 Notes as Substack drafts using the MCP.

Step 5: Give me a summary of what's been saved and what I need to do manually (scheduling times, LinkedIn posting).
```

---

## Tips for Better Results

1. **Be specific about length** — Claude will write appropriately for the format if you specify character or word limits
2. **Ask for drafts first, post second** — always review before publishing; add "save as draft, don't post yet" to your prompt
3. **Specify the audience** — "write for newsletter writers who are non-technical" vs. "write for developers" changes output significantly
4. **Batch similar tasks** — Claude works faster and more coherently when writing 5 Notes in one prompt vs. 5 separate conversations

---

## Narrareach Integration Note

MCP prompts give you Claude-native control over your Substack drafts. For the publishing, scheduling, and cross-platform distribution layer — [Narrareach](https://narrareach.com) handles automatic cross-posting to LinkedIn, Medium, and X with cloud-based scheduling and subscriber attribution analytics. Many writers use both: Claude + MCP for writing, Narrareach for distribution.
