# Music Genre Classification

A deep learning project that classifies music genres using audio features and spectrogram-based inputs.

## Project Structure

- `Music_Genre_App.py` — Streamlit app for interactive predictions.
- `Train_Music_Genre_Classifier.ipynb` — Notebook to train the classifier.
- `Test_Music_Genre.ipynb` — Notebook to evaluate/test the model.
- `ML_Package.ipynb` — Supporting exploration or packaging work.
- `Trained_model.h5` — Trained Keras model (large file).
- `training_hist.json` — Training history.
- `Data/` — Dataset and precomputed features.

## Setup

1. Create a virtual environment (recommended) and install dependencies:

```bash
pip install -r requirements.txt
```

2. (Optional) Use Git LFS for large artifacts like models and audio files:

```bash
git lfs install
git lfs track "*.h5"
```

## Run the Streamlit App

```bash
streamlit run Music_Genre_App.py
```

## Notes

- The current app references absolute paths. You may want to update `load_model()` and image paths in `Music_Genre_App.py` to use relative paths.
- Large raw datasets under `Data/genres_original` and `Data/images_original` are ignored by Git by default.

## Dataset

Uses the GTZAN dataset (10 genres, 100 clips each). Ensure you have rights to use and redistribute any included audio.
