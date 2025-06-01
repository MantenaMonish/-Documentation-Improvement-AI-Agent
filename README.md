# MoEngage Documentation AI Assistant

This project is designed to analyze and improve technical documentation from [MoEngage's Developer Portal](https://help.moengage.com). It consists of two intelligent agents:

- **Agent 1: Documentation Quality Analyzer** – Evaluates documentation against readability, structure, completeness, and Microsoft Style Guide compliance.
- **Agent 2: Documentation Revision Agent** – Applies AI-powered improvements to enhance clarity, style, and structure based on Agent 1’s suggestions.

---

## 🛠 Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/moengage-doc-ai.git
cd moengage-doc-ai
```

### 2. Create and Activate Virtual Environment
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Environment Variables
Create a `.env` file in the root directory with the following:
```env
BRIGHTDATA_USERNAME=your_username
BRIGHTDATA_PASSWORD=your_password
BRIGHTDATA_PORT=your_port
BRIGHTDATA_IP=your_ip

GEMINI_API_KEY=your_google_gemini_api_key
```

> **⚠️ Do NOT commit your `.env` or API keys.**

---

## 📚 Components Overview

### 🔍 Scraper
**Objective:** Extract clean, Markdown-formatted content from MoEngage’s documentation pages.

- **Tools Used:** `requests`, `BeautifulSoup`, `html2text`, `re`, Bright Data proxies
- **Key Features:**
  - Proxy support with automatic retries
  - Targeted scraping of article body
  - Cleans and converts content to Markdown
  - Saves to `scraped_docs/` with sanitized filenames

### 🧹 Preprocessing
**Objective:** Convert Markdown to clean, structured plain text for LLM analysis.

- **Tools Used:** `frontmatter`, `markdown`, `BeautifulSoup`, `re`
- **Key Features:**
  - YAML removal and structure preservation
  - Code block and image placeholder handling
  - Heading hierarchy with level markers
  - Consistent and readable format for LLMs

---

## 📈 Task 1: Documentation Quality Analyzer

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

> Output saved in `analysis_reports/<filename>.json`

---

## ✨ Task 2: Documentation Revision Agent

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

## 📄 Example Output

### Example 1 – URL: https://help.moengage.com/docs/android-sdk-integration
- **Agent 1 Output:** `analysis_reports/android-sdk-integration.json`
- **Agent 2 Output:** `revised_docs/android-sdk-integration.md`

### Example 2 – URL: https://help.moengage.com/docs/segmentation
- **Agent 1 Output:** `analysis_reports/segmentation.json`
- **Agent 2 Output:** `revised_docs/segmentation.md`

---

## 📌 Assumptions

- MoEngage documentation layout remains consistent (targeting `.article__body.markdown`)
- All content is in English and follows Markdown formatting
- API rate limiting is essential (1 request/sec for Gemini API)
- Code blocks and YAML metadata must remain untouched

---

## 🧠 Design Choices

- **Bright Data Proxies:** To avoid bot detection while scraping
- **Markdown + HTML parsing:** Combines best of structure preservation and cleaning
- **Gemini Flash Model:** Balances cost and performance for large-scale analysis
- **Regex + LLM Hybrid Revision:** Efficient and context-aware improvements
- **Structured Suggestions:** Makes the AI output directly usable for content teams

---

## ⚠️ Challenges and Workarounds

| Challenge | Solution |
|----------|----------|
| Anti-scraping measures | Used Bright Data residential proxies |
| Noisy HTML structure | Targeted only `.article__body.markdown` and removed unrelated content |
| Readability bias in code blocks | Replaced with placeholders during analysis |
| LLM output hallucinations | Applied strict revision boundaries and fallbacks |
| Rate limits | Implemented sleep intervals between requests |

---

## 🚀 Future Enhancements

- Add multi-language support for non-English docs
- Integrate `textstat` for quantitative readability metrics
- Build a Streamlit-based UI for documentation review
- Track versioned diffs for before/after comparisons

---

## 📂 Project Structure

```bash
.
├── scraped_docs/            # Raw Markdown from scraping
├── analysis_reports/        # JSON output from quality analyzer
├── revised_docs/            # Revised documentation from Agent 2
├── scraper.py               # Scrapes and saves documentation
├── preprocess.py            # Prepares docs for LLM analysis
├── analyzer.py              # Agent 1: Quality analyzer
├── reviser.py               # Agent 2: Revision agent
├── .env                     # Environment variables (not committed)
├── requirements.txt         # Dependencies
└── README.md                # This file
```

---

## 🤝 Acknowledgments

- MoEngage for open documentation
- Google Gemini API for powering intelligent analysis
- Bright Data for proxy support during scraping
