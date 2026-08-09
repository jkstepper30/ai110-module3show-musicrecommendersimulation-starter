# 🎧 Model Card: Music Recommender Simulation

## 1. Model Name  

Give your model a short, descriptive name.  
Example: **VibeFinder 1.0**  

---

## 2. Intended Use  

Describe what your recommender is designed to do and who it is for. 

Prompts:  

- What kind of recommendations does it generate  
- What assumptions does it make about the user  
- Is this for real users or classroom exploration  

---

## 3. How the Model Works  

Explain your scoring approach in simple language.  

Prompts:  

- What features of each song are used (genre, energy, mood, etc.)  
- What user preferences are considered  
- How does the model turn those into a score  
- What changes did you make from the starter logic  

Avoid code here. Pretend you are explaining the idea to a friend who does not program.

---

## 4. Data  

Describe the dataset the model uses.  

Prompts:  

- How many songs are in the catalog  
- What genres or moods are represented  
- Did you add or remove data  
- Are there parts of musical taste missing in the dataset  

---

## 5. Strengths  

Where does your system seem to work well  

Prompts:  

- User types for which it gives reasonable results  
- Any patterns you think your scoring captures correctly  
- Cases where the recommendations matched your intuition  

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

Prompts:  

- Additional features or preferences  
- Better ways to explain recommendations  
- Improving diversity among the top results  
- Handling more complex user tastes  

---

## 9. Personal Reflection  

A few sentences about your experience.  

Prompts:  

- What you learned about recommender systems  
- Something unexpected or interesting you discovered  
- How this changed the way you think about music recommendation apps  
