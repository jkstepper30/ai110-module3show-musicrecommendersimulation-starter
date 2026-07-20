# 🎵 Music Recommender Simulation

## Project Summary

In this project you will build and explain a small music recommender system.

Your goal is to:

- Represent songs and a user "taste profile" as data
- Design a scoring rule that turns that data into recommendations
- Evaluate what your system gets right and wrong
- Reflect on how this mirrors real world AI recommenders

Replace this paragraph with your own summary of what your version does.

---

## How The System Works

- Real platforms run a pipeline: collect interactions → generate candidates (millions→hundreds) → score each candidate for the user → apply list-level reranking

- My system will implement a small, content-based pipeline: build per-song vectors, form a user vector from liked history, score candidates by closeness, then pick and lightly rerank top results.

 The features that my song will use in my system include: 
 
  •	Numeric audio features: energy, tempo_bpm, valence, danceability, acousticness.
  •	Categorical metadata: genre, mood.
  •	Identifier fields: id, title, artist (used for lookup and optional artist-based rules).

My UserProfile will store: 

•	Liked/seed song ids and short recent history (last N plays).
•	Preferred genres and mood weights (counts or normalized frequencies).
•	Simple exposure/history counters (to avoid re-recommending immediately).

My Recommender will compute a score for each song by: 
•	Preprocess: min–max scale numeric features to [0,1] (or z-score).
•	Categorical match: add a boost for genre/mood matches (e.g., +g_weight if genre == preferred; or use cosine on one-hot vectors).

Algorithm Recipe (finalized)
•	Inputs: user target = {genre?, mood?, numeric targets: energy, tempo_bpm, valence, danceability, acousticness}. Song record has same fields.

 Categorical scoring
•	Genre: exact = +2.0, related/subgenre = +1.0, same parent category = +0.75
•	Mood: exact = +1.0, related = +0.5

Expected Biases: 
•	Genre dominance: strong genre points will favor same-genre items and can hide great matches from other genres that fit mood/energy. Mitigation: reduce genre weight slightly or add a diversity/serendipity boost (e.g., +small score for cross-genre high numeric similarity).

•	Feedback loop & popularity bias: optimizing for clicks can amplify already-popular songs. Mitigation: include exploration (epsilon-greedy), exposure caps, or re-weight novelty.

---

## Getting Started

### Setup

1. Create a virtual environment (optional but recommended):

   ```bash
   python -m venv .venv
   source .venv/bin/activate      # Mac or Linux
   .venv\Scripts\activate         # Windows

2. Install dependencies

```bash
pip install -r requirements.txt
```

3. Run the app:

```bash
python -m src.main
```

### Running Tests

Run the starter tests with:

```bash
pytest
```

You can add more tests in `tests/test_recommender.py`.

---

## Sample Recommendation Output

Paste a sample of your recommender's output here as a text block so a reader can see what it produces:

```
# e.g.:
# User profile: genre=indie, mood=chill, energy=low
# Recommendations:
#   1. ...
#   2. ...
#   3. ...
```

**Screenshot or video** *(optional)*: <!-- Insert a screenshot or demo video link here -->

---

## Experiments You Tried

Use this section to document the experiments you ran. For example:

- What happened when you changed the weight on genre from 2.0 to 0.5
- What happened when you added tempo or valence to the score
- How did your system behave for different types of users

---

## Limitations and Risks

Summarize some limitations of your recommender.

Examples:

- It only works on a tiny catalog
- It does not understand lyrics or language
- It might over favor one genre or mood

You will go deeper on this in your model card.

---

## Reflection

Read and complete `model_card.md`:

[**Model Card**](model_card.md)

Write 1 to 2 paragraphs here about what you learned:

- about how recommenders turn data into predictions
- about where bias or unfairness could show up in systems like this



