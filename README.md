# Esports Match Prediction Script

## Overview

This Python script is designed to predict outcomes for Week 6 matches in a double round-robin esports tournament (e.g., similar to MPL ID for Mobile Legends: Bang Bang). It uses historical match data, current standings, and a simple prediction model based on team performance metrics such as win rates, game differentials, and head-to-head results.

The script processes input data from past weeks (matches, scores, and standings) and generates predicted scores for upcoming matches. Predictions are for Best-of-3 (Bo3) format matches.

**Note:** This is a basic predictive tool for entertainment purposes. Real outcomes depend on many factors like team form, player performance, and meta changes. Predictions are not guaranteed.

## Features

- Parses historical match results and standings.
- Calculates team statistics (e.g., win percentage, average games won/lost).
- Uses a weighted scoring system to predict match outcomes:
  - 60% based on overall standings (match wins, game diff).
  - 30% based on recent form (last 3 matches).
  - 10% based on head-to-head history.
- Outputs predictions in a structured text format (e.g., "TeamA 2 1 TeamB").
- Supports easy input via JSON or text files for scalability.

## Requirements

- Python 3.8+
- Libraries:
  - `pandas` for data handling.
  - `numpy` for calculations.
  - `scikit-learn` (optional, for advanced ML-based predictions if extended).

Install dependencies:
```
pip install pandas numpy scikit-learn
```

## Installation

1. Clone the repository:
   ```
   git clone https://github.com/dimasbayusujiwo/emps.git
   ```
2. Navigate to the directory:
   ```
   cd emps
   ```
3. Install requirements:
   ```
   pip install -r requirements.txt
   ```

## Usage

### Basic Command-Line Usage

Run the script with input files:
```
python predict_matches.py --input_matches past_matches.txt --input_standings standings.txt --output predictions.txt
```

- `--input_matches`: Path to a text file with historical match data (format as in the example below).
- `--input_standings`: Path to a text file with current standings.
- `--output`: (Optional) Path to save predictions. Defaults to console output.

### Input Format

#### Past Matches (e.g., `past_matches.txt`)
Follow this structure:
```
Week 1
Day 1
ONIC 2 0 DEWA
NAVI 0 2 EVOS
...
```

#### Standings (e.g., `standings.txt`)
```
# Team Match Game Diff
1. ONIC 9-0 18-3 +15
2. Bigetron by Vitality 7-2 15-8 +7
...
```

### Example Output

For Week 6 predictions:
```
Week 6
Day 1
NAVI 1 2 DEWA
AE 2 1 GEEK

Day 2
EVOS 1 2 AE
TLID 0 2 ONIC
RRQ 1 2 BTR

Day 3
NAVI 2 1 TLID
ONIC 2 1 RRQ
GEEK 1 2 EVOS
```

### Customizing Predictions

- Edit `prediction_model.py` to adjust weights or add ML models (e.g., logistic regression on team stats).
- For real-time data, integrate with APIs (not included; extend as needed).

## How Predictions Work

1. **Data Parsing:** Reads matches to build team histories.
2. **Stat Calculation:** Computes win rates, form streaks, etc.
3. **Match Simulation:** For each upcoming match, simulates Bo3 by comparing stats and randomly adjusting for variance (seeded for reproducibility).
4. **Output Generation:** Formats results as text.

Example prediction logic (simplified):
```python
def predict_score(team_a, team_b):
    score_a = round(team_a.win_rate * 2 + random.uniform(-0.5, 0.5))
    score_b = 2 - score_a if score_a > 1 else random.choice([0, 1, 2])
    return max(0, min(2, score_a)), max(0, min(2, score_b))
```

## Limitations

- Assumes all matches are Bo3; no support for other formats.
- No real-time data fetching; inputs must be manual.
- Basic model—does not account for patches, roster changes, or external factors.
- Predictions are deterministic with a seed; add more randomness if desired.

## Contributing

Feel free to fork and submit pull requests. Suggestions for improving the model (e.g., adding Elo ratings) are welcome!

## License

MIT License. See `LICENSE` for details.
