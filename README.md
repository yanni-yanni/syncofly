# SYNCOFLY

A browser-based simulation platform for studying collective rhythmic synchronization under perturbation.

## Overview

SYNCOFLY runs entirely in the browser. Five simulated agents (B1-B5) synchronize to a rhythmic source (Source A) while socially coupling to one another. Each agent can operate as a **predictive** agent, maintaining a hierarchical meter representation via the Grid Model, or as a **reactive** agent that aligns through local error correction. This lets you systematically vary how predictive timing capacity is distributed across a group and observe its effect on collective resilience.

## Features

- **Self-defined rhythm pattern**: combinations of binary (up to 16th-note) and ternary (up to 24th-note) subdivisions via a polar clock editor.
- **Two agent architectures**: Predictive (Grid Model) and Reactive, configurable per agent
- **Perturbations**: Beat Omission (signal dropout) and Pattern Switch (A→B→A structural transitions), with user-defined magnitude and epoch durations
- **Noise injection**: per-agent phantom-event injection to study instability propagation
- **Exportable logs** : CSV exports of time-series log, epoch summary, beat-event log, parameter snapshot, and parameter change

## Getting Started

No build step required. Open 'syncofly_sab.html' in a modern browser (Chrome recommended for Web Audio API compatibility).

## Usage

1. **Pattern tab**: set cycle period *T*, choose or draw a rhythm, and set the match tolerance window.
2. **Agents tab**: configure each agent as predictive or reactive; set Source A and peer-coupling weights; optionally enable noise injection.
3. **Perturbations tab**: select perturbation type, configure probability/duration, and set epoch lengths.
4. **Launch**: click Launch to begin the simulation. Specific live controls (hearing range, source reach) remain adjustable during the run.
5. **Export**: download CSVs from the right panel for further analysis.

## Citation
