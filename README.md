# Replicating Lee (2008), "Randomized Experiments from Non-random Selection in U.S. House Elections"

## The paper and its headline claim

- **Paper:** Lee, D. S. (2008). Randomized experiments from non-random selection in U.S. House elections. *Journal of Econometrics* 142(2): 675–697.
- **Identification strategy:** sharp regression discontinuity on the Democratic margin of victory in the previous election, centred at 50 percent of the two-party vote. Treatment is having won that previous election.
- **Headline claim:** a party that narrowly wins a U.S. House election takes about 7.7 percentage points more of the two-party vote in the following election (Table 2, column 1).
- **My replication:** **8.61 percentage points** (HC1 s.e. 0.69, N = 13,566) against the paper's 7.7, a gap of **+11.9%**, exactly as `python reproduce.py` prints it.

## Reproduce the headline table

Python 3.11 or newer. From the repository root:

```bash
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
python reproduce.py
```

`python reproduce.py` is the one command. `MY_PAPER` is already set to `lee` in
`download_data.py`, so on the first run it downloads `data/lmb-data.dta` if it is missing,
runs `notebooks/01_positioning_and_replication.ipynb` and then
`notebooks/02_robustness.ipynb` top to bottom in a fresh kernel, and prints the headline
table from `output/headline_table.csv`. Executed copies of the notebooks, with their
outputs, go to `output/executed/`.

- **Expected runtime:** about 5 seconds for the two notebooks once the environment is built (measured on a laptop from a clean clone); allow roughly a minute more for `pip install` and the 7 MB data download on the first run.

## Data: source and licence

- **Source:** `https://raw.githubusercontent.com/scunning1975/mixtape/master/lmb-data.dta`, downloaded by `download_data.py`. The file is the U.S. House elections panel compiled by Lee, Moretti and Butler (2004), *Quarterly Journal of Economics* 119(3): 807–859, from election returns for 1948–1990.
- **Included or downloaded:** **downloaded, not committed.** `.gitignore` keeps `data/*.dta` out of the repository, and `download_data.py` fetches the file on the first run. The mixtape repository is under an MIT-style licence that would permit committing the file with its notice, but it is 7 MB of third-party data and there is no need to carry it in version control; the download keeps the repository small and the provenance explicit. The command to fetch it by hand is `python download_data.py --paper lee`.

## Repository map

| Path | What it is |
|---|---|
| `reproduce.py` | The one command: runs the notebooks in name order, prints the headline table |
| `download_data.py` | Data URLs for the six papers; `MY_PAPER = "lee"`; `python download_data.py --paper lee` fetches one into `data/` |
| `notebooks/01_positioning_and_replication.ipynb` | Sections 1 and 2: positioning notes, the replication, the theirs-vs-mine table, the discrepancy log. **No AI.** |
| `notebooks/02_robustness.ipynb` | Section 3: the robustness exercises. AI allowed, logged in `ai-appendix.md` |
| `output/headline_table.csv` | The theirs-vs-mine table, written by notebook 01 and printed by `reproduce.py` |
| `output/` | Every table and figure the report uses |
| `report/` | The report PDF |
| `ai-appendix.md` | P.R.I.M.E. entries and full transcripts for Sections 3 to 6, and the no-AI statement for Sections 1 and 2 |
| `AUDIT.md` | How to run the peer audit you file on a classmate's repository |
| `requirements.txt` | Pinned package versions |

## Use of AI

Sections 1 and 2 were completed without AI. The replication code in
`notebooks/01_positioning_and_replication.ipynb` is my own; the two lines that read the
data file and build the running variable are taken verbatim from the given (non-YOUR-TURN)
cells of the course starter notebook.

Sections 3 to 6 have not been drafted yet; this section, and
[`ai-appendix.md`](ai-appendix.md), will be updated when they are. If no AI is used there,
this paragraph will say so.
