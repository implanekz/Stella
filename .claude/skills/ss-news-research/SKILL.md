---
name: ss-news-research
description: Search YouTube, Reddit, and the web for Social Security news relevant to Ret1re.com's focus on strategic filing decisions, delayed benefits, and the 62-70 window. Uses OpenRouter API (Perplexity Sonar model).
---

# Social Security News Research Skill

## When to Use

Use this skill when Kurt asks for:
- Social Security news, updates, or policy changes
- Research on SS-related content across YouTube, Reddit, or other platforms
- Competitive intelligence on what others are saying about Social Security filing strategy
- Content ideas based on current SS discussions and trends

## Process

### 1. Load Context

Read these files to understand what's relevant:
- `@context/work.md` — business focus, key frameworks, target audience
- `@context/current-priorities.md` — what Kurt is working on right now

### 2. Review Previous Reports

Read all existing files in `research/` (most recent first). Note what topics, stories, videos, Reddit threads, and competitive findings have already been reported. **Do not repeat these in the new report.** Only include:
- Genuinely new developments since the last report
- Significant updates to previously reported stories (e.g., a bill that was proposed last time has now passed)
- New content creators, videos, or discussions not previously covered

If nothing meaningfully new has emerged in a category, say so briefly (e.g., "No new policy changes since last report") rather than restating old information.

### 3. Formulate Queries

Build search queries targeting these angles:
- **Policy & legislative:** Social Security rule changes, COLA updates, earnings limits, FRA changes
- **Strategy & filing:** delayed filing, spousal benefits, break-even analysis, claiming strategies
- **Content & media:** YouTube creators covering SS topics, trending Reddit threads (r/SocialSecurity, r/retirement, r/financialplanning, r/personalfinance)
- **Demographic:** content targeting the 55+ educated professional audience (Kurt's "Strategic 15%")

### 4. Run Research

Call the OpenRouter API using the key from `.env`:

```bash
curl -s "https://openrouter.ai/api/v1/chat/completions" \
  -H "Authorization: Bearer $OPENROUTER_API_KEY" \
  -H "Content-Type: application/json" \
  -H "HTTP-Referer: https://ret1re.com" \
  -H "X-Title: Stella Research" \
  -d '{
    "model": "perplexity/sonar",
    "messages": [
      {
        "role": "system",
        "content": "You are a research assistant focused on Social Security news and filing strategies. Return detailed findings with sources. Focus on: policy changes, filing strategy discussions, content trends on YouTube and Reddit, and anything relevant to educated professionals aged 55+ making strategic SS decisions."
      },
      {
        "role": "user",
        "content": "<INSERT QUERY HERE>"
      }
    ]
  }'
```

Run multiple queries to cover different angles. Suggested searches:
1. Recent Social Security news and policy changes (last 7-30 days)
2. YouTube videos about Social Security filing strategy (recent, high engagement)
3. Reddit discussions on Social Security timing and delayed filing (r/SocialSecurity, r/retirement)
4. Any new calculators, tools, or competitors in the SS optimization space

### 5. Synthesize & Filter

Filter results through Kurt's lens:
- **Relevant:** Anything about the 62-70 filing window, delayed benefits, spousal strategy, COLA, policy changes, misinformation correction
- **Irrelevant:** Generic retirement advice, 401k/IRA content, disability claims, SSI (not retirement)
- **Competitive:** Other SS calculators, coaches, or content creators in this space
- **Content opportunity:** Topics trending that Kurt could create content around

### 6. Save Report

Save the full report to `research/` with this naming convention:
```
research/YYYY-MM-DD-ss-news.md
```

Report format:

```markdown
# Social Security News Research — [DATE]

## Headlines & Policy
- [Key findings with source links]

## YouTube Landscape
- [Notable videos, creators, engagement levels]

## Reddit Pulse
- [Trending threads, common questions, sentiment]

## Competitive Intel
- [Other tools, calculators, coaches in the space]

## Content Opportunities
- [Topics Kurt could create content around, tied to his frameworks]

## Sources
- [All URLs referenced]
```

### 7. Present Summary

Give Kurt a concise summary:
- Top 3-5 bullet points of what matters most
- 50-100 word synthesis of the overall landscape
- Flag anything that directly impacts Ret1re.com strategy or creates a content opportunity
