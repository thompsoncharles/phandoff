# Public Handoff: BTC Quant Paper Observation Workflow

**Date:** 2026-07-05  
**Project type:** College engineering / quantitative research project  
**Development history:** Four major iterations over roughly eight months 
**Current state:** One Bitcoin strategy candidate promoted from backtesting into daily paper observation. Live trading is disabled.

---

## 1. Project Overview

This project is a Bitcoin quantitative trading research and automation system. The current version is not a live trading bot and does not claim live profitability. It is a paper observation workflow designed to test whether a backtested daily BTC candidate can hold up in forward observation.

The main engineering focus is not just the model. The system emphasizes:

- data quality checks
- realistic fees and slippage
- walk forward out of sample testing
- frozen candidate configuration
- paper only safety rules
- scheduled daily observation
- operational reporting
- separate lab research for rejected or future ideas

This document is a public, sanitized version of the internal project handoff.

---

## 2. Current Phase

The system is in **paper observation mode**.

The candidate is frozen. The next milestone is to collect forward evidence before making strategy changes.

Reconsideration requires:

- at least 20 paper signals, or
- at least 60 calendar days of observation

Until one of those gates is met, the correct verdict is **keep observing**.

---

## 3. Daily Workflow

The daily routine runs once per day after the BTC daily bar is available.

Conceptually, it performs this sequence:

1. Verify paper only safety rules.
2. Refresh or validate BTC daily data.
3. Run the data quality gate.
4. Score the frozen daily candidate.
5. Log whether the system would enter or stay flat.
6. Record gate pass or fail reasons.
7. Update paper observation reports.
8. Write daily status and operational logs.

The workflow is intentionally paper only. It is designed to observe and report, not place orders.

---

## 4. How Status Is Checked

The system writes human readable and spreadsheet friendly outputs:

- concise daily status report
- paper observation scoreboard
- observation journal
- reason code summaries
- hypothetical trade ledger
- Markdown report
- CSV export
- Excel workbook export
- operational run log

The report includes a manual paper trade checklist. A hypothetical trade is only considered valid when the data gate, safety gate, candidate match, entry signal, regime filter, probability gate, edge to cost gate, and fee checks all pass.

---

## 5. Frozen Candidate

The current paper observation candidate is a daily BTC strategy selected through anchored walk forward validation across market regimes.

High level candidate summary:

| Field | Value |
|---|---|
| Cadence | Daily BTC bars |
| Label | Five day cost aware forward return label |
| Feature set | Full technical feature set |
| Regime filter | Long term trend plus volatility band |
| Model family | Linear/logistic BTC model |
| Risk model | Fixed stop, target, and max hold structure |
| Sizing | Small account, fee aware notional sizing |
| Fees | Realistic crypto commission assumptions |
| Status | Paper observation only |

The candidate was not promoted because of a single good backtest. It was promoted to paper observation only after passing predefined rules: positive net expectancy after fees and slippage, sufficient trade count, majority positive walk forward folds, multi regime survival checks, and comparison against simpler baselines. It is not treated as proven. Paper observation exists to test whether the historical behavior persists.

---

## 6. Why Live Trading Is Disabled

Live trading is disabled because the evidence is still paper/backtest evidence.

Important caution points:

- The most recent walk forward fold was negative.
- The strategy is concentrated in favorable trend regimes.
- Long periods of no signal are expected and are not necessarily bugs.
- Paper observation is needed before any live execution discussion.

The observation path is designed not to import or call order placement code. Safety checks are run as part of the routine, and records explicitly mark that no live orders are placed.

---

## 7. Paper Observation Rules

Rules during the observation window:

1. Do not change the frozen candidate.
2. Do not tune thresholds during observation.
3. Do not promote based on a small number of paper signals.
4. Do not reinterpret no signal days as failures if the regime filter is doing its job.
5. Do not enable live trading.
6. Reconsider only after 20 paper signals or 60 calendar days.

The purpose of the observation period is to collect forward evidence, not to keep reshaping the model.

---

## 8. Major Components Built

The current workflow includes:

- daily BTC observer
- paper report generator
- one command daily routine
- frozen candidate metadata
- signal search research command
- data quality gate
- optional derivatives data cache for future research
- scheduled daily run support
- Markdown/CSV/Excel report outputs
- alerting and operational logging
- smoke tests covering the workflow
- separate lab copy for experiments

The project also has a lab environment where experiments can be tested without touching the frozen paper observation workflow.

---

## 9. What Not To Change During Observation

The following should remain frozen while collecting paper evidence:

- candidate configuration
- model settings
- BTC signal thresholds
- stop/target/hold rules
- sizing assumptions
- observation journal
- paper report decision rules
- scheduled paper observation workflow

The lab copy is the correct place for new research experiments.

---

## 10. Troubleshooting Philosophy

If the daily routine fails, fixes should be operational only:

- data availability issue
- report generation issue
- scheduled run issue
- alert/logging issue
- safety check issue

A failed run should not trigger strategy changes. Strategy research belongs in the lab copy and should be judged by the same walk forward out of sample process.

---

## 11. Testing

The workflow is covered by smoke tests. These tests check the major research, reporting, safety, and monitoring paths.

Passing tests do not prove the strategy is profitable. They prove the workflow is internally consistent and that safety/reporting assumptions have not drifted.

---

## 12. Known Weaknesses

Current known weaknesses:

1. **Most recent fold was negative.**  
   The edge may have weakened in current market conditions. Paper observation is intended to test this.

2. **Bull regime concentration.**  
   Most historical profit came from favorable trend regimes. A long flat or no signal period can be correct behavior.

3. **Shorter timeframe path was not viable.**  
   The daily setup has the strongest evidence. The intraday/12 hour path did not pass the same standard.

4. **Derivatives features are not ready.**  
   Funding, open interest, liquidation, and related crypto native features need longer clean history before being used.

5. **This is not live execution infrastructure.**  
   Live trading would require separate broker/exchange execution controls, kill switches, capital controls, monitoring, and review.

---

## 13. Rejected Experiments

A useful part of the project was building a system strict enough to reject ideas.

One of the most useful parts of the project was building a system strict enough to reject my own ideas. Rejected or not promoted experiments included:

- hidden state regime modeling
- probability calibration
- shorter timeframe variants
- unstable or low trade count artifacts

These were rejected because they did not beat the frozen candidate under the same walk forward evaluation standards.

---

## 14. Future Improvements

Near term improvements:

- continue paper observation
- monitor scheduled runs
- maintain reports and logs
- back up journals and report artifacts

Future research ideas:

- derivatives regime features such as funding, basis, open interest, and liquidation stress
- macro or sentiment regime context
- on chain cycle features
- strategy ensembles or bandit selection once multiple viable candidates exist
- more durable database backed logging
- live execution design only after paper evidence and safety review

---

## 15. Next Decision Rules

After the paper gate is met:

- If paper evidence supports the backtest reference, continue paper observation or consider a separate minimum size execution design review.
- If paper evidence contradicts the backtest, reject the candidate and return to research.
- If too few trades occur, extend observation rather than forcing a decision.
- Nothing automatically promotes to live trading.

---

## Disclaimer

This is an educational engineering and quantitative research project. It is not financial advice, investment advice, or a recommendation to buy, sell, or trade Bitcoin or any other asset.

