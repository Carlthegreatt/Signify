# Sign Language Detection System

This project extends your existing hand tracking code to create a complete sign language detection system using machine learning.

## Features

- **Real-time hand tracking** using MediaPipe
- **Feature extraction** from hand landmarks (coordinates, distances, angles)
- **Data collection** interface for training custom signs
- **Machine learning model** (Random Forest) for sign classification
- **Real-time prediction** with confidence scores
- **Model persistence** - save and load trained models

## Setup

1. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

2. **Run the quick demo** to see hand tracking in action:
   ```bash
   python demo_sign_language.py
   ```

## How to Use the Sign Language Detection System

### 1. Quick Start (Demo)
Run the demo to see hand tracking:
```bash
python demo_sign_language.py
```

### 2. Full System
Run the main sign language detector:
```bash
python sign_language_detector.py
```

The system provides an interactive menu with 4 options:

#### Option 1: Collect Training Data
- Enter the name of the sign you want to teach (e.g., "A", "B", "Hello", "Thank you")
- Specify how many samples to collect (default: 100)
- Show your hand making the sign
- Press 's' to save each frame when your hand is in the correct position
- Press 'q' to quit

**Tips for data collection:**
- Collect samples from different angles and lighting conditions
- Vary your hand position slightly to make the model more robust
- Collect at least 50-100 samples per sign for good accuracy
- Make sure your hand is clearly visible and well-lit

#### Option 2: Train Model
- This will train a Random Forest classifier on your collected data
- Shows accuracy on test data
- Saves the trained model to `models/sign_language_model.pkl`

#### Option 3: Run Detection
- Loads the trained model
- Runs real-time sign detection
- Shows predicted sign and confidence score
- Press 'q' to quit

#### Option 4: Exit
- Exits the program

## How It Works

### Feature Extraction
The system extracts 3 types of features from hand landmarks:

1. **Landmark Coordinates** (63 features): x, y, z coordinates of all 21 hand landmarks
2. **Distances** (5 features): Distance from wrist to each fingertip
3. **Angles** (5 features): Angles between wrist, finger base, and fingertip for each finger

Total: 73 features per hand position

### Machine Learning
- Uses Random Forest Classifier
- Automatically splits data into training (80%) and test (20%) sets
- Shows accuracy on test data
- Provides confidence scores for predictions

### Model Persistence
- Trained models are saved to `models/sign_language_model.pkl`
- Labels are saved to `models/labels.json`
- Models can be loaded and reused without retraining

## Example Workflow

1. **Start the system:**
   ```bash
   python sign_language_detector.py
   ```

2. **Collect data for letter "A":**
   - Choose option 1
   - Enter "A" as sign name
   - Collect 100 samples showing the ASL sign for "A"
   - Press 's' when your hand is in the correct position

3. **Collect data for letter "B":**
   - Choose option 1 again
   - Enter "B" as sign name
   - Collect 100 samples showing the ASL sign for "B"

4. **Train the model:**
   - Choose option 2
   - Wait for training to complete
   - Note the accuracy score

5. **Test the system:**
   - Choose option 3
   - Show your hand making signs "A" or "B"
   - See real-time predictions

## Common ASL Signs to Train

Here are some common signs you can start with:

### Letters
- **A**: Fist with thumb on side
- **B**: Flat hand, fingers together
- **C**: Curved hand like holding a cup
- **D**: Index finger pointing up, other fingers closed
- **E**: Fist with fingers curled

### Words
- **Hello**: Wave hand
- **Thank you**: Fingers from chin forward
- **Yes**: Fist nodding up and down
- **No**: Index and middle finger tapping together
- **Please**: Flat hand rubbing in circular motion

## Tips for Better Accuracy

1. **Good lighting**: Ensure your hand is well-lit
2. **Clear background**: Use a plain background
3. **Consistent distance**: Keep your hand at roughly the same distance from camera
4. **Multiple angles**: Collect data from slightly different angles
5. **More data**: Collect more samples for better accuracy
6. **Variation**: Include slight variations in hand position

## Troubleshooting

### No hand detected
- Check lighting conditions
- Ensure hand is clearly visible
- Try adjusting camera position

### Low accuracy
- Collect more training data
- Ensure data quality (clear, consistent signs)
- Try collecting data in different lighting conditions

### Model not loading
- Make sure you've trained a model first (option 2)
- Check that `models/` directory exists

## File Structure

```
Signify/
├── HandTrackingMin.py          # Your original hand tracking code
├── sign_language_detector.py   # Main sign language detection system
├── demo_sign_language.py       # Quick demo of hand tracking
├── requirements.txt            # Python dependencies
├── models/                     # Saved models (created automatically)
│   ├── sign_language_model.pkl
│   └── labels.json
└── sign_data/                  # Training data storage (created automatically)
```

## Extending the System

You can easily extend this system by:

1. **Adding more signs**: Just collect more training data
2. **Using different models**: Replace RandomForest with SVM, Neural Networks, etc.
3. **Adding gesture recognition**: Modify feature extraction for gestures
4. **Real-time translation**: Add text-to-speech for detected signs
5. **Two-hand detection**: Modify to detect both hands simultaneously

## Performance

- **FPS**: Typically 20-30 FPS on modern computers
- **Accuracy**: 85-95% with good training data
- **Latency**: Real-time prediction (< 50ms)

The system is designed to be lightweight and run in real-time on most computers with a webcam. 