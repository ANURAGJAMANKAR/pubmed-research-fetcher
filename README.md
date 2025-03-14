# 📌 PubMed Research Paper Fetcher

## 📖 Overview
This project fetches research papers from **PubMed** using the **NCBI Entrez API**, filters papers with **non-academic authors**, and exports the results to a CSV file. It includes:
- A **CLI (Command-Line Interface)** to search and fetch papers.
- Automated **filtering** of biotech/pharmaceutical company authors.
- Export functionality to save results in structured CSV files.
- **Unit tests** to ensure reliability.

---

## 🛠 Tech Stack & Dependencies
- **Python 3.9+** (Recommended version: 3.11+)
- **Poetry** (Dependency & virtual environment management)
- **NCBI Entrez API** (For PubMed data retrieval)
- **Pandas** (For data processing & CSV handling)
- **Biopython** (For parsing PubMed records)
- **Dotenv** (For securely storing API keys)
- **Logging** (For debugging and tracking execution)

---

## 🚀 Installation Guide
### 1️⃣ Clone the Repository
```sh
$ git clone <repository_url>
$ cd backend-takehome
```

### 2️⃣ Install Dependencies
```sh
$ poetry install
```

### 3️⃣ Setup Environment Variables
Create a `.env` file in the root directory and add:
```sh
PUBMED_API_KEY=your_api_key_here
```
(Your API key is required to make higher-limit requests to PubMed.)

### 4️⃣ Activate Virtual Environment
```sh
$ poetry shell
```

### 5️⃣ Run CLI Application
To fetch and filter PubMed papers, use:
```sh
$ poetry run python -m cli.main "cancer research" -e "your_email@example.com" -f output.csv
```

---

## 📂 Project Structure
```plaintext
backend-takehome/
│── cli/                      # Command-line interface
│   ├── main.py               # CLI entry point
│── backend_takehome/         # Core backend functionality
│   ├── fetch.py              # Fetches papers from PubMed
│   ├── filter.py             # Filters non-academic authors
│   ├── export.py             # Exports data to CSV
│── tests/                    # Unit tests
│   ├── test_fetch.py         # Tests fetching functionality
│   ├── test_cli.py        # Tests cli 
│   ├── test_export.py        # Tests CSV export
│── data/                     # Stores generated CSV files
│── .env                      # Stores API key (DO NOT SHARE)
│── .gitignore                # Excludes unnecessary files
│── README.md                 # Project documentation
│── pyproject.toml            # Poetry dependencies & configuration
```

---

## 🛠 How Each File Works

### **1️⃣ `fetch.py`** (Fetching Papers)
- Connects to **NCBI Entrez API** using `email` and `API key`.
- Searches PubMed for papers based on user query.
- Fetches metadata like **authors, affiliations, publication date**.

### **2️⃣ `filter.py`** (Filtering Papers)
- Identifies **non-academic authors** using predefined **company/academic keywords**.
- Extracts **company affiliations** (e.g., Pfizer, Moderna).
- Filters out **academic-only papers**.

### **3️⃣ `export.py`** (Exporting Data)
- Converts **filtered results** into a structured CSV format.
- Saves the file to the `data/` folder.

### **4️⃣ `cli/main.py`** (Command-Line Interface)
- Accepts user inputs for search queries.
- Calls `fetch.py` to retrieve papers.
- Calls `filter.py` to process authors.
- Calls `export.py` to save results.

---

## 📌 Running Tests
To ensure everything is working correctly, run:
```sh
$ poetry run python -m unittest discover tests
```
This will automatically execute all test cases.

---

## 🔧 Customization Guide
### Modify the Default Number of Papers Fetched
Edit `fetch.py`:
```python
def fetch_papers(query: str, email: str, max_results: int = 100):
```
Change `max_results` to any number.

### Add New Keywords for Filtering
Edit `filter.py` and update the keyword sets:
```python
PHARMA_BIOTECH_KEYWORDS = {"pharma", "biotech", "genentech", "pfizer", "moderna"}
```

### Change Output File Location
Modify `export.py`:
```python
def export_to_csv(results, filename="data/output.csv"):
```
Change `"data/output.csv"` to any desired path.

---

## 🛠 Troubleshooting
### ❌ `requests.exceptions.HTTPError`
**Cause:** Invalid API Key or Exceeded PubMed Request Limit.
✅ **Solution:** Check your `.env` file and ensure `PUBMED_API_KEY` is correct.

### ❌ `No Papers Found`
**Cause:** Query might be too specific.
✅ **Solution:** Try using broader search terms.

### ❌ `CLI Not Working`
**Cause:** Poetry environment not activated.
✅ **Solution:** Run:
```sh
$ poetry shell
$ poetry run python -m cli.main --help
```

---

## 📜 License
This project is open-source and available under the MIT License.

