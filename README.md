### What is Kannada MNIST?

The standard MNIST dataset is a famous collection of handwritten digits from 0 to 9 using standard Western Arabic numerals. **Kannada MNIST** uses the exact same concept, but with handwritten digits from the **Kannada script** (a language spoken predominantly in southwestern India). It consists of grayscale images that are $28 \times 28$ pixels in size.

### Why do we need PCA?

Each image is made up of $28 \times 28 = 784$ individual pixels. In machine learning, each pixel is treated as a separate feature, meaning your models have to analyze a **784-dimensional space**. This is highly resource-intensive and contains a lot of redundant information (like blank background pixels).

**Principal Component Analysis (PCA)** acts like an ultra-smart compression algorithm. It looks at the dataset and finds a brand-new set of coordinates (called Principal Components) that capture the absolute maximum amount of variation/patterns in the data.

* By asking PCA for **10 components**, you are compressing 784 pixels down to just 10 essential values that best summarize the unique features of that handwritten digit.

---

## 2. Step-by-Step Project Workflow

The project processes the data in a linear, structured pipeline:

### Step 1: Data Gathering & Reshaping

* **Loading:** The raw data is read from your individual files (`xtrain`, `ytrain`, etc.).


* **Flattening:** The grid-like images ($28 \times 28$) are unwrapped into a single flat line of 784 pixels.


* **Normalization:** The pixel values (which originally range from 0 to 255 for darkness) are scaled down to a strict range between 0 and 1. This prevents massive numbers from over-complicating the math later on.

### Step 2: The Dimensionality Loop (The Core Experiment)

The assignment asks you to test how much data compression affects model accuracy. The workflow sets up a loop to test five different compression levels: **10, 15, 20, 25, and 30 components**.

For each level:

1. **Train the PCA:** The algorithm learns the underlying patterns *only* from the training dataset.
2. **Transform:** Both the training images and testing images are compressed into the smaller size (e.g., changing them from 784 features down to 10 features).

### Step 3: Multi-Model Evaluation

Once the data is compressed for a given run, it is simultaneously fed into 5 different algorithms:

* **Decision Tree:** Makes a chain of "if/then" rules to classify the digits.


* **Random Forest:** An ensemble of many different decision trees that vote on the final digit.


* **Naive Bayes:** Uses probability mathematics to guess the digit based on pixel combinations.


* **K-Nearest Neighbors (K-NN):** Compares a test image to its closest neighbors in the data space to see what digit they are.


* **Support Vector Machine (SVM):** Draws complex, mathematical boundary lines to cleanly separate the 10 digit classes from each other.



### Step 4: Performance Telemetry

For every single model, at every single compression level, the pipeline calculates three core validation metrics:

* **Precision, Recall, & F1-Score:** These tell you exactly how accurate the model is, how many digits it missed, and the balanced score between the two.


* **Confusion Matrix:** A grid layout showing exactly which numbers are confusing the model (e.g., if it frequently mistakes a `3` for an `8`).


* **ROC-AUC Curve:** A graph showing how confident the model is when separating a specific digit from all other numbers.



---

## 3. The Big Picture Goal

By looking at the final comparison table, you are trying to find the **sweet spot**.

If you use too few components (like 10), the models will run incredibly fast, but they might miss subtle curves in the handwritten script. If you use more components (like 30), the models get access to richer details and will likely achieve much higher accuracy, but they will take slightly more computational time and power to train.
