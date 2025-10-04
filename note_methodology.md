# Methodological Note

## Stata Task — Multi-table Merging and Local Experience

The Stata multi-table exercise was **reproduced in Python** (`pandas`) using the `.dta` inputs. As all operations were descriptive, no econometric modules were required.

### Approach
1. **Data preparation:**  
   All datasets (`tender`, `bid`, `bidder`) were imported, validated, and standardised. Identifiers were cast as integers to secure clean joins, and checks confirmed no duplicate tender IDs or missing city names.

2. **Tenders per city and bidders per tender:**  
   Frequency tables summarised tender counts by city and bidder counts per tender.

3. **City-pair bidding flows:**  
   Merging `bid` with `bidder` and `tender` produced origin–destination city pairs. Bid counts were aggregated by `(bidder_city, tender_city)`, showing local and cross-city activity.

4. **Local experience variable:**  
   For each potential bidder–tender pair, `local_experience = 1` if the bidder had placed a bid in the same tender city **before** the tender year. The earliest bid year per city determined prior experience.

### Challenges & Assumptions
- Stata was unavailable locally, so the procedure was executed in Python while replicating the exact Stata logic.  
- In **Budapest (2016)**, two tenders shared the same year with no sequencing variable (e.g. bid date). Their temporal order was unknowable, both were conservatively assigned `local_experience = 0` for first-time bidders in that year.  
- This rule avoids unsupported assumptions while maintaining internal consistency.  

---

## Python Task — Name Matching (Congress & Elections)

The objective was to **link** individuals in the congressional members register to election records using **names only**. The workflow was implemented in Python (`pandas`, `rapidfuzz`).

### Approach
1. **Normalisation:**  
   Both sources (`congress_members_with_parties.csv` and yearly `congressional_elections_YYYY.csv`, 1992–2025) were cleaned to lower case, stripped of accents, punctuation, and suffixes.  
   Two standard views were created:  
   - `display_name_std`: removes onomastic particles (e.g. *de*, *van*).  
   - `display_name_ns`: retains them for full-string similarity.  
   Middle initials were preserved.

2. **Surname blocking & given-name logic:**  
   Comparison occurred only within surname blocks (optionally two tokens for compound surnames). Given names had to match canonically, by nickname, or by initial. Missing middle names were tolerated, but inconsistent initials were rejected.

3. **Aliases and fuzzy scoring:**  
   A compact nickname dictionary (e.g. *Tom–Thomas*, *Bill–William*) generated variants.  
   Similarity was computed via `RapidFuzz.token_sort_ratio` on both full and first–last views; the **maximum** score was used.

4. **Thresholds and outputs:**  
   Matches with `score ≥ 90` were accepted (`match_type = fuzzy` or `exact`), keeping up to 35 candidates per member per cycle.  
   Results include `final_matches.csv`, `unmatched_members.csv`, and `borderline_review.csv` (scores 80–89 for manual inspection).

### Checks, Assumptions & Challenges
- Row counts before/after normalisation matched, empty election files were recorded.  
- The `status` field was ignored (per specification).  
- No geographic or temporal filters were applied, robustness relies on surname blocking, given-name rules, and a high threshold.  
- The alias dictionary can be extended (e.g. *Peggy–Margaret*).  
- Removing suffixes (*Jr.*, *Sr.*, *II/III*) does not affect comparisons, as matching is based on normalised forms.


