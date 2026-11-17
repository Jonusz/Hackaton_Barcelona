# FC Po Nalewce: ball possession labelling

Our submission for **More than a Hack 2027, Phase 1: Ball Possession** (Metrica Sports / FC Barcelona).

The pipeline labels every frame of the tactical video as home possession (H), away possession (A), dead ball (D) or no answer (X).

## Team

- Aleksandra Michałowska
- Krzysztof Wesołowski
- Janusz Bekas

## How it works

1. **Nearest player.** For each frame, the team of the tracked player closest to the ball (`starter/baseline.py`).
2. **Dead-ball hint.** Smart Tagging set-piece, goal and dead-ball intervals.
3. **Smoothing.** A majority vote over neighbouring frames removes flicker.
4. **Combination.** The smoothed labels, overridden with D where a three-state sequence model (Viterbi decoding, hand-set costs) labels a frame D.

Full details are in the technical document: `TEAM_NAME.pdf`.

## Setup

follow notebook to install all dependencies

The match data is not in this repository and must not be committed.

## Reproduce the submission

1. Open `FCPN_Analysis.ipynb` in a fresh kernel.
2. Run all cells from the top. 
3. The submission is written to `evaluation/results/baseline_smooth50_with_hmm_setpiece_bias_low_D.csv`.

Check it with:

```bash
python evaluation/validate_submission.py evaluation/results/baseline_smooth50_with_hmm_setpiece_bias_low_D.csv
```

## Files

- `FCPN_Analysis.ipynb`: the full pipeline and analysis.
- `starter/`: the organisers' starter code, unchanged.
- `evaluation/`: the organisers' evaluation tools.
- `TEAM_NAME.pdf`: technical document.
- `TEAM_NAME.csv`: the submitted possession file.

## Limitations

See section 8 of the technical document.
