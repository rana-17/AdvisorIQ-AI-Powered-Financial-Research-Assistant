# AdvisorIQ — AI-Powered Financial Research Assistant

AdvisorIQ is an AI-powered financial research assistant that helps users explore financial topics, check market data, and analyze potentially suspicious transactions.

It uses a Gemini AI model, a research document search system, and a machine learning model to provide useful information through a simple web interface.

**Note:** This is an educational project and is not intended for real financial decisions or production fraud detection.

## Features

- **AI Financial Assistant:** Ask questions about financial concepts and company research.
- **Market Data:** Retrieve recent market data for publicly traded companies using Yahoo Finance.
- **Document Search (RAG):** Search financial research documents and retrieve relevant information using ChromaDB.
- **Transaction Risk Analysis:** Use a Random Forest model to assign risk scores and flag potentially suspicious transactions.
- **CSV Upload:** Upload transaction data for analysis.
- **Adjustable Risk Threshold:** Change the threshold used to flag transactions.
- **Interactive Interface:** Use the application through a Gradio web interface.
- **Basic Data Protection:** Validate uploaded CSV files and redact some personal information patterns from questions.

## Technologies Used

- Python
- Google Gemini 2.5 Flash
- LangChain
- ChromaDB
- Google Gemini Embeddings
- Scikit-learn
- Pandas and NumPy
- Yahoo Finance (`yfinance`)
- Gradio
- Joblib

## How It Works

AdvisorIQ has three main tools:

1. **Market Data Tool:** Retrieves market information for a given stock ticker.
2. **Research Tool:** Searches stored financial documents and returns relevant passages.
3. **Transaction Analysis Tool:** Uses a trained Random Forest model to score transactions from a CSV file.

The AI assistant selects the appropriate tool based on the user's question and combines the results into a response.

The research feature uses Retrieval-Augmented Generation (RAG). It splits documents into smaller sections, converts them into embeddings, stores them in ChromaDB, and retrieves relevant sections when a user asks a question.

## Transaction Data Format

The transaction checker expects a CSV file with these columns:

| Column | Description |
|---|---|
| `amount` | Transaction amount |
| `hour` | Hour of the transaction, from 0 to 23 |
| `is_foreign` | `1` for foreign transactions and `0` otherwise |
| `merchant_risk` | Merchant risk score, from 0 to 10 |

An optional `transaction_id` column can also be included.

Example:

```csv
transaction_id,amount,hour,is_foreign,merchant_risk
TXN001,150,14,0,2
TXN002,3200,3,1,8
TXN003,500,11,0,4
```

Use sample or synthetic data when testing this project.

## Getting Started

### Requirements

- Python
- A Google Gemini API key
- A Google Colab account is recommended for running the notebook

### Installation

1. Download or clone this repository.
2. Open `AdvisorIQ.ipynb` in Google Colab.
3. Run the dependency installation cell.
4. Configure your Gemini API key when prompted, or add it to Google Colab Secrets using the name `googleapikey`.
5. Run the notebook cells in order.
6. Open the Gradio interface and start asking questions or uploading a sample transaction CSV.

The notebook installs the required Python packages automatically.

### API Key Security

Never upload your Gemini API key or other secrets to GitHub. Use Google Colab Secrets or environment variables to configure your API key.

## Machine Learning Model

AdvisorIQ uses a Random Forest classifier to analyze four transaction features:

- Transaction amount
- Transaction hour
- Foreign transaction indicator
- Merchant risk score

The notebook generates **2,000 synthetic transactions** using predefined rules and trains the model using an 80/20 train-test split.

The model is evaluated using:

- Precision
- Recall
- F1-score
- ROC-AUC
- Confusion matrix

These results measure how well the model learns the synthetic rules. They do not demonstrate real-world fraud-detection performance.

## Current Limitations

- The research library contains example documents, not verified financial research.
- Market data availability depends on the external data source.
- The transaction model uses synthetic data and needs evaluation on an appropriate real-world dataset.
- AI-generated responses may contain errors and should be checked against reliable sources.
- The project does not provide personalized investment advice or make automated financial decisions.
- Basic PII redaction does not guarantee that all sensitive information will be removed.

## Future Improvements

- Add trusted financial documents and source links.
- Evaluate the transaction model on a suitable public dataset.
- Improve model evaluation and explain why transactions receive high risk scores.
- Add more financial data sources.
- Improve automated tests and application deployment.

## Disclaimer

AdvisorIQ is an educational prototype developed for learning about AI agents, RAG, machine learning, and financial data analysis.

It is not a financial advisor or a validated fraud-detection system. A flagged transaction is not proof of fraud. Always verify financial information independently.

## Author

Developed as a personal project to explore AI agents, financial research, Retrieval-Augmented Generation, and machine learning.
