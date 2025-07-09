# Agentic Workflow - Example: ML Pipeline (with enhancements)

*Using: "agentic natural with checkpoints and metrics tracking"*

## Task: Build ML pipeline for customer churn prediction

Create an end-to-end pipeline that ingests customer data, trains a model, and serves predictions via API.

---

## Plan 
*Time: 15 minutes*

**Break down the task:**
- [x] Step 1: Data ingestion and validation
- [x] Step 2: Feature engineering pipeline
- [x] Step 3: Model training with hyperparameter tuning
- [x] Step 4: Model evaluation and selection
- [x] Step 5: API deployment with monitoring

**Identify risks:**
- [x] Main technical risk: Data quality and drift
- [x] Main complexity: Feature engineering choices
- [x] Key dependency: Scikit-learn, FastAPI

**Initial confidence:** 70/100

*Why this confidence level?* ML projects have inherent uncertainty, depends heavily on data quality

---

## 🔖 Checkpoint: Plan Approved
- Timestamp: 2024-01-10 10:30 AM
- Reviewer: Team Lead
- Notes: Good breakdown, add data privacy considerations

---

## Build
*Time: 2 days*

### Step 1: Data ingestion and validation
- [x] Implemented
- [x] Self-tested
- [x] Issues noted: 5% missing values in key features
- **Step confidence:** 85/100

**Metrics:**
- Records processed: 50,000
- Invalid records: 243 (0.5%)
- Processing time: 4.2 seconds

### Step 2: Feature engineering pipeline
- [x] Implemented
- [x] Self-tested
- [x] Issues noted: Created 47 features, some highly correlated
- **Step confidence:** 75/100

**Metrics:**
- Features created: 47
- Correlation > 0.9: 6 pairs
- Missing value imputation: Mean for numeric, mode for categorical

---

## 🔖 Checkpoint: Features Validated
- Timestamp: 2024-01-10 2:45 PM
- State saved: features_v1.pkl
- Rollback command: `git checkout checkpoint-features`

---

### Step 3: Model training with hyperparameter tuning
- [x] Implemented
- [x] Self-tested
- [x] Issues noted: Random Forest performs best
- **Step confidence:** 80/100

**Metrics:**
- Models tested: 4 (LogReg, RF, XGB, SVM)
- Best CV score: 0.847 (Random Forest)
- Training time: 12 minutes
- Hyperparameter trials: 50

### Step 4: Model evaluation and selection
- [x] Implemented
- [x] Self-tested
- [x] Issues noted: Slight class imbalance affecting recall
- **Step confidence:** 82/100

**Metrics:**
- Test accuracy: 0.834
- Precision: 0.791
- Recall: 0.743
- F1-score: 0.766
- AUC-ROC: 0.881

### Step 5: API deployment with monitoring
- [x] Implemented
- [x] Self-tested
- [x] Issues noted: Need to add rate limiting
- **Step confidence:** 78/100

**Metrics:**
- Endpoint latency: p50=23ms, p95=67ms, p99=125ms
- Memory usage: 512MB
- CPU usage: 15% average

**Overall build confidence:** 80/100

---

## 🔖 Checkpoint: Model Deployed
- Timestamp: 2024-01-11 4:30 PM
- Model version: v1.0.0
- API endpoint: /api/v1/predict
- Rollback: `kubectl rollout undo deployment/churn-model`

---

## Review
*Time: 30 minutes*

**Functionality Check:**
- [x] All requirements met?
- [x] Core functionality works?
- [x] Edge cases handled?
- [x] Tests passing?

**Quality Check:**
- [x] Code is clean and readable?
- [x] Follows ML best practices?
- [x] No data leakage?
- [x] Performance acceptable?

**Model Quality:**
- [x] Metrics meet business requirements?
- [x] No obvious bias issues?
- [x] Generalizes well to test set?
- [x] Interpretability documented?

**Issues Found:**
1. Need rate limiting on API
2. Should add model drift monitoring
3. Consider addressing class imbalance

**Final confidence:** 81/100

---

## Decision

✅ **Ready to ship!** (81/100)

Solid v1 model meeting business requirements. Issues identified are improvements for v2.

**Next action:** Deploy to production with monitoring, plan v2 improvements

---

## Performance Tracking

### Model Performance Over Time
- Day 1: F1=0.766, Requests=1,250
- Day 2: F1=0.764, Requests=4,820
- Day 3: F1=0.761, Requests=5,103
- Week 1 Average: F1=0.763, Total Requests=28,450

### System Performance
- Uptime: 99.9%
- Average latency: 31ms
- Error rate: 0.02%