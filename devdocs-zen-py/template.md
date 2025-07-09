# Zen Python Template - Audio ML Focus

## Task
Build an audio distortion validation system using PANN (Pre-trained Audio Neural Networks) that can:
1. Analyze audio files for various types of distortion
2. Apply controlled distortions for training data
3. Validate distortion detection accuracy

## Config
```yaml
mode: python-ml
framework: pytorch
confidence_min: 75
zen_integration: true
gpu_enabled: true
```

## Agents (ML-Adapted)

### Planner (Data-First)
- Analyzes data requirements
- Plans preprocessing pipeline
- Identifies model architecture
- Estimates compute needs

### Implementer (ML Engineer)
- Writes PyTorch/TensorFlow code
- Implements data loaders
- Builds training loops
- Reports training metrics

### Reviewer (ML Scientist)
- Validates model performance
- Checks for overfitting
- Runs ablation studies
- Simple PASS/RETRY decision

## ML Workflow

### Phase 1: Data Preparation
```python
# Zen pre-analysis
zen analyze . --check "data_leakage,reproducibility"

# Implementation checkpoints
- [ ] Load audio dataset
- [ ] Extract PANN embeddings
- [ ] Apply distortion augmentations
- [ ] Create train/val/test splits

# Confidence factors
✓ PANN pretrained model loaded
✓ Audio preprocessing validated
⚠️ Distortion parameters need tuning
```

### Phase 2: Model Development
```python
# Training with live metrics
Epoch 10/50 ████████░░ Loss: 0.0234
Val F1: 0.89 | Best: 0.91 | Target: 0.95

# Automatic experiments
if confidence < 80:
    try_architectures = ['CNN', 'LSTM', 'Transformer']
    run_hyperparameter_search()
```

### Phase 3: Validation & Integration
```python
# Zen validation
zen analyze model/ --ml-checks
# Checks for:
# - Proper error handling
# - Batch processing capability  
# - Memory efficiency
# - Inference speed
```

## Python-Specific Features

### Data Pipeline Structure
```python
class AudioDistortionPipeline:
    """
    Confidence: MEDIUM (78/100)
    - Core pipeline working ✓
    - PANN integration tested ✓
    - Real-time processing uncertain ⚠️
    """
    
    def __init__(self):
        self.pann = self.load_pann_model()
        self.distortion_detector = None
        
    def process_audio(self, audio_path):
        # Load audio
        audio, sr = librosa.load(audio_path, sr=16000)
        
        # Extract PANN features
        features = self.pann.extract_features(audio)
        
        # Detect distortion
        distortion_type, confidence = self.detect_distortion(features)
        
        return {
            'type': distortion_type,
            'confidence': confidence,
            'details': self.get_distortion_details(audio)
        }
```

### Training Configuration
```python
config = {
    'model': {
        'architecture': 'ResNet18',
        'pretrained': 'PANN',
        'num_classes': 5  # Clean, Clipping, Noise, Compression, Other
    },
    'training': {
        'batch_size': 32,
        'lr': 1e-4,
        'epochs': 50,
        'early_stopping': True
    },
    'audio': {
        'sample_rate': 16000,
        'duration': 10,  # seconds
        'augmentations': ['pitch_shift', 'time_stretch', 'add_noise']
    }
}
```

### Distortion Generation
```python
def apply_distortions(audio, sr):
    """Generate training data with various distortions"""
    distortions = {}
    
    # Clipping distortion
    distortions['clipping'] = np.clip(audio * 10, -1, 1)
    
    # Compression artifacts
    distortions['compression'] = apply_mp3_compression(audio, bitrate=64)
    
    # Background noise
    noise = np.random.normal(0, 0.05, audio.shape)
    distortions['noise'] = audio + noise
    
    # Frequency distortion
    distortions['eq_distortion'] = apply_extreme_eq(audio, sr)
    
    return distortions
```

## Interactive Mode for ML
```bash
agentic> train "distortion detector"
Loading data... [████████░░] 80%
Train samples: 10,000 | Val: 2,000 | Test: 2,000

Starting training...
Epoch 1/50 - Loss: 0.532 - Val F1: 0.72
Confidence: 72% ⚠️ 
Action: Adjusting learning rate

agentic> explain
The confidence dropped because validation F1 
is below target (0.95). The model might be
underfitting. Trying different architectures.

agentic> zen-analyze --ml
Running ML-specific analysis...
Found: Imbalanced dataset (clean:80%, distorted:20%)
Suggestion: Use weighted loss or SMOTE

agentic> continue --apply-suggestions
Applying class weights...
Epoch 10/50 - Loss: 0.123 - Val F1: 0.91
Confidence: 88% ✓
```

## Output Structure
```
output/
├── models/
│   ├── best_model.pth
│   ├── checkpoints/
│   └── model_config.json
├── data/
│   ├── processed_audio/
│   ├── features/
│   └── splits.json
├── notebooks/
│   ├── exploration.ipynb
│   └── final_results.ipynb
├── src/
│   ├── dataset.py
│   ├── model.py
│   ├── train.py
│   └── inference.py
├── tests/
│   └── test_distortion_detection.py
├── requirements.txt
├── confidence.json
└── zen-report.md
```

## Success Criteria
- Model F1 score: ≥0.95 ✓
- Inference time: <100ms per file ✓
- Memory usage: <1GB ✓
- Zen code quality: B+ or higher ✓
- Test coverage: >80% ✓

## ML-Specific Confidence Boosts
```python
# Confidence increases when:
+ Cross-validation shows consistent results (+10)
+ Model generalizes to unseen distortion types (+15)
+ Inference speed meets requirements (+5)
+ Reproducible results across runs (+10)
+ Proper data versioning in place (+5)

# Confidence decreases when:
- Overfitting detected (-15)
- Data leakage found (-20)
- Non-deterministic results (-10)
- Missing error handling (-5)
```

That's it! Pythonic simplicity meets ML power. 🐍🎵