# Evaluating the Impact of FOMC Communications on Asset Prices

**FRE-GY 7871 A - NLP and the Investment Process**  
**Name:** Alan Wang
**NetID** aw4437
**GitHub repo:** https://github.com/alanywang25/FRE-GY-7871A-Assignment2

## Executive summary

The latest live run contains 299 documents: FOMC statements and minutes, press-conference records, and Chair speeches. The Warsh subset has 11 records. Same-day releases are combined into 229 event days for inference. Across the word-list, FinBERT, and factor-similarity measures, no tone coefficient is statistically significant at conventional levels for DXY, 10s2s, the 1-year yield, or growth minus value. The defensible result remains weak and method-sensitive evidence, not a directional trading signal. The notebook's stated rate scenario remains a September **hold** with a 65% probability of a more hawkish statement; its current market calculation is a mechanical lexicon scenario, not a standalone investment signal.

## Data and methods

The sample begins in February 2018. Powell is the baseline Chair through May 21, 2026; the Warsh period begins May 22, 2026. Documents come from Federal Reserve calendars, historical materials, press-conference transcripts, and speech archives. The one-day outcomes are DXY, 10s2s, the 1-year Treasury yield, and IWF-minus-IWN. Regressions include the DGS3MO change, separating text-tone associations from contemporaneous short-rate news.

Tone is measured three ways: a monetary-policy hawkish/dovish word list normalized by document length; sentence-level FinBERT sentiment (positive minus negative probability); and a TF-IDF/cosine-similarity score against hawkish and dovish seed language. Table 3 uses one row per event day, averaging tone measures where multiple communications share that day. 

## Table 1. Documents collected, by type and Chair

| Document type | Powell | Warsh |
|---|---:|---:|
| Minutes | 67 | 2 |
| Press-conference transcripts | 63 | 3 |
| Chair speeches | 86 | 3 |
| Post-meeting statements | 72 | 3 |

The live collection audit flags 155 records whose source time still needs verification before a precise intraday event study.

## Figure 1. Hawkish/dovish tone over time by document type

