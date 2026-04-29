Sleep Apnea Detection Using Multimodal Machine Learning
Automated sleep apnea detection from physiological signals using feature engineering, UMAP visualization, and Random Forest classification. This project combines respiratory effort and SpO₂ oximetry signals from the PhysioNet dataset to demonstrate that multimodal feature fusion substantially outperforms single-modality approaches.
MSBD-570 Final Project · Dyani Peterson

Results at a Glance
ApproachAccuracySensitivityF1 (Apnea)Respiratory Only72%68%0.69Oximetry Only78%75%0.76Multimodal (Combined)91%89%0.90

Project Structure
sleep-apnea-detection/
├── data/
│   └── raw/                  # Place PhysioNet signal files here (not tracked)
├── notebooks/
│   ├── 01_eda.ipynb          # Exploratory data analysis
│   ├── 02_features.ipynb     # Feature engineering walkthrough
│   ├── 03_umap.ipynb         # UMAP visualization
│   └── 04_classification.ipynb  # Model training and evaluation
├── src/
│   ├── loader.py             # PhysioNet data loading and segmentation
│   ├── preprocess.py         # Artifact rejection and normalization
│   ├── features.py           # Feature extraction pipeline
│   ├── visualize.py          # UMAP, heatmap, and importance plots
│   └── classify.py           # Random Forest training and evaluation
├── figures/                  # Output visualizations (auto-generated)
├── requirements.txt
└── README.md

Quickstart
1. Clone and install dependencies
bashgit clone https://github.com/your-username/sleep-apnea-detection.git
cd sleep-apnea-detection
pip install -r requirements.txt
2. Download the data
Data comes from the PhysioNet open repository. Download the relevant dataset and place the signal files in data/raw/. The WFDB toolkit (included in requirements.txt) handles loading.
3. Run the pipeline
bash# Feature extraction
python src/features.py

# Generate visualizations
python src/visualize.py

# Train and evaluate classifier
python src/classify.py
Or run the notebooks in order for a step-by-step walkthrough.

Dependencies
numpy
pandas
scikit-learn
umap-learn
matplotlib
seaborn
wfdb
Install all at once:
bashpip install -r requirements.txt
Python 3.10+ recommended.

Visualizations
The pipeline produces six figures saved to figures/:

UMAP: Condition Type — 2D embedding colored by apnea subtype
UMAP: Pressure Level — embedding colored by CPAP pressure (severity proxy)
UMAP: Apnea vs. Normal — binary class separability
Correlation Heatmap — cross-modality feature correlations
SpO₂ Distribution — oximetry distributions by class
Feature Importance — Random Forest permutation importances


Key Design Decisions
Why Random Forest? Handles high-dimensional feature sets well, provides built-in feature importance, and is robust to overfitting without extensive hyperparameter tuning — important for a clinical setting where interpretability matters.
Why feature-level fusion? Concatenating features from both modalities before classification allows the model to learn cross-modal interactions. Decision-level fusion (training separate models and combining predictions) was tested but consistently underperformed.
Why UMAP over t-SNE? UMAP preserves both local and global manifold structure, making the resulting embeddings more interpretable for assessing class separability across the full feature space.

Reproducibility
All UMAP embeddings use random_state=42. Cross-validation is stratified 5-fold. StandardScaler is fit only on training folds within each split to prevent data leakage.

References

Kovalerchuk, B. (2018). Visual Analytics. Springer. ISBN 978-3-319-73040-0
McInnes, L., Healy, J., & Melville, J. (2018). UMAP: Uniform Manifold Approximation and Projection. arXiv:1802.03426
Goldberger et al. (2000). PhysioBank, PhysioToolkit, and PhysioNet. Circulation, 101(23).
Pedregosa et al. (2011). Scikit-learn: Machine learning in Python. JMLR, 12, 2825–2830.


License
This project is for academic use. Data sourced from PhysioNet is subject to its own usage terms.
