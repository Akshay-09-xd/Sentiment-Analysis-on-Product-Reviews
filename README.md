# Sentiment Analysis on Product Reviews

A machine learning application that classifies product review text as **Positive** or **Negative**. It includes a Flask API and browser interface for individual reviews and CSV files, plus a Streamlit interface.

## Features

- Predict sentiment for a single review.
- Upload a CSV to label multiple reviews and download the results.
- View a sentiment distribution chart for bulk predictions.
- Use the included trained XGBoost model, scaler, and CountVectorizer.

## Project structure

```text
.
├── api.py                         # Flask API and browser interface
├── main.py                        # Streamlit interface
├── requirements.txt
├── Data/                          # Example review data and sample predictions
├── Models/                        # Serialized model and preprocessing objects
└── templates/                     # Flask HTML pages
```

## Requirements

- Python 3.10 or newer
- pip

## Setup

Clone the repository and enter its directory:

```bash
git clone https://github.com/Akshay-09-xd/Sentiment-Analysis-on-Product-Reviews.git
cd Sentiment-Analysis-on-Product-Reviews
```

Create and activate a virtual environment (recommended):

```bash
python -m venv .venv
```

On Windows:

```powershell
.venv\Scripts\Activate.ps1
```

On macOS or Linux:

```bash
source .venv/bin/activate
```

Install the dependencies and download the NLTK English stopword list used during text preprocessing:

```bash
python -m pip install -r requirements.txt
python -m nltk.downloader stopwords
```

## Run the Flask app

Start the Flask server:

```bash
python api.py
```

Open [http://127.0.0.1:5000](http://127.0.0.1:5000) for the browser interface. The API also exposes a health check at `/test` and predictions at `/predict`.

### Predict one review with the API

Send a JSON `POST` request to `/predict`:

```bash
curl -X POST http://127.0.0.1:5000/predict \
  -H "Content-Type: application/json" \
  -d "{\"text\": \"The product works great and arrived quickly.\"}"
```

The response contains a `prediction` field with `Positive` or `Negative`.

### Predict from a CSV

Upload a CSV as multipart form data to `/predict`. The CSV must contain a column named `Sentence` with one review per row. The response is a downloadable CSV with an additional `Predicted sentiment` column. The browser interface also displays a sentiment distribution chart.

Example input:

```csv
Sentence
"The quality exceeded my expectations."
"Stopped working after one day."
```

## Run the Streamlit interface

The Streamlit interface sends prediction requests to the Flask API, so keep the Flask server running in one terminal. In another terminal, activate the same virtual environment and run:

```bash
streamlit run main.py
```

## Data and models

The `Data/` directory contains sample review data and prediction outputs. The `Models/` directory contains the trained model and preprocessing artifacts used by the application. The model files are loaded with Python pickle; only use model files from a source you trust.

## Author

Akshay
