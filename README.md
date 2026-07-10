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

## Batch Run
The batch run feature repeats the experiment N times under identical model settings. This lets you assess the variability of outcomes (e.g., time-to-recover, retention rate) across stochastic replications without manually re-launching.

**Enabling batch mode.** At the bottom of the setup dialog, expand the **Batch / Repeated Runs** section by checking its toggle. Set the number of runs using the slider (minimum 2, maximum 50). The badge next to the toggle updates to show the selected count.

- syncofly_batch_summary_*.csv: one row per run (including Run 1 prepended). Columns include condition, perturbation type, epoch durations, baseline match mean, time-to-group-sync, retention rate, recovery rate, full-recovery time.
- syncofly_batch_beats_*.csv: every Source A and agent beat event across all runs, tagged with run_index. Suitable for downstream analysis of emission patterns or beat-level statistics.

## Swapping the Grid Model (Advanced Developer Guide)

Each predictive agent runs an instance of M4p (abbreviation for Grid Model), a hierarchical meter-predictive oscillator defined as a JavaScript class in the source file. If you want to replace this with a different timing model (i.e. a phase oscillator, a recurrent network, a Bayesian meter tracker, or anything else) you only need to satisfy the interface that Robot expects from its this.model object.

**Where to look:**
The M4p class definition begins around line 1091 (search for class M4p). The Robot class begins around line 1507 (search for class Robot). The model is instantiated inside the Robot constructor. The batch runner re-instantiates it at the same pattern. Replace both occurrences with your own class to use it everywhere.

Robot reads three properties and calls three methods on this.model each frame: (1) cycle_period, (2) last_onset_time, (3) structural_memory.

The batch runner calls b5.model.cycle_period and b5.model.last_onset_time. As long as your model keeps those two properties updated, the batch evaluator should work without modification.


## Citation

Wu, Y.: Syncofly. https://github.com/yanni-yanni/syncofly (2026)

