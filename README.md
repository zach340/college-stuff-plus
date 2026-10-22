# College Stuff+

A Stuff+ model for college (Power 4) pitchers, built from pitch characteristics only: velocity, spin, movement, release point and extension. Location isn't used.

## How it works
- A LightGBM model predicts the chance of a whiff on each swing. Whiffs are the outcome most driven by pitch quality.
- Left-handed pitchers are mirrored, and each pitch is compared to the pitcher's own fastball.
- Predictions are made out-of-fold by pitcher, so no pitcher is scored by a model that trained on him.
- Stuff+ is scaled within pitch type: 100 is an average college pitch of that type, and each 10 points is one standard deviation.

## Validation
Each pitcher's games were split into odd and even halves. Stuff+ from one half, against results in the other:

| Predicts | Correlation |
|---|---|
| Whiff % | 0.69 |
| Run value per pitch | 0.24 |
| Baseline: a pitcher's own run value | 0.12 |

## Files
- `model3.ipynb`: the full pipeline
- `StuffPlus_ByPitcher.csv`: one row per pitcher (300+ pitches), with overall Stuff+ and each pitch's Stuff+ and usage
- `StuffPlus_ByPitch.csv`: one row per pitcher and pitch type (100+ pitches), with velocity and movement
- `run_values.csv`: run value of each outcome by count

The raw pitch data (`MovementP4.csv`) isn't included. To rerun the model, put it in this folder and run `model3.ipynb`.

```
pip install -r requirements.txt
```
