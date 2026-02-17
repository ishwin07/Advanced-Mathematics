# 📘 Assignment–2  
## Learning Probability Density Functions using Data Only (GAN Based)


---

## 📂 Dataset
**India Air Quality Dataset (Kaggle)**  
https://www.kaggle.com/datasets/shrutibhargava94/india-air-quality-data

Feature used:
- **NO₂ concentration (x)**

---

## ⚙️ Methodology

###  Step-1: Non-Linear Transformation

Each value of NO₂ concentration (x) is transformed into a new variable z using:

z = Tr(x) = x + a_r * sin(b_r * x)

where:

a_r = 0.5 × (r mod 7)  
b_r = 0.3 × (r mod 5 + 1)

Here,
- r = University Roll Number
- mod = remainder operator

For this submission:

a_r = 1.0  
b_r = 1.5

---

###  Step-2: PDF Learning using GAN 

No analytical probability density function is assumed.

A **Generative Adversarial Network (GAN)** is trained using only samples of the transformed variable z.

The GAN consists of two neural networks:

#### Generator (G)
- Input: Random noise sampled from N(0,1)
- Output: Synthetic samples resembling z

Architecture:
Noise(1) → Dense(16) → ReLU → Dense(16) → ReLU → Dense(1)

#### Discriminator (D)
- Input: Real or generated samples
- Output: Probability of being real

Architecture:
z(1) → Dense(16) → LeakyReLU → Dense(16) → LeakyReLU → Dense(1) → Sigmoid

Training Objective:
- Discriminator learns to distinguish real vs fake samples.
- Generator learns to fool the discriminator.
- Through adversarial learning, the generator captures the underlying data distribution.

Loss Function:
Binary Cross Entropy (BCE)

Optimizer:
Adam Optimizer

---

###  Step-3: PDF Approximation

After GAN training:

1. Large number of samples are generated using the trained generator.
2. Probability density is estimated using **Kernel Density Estimation (KDE)**.
3. The KDE curve represents the learned probability density function.

---

## 🛠️ Technologies Used

- Python
- Google Colab / Jupyter Notebook
- PyTorch
- NumPy
- Pandas
- Matplotlib
- Scikit-learn (KDE)

---

## ▶️ How to Run

1. Open notebook in Google Colab.
2. Download and load dataset.
3. Perform transformation to obtain z.
4. Train GAN using transformed samples.
5. Generate synthetic samples from generator.
6. Apply KDE to estimate PDF.
7. Plot learned probability density.

---

## 📊 Output

- Learned distribution of transformed variable z
- GAN generated samples
- Estimated Probability Density Function plot

---

## 🔍 Observations

### Mode Coverage
The generator captures major modes of the transformed data distribution, showing successful learning.

### Training Stability
Training stabilizes after multiple epochs as generator and discriminator reach equilibrium.

### Quality of Generated Distribution
Generated samples closely match the real data distribution, indicating effective implicit density learning.

---

## 🧠 Key Insight
GAN does not explicitly compute a mathematical PDF.  
Instead, the generator implicitly models the probability distribution by producing samples that follow the same distribution as the real data.

---

