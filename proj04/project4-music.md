---
layout: page
title: Spotify Music Tracks 🎵
description: Description of the Spotify music tracks dataset in Project 4.
parent: 📊 Final Project
nav_exclude: true
---

# Spotify Music Tracks 🎵

This dataset contains audio and metadata features for 114,000 tracks spanning 114 genres, collected from the [Spotify Web API](https://developer.spotify.com/documentation/web-api). Each row corresponds to one track. The features include both audio characteristics computed by Spotify's algorithms (like danceability and energy) and metadata like popularity and whether the track contains explicit content.

`music_tracks.csv` is adapted from the [Spotify Dataset 1921-2020 by Yamac Eren Ay](https://www.kaggle.com/datasets/yamaerenay/spotify-dataset-19212020-600k-tracks) on Kaggle, with additional columns and modifications for this assignment. `artists.csv` is used as-is from the same source.

---

## Getting the Data

Download the data [here](https://drive.google.com/drive/folders/12YLD_cnfUL_aQjhGifckIcCIrWtt6D7H?usp=share_link). You'll find:
  
  - `music_tracks.csv`: contains one row per track with audio features, metadata, and a genre label.
  - `artists.csv`: contains one row per artist with follower counts, artist-level popularity, and genre tags.
  - `audio_exploration.ipynb`: a starter notebook that walks through how audio features are extracted
  from raw audio files.

---

## Dataset Description

### `music_tracks.csv`

| Column | Description |
|---|---|
| `track_id` | Spotify's unique identifier for the track |
| `artists` | Name(s) of the artist(s). Multiple artists are separated by semicolons |
| `album_name` | Name of the album |
| `track_name` | Name of the track |
| `popularity` | Spotify popularity score from 0–100, based on total plays and recency. Higher = more popular. |
| `duration_ms` | Duration of the track in milliseconds |
| `release_date` | Release date of the track — format varies: `YYYY-MM-DD`, `YYYY-MM`, or `YYYY` |
| `explicit` | Whether the track contains explicit content |
| `danceability` | How suitable the track is for dancing, based on tempo, rhythm stability, and beat strength (0–1) |
| `energy` | Perceptual intensity and activity: fast, loud, noisy tracks score high; classical scores low (0–1) |
| `key` | The musical key of the track (0 = C, 1 = C♯, ..., 11 = B). -1 if no key was detected. |
| `loudness` | Overall loudness of the track in decibels (dB). Typically ranges from −60 to 0 dB. |
| `mode` | Whether the track is in a major (1) or minor (0) key |
| `speechiness` | Presence of spoken words: values above 0.66 are likely spoken word content; below 0.33 is music (0–1) |
| `acousticness` | Confidence that the track is acoustic rather than electronically produced (0–1) |
| `instrumentalness` | Probability that the track contains no vocals: values above 0.5 suggest instrumental content (0–1) |
| `liveness` | Probability that the track was recorded with a live audience (0–1) |
| `valence` | Musical positiveness: high values sound happy and cheerful; low values sound sad or angry (0–1) |
| `tempo` | Estimated beats per minute (BPM) |
| `time_signature` | Estimated number of beats per measure (typically 3 or 4) |
| `track_genre` | Genre of the track, as labeled by Spotify |

### `artists.csv`

| Column | Description |
|---|---|
| `id` | Spotify's unique identifier for the artist |
| `name` | Name of the artist |
| `followers` | Total number of followers on Spotify |
| `popularity` | Artist-level popularity score from 0–100, which is distinct from track popularity |
| `genres` | List of genre tags associated with the artist, stored as a string (e.g., `"['indie rock', 'alternative']"`) |

---

## Example Questions and Prediction Problems

Feel free to base your exploration in Steps 1–4 around one of these questions, or come up with your own.

- Do tracks that are more danceable tend to be more popular? Does this relationship hold within each genre, or does genre confound it?
- Which genres tend to produce the most "positive" (high valence) music? Which produce the most "negative"?
- Are explicit tracks more energetic on average than non-explicit tracks? Is this true across all genres, or only some?
- How does the relationship between acousticness and energy differ across genres?
- Within your chosen genres, which audio features best separate one genre from another?
- How have audio features (energy, valence, danceability) changed over decades? Do certain genres show stronger trends than others?
- Do tracks from artists with more followers tend to be more popular? Is artist size a better predictor of track popularity than audio features?

Feel free to use one of the prompts below to build your predictive model in Steps 5–8, or come up with your own.

- Predict the genre of a track from its audio features.
- Predict whether a track will be popular (e.g., popularity ≥ 70) from its audio and metadata features.
- Predict whether a track is explicit from its audio features.

Make sure to justify what information you would know at the "time of prediction" and to only train your model using those features (in other words, avoid data leakage).

---

## Special Considerations

### Data Cleaning and Exploratory Data Analysis

**Genre selection:** Select at least 5 genres and justify your choice. Consider how musically distinct they are — projects that compare very similar genres tend to produce less interesting results. Document any decisions about genres that could reasonably be combined or split.

**Data formats and joins:** Some columns require parsing before use. When joining the two files, think carefully about what to join on and how to handle tracks that don't find a match — document your approach.

**Prediction time:** Not every column is a valid input feature for every problem. Before training any model, ask: when would this actually be used, and what information would be available at that moment? Justify each feature you include rather than including a column simply because it exists.

### Assessment of Missingness

Your dataset contains missing values in more than one column. For each column with missing values, determine which mechanism (MCAR, MAR, or NMAR) best describes the missingness and support your conclusion with permutation tests. Choose your test statistic based on the type of column you're testing against.

### Framing a Prediction Problem

Your model will only be evaluated on your chosen genres. Since everyone picks different genres, focus on improvement over your own baseline rather than comparison to classmates. **Choose and justify your evaluation metric**. Explain why it's appropriate for your specific problem, not just what the final number is.
