========================================================
Dataset: Cats vs Dogs (Kaggle)
Classes : 2 (cats, dogs)
Original size: ~12,500 images per class (25,000 total)
========================================================

──────────────────────────────────────────────────────
2. KEY FINDINGS FROM EDA (Exploratory Data Analysis)
──────────────────────────────────────────────────────
- The dataset is nearly balanced: ~12,500 cats and ~12,500 dogs.
  
- Some images were corrupted

- Both classes had an equal number of images for fair training after undersampling.

──────────────────────────────────────────────────────
3. DATA AUGMENTATION DECISIONS
──────────────────────────────────────────────────────
Applied only to TRAINING data (not validation or test).

- horizontal_flip   = True    → mirror images left-right
- rotation_range    = 20°     → rotate up to 20 degrees
- zoom_range        = 15%     → randomly zoom in or out
- width_shift_range = 10%     → shift image sideways
- height_shift_range= 10%     → shift image up or down


──────────────────────────────────────────────────────
4. MODEL ARCHITECTURES
──────────────────────────────────────────────────────

MODEL 1: FNN (Feedforward Neural Network)
  - Flatten → Dense(256, ReLU) → Dropout(0.4)
           → Dense(128, ReLU)  → Dropout(0.3)
           → Dense(1, Sigmoid)

MODEL 2: Basic CNN (Convolutional Neural Network)
  - Conv2D(32) → MaxPool → Conv2D(64) → MaxPool
  - Flatten → Dense(128) → Dense(1, Sigmoid)

MODEL 3: Deep CNN with Dropout + Batch Normalisation
  - Conv2D(32) → BatchNorm → MaxPool
  - Conv2D(64) → BatchNorm → MaxPool
  - Conv2D(128)→ BatchNorm → MaxPool
  - Flatten → Dense(256) → Dropout(0.5)
           → Dense(128)  → Dropout(0.3)
           → Dense(1, Sigmoid)

──────────────────────────────────────────────────────
5. BEST MODEL AND WHY
──────────────────────────────────────────────────────
Expected best model: Deep CNN

Reasons:
1. More convolutional layers → can detect complex patterns
2. Batch Normalisation keeps internal values stable,
3. Dropout (50% + 30%) strongly prevents overfitting,
   which is critical when dealing with natural images.
4. The FNN is weakest because it ignores spatial structure —
5. The Basic CNN improves on FNN but lacks regularisation,
   

========================================================