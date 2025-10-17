# Statistical Analysis of Customer Complaint Topics

## 1. Project Overview

This project executes a data science workflow to extract actionable business intelligence from unstructured customer feedback. It is divided into two primary phases:

1. **Natural Language Processing (Python):** We analyze a large corpus of customer complaints from the Consumer Financial Protection Bureau (CFPB) using unsupervised machine learning. A Latent Dirichlet Allocation (LDA) model is trained to automatically discover and categorize the primary themes within the text.

2. **Statistical Inference (R):** We then use the structured output from the NLP phase to perform a rigorous statistical analysis. A **two-proportion z-test** is employed to determine if certain complaint topics result in a statistically significant higher rate of customer dissatisfaction, measured by the consumer dispute rate.

The project's final output is a data-driven conclusion on which operational areas are the most significant drivers of customer friction.

-----

## 2. Business Problem

Financial institutions receive a high volume of customer complaints through various channels. This unstructured text data is a valuable resource for understanding customer pain points, but its volume and lack of structure make manual analysis impractical. This project addresses the need for a systematic, scalable method to identify and prioritize the most critical issues impacting customer satisfaction.

-----

## 3. Technical Methodology

### Phase 1: NLP Topic Modeling (Environment: Python)

* **Data Acquisition and Cleaning:**

    * The raw `complaints.csv` dataset is loaded using the **pandas** library.
    * Key columns (`Consumer complaint narrative`, `Consumer disputed?`) are selected, and records with null values are dropped, yielding a clean dataset of 164,003 complaints.
    * A comprehensive NLP pre-processing pipeline is applied to each complaint narrative using the **NLTK** library, including lowercasing, tokenization, stopword removal, and lemmatization.

* **Modeling:**

    * The pre-processed text is vectorized into a Bag-of-Words corpus using the **Gensim** library.
    * This corpus is transformed into a weighted representation using a **TF-IDF (Term Frequency-Inverse Document Frequency)** model.
    * A **Latent Dirichlet Allocation (LDA)** model is trained on the TF-IDF corpus to discover 7 latent topics.

* **Data Export:**

    * Each complaint is assigned a dominant topic label. The `Consumer disputed?` column is encoded into a binary format (1 for Yes, 0 for No).
    * The final, structured dataset is exported to `statistical_analysis_data.csv` for use in the next phase.

### Phase 2: Statistical Inference (Environment: R)

* **Exploratory Data Analysis (EDA):**

    * The `statistical_analysis_data.csv` is loaded into R using the **Tidyverse** suite.
    * The point estimate of the dispute rate (sample proportion) is calculated for each of the 7 topics.
    * A bar chart is generated with **`ggplot2`** to visualize the differences in dispute rates.

* **Hypothesis Testing:**

    * **Hypothesis Formulation:** A null hypothesis ($H_0$) is stated, positing no difference in dispute rates between the topics with the highest and lowest observed rates. An alternative hypothesis ($H_a$) posits a significant difference.
    * **Statistical Test:** A **two-proportion z-test** is performed using R's `prop.test()` function.
    * **Conclusion:** The resulting **p-value** is compared against a significance level of $\alpha = 0.05$, and a **95% confidence interval** for the difference is calculated to determine if the observed difference is statistically significant.

-----

## 4. Data Source

* **Provider:** Consumer Financial Protection Bureau (CFPB)
* **Dataset:** Consumer Complaint Database
* **Link:** `https://www.consumerfinance.gov/data-research/consumer-complaints/`

-----

## 5. Project Structure

```
/
├── .venv/                      # Python virtual environment
├── nltk_data/                  # Local NLTK models
├── 1_preprocessing.ipynb       # Jupyter Notebook for data cleaning
├── 2_Topic_Modeling.ipynb      # Jupyter Notebook for NLP modeling
├── statistical_analysis.Rmd    # R Markdown file for statistical analysis
├── statistical_analysis.html   # Rendered R Markdown report
├── statistical_analysis_data.csv # Data prepared for R analysis
├── processed_complaints.pkl    # Intermediate processed Python data
├── requirements.txt            # Python dependencies
└── README.md                   # Project documentation
```

-----

## 6. Setup Instructions

### Prerequisites
- Python 3.8+
- R 4.0+
- An IDE such as VS Code or RStudio
- Git

### Installation

1. **Clone Repository:**
   ```bash
   git clone https://github.com/Prajwalparajuli/Statistical-Analysis-of-Customer-Complaint-Topics.git
   cd Statistical-Analysis-of-Customer-Complaint-Topics
   ```

2. **Configure Python Environment:**
   ```bash
   python -m venv .venv
   .\.venv\Scripts\activate  # Windows
   # source .venv/bin/activate  # Linux/Mac
   pip install -r requirements.txt
   ```

3. **Configure R Environment:**
   - Install R from [CRAN](https://cran.r-project.org/)
   - Install required packages:
   ```r
   install.packages("tidyverse")
   ```

4. **Download Data:**
   - Visit: [CFPB Consumer Complaint Database](https://www.consumerfinance.gov/data-research/consumer-complaints/)
   - Download full database as CSV (≈6.8GB)
   - Save as `complaints.csv` in project root directory

-----

## 7. Execution Instructions

### Step 1: Data Preprocessing (Python)
Run `1_preprocessing.ipynb` to clean and preprocess the raw complaint data.

### Step 2: Topic Modeling (Python)
Run `2_Topic_Modeling.ipynb` to perform LDA topic modeling and generate `statistical_analysis_data.csv`.

### Step 3: Statistical Analysis (R)
Open and run `statistical_analysis.Rmd` to perform two-proportion z-test and generate final report.

-----

## 8. Dependencies

### Python Packages
- pandas: Data manipulation
- numpy: Numerical computing  
- nltk: Natural language processing
- gensim: Topic modeling (LDA)
- scikit-learn: Machine learning utilities
- jupyter: Interactive notebooks

### R Packages
- tidyverse: Data manipulation and visualization

See `requirements.txt` for complete list with versions.

-----

## 9. License

This project is licensed under the MIT License.

-----

## 10. Contact

**Prajwal Parajuli**
- GitHub: [@Prajwalparajuli](https://github.com/Prajwalparajuli)
- Project Link: [https://github.com/Prajwalparajuli/Statistical-Analysis-of-Customer-Complaint-Topics](https://github.com/Prajwalparajuli/Statistical-Analysis-of-Customer-Complaint-Topics)