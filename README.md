# AI Mini-DJ v0.1

Ever wondered if an AI could learn the 'art' of DJing? This project is my dive into that very question. It's an end-to-end prototype of an AI DJ, built from scratch, that tries to automatically find compatible songs and mix them together.

It's not perfect, it's not Skrillex, but it's a fully functional proof-of-concept that shows just how far we can get with open-source tools.

---

### Inspiration

The idea for this sparked after seeing Apple Music's slick **AutoMix** feature (introduced in iOS 26) and hearing about **Spotify's AI DJ**. These tools create seamless transitions that feel like a professional DJ set, blending tracks in a way that's genuinely impressive. That got me thinking: what kind of magic is happening under the hood? Could I try to replicate some of that magic myself?

### The Gap This Project Tries to Fill

As cool as these commercial features are, they're often locked inside specific ecosystems and subscriptions. For many of us (shout-out to my fellow Indonesians where Spotify DJ isn't available!), these tools are out of reach.

This project is a "for fun, for science" attempt to explore and democratize that tech. The goal wasn't to compete with multi-billion dollar companies, but to build a transparent, open-source prototype that shows the core logic. It's for anyone who wants to peek behind the curtain, play with the code, and learn how an AI can be taught to "think" about music.

**[Try the Live Demo on Google Colab](https://colab.research.google.com/drive/1-2rRQUsLdZuv4xS97jOeQ-2h5eDlcUt3?usp=sharing)**
*(The notebook is self-contained! All the necessary models and data are automatically downloaded from a Hugging Face repository, so you can run it with just a few clicks.)*

---

### How It Works: The Three-Part Brain

The whole system is built on a three-stage pipeline:

1.  **The Ears (Feature Extraction):** A script that "listens" to thousands of songs from the Free Music Archive (FMA) dataset and extracts key musical features like BPM (tempo), key, energy (RMS), and brightness (spectral centroid) using `librosa`.

2.  **The Brain (The Scorer AI):** A PyTorch-based neural network trained to act as the "taste-maker." It looks at the features of two different songs and outputs a "mixability score" from 0 to 1. It was trained with a simple rulebook: a "good mix" involves similar BPMs and harmonically compatible keys.

3.  **The Hands (The Mixing Engine):** If the AI Brain gives a high score (thinks the tracks are a good match), this engine takes over. It performs a sophisticated, automated mix by:
    * **Beat-matching** the tempos via time-stretching.
    * **Beat-syncing** the downbeats to avoid rhythmic clashes ("trainwrecks").
    * Performing an **EQ-filtered crossfade** to create a smoother textural blend than just swapping volumes.

---

### The Good, The Bad, and The Ugly (Honest Review)

So, what's the catch? Here's the real talk on what this experimental project can and can't do.

#### The Good (The Wins)
* **It Works!** The pipeline is fully functional end-to-end. It can analyze, score, recommend, and mix songs completely autonomously.
* **The AI Learns:** The neural network achieved over 99% validation accuracy on its defined task. This proves it's extremely good at learning and applying the rules it was taught.
* **Smart(er) Transitions:** The mixing engine is more than a simple crossfader. The beat-sync and EQ-filtering logic helps prevent obvious "trainwrecks" and makes the technical transition cleaner.

#### The Bad & The Ugly (The Limitations)
* **The AI has no "real" taste.** The AI's definition of a "good mix" is based on a very simple, rigid set of rules (BPM + Key). It doesn't understand nuance or context. This is why it sometimes recommends pairs that are technically compatible but texturally jarring.
* **It's Structurally Deaf.** This is the biggest weakness. The AI has no concept of song structure (intros, drops, choruses, vocals vs. instrumentals). This is why some transitions feel abrupt—like a "roller coaster"—because it might mix a quiet intro with a loud drop without understanding the energy shift.
* **Dataset Mismatch.** It was trained on the FMA-small dataset, which is a wild mix of genres (Rock, Hip-Hop, Folk, etc.). This is very different from a typical, genre-consistent DJ set (like EDM or House), making truly "club-ready" smooth transitions challenging.

---

### Tech Stack
* **PyTorch** (for the neural network)
* **Librosa** (for audio feature extraction)
* **Pydub** (for audio manipulation and mixing)

### Acknowledgements

This project would have been impossible without the incredible open-source community and data providers.

* A huge thank you to the **Free Music Archive (FMA)** and all the artists who generously shared their music. The `fma_small` dataset was the backbone of this entire experiment.
* Massive props to the teams and contributors behind **PyTorch**, **Librosa**, **Pydub**, and **scikit-learn**. Your tools are amazing and make complex projects like this accessible to solo developers everywhere.
* And Gemini 2.5 Pro from [@google](https://github.com/google), to assist and help me creating this experimental + crazy project with amazing AI model.
