# Zen-Python Agentic Workflow

A streamlined, Python-focused version of the Agentic Loop for ML/Audio processing tasks with zen-mcp integration.

## Philosophy
"Pythonic simplicity with ML power" - Optimized for data science and audio processing workflows.

## Quick Start

```bash
# One-line setup
echo "mode: python-ml\nzen: auto" > .agentic

# Run audio analysis task
agentic run "build distortion validator" --zen
```

## Core Features (Python-Focused)

### 1. Simple Confidence Score
```python
confidence = 75  # 0-100
reason = "Model accuracy validated but edge cases uncertain"
action = "Run additional audio samples" if confidence < 80 else "Deploy"
```

### 2. ML-Aware Checkpoints
- Model state preservation
- Dataset versioning
- Experiment tracking
- Simple pickle/joblib format

### 3. Zen Integration for Python
```python
# Automatic code quality analysis
def enhance_confidence(code):
    zen_report = zen.analyze(code, lang="python")
    if zen_report.quality == "A" and zen_report.ml_best_practices:
        return confidence + 15
    return confidence
```

### 4. Visual Progress with ML Metrics
```
Task: Audio Distortion Validator
█████████░░░░░░ 65% [🔊 Processing audio batch 130/200]

P: ✓ Data prep (100%)
I: ⚠ Model training (65%) - Loss: 0.0234
R: ○ Validation (0%)

Current: F1=0.89 | Target: F1=0.95
```

## Python-Specific Enhancements

### Interactive Notebook Mode
```python
# Jupyter integration
agentic.notebook_mode()
# Shows progress in cell outputs
# Preserves experiment history
```

### ML Pipeline Integration
```yaml
pipelines:
  audio_analysis:
    - zen: "analyze --ml-patterns"
    - prep: "load and preprocess audio"
    - train: "with wandb tracking"
    - zen: "verify model quality"
```

### Package Management
```python
# Auto-detects and manages dependencies
requirements = {
    'core': ['numpy', 'pandas', 'librosa'],
    'ml': ['torch', 'torchaudio'],
    'audio': ['pydub', 'soundfile'],
    'analysis': ['mir_eval', 'pesq']
}
```

## Audio ML Example Structure

### Task: Distortion Validation System
```
Phase 1: Data Preparation
- Load clean audio samples
- Apply various distortions
- Extract PANN features

Phase 2: Model Development  
- Train distortion classifier
- Validate on test set
- Optimize thresholds

Phase 3: System Integration
- Build inference pipeline
- Add real-time processing
- Create evaluation metrics
```

## Simplified Configuration

```yaml
# .agentic (complete config for Python ML)
mode: python-ml
confidence:
  min: 75
  auto_help: true

ml:
  framework: pytorch
  tracking: wandb
  gpu: auto

audio:
  sample_rate: 16000
  format: wav
  
zen:
  pre_analyze: true
  check_ml_patterns: true
```

## Python Agent Adaptations

### Planner (Pythonic)
- Analyzes Jupyter notebooks
- Understands pip/conda environments
- Plans data pipeline stages
- Considers GPU availability

### Implementer (ML-Focused)
- Writes clean sklearn/torch code
- Implements proper train/val/test splits
- Adds appropriate metrics
- Documents hyperparameters

### Reviewer (Data-Aware)
- Checks for data leakage
- Validates model metrics
- Reviews computational efficiency
- Ensures reproducibility

## Benefits for Python/ML Workflows

1. **Notebook-Friendly**: Works seamlessly with Jupyter
2. **Experiment Tracking**: Integrated with MLflow/W&B
3. **Data-Aware**: Understands datasets and splits
4. **GPU-Optimized**: Automatic device management
5. **Package Smart**: Handles complex dependencies

## Getting Started with Audio ML

1. Install: `pip install agentic-zen[audio]`
2. Configure: `echo "mode: python-ml" > .agentic`
3. Run: `agentic run "build PANN distortion validator"`

The system handles the ML complexity while maintaining zen simplicity!