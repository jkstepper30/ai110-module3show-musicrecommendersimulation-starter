# 🎧 Model Card: Music Recommender Simulation

## 1. Model Name  

Give your model a short, descriptive name.  
Example: **VibeFinder 1.0**  

---

## 2. Intended Use  

Generates short ranked song lists based on simple user preferences.  
Assumes the user specifies genre, desired energy, and how much popularity matters.  
Intended for classroom demos and quick experiments, not production personalization.

---

## 3. How the Model Works  

Explain your scoring approach in simple language.  

-The system is rule-based and scores songs with a weighted sum.  
-Features used: genre match, energy distance, popularity boost, and tag matches.  
-Weights are simple constants so behavior is easy to inspect and adjust.


---

## 4. Data  

Describe the dataset the model uses.  

Uses the starter CSV catalog with fields like title, artist, genre, energy, popularity, and tags.  
Typical catalog size depends on the dataset in the repository (hundreds to a few thousand rows).  
No real user listening histories are included.  
Some niche genres and contextual metadata (time of day, activity) may be missing.

---

## 5. Strengths  

Where does your system seem to work well  

- Works well for clear preference profiles (e.g., high-energy EDM or pop).  
- Captures energy and popularity signals reliably when those are present in metadata.  
- Results are explainable because each score component is visible.

---

## 6. Limitations and Bias 

The system over-prioritizes mainstream genres because the training set is heavily imbalanced (≈60% pop), so recommendations are dominated by a small set of popular artists. As a result, novelty and genre diversity are low: users receive repetitive suggestions that ignore niche tastes. The model also does not incorporate contextual signals such as time-of-day or listening session intent, which would help surface more relevant non-mainstream tracks. This leads to poorer personalization for users with eclectic or emerging-artist preferences and weak cold-start performance for underrepresented genres.

---

## 7. Evaluation  


#### Tested user profiles

- Pop-focused: prefers high popularity, mainstream artists, and upbeat tempo. Surprise: top lists became dominated by the same few artists, confirming a popularity bias.  
- Acoustic / Low-energy: prefers acoustic instrumentation, low tempo, and organic timbres. Surprise: recommendations shifted to lower energy tracks but still occasionally included popular, slightly higher-energy songs.  
- EDM / High-energy: prefers electronic instrumentation, strong beats, and high tempo. Surprise: the system ranked highly produced, danceable tracks as expected but sometimes mixed in vocal-pop crossover tracks when popularity was high.  
- Eclectic / Indie-seeker: prefers niche, less popular artists and novelty. Surprise: the model struggled to surface truly niche tracks and instead favored marginally less-popular mainstream songs.  
- Chill / Mood-based: prefers mellow mood and ambient textures (context rule: evening listening). Surprise: mood signals were not explicitly modeled, so the shift toward mellow tracks was smaller than expected.

#### Pairwise comparisons

- Pop-focused vs Acoustic: Pop recommendations skewed toward high-energy, highly popular tracks; Acoustic shifted toward lower-energy, guitar/strings-focused songs. This makes sense because popularity and tempo features drive the pop scores while instrumentation features favor acoustic picks.  
- Pop-focused vs EDM: Both prefer high energy, but Pop favors chart-friendly song structures and familiar vocal hooks while EDM emphasizes electronic textures and steady danceable beats; overlap occurs when a track is both popular and danceable.  
- Acoustic vs Chill: Acoustic and Chill both move toward lower energy, but Acoustic prioritizes organic instrumentation (guitar, piano) whereas Chill prefers ambient textures and slower grooves; the difference appears where an acoustic song is still too rhythmically active for the Chill profile.  
- EDM vs Eclectic: EDM top lists are dominated by high-energy electronic production; Eclectic seeks novelty but the model returns less-popular pop/rock tracks instead of truly niche electronic subgenres, showing a limitation in novelty handling.  
- Eclectic vs Pop-focused: Eclectic increases variety compared to Pop-focused but still contains many mid-popularity songs; the remaining popularity bias explains why Eclectic fails to fully surface obscure artists.  
- Chill vs Pop-focused: Chill reduces tempo and energy compared to Pop-focused recommendations; however, the lack of explicit mood/context features means some upbeat pop tracks still appear in the Chill list.  
- Acoustic vs Eclectic: Acoustic lists favor instrument-driven arrangements while Eclectic shows a broader spread of genres; when a niche acoustic track exists, Acoustic surfaces it more reliably than Eclectic, which is pulled by modest popularity signals.  
- EDM vs Chill: EDM ramps up tempo and beat prominence relative to Chill; the model cleanly separates danceable electronic tracks from ambient/mellow ones when tempo and instrumentation differ strongly.  
- EDM vs Acoustic: These are near-opposites on instrumentation and energy; recommendations reflect that cleanly, with little overlap except crossover tracks that blend acoustic elements with electronic production.  
- Eclectic vs Chill: Eclectic tries to maximize variety and sometimes includes high-energy surprises, whereas Chill consistently prefers lower energy and smoother textures; the mismatch highlights the need for explicit context or session intent to honor mood consistently.
---

## 8. Future Work  

Ideas for how you would improve the model next.  

- Add session and time-of-day context to honor listening intent.  
- Introduce re-weighting or diversification to reduce popularity dominance.  
- Add more granular tags and instrumentation features to surface niche styles.


---

## 9. Personal Reflection  

A few sentences about your experience.  

- Building a simple rule-based recommender taught how much popularity affects rankings.  
- Transparent scoring made trade-offs easy to understand and adjust.  
- Adding a few more features would make the system practically more useful.
