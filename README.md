# Music Genre Classification

Classify music into genres using a deep learning model trained on spectrogram-based features. This repo includes training notebooks, a ready-to-use trained model, and a Streamlit app for interactive predictions.

## Highlights

- 10-class genre prediction: blues, classical, country, disco, hiphop, jazz, metal, pop, reggae, rock
- Streamlit web app for quick inference on your own audio files
- Notebooks for training and evaluating the model
- Large artifacts handled via Git LFS (e.g., `.h5` model)

## Repository structure

```
.
├── Music_Genre_App.py                 # Streamlit app for inference
├── Train_Music_Genre_Classifier.ipynb # Train the classifier
├── Test_Music_Genre.ipynb             # Evaluate/test the model
├── ML_Package.ipynb                   # Additional exploration/packaging
├── Trained_model.h5                   # Trained Keras model (tracked via Git LFS)
├── training_hist.json                 # Training history (loss/accuracy over epochs)
├── Data/
│   ├── features_3_sec.csv             # Precomputed features (3s chunks)
│   ├── features_30_sec.csv            # Precomputed features (30s tracks)
│   ├── genres_original/               # GTZAN audio (ignored by Git)
│   └── images_original/               # Spectrogram images (ignored by Git)
└── Test_Music/                        # Sample audio files for quick tests
```

## Requirements

- Python 3.9+ (3.10 recommended)
- pip

Python packages (see `requirements.txt`):

- streamlit, tensorflow, numpy, librosa, matplotlib, soundfile

## Quick start

Create and activate a virtual environment, then install dependencies.

Windows PowerShell:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -U pip
pip install -r requirements.txt
```

macOS/Linux (bash):

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -U pip
pip install -r requirements.txt
```

If you plan to commit or download large files (like the model), install and enable Git LFS:

```bash
git lfs install
```

## Run the Streamlit app

Start the web app and open the provided local URL.

```bash
streamlit run Music_Genre_App.py
```

In the app:

- Go to “Prediction”, upload an MP3/WAV, optionally play it, then click “Predict”.
- The predicted genre will be shown based on the majority vote over chunked spectrograms.

### Note on model path

The app’s `load_model()` may reference an absolute path. For portability, change it to a relative path, e.g.:

```python
def load_model():
	model = tf.keras.models.load_model("./Trained_model.h5")
	return model
```

## Training and evaluation

This repo provides notebooks to train and evaluate the classifier.

1. Training — `Train_Music_Genre_Classifier.ipynb`

- Ensure the GTZAN dataset (or your dataset) is available under `Data/genres_original/`.
- Run the notebook cells to preprocess features, train the model, and save outputs.
- Artifacts produced include `Trained_model.h5` and `training_hist.json`.

2. Evaluation — `Test_Music_Genre.ipynb`

- Load the trained model and run evaluation on validation/test sets or sample files.
- You can also visualize training curves by loading `training_hist.json`.

## Dataset

The project is designed around the GTZAN dataset (10 genres, 100 clips each). Place audio files under `Data/genres_original/` using the standard folder-per-genre structure. Make sure you have the right to use and redistribute any audio contained in this repository.

Classes used by the model:

```
['blues', 'classical', 'country', 'disco', 'hiphop', 'jazz', 'metal', 'pop', 'reggae', 'rock']
```

## How it works (overview)

- Audio is split into overlapping chunks.
- Each chunk is converted to a Mel spectrogram and resized for the model.
- The TensorFlow/Keras model predicts classes for chunks; a majority vote yields the final genre.

## Tips and troubleshooting

- TensorFlow install on Windows can be sensitive to Python/CPU/GPU versions. Use a fresh virtual environment and the recommended Python versions.
- If MP3 loading fails with librosa, install FFmpeg and ensure it’s on your PATH.
- Large raw data (`Data/genres_original/`, `Data/images_original/`) is excluded via `.gitignore`.
- The model file `Trained_model.h5` is tracked via Git LFS to avoid hitting GitHub file-size limits.

## Contributing

Issues and pull requests are welcome. If proposing major changes, please open an issue first to discuss what you’d like to change.

## License

Add a license (e.g., MIT, Apache-2.0) to clarify usage and redistribution rights. If you add a `LICENSE` file, reference it here.
