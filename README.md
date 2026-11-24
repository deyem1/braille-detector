# Braille Detector 👆📖

Detects Braille in a photo or live camera feed, transcribes each character to text and reads it aloud. It was built to make printed Braille more accessible to sighted carers, teachers and family members of visually impaired people.

> Group project for the Artificial Intelligence module, MSc AI & Data Science, Keele University.

## How it works

```
image / webcam frame
        │
        ▼
┌───────────────────┐   bounding box   ┌──────────────────────┐   characters   ┌────────────┐
│ Detection model   │ ───────────────▶ │ Transcription model  │ ─────────────▶ │ Text + TTS │
│ (VGG16, transfer) │                  │ (CNN, per character) │                │  (gTTS)    │
└───────────────────┘                  └──────────────────────┘                └────────────┘
```

1. **Detection:** a VGG16-based model (transfer learning) finds the Braille region in the image.
2. **Transcription:** a sequential CNN classifies each Braille cell into a letter.
3. **Output:** the text is shown in a Streamlit web app and spoken with gTTS.

## Run it

```bash
git clone https://github.com/deyem1/braille-detector.git
cd braille-detector
pip install -r requirements.txt

# Web app
streamlit run main.py

# Live webcam tracker
python "live tracker.py"   # if no camera opens, change cv2.VideoCapture(0) to 1 or 2
```

The trained model `brailledetect2.h5` must sit in the project folder.

## Project structure

| File | Purpose |
|---|---|
| `main.py` | Streamlit web app |
| `live tracker.py` | Real-time detection from a webcam |
| `Brai Detection - Copy.ipynb` | Detection model training (VGG16) |
| `Braille-character-transcription-cnn.ipynb` | Character classifier training |
| `brailledetect*.h5` | Trained model weights |

## Data

- **Detection:** augmented Braille images ([Google Drive](https://drive.google.com/drive/folders/1vHuEg5pr3S8fvYu0RCi27C4NsFPrMV-x?usp=sharing)), partly from the [Angelina Braille Images Dataset](https://github.com/IlyaOvodov/AngelinaDataset)
- **Transcription:** [Braille Character Dataset](https://www.kaggle.com/datasets/shanks0465/braille-character-dataset) (Kaggle)

## Credits

The detection architecture was inspired by [nicknochnack/FaceDetection](https://github.com/nicknochnack/FaceDetection), and the classifier by [this Kaggle notebook](https://www.kaggle.com/code/amanrosekaursethi/braille-character-detection-using-cnn).

## Possible next steps

- Transcribe whole lines and words, not just single characters
- Export to TensorFlow Lite for on-device use on a phone
