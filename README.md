# Conversion Dashboard (Python)

A Jupyter Notebook analysis that fetches registration and visit data from configured API endpoints, calculates conversion by day and platform, combines it with local advertising-cost data, and writes JSON and static PNG chart artifacts.

> This is a notebook-based analysis and artifact repository, not a deployed web dashboard.

## Contents

| Path | Description |
|---|---|
| `charts_project.ipynb` | Analysis and chart-generation notebook |
| `ads.csv` | Advertising data with date, UTM dimensions and cost |
| `conversion.json`, `ads.json` | Committed serialized analysis outputs |
| `charts/` | Static charts for visits, registrations, conversion and advertising costs |
| `presentation.pdf` | Project presentation |

## Requirements

The notebook imports Python packages including `pandas`, `matplotlib`, `seaborn`, `requests`, `python-dotenv` and Jupyter. Install these in an isolated environment before running.

Create a local `.env` file (not committed):

```env
DATE_BEGIN=<start date accepted by the API>
DATE_END=<end date accepted by the API>
API_URL=<base API URL>
```

The notebook calls `${API_URL}/registrations?begin=...&end=...` and `${API_URL}/visits?begin=...&end=...`.

## Run

1. Clone the repository and install the requirements above.
2. Create `.env` with the API URL and date range.
3. Start Jupyter in the repository root and open `charts_project.ipynb`.
4. Run cells in order.

With an API matching the expected records, the notebook writes `conversion.json`, `ads.json` and PNGs under `charts/`.

## Processing notes

- visits are deduplicated by `visit_id` and rows with `user_agent == 'bot'` are excluded;
- registrations are deduplicated by `user_id`;
- both datasets are grouped by day and platform;
- conversion is `registrations / visits * 100`;
- advertising data comes from `ads.csv` and is aggregated for charts.

## Data and reproducibility notes

- API URL, auth method, response schema, source-data provenance and refresh policy are not documented here.
- Committed JSON/chart files are historical artifacts, not proof that the API remains available.
- The repository has no automated analysis tests or environment lockfile.
- The notebook should be reviewed before relying on generated outputs: API requests have no visible timeout/schema validation, and historical generated files may not match the current notebook exactly.

## License

MIT — see [LICENSE](LICENSE). Dataset and third-party artifact reuse may be subject to separate terms.
