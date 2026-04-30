# Trump Headline Analysis: Sentiment & Topic Modeling Across the Political Spectrum

This repository contains a data science project that investigates how the political alignment of media outlets affects their coverage of Donald Trump. By analyzing news headlines from early 2026, this project aims to uncover differences in both the **emotional tone (sentiment)** and the **underlying themes (framing)** used by left-leaning, centrist, and right-leaning news sources.

## Authors

- Juho Kallunki
- Niko Vilander
- Hans Ravna-Pieski

## Project Overview

It is generally expected that journalism strives for objectivity. However, modern media is often highly polarized. Using the **AllSides Media Bias Chart**, we categorized nine major news outlets into three groups (Left, Center, Right) and analyzed how they framed headlines containing the word "Trump" between **January 1, 2026, and March 31, 2026**.

### The Media Outlets Analyzed:

- **Left (L):** Democracy Now!, The Guardian, The Atlantic
- **Center (C):** Forbes, BBC, Reuters
- **Right (R):** Fox News, The Post Millennial, Breitbart

## Data Collection

Data was systematically gathered using the open-source **Media Cloud** platform.

- **Search Query:** `(article_title: Trump) AND ("Donald Trump" OR "President Trump") language:en`
- **Dataset Size:** Originally 4,579 headlines, which were then randomly sampled and balanced to ensure equal representation, resulting in exactly **1,018 headlines per political group** (3,054 total).

## Methodology

The analysis was conducted in three distinct phases:

1. **Simple Emotion Word Counter:** Using the Hu & Liu open-source opinion lexicon to calculate the frequency of positive and negative words in the headlines.
2. **VADER Sentiment Analysis:** Utilizing the Valence Aware Dictionary and sEntiment Reasoner to capture the overall emotional polarity (from -1 to 1) of the headlines, accounting for sentence structure and modifiers.
3. **Topic Modeling (NMF):** Because sentiment analysis models struggle with context and irony, we used Non-Negative Matrix Factorization (NMF) with TF-IDF vectorization to cluster the headlines into 5 distinct "topics" to see _what_ the media was actually talking about.

## Key Findings

- **The Sentiment Baseline is Negative:** Across all political spectrums, the average sentiment towards Trump in headlines was negative. The **Left** was definitively the most negative (-0.179 VADER score). The **Center** (-0.078) and **Right** (-0.068) were closer to neutral and virtually tied.
- **Algorithmic Blind Spots:** VADER struggled with political context. For example, a Breitbart headline stating Trump _"Vows to Fix"_ a _"Giant Scam"_ was rated heavily negative by VADER due to the words "scam" and "fraud," even though the context portrayed Trump heroically.
- **Polarization Through Framing:** The NMF Topic Modeling revealed that media polarization is not just about the _tone_ of the news, but the _choice_ of news.
  - **Right-leaning media** focused heavily (28.2%) on domestic clashes (State of the Union, Congress).
  - **Left-leaning media** over-indexed on global conflicts (Iran, Ukraine) and European relations (NATO).
  - **Centrist media** strongly emphasized institutional and legal frameworks (Supreme Court, Tariffs).

## Repository Contents

- `analysis.ipynb` - The main Jupyter Notebook containing all code, data cleaning, analysis, and visualizations.
- `data.csv` - The raw dataset containing the news headlines and metadata.
- `media_bias_chart.png` - Reference image of the AllSides bias ratings used for categorization.
- `requirements.txt` - List of Python dependencies required to run the notebook.

## How to Run Locally

1. Clone this repository:

   ```bash
   git clone [https://github.com/ravnapieski/trump-analysis.git](https://github.com/ravnapieski/trump-analysis.git)
   cd trump-analysis

   ```

2. Create a virtual environment (optional but recommended):

   ```bash
   python3 -m venv venv
   source venv/bin/activate # On Windows use: venv\Scripts\activate
   ```

3. Install the required packages:

   ```bash
   pip install -r requirements.txt
   ```

4. Launch Jupyter Notebook:
   ```bash
   jupyter notebook
   ```

## Limitations

Headlines Only: The analysis is restricted to headlines, which are often sensationalized for click-through rates and may not fully reflect the nuance of the article's body text.

Short Timeframe: The data spans a specific 3-month window, meaning the topics are heavily influenced by the immediate news cycle of early 2026 (e.g., Iran, Venezuela) rather than long-term structural trends.

Algorithmic constraints: Lexicon-based sentiment analyzers (VADER) lack contextual reading comprehension, highlighting the need for LLM-based analysis in future research.
