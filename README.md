# MoEngage Documentation AI Assistant

This project is designed to analyze and improve technical documentation from [MoEngage's Developer Portal](https://help.moengage.com). It consists of two intelligent agents:

- **Agent 1: Documentation Quality Analyzer** – Evaluates documentation against readability, structure, completeness, and Microsoft Style Guide compliance.
- **Agent 2: Documentation Revision Agent** – Applies AI-powered improvements to enhance clarity, style, and structure based on Agent 1’s suggestions.

---

##  Components Overview

###  Scraper
**Objective:** Extract clean, Markdown-formatted content from MoEngage’s documentation pages.

- **Tools Used:** `requests`, `BeautifulSoup`, `html2text`, `re`, Bright Data proxies
- **Key Features:**
  - Proxy support with automatic retries
  - Targeted scraping of article body
  - Cleans and converts content to Markdown
  - Saves to `scraped_docs/` with sanitized filenames

###  Preprocessing
**Objective:** Convert Markdown to clean, structured plain text for LLM analysis.

- **Tools Used:** `frontmatter`, `markdown`, `BeautifulSoup`, `re`
- **Key Features:**
  - YAML removal and structure preservation
  - Code block and image placeholder handling
  - Heading hierarchy with level markers
  - Consistent and readable format for LLMs

---

##  Task 1: Documentation Quality Analyzer

**Goal:** Analyze documentation quality using Gemini API and readability metrics.

- **Technologies Used:** `google.generativeai` (Gemini 1.5 Flash), `textstat` (future extension)
- **Design Highlights:**
  - Combines readability, structure, style, and completeness in one analysis
  - Generates JSON-formatted reports with actionable feedback
  - Prepares LLM-friendly input via custom preprocessing

### Analysis Dimensions:
- **Readability:** Sentence complexity, jargon, non-technical tone
- **Structure:** Heading hierarchy, flow, paragraph length
- **Completeness:** Examples, edge cases, depth
- **Style Compliance:** Microsoft Voice & Tone

---

##  Task 2: Documentation Revision Agent

**Goal:** Automatically revise documentation based on analysis suggestions.

- **Technologies Used:** `google.generativeai`, `re`, `json`, `os`
- **Design Highlights:**
  - Hybrid editing: regex + Gemini AI
  - Preserves YAML frontmatter, code blocks, and document structure
  - Only modifies sections flagged in the quality report

### Revision Workflow:
1. Read suggestions from JSON report
2. Apply regex-based simple fixes (e.g., jargon replacement)
3. Use AI to rephrase complex sentences and restructure paragraphs
4. Save output as improved `.md` files in `revised_docs/`

---

##  Example Output

### Example 1 – URL: https://help.moengage.com/docs/android-sdk-integration
- **Agent 1 Output:** `Outputs_Task1/android-sdk-integration.json`
- **Agent 2 Output:** `Outputs_Task2/android-sdk-integration.md`

### Example 2 – URL: https://help.moengage.com/docs/segmentation
- **Agent 1 Output:** `Outputs_Task1/segmentation.json`
- **Agent 2 Output:** `Outputs_Task2/segmentation.md`

---
> ** Do NOT commit your API keys.**
---

##  Assumptions

- MoEngage documentation layout remains consistent (targeting `.article__body.markdown`)
- All content is in English and follows Markdown formatting
- API rate limiting is essential (1 request/sec for Gemini API)
- Code blocks and YAML metadata must remain untouched

---

##  Design Choices

- **Bright Data Proxies:** To avoid bot detection while scraping
- **Markdown + HTML parsing:** Combines best of structure preservation and cleaning
- **Gemini Flash Model:** Balances cost and performance for large-scale analysis
- **Regex + LLM Hybrid Revision:** Efficient and context-aware improvements
- **Structured Suggestions:** Makes the AI output directly usable for content teams

---

##  Challenges and Workarounds

| Challenge | Solution |
|----------|----------|
| Anti-scraping measures | Used Bright Data residential proxies |
| Noisy HTML structure | Targeted only `.article__body.markdown` and removed unrelated content |
| Readability bias in code blocks | Replaced with placeholders during analysis |
| LLM output hallucinations | Applied strict revision boundaries and fallbacks |
| Rate limits | Implemented sleep intervals between requests |

---

##  Project Structure

```bash
.
├── Scraped_Docs/            # Raw Markdown from scraping
├── Output_Task1/            # JSON output from quality analyzer
├── Output_Task2/            # Revised documentation from Agent 2
├── scraper.ipynb            # Scrapes and saves documentation
├── preprocess.ipynb         # Prepares docs for LLM analysis
├── Task1_Agent.ipynb        # Agent 1: Quality analyzer
├── Task1_Agent.ipynb        # Agent 2: Revision agent
├── requirements.txt         # Dependencies
└── README.md                # This file
```

---

##  Acknowledgments

- Google Gemini API for powering intelligent analysis
- Bright Data for proxy support during scraping
- Thank you to MoEngage for providing this opportunity to work on a real-world documentation quality challenge.
