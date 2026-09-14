# FRE-GY-7871A Assignment 2

This repository contains the reproducible analysis for *Evaluating the Impact of FOMC Communications on Asset Prices*.

## Deliverables

- `Assignment_2_FOMC_Communications.ipynb` - document collection, two tone measures, market-event regressions, and the September-meeting forecast template.
- `AI_USE.md` - completed disclosure of AI assistance.

No source data are stored here. The notebook obtains public documents from Federal Reserve pages and market series from FRED/Yahoo Finance when `RUN_LIVE_COLLECTION = True`. It traverses the current calendar for 2021 onward and the Federal Reserve's historical-year pages for 2018-2020.

## Reproduce

For the supplied Anaconda environment, prefer a conda solve so NumPy, SciPy,
and Statsmodels binary extensions are built for one another (fe-course is the name of the Python kernel used for this project):

```bash
conda activate fe-course
conda install -c conda-forge --force-reinstall "numpy>=1.26,<2.0" "scipy>=1.11,<1.15" "statsmodels>=0.14,<0.15"
python -m pip install -r requirements.txt
```

If `fe-course` has other conflicting packages, create a clean environment:

```bash
conda create -n fre-assignment python=3.11 "numpy>=1.26,<2.0" "scipy>=1.11,<1.15" "statsmodels>=0.14,<0.15" -c conda-forge
conda activate fre-assignment
python -m pip install -r requirements.txt
```

Open the notebook and run all cells. The first execution may download the FinBERT model. Review the `DOCUMENT_OVERRIDES` cell before collection: it is the auditable place to add any missed Chair speeches, testimony, or press-conference transcripts and to correct release timestamps. Keep notebook output saved before publishing.

The collection code uses Python's built-in HTML parser, so `lxml` is optional. To install the faster parser in the environment selected by the notebook kernel, run `python -m pip install lxml`.

The live collector now includes post-meeting statements, minutes, FOMC
press-conference transcripts, and Chair speeches/testimony. It labels timestamps
whose exact release time could not be verified; review those records and correct
them in `DOCUMENT_OVERRIDES` before running the event-study regressions.

## FinBERT troubleshooting

FinBERT requires compatible PyTorch and Transformers versions. If loading
`BertForSequenceClassification` fails, run the following in a notebook cell,
restart the kernel, and rerun the notebook:

```python
%pip uninstall -y torchvision torchaudio
%pip install --upgrade --force-reinstall --no-cache-dir "torch>=2.5,<2.7" "transformers>=4.41,<4.49"
%pip install ipywidgets jupyterlab_widgets
```

`torchvision` and `torchaudio` are not needed for this text-only task and are
removed because incompatible versions can prevent Transformers from importing
the BERT model class. Hugging Face authentication is optional for the public
`ProsusAI/finbert` model; it only raises download-rate limits.

## Method summary

The notebook treats Powell (from February 2018) as the baseline and classifies documents released on or after Kevin Warsh's May 22, 2026 start date as Warsh-era. It scores every document using a monetary-policy phrase list and FinBERT sentence sentiment, computes release-day changes in DXY, 10s2s, 1-year Treasury yield, and growth-minus-value, and regresses each outcome on each score with the DGS3MO change as a control. It prints Tables 1-3, plots Figure 1, and creates a data-driven forecast and falsifiable trade recommendation.
