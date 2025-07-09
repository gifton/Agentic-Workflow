# Audio Distortion Validator - Task Context

## Task Overview
Build a machine learning system that can detect and classify audio distortions using PANN (Pre-trained Audio Neural Networks) embeddings. The system should handle real-world audio quality issues in music production and streaming applications.

## Technical Requirements

### Core Functionality
1. **Distortion Detection**: Identify if audio contains distortion
2. **Distortion Classification**: Categorize type (clipping, compression, noise, etc.)
3. **Severity Assessment**: Rate distortion level (0-100%)
4. **Real-time Processing**: <100ms inference per 10-second audio clip

### Supported Distortion Types
- **Clipping**: Amplitude exceeds maximum (harsh distortion)
- **MP3 Artifacts**: Low-bitrate compression artifacts  
- **Background Noise**: Environmental/electronic noise
- **Frequency Distortion**: EQ imbalances, missing frequencies
- **Phase Issues**: Stereo image problems, cancellations

## Implementation Phases

### Phase 1: Data Pipeline (Day 1)
```python
# Key deliverables
- Audio dataset loader with augmentation
- PANN feature extractor integration
- Distortion synthesis functions
- Train/val/test split creator
```

### Phase 2: Model Development (Day 2-3)
```python
# Key deliverables  
- Distortion classifier (PANN → MLP/CNN)
- Multi-task learning for type + severity
- Training pipeline with W&B logging
- Model checkpointing system
```

### Phase 3: Evaluation & Deployment (Day 4)
```python
# Key deliverables
- Comprehensive test suite
- Performance benchmarks
- Inference optimization
- API endpoint wrapper
```

## Dataset Specifications

### Training Data
```yaml
clean_audio:
  source: "MusicNet, FMA-small"
  count: 10000 samples
  duration: 10 seconds each
  format: "WAV 16kHz mono"

distortion_augmentation:
  clipping_levels: [5%, 10%, 20%, 40%]
  compression_bitrates: [64, 96, 128] kbps
  noise_snr: [20, 10, 5, 0] dB
  eq_curves: ["telephone", "underwater", "tinny"]
```

### Validation Strategy
- 70% train, 15% validation, 15% test
- Stratified by distortion type
- Include real-world distorted samples
- Cross-validation for robustness

## Technical Stack

```python
dependencies = {
    # Core
    'numpy>=1.21.0',
    'pandas>=1.3.0',
    
    # Audio
    'librosa>=0.9.0',
    'soundfile>=0.10.0',
    'pydub>=0.25.0',
    
    # ML
    'torch>=1.10.0',
    'torchaudio>=0.10.0',
    'timm>=0.5.0',  # For PANN models
    
    # Evaluation
    'scikit-learn>=1.0.0',
    'wandb>=0.12.0',
    'pesq>=0.0.3',  # Audio quality metrics
    
    # Deployment
    'fastapi>=0.70.0',
    'uvicorn>=0.15.0'
}
```

## Model Architecture

```python
class DistortionValidator(nn.Module):
    def __init__(self):
        super().__init__()
        # PANN feature extractor (frozen)
        self.pann = load_pretrained_pann()
        self.pann.eval()
        
        # Distortion classifier head
        self.classifier = nn.Sequential(
            nn.Linear(2048, 512),  # PANN embedding size
            nn.ReLU(),
            nn.Dropout(0.3),
            nn.Linear(512, 128),
            nn.ReLU(),
            nn.Dropout(0.3),
            nn.Linear(128, 6)  # 5 distortion types + clean
        )
        
        # Severity regressor head  
        self.severity = nn.Sequential(
            nn.Linear(2048, 256),
            nn.ReLU(),
            nn.Linear(256, 1),
            nn.Sigmoid()  # 0-1 severity score
        )
```

## Evaluation Metrics

### Primary Metrics
- **F1 Score**: ≥0.95 for binary detection
- **Macro F1**: ≥0.90 for multi-class
- **MAE**: ≤5% for severity prediction

### Secondary Metrics  
- **Inference Speed**: <100ms per sample
- **Memory Usage**: <500MB model size
- **CPU Compatibility**: Must run without GPU

## Example Usage

```python
# Initialize validator
validator = AudioDistortionValidator()
validator.load_checkpoint('best_model.pth')

# Process audio file
result = validator.analyze('song.mp3')
print(f"Distortion detected: {result['has_distortion']}")
print(f"Type: {result['distortion_type']}")
print(f"Severity: {result['severity']:.1%}")
print(f"Confidence: {result['confidence']:.1%}")

# Batch processing
results = validator.analyze_batch(['song1.mp3', 'song2.wav'])
```

## Zen Integration Points

1. **Pre-task**: Analyze codebase for ML best practices
2. **During training**: Monitor for common ML pitfalls
3. **Post-implementation**: Validate model robustness
4. **Deployment**: Check API security and performance

## Success Criteria

- [ ] All distortion types detected with >90% accuracy
- [ ] Real-time processing achieved (<100ms)
- [ ] Model size under 50MB
- [ ] Comprehensive test coverage (>80%)
- [ ] Clean, documented, zen-approved code
- [ ] Reproducible training pipeline

## Notes

- PANN provides robust audio embeddings but may need fine-tuning
- Consider ensemble methods if single model underperforms
- Real-world audio often has multiple simultaneous distortions
- Ensure model works across different music genres