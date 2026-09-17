# Week 02 Lab

Instrument a provided training script (`train.py`) with MLflow experiment tracking; log params, metrics, and artifacts across a few runs, then compare them in the MLflow UI.

Starter files for this week's lab are pulled into your repo via `git fetch upstream && git merge upstream/main`, as introduced in the Week 1 lab.


## Reflection

The best-performing run was Run 3, using `n_estimators=200` and `max_depth=None`. It achieved roughly 0.97 accuracy, compared with about 0.83 for the baseline (`n_estimators=10`, `max_depth=3`), an improvement of around 0.14, or 14 percentage points.

This combination likely performed best because it used more trees and allowed them to grow without a depth limit. More trees make the Random Forest more stable, while deeper trees can learn the more detailed patterns needed to distinguish handwritten digits.

Part 2's bare script already contained the code, used the built-in dataset, and ran in my local environment, but it did not preserve the experiment configuration. MLflow now tracks the configuration by recording the hyperparameters and metrics for every run, so I can reproduce and compare results later.
