# entity-resolution
Deduplicates company records by identifying similar entries based on fuzzy matching and normalization techniques. The goal is to group duplicate companies from multiple systems into unique entities using relevant attributes like name and address.


# Company Entity Resolution – Deduplication Project

This project solves the challenge of identifying and grouping duplicate company records across multiple systems. The dataset contains slightly varying entries for the same companies, caused by inconsistencies like typos, formatting, or missing data.

## Solution Explanation / Presentation

### Problem Understanding
Duplicate records often occur when data is collected from different sources or systems. These duplicates may differ slightly in naming conventions (e.g., "Veridion SRL" vs "VERIDION S.R.L.") or include legal suffixes, punctuation, and spacing inconsistencies. Identifying such duplicates requires careful normalization and similarity analysis.

### Process

1. **Data Cleaning and Preprocessing**
   - Converted all text to lowercase for uniform comparison.
   - Removed legal suffixes such as "SRL", "SA", "Ltd", etc.
   - Eliminated special characters and extra whitespace to reduce noise in matching.

2. **Similarity Matching**
   - Used the `fuzzywuzzy` library to apply `token_sort_ratio`, which compares the similarity between company names regardless of word order.
   - Defined a similarity threshold to classify pairs of companies as duplicates. This threshold was manually tuned based on exploratory testing.

3. **Grouping Duplicates**
   - Iterated through the dataset, comparing each record against others to find matches above the threshold.
   - Assigned a unique group ID to each cluster of similar records, representing one unique company.
   - Ensured each company belonged to only one group by tracking visited records.

4. **Result**
   - The output is the original dataset enriched with a new column: `group_id`.
   - Each `group_id` identifies a unique company, with all its duplicate records grouped together under the same identifier.

This method offers a lightweight and effective solution to the entity resolution problem, relying on textual similarity and custom preprocessing steps to detect duplicates accurately.

## Output

The final dataset correctly identifies and groups duplicate records. Each entry is assigned a `group_id` corresponding to a distinct company.

## Code and Logic

The solution was implemented in Python using:
- `pandas` for data manipulation
- `fuzzywuzzy` for approximate string comparison

You can find the full code and logic in the accompanying Colab notebook:
[Google Colab Notebook](https://colab.research.google.com/drive/10GHeuAkFfvskyS4KGASe70zU4KZN5dTO)
