# RiskLens

A custom TradingView (Pine Script) indicator that automates futures risk management and position sizing directly on the chart — built to replace manual, error-prone risk math during live trading.

## The Problem

Before building this, I calculated position size manually for every trade: converting price distance to points, points to dollars, checking that against my risk-per-trade limit, and verifying the reward-to-risk ratio — all under time pressure while a chart is moving. It was slow, and small arithmetic mistakes had real financial consequences.

## What It Does

- **Auto-detects the contract from the chart and converts it to its micro equivalent** — e.g. pull up a GC chart and it recognizes MGC, pull up an ES chart and it recognizes MES — then pulls in the correct dollar-per-point value for that micro contract. Built this way because I trade micros exclusively; a manual override is also available if a standard contract's own value is ever needed.
- **Interactive on-chart placement** — click to set Entry, Stop, and Target directly on the chart, similar to TradingView's native long/short tool, with draggable points that recalculate live as they're moved.
- **Automatic position sizing** — enter a preferred risk amount (e.g. $300) and a hard risk ceiling (e.g. $350), and the tool calculates the exact number of contracts that fits within those limits.
- **Reward-to-risk validation** — flags whether a setup meets a minimum acceptable R:R before you take the trade.
- **Real-time, color-coded status flags** — the decision box turns blue for a valid setup or red when a hard-risk or R:R rule is broken, with text status (`VALID`, `CAUTION — ABOVE PREF`, `NO TRADE — HARD RISK`) so you can tell at a glance without reading numbers first.
- **Multiple display modes** (Compact / Full / Minimal) with adjustable label positioning and an outside-label offset, so labels stay clear of the trade zone regardless of chart layout or zoom level.

## How It Works

The script reads the chart's ticker to identify the underlying contract, converts it to its micro equivalent, then applies a lookup table of real point values (matching actual CME contract specs). It converts the price distance between your entry/stop/target clicks into dollar risk and reward, compares those figures against your input thresholds, and renders color-coded boxes, lines, and labels directly on the chart — redrawing live as you adjust your levels.

## Development Notes

Built and refined through several iterations, using AI-assisted development (ChatGPT) to translate risk-management logic and UI requirements into working Pine Script. I designed the risk rules, contract logic, and interface behavior; AI assistance helped implement and debug the code. Each version was tested against live trading use before moving to the next.

## Screenshots

<img width="2602" height="1598" alt="Image 1" src="https://github.com/user-attachments/assets/644e92b7-4750-46be-983d-738005e04060" />

*A rejected setup on ES/MES — risk exceeds the hard limit and R/R falls short, so the tool flags "NO TRADE" instead of green-lighting it. (Shown in TradingView's bar replay mode for demonstration.)*

<img width="2589" height="1856" alt="Image 2" src="https://github.com/user-attachments/assets/a63f3df8-6b14-49bc-b1da-b2260f7ed941" />

*An approved setup on NQ/MNQ — strong 7.75 R/R, tool confirms "VALID" and suggests position size.*

<img width="1425" height="1598" alt="Image 3" src="https://github.com/user-attachments/assets/e33f1b4f-eb3b-4729-a47c-a840270a09fe" />
*The full settings panel — direction, display mode, label positioning/offset, auto vs. manual contract mode, and risk thresholds are all user-configurable.*

## Disclaimer

This tool is for personal trading and educational purposes. It does not constitute financial advice. Futures trading involves substantial risk of loss.