![Figure 1: Word-list and FinBERT tone, by document type, with May 22, 2026 marking the start of Warsh's term.](figure_1_tone_trends.png)

The figure displays the two directly comparable document-level scores. In the current run, the September 16 statement is positive on both methods (lexicon 2.000; FinBERT 0.355), reinforcing the earlier positive July-statement and August-minutes readings. The automatically collected September 16 press-conference record is a meeting landing page, not the official transcript; its displayed scores should not be interpreted as Q&A tone. The official transcript is scored separately in the supplemental analysis. The factor-similarity measure is reported in Table 3 as a robustness specification.

## Table 2. One-day market changes after each Warsh-era release

DXY and growth-minus-value are percentage changes. Treasury values and 10s2s are percentage-point changes. Speech timestamps shown at noon are provisional.

| Release | Type | Lexicon | FinBERT | DXY | 10s2s | 1-year | Growth minus value |
|---|---|---:|---:|---:|---:|---:|---:|
| 2026-05-31 12:00 | Speech | 0.000 | 0.060 | 0.293 | -0.050 | 0.040 | 1.248 |
| 2026-06-17 14:00 | Statement | 0.000 | 0.261 | 0.553 | -0.090 | 0.140 | -0.258 |
| 2026-06-17 14:00 | Press conference | 1.065 | 0.070 | 0.553 | -0.090 | 0.140 | -0.258 |
| 2026-07-08 14:00 | Minutes | 1.053 | 0.130 | -0.089 | -0.010 | 0.000 | 1.506 |
| 2026-07-29 14:00 | Press conference | 0.401 | 0.065 | -0.572 | 0.100 | -0.050 | -0.966 |
| 2026-07-29 14:00 | Statement | 2.000 | 0.216 | -0.572 | 0.100 | -0.050 | -0.966 |
| 2026-08-19 14:00 | Minutes | 1.291 | 0.104 | -0.823 | -0.060 | 0.010 | -0.842 |
| 2026-08-28 12:00 | Speech | 0.208 | 0.060 | 0.545 | -0.080 | 0.110 | -0.208 |
| 2026-09-16 14:00 | Statement | 2.000 | 0.355 | 0.662 | -0.060 | 0.060 | 0.911 |
| 2026-09-16 14:00 | Press conference landing page | 0.000 | -0.022 | 0.662 | -0.060 | 0.060 | 0.911 |
| 2026-09-18 12:00 | Speech record | 0.000 | 0.035 | 0.000 | -0.020 | 0.000 | 1.118 |

The same-day statement and press-conference rows deliberately share a market move: they were released on the same announcement date. They should not be treated as independent events in a final inference exercise.

## Table 3. One-day regressions with the 3-month bill control

Each row regresses the one-day outcome on one tone score and DGS3MO, using HC3 robust standard errors. Same-day communications are aggregated before estimation, so the 229 observations are event days rather than documents.

| Indicator | Tone method | N | Tone beta | Tone p-value | DGS3MO beta | R-squared |
|---|---|---:|---:|---:|---:|---:|
| DXY | Lexicon | 229 | -0.024 | 0.203 | 3.463 | 0.063 |
| DXY | FinBERT | 229 | 0.356 | 0.283 | 3.484 | 0.062 |
| DXY | Factor similarity | 229 | -2.127 | 0.559 | 3.512 | 0.058 |
| 10s2s | Lexicon | 229 | -0.002 | 0.356 | -0.392 | 0.082 |
| 10s2s | FinBERT | 229 | -0.030 | 0.321 | -0.383 | 0.082 |
| 10s2s | Factor similarity | 229 | -0.022 | 0.963 | -0.387 | 0.077 |
| 1-year Treasury yield | Lexicon | 229 | -0.001 | 0.435 | 0.846 | 0.272 |
| 1-year Treasury yield | FinBERT | 229 | -0.000 | 0.994 | 0.850 | 0.270 |
| 1-year Treasury yield | Factor similarity | 229 | -0.314 | 0.317 | 0.847 | 0.273 |
| Growth minus value | Lexicon | 229 | 0.087 | 0.141 | 1.389 | 0.011 |
| Growth minus value | FinBERT | 229 | -1.315 | 0.145 | 1.314 | 0.010 |
| Growth minus value | Factor similarity | 229 | -16.431 | 0.103 | 0.968 | 0.012 |

All 12 tone coefficients have p-values above 0.10. Growth-minus-value remains the closest case—positive for the lexicon and negative for FinBERT and factor similarity—but its sign is method-dependent and its estimated relationship is not conventionally significant. The short-rate control explains more variation in the 1-year yield than text does, while every tone specification has low explanatory power. The addition of the September 16/18 records does not change this conclusion.

## Comparison with the readings

Doh, Kim, and Yang (2021) argue that qualitative statement language can move financial conditions independently of the target-rate decision. This project uses DGS3MO as a control in the same spirit, but its broad daily window and mixed document types produce weaker yield results. The disagreement between the lexicon and FinBERT results also reinforces their concern that measuring policy language is not straightforward. [Doh, Kim, and Yang (2021)](https://www.kansascityfed.org/documents/7577/erv106n1dohkimyang.pdf)

Doh, Song, and Yang separate tone, novelty, and the surprise component using alternative FOMC statements and high-frequency data. This project improves on a single word list by adding FinBERT, but it still uses absolute tone and daily returns. It cannot make their counterfactual or surprise-based causal claims. Adding novelty, a narrow event window, and clustered treatment of same-day
statement/press-conference pairs would improve the design. [Doh, Song, and Yang](https://www.kansascityfed.org/documents/5642/rwp20-14dohsongyang.pdf)

The *Parsing the Fed* comparison includes a factor-similarity robustness measure alongside the word-list and FinBERT scores. Its results do not rescue a directional conclusion: its coefficients are also statistically weak. The exercise therefore illustrates why measurement choice, release timing, and event-window design matter more than selecting a preferred text score.

## Supplemental ex-post analysis: September 16 FOMC press conference

This is an ex-post update, kept separate from the September 13 forecast below. September 16 was an FOMC statement and Chair Warsh press conference, not a standalone Chair speech. At 2:00 p.m. EDT, the FOMC unanimously raised the target range by 25 basis points to 3.75%–4.00%; the statement described solid activity and elevated inflation. [Official statement](https://www.federalreserve.gov/newsevents/pressreleases/monetary20260916a.htm)

### Supplemental Table. One-day market reaction

The values below use the notebook's close-to-close definitions: DXY and IWF-minus-IWN are percent changes, while Treasury measures are percentage-point changes. They are not added to Tables 1–3 or the pre-event regression sample in this report, preserving the original forecast.

| Event day | DXY | 10s2s | 1-year | Growth minus value | DGS3MO control |
|---|---:|---:|---:|---:|---:|
| 2026-09-16 | +0.662% | -0.060 | +0.060 | +0.911% | +0.030 |

The realized move was strongly consistent with a hawkish policy-event interpretation: the dollar and one-year yield rose, the curve flattened, and growth outperformed value. Relative to the pre-event lexicon scenario, the sign was correct for curve flattening and growth-minus-value, but wrong for DXY and the one-year yield; the observed growth-minus-value move (+0.911%) was also much larger than the +0.115% scenario estimate. This single event is descriptive evidence, not a new regression result or a causal decomposition of the statement, projections, decision, and Q&A.

### Q&A interpretation and transcript scoring

The official preliminary transcript confirms that the associated reporter questions tested whether a small hike can address supply-side inflation, whether more hikes are likely, whether conditions are restrictive, the neutral rate, consumer costs, political independence, long yields, and the employment consequences of tightening. Warsh's responses reinforced the hawkish message: he described the action as removing accommodation, prioritized price stability, rejected short-term data-point dependence and forward guidance, and did not commit to a specific next move. His answers on independence also avoided discussing conversations with the President. [Official transcript](https://www.federalreserve.gov/mediacenter/files/FOMCpresconf20260916.pdf)

Using the complete official transcript (prepared remarks plus Q&A), the supplemental notebook cell reports lexicon **+1.236**, corpus-anchored factor similarity **+0.007**, and FinBERT **+0.085**. The word-list result reflects four occurrences of `restrictive` and one of `raise the target range`, normalized by 4,853 words. All three scores are positive, so the quantitative measures now agree with the qualitative hawkish reading, although the FinBERT and similarity magnitudes are modest. The official transcript remains outside Tables 1–3 to preserve the pre-forecast regression sample and avoid adding a single post-event observation without re-estimating the full analysis.

## September FOMC forecast

This section preserves the stated rate and tone probabilities, but the latest notebook run recalculates the mechanical market scenario using the now-expanded event sample. Because September 16 has already occurred, the values below should be interpreted as current model output rather than an ex-ante forecast.

### Rate decision

| Cut | Hold | Hike |
|---:|---:|---:|
| 20% | 75% | 5% |

The hold remains the modal outcome. Communication-tone evidence does not itself identify a policy-rule change, and the small Warsh sample argues against a more aggressive rate call.

### Statement tone

There is a **65% probability** that the September statement is more hawkish than the prior statement. Recent Warsh communications are generally positive on both scores, though the modest FinBERT magnitudes argue against a high-confidence hawkish surprise.

### Market reaction

The current lexicon-based forecast uses the latest statement tone scenario.

| Indicator | Probability it rises | Expected one-day change |
|---|---:|---:|
| DXY | 44.6% | -0.056% |
| 10s2s spread | 42.9% | -0.007 percentage points |
| 1-year Treasury yield | 48.8% | -0.001 percentage points |
| Growth minus value | 53.9% | +0.121% |

These are lexicon-based scenario estimates, not a consensus forecast. FinBERT and factor similarity point in the opposite direction for growth minus value, and no event-level tone coefficient is conventionally significant. The point estimates should therefore be read as a transparent mechanical mapping from the latest statement tone, not as evidence of an expected tradeable return.

## Recommendation and falsification

**Position:** take a *very small* long-IWF/short-IWN position (long growth minus value) ahead of the meeting.

**Why:** This is a deliberately low-conviction scenario trade, not a statistically supported signal. The current lexicon mapping assigns growth minus value the highest probability of rising (53.9%) and an expected one-day move of +0.121%. However, after aggregating same-day communications, the lexicon estimate is not significant (p = 0.141), while FinBERT and factor similarity have the opposite sign. Position size should therefore be small enough that the trade is expendable.

**What proves it wrong:** Close the position if statement-day growth-minus-value is -0.50% or lower, or if the 1-year Treasury yield rises by at least 10 basis points. Either outcome contradicts the mild lexicon scenario. More fundamentally, a revised design with verified timestamps and a consistent, statistically supported result across the three methods would supersede this tentative recommendation.
