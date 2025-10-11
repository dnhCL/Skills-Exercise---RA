# Research Assistant Submission

This submission contains both tasks. Although the original instructions requested a Stata `.do` file, the full workflow was implemented in **Python (pandas)** within Jupyter Notebooks, ensuring transparency, reproducibility, and clear documentation of each step.

---

## 📂 Structure

- **Multi-table task (Stata equivalent):**  
  - Implemented in `stata/stata_tasks_report.ipynb`  
  - Data in `stata/data/` (`bid.dta`, `bidder.dta`, `tender.dta`)  
  - Outputs in `stata/output/` (`tenders_per_city.csv`, `bidders_per_tender_distribution.csv`, `bids_per_city_pair.csv`, `local_experience_by_year.csv`, etc.)

- **Name-matching task (Python):**  
  - Implemented in `python/match_names.py` and `python/python_tasks_report.ipynb`  
  - Data in `python/data/` (`congress_members_with_parties.csv`, `congressional_elections_YYYY.csv`)  
  - Outputs in `python/output/` (`final_matches.csv`, `unmatched_members.csv`, `borderline_review.csv`, etc.)

- **Methodological note:** `note_methodology.md` 

---

## ⚙️ How to Run

### Multi-table Task (originally Stata)
1. Navigate to `submission/notebooks/`.  
2. Open and run the notebook `stata_tasks_report.ipynb` in Jupyter.  
3. Outputs will be generated in `/submission/stata/output/`.

### Python Task 
1. Navigate to `submission/notebooks/`.  
2. Open and run the notebook `python_tasks_report.ipynb` in Jupyter.  
3. Outputs will be generated in `/submission/python/output/`.

**Note** Change the data files path

### Name-Matching Task
1. Navigate to `submission/python/`.  
2. Install requirements:  
   ```bash
   pip install -r requirements.txt
