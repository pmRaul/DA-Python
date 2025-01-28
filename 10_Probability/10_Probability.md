[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pmRaul/DA-Python/blob/main/10_Probability/10_Probability.ipynb) 
[![Interactive Visualization](https://img.shields.io/badge/Plotly-Interactive_Brightgreen)](https://plotly.com/python/)  

# Probability Theory 📊✨: The Language of Uncertainty  

Probability theory is the mathematical framework that allows us to reason about uncertainty - essential for AI systems that operate in real-world environments filled with incomplete information. Let's explore this fascinating world with practical examples, interactive visualizations, and everyday analogies!  

---

## 🌪️ Why Uncertainty Matters in AI?  
Modern AI systems must handle uncertainty in **3 key dimensions**:  

1. **Inherent Randomness** (Chaos Theory in Action):  
   - Quantum mechanics 🎚️, genetic mutations 🧬, or even lottery draws 🎱  
   - Example: Predicting radioactive decay times ⏳ - inherently probabilistic  

2. **Partial Observability** (The Fog of Information):  
   - Self-driving cars 🚗 can't see occluded pedestrians  
   - Stock market prediction 📈 with hidden economic factors  

3. **Modeling Imperfections** (Simplified Reality):  
   - Weather forecasting 🌦️ ignoring microscopic air movements  
   - Chatbots 🤖 using simplified language models  

**Key Insight**: "All models are wrong, but some are useful" - George Box. We use probabilistic models because they're **robust** and **computationally tractable**.  

---

## 🎲 Random Variables: Quantifying Uncertainty  

A **random variable** is a numerical description of uncertain events. Think of it as a "numerical alias" for outcomes.  

### Types with Everyday Examples:  
1. **Discrete** (Countable Outcomes):  
   - $X$: Number of pizza deliveries 🍕 in an hour (0, 1, 2, ...)  
   - $Y$: Roll of a magic: the gathering die 🎲 (1-20)  

2. **Continuous** (Measurable Quantities):  
   - $Z$: Time until your next Zoom call 📅 (any positive real number)  
   - $W$: Battery percentage of your phone 📱 (0-100% continuum)  

```python
# Interactive random variable demo
import numpy as np
import plotly.express as px

# Discrete: Dice rolls
dice_rolls = np.random.randint(1, 21, size=1000)
fig_discrete = px.histogram(dice_rolls, nbins=20, 
                           title="D20 Dice Rolls Distribution 🎲")
fig_discrete.show()

# Continuous: Battery life simulation
battery_life = np.random.normal(loc=8, scale=1.5, size=1000)
fig_cont = px.histogram(battery_life, 
                       title="Smartphone Battery Life 📱 (Hours)")
fig_cont.show()
```

---

## 📈 Probability Distributions Deep Dive  

### Discrete Distributions Cheat Sheet:  

| Distribution | PMF Formula 📝 | Real-World Example 🌍 |
|--------------|----------------|-----------------------|
| Bernoulli | $P(k;p) = p^k(1-p)^{1-k}$ | Coin flip (Heads=1, Tails=0) |
| Binomial | $P(k;n,p) = \binom{n}{k}p^k(1-p)^{n-k}$ | Number of spam emails in 100 messages 🗑️ |
| Poisson | $P(k;\lambda) = \frac{\lambda^k e^{-\lambda}}{k!}$ | Website visits per hour 🌐 |

```python
# Interactive Binomial Distribution Explorer
from scipy.stats import binom
import ipywidgets as widgets
import plotly.graph_objects as go

@widgets.interact(n=(1, 20), p=(0.0, 1.0))
def plot_binomial(n=5, p=0.5):
    x = np.arange(0, n+1)
    pmf = binom.pmf(x, n, p)
    fig = go.Figure([go.Bar(x=x, y=pmf)])
    fig.update_layout(title=f"Binomial(n={n}, p={p})", 
                     xaxis_title="Successes", yaxis_title="Probability")
    fig.show()
```

### Continuous Distributions Showcase:  

**Normal (Gaussian) Distribution** 🌟:  
$$
\mathcal{N}(x; \mu, \sigma^2) = \frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{(x-\mu)^2}{2\sigma^2}}
$$  
- 68-95-99.7 Rule: Memorize this!  
  - $\mu \pm \sigma$ → 68% data  
  - $\mu \pm 2\sigma$ → 95% data  
  - $\mu \pm 3\sigma$ → 99.7% data  

**Exponential Distribution** ⏳:  
$$
f(x;\lambda) = \lambda e^{-\lambda x} \quad (x \geq 0)
$$  
- Models time between events:  
  - Earthquake intervals 🌋  
  - Social media post times 📱  

```python
# Interactive Gaussian Mixture Model
import plotly.graph_objects as go
from scipy.stats import norm

@widgets.interact(mu1=(-5,5), sigma1=(0.1,2), mu2=(-5,5), sigma2=(0.1,2))
def plot_gmm(mu1=0, sigma1=1, mu2=1, sigma2=0.5):
    x = np.linspace(-10, 10, 500)
    y1 = norm.pdf(x, mu1, sigma1)
    y2 = norm.pdf(x, mu2, sigma2)
    
    fig = go.Figure()
    fig.add_trace(go.Scatter(x=x, y=y1, name=f"μ={mu1}, σ={sigma1}"))
    fig.add_trace(go.Scatter(x=x, y=y2, name=f"μ={mu2}, σ={sigma2}"))
    fig.add_trace(go.Scatter(x=x, y=0.5*(y1+y2), name="Mixture"))
    
    fig.update_layout(title="Gaussian Mixture Model (Drag Sliders!)")
    fig.show()
```

---

## ⚖️ Bayes' Theorem: Updating Beliefs with Evidence  

**Bayesian Reasoning** is the mathematical framework for updating probabilities as new data arrives:  

$$
P(A|B) = \frac{P(B|A)P(A)}{P(B)} = \frac{P(B|A)P(A)}{\sum_i P(B|A_i)P(A_i)}
$$  

### Real-World Bayesian Scenario: Spam Detection 🛡️  

Let's calculate the probability an email is spam ($S$) given it contains "FREE" ($F$):  

- **Priors**:  
  - $P(S) = 0.3$ (30% of emails are spam)  
  - $P(F|S) = 0.8$ (80% of spam has "FREE")  
  - $P(F|\neg S) = 0.05$ (5% of non-spam has "FREE")  

**Calculation**:  
$$
P(S|F) = \frac{0.8 \times 0.3}{0.8 \times 0.3 + 0.05 \times 0.7} = \frac{0.24}{0.24 + 0.035} \approx 0.873
$$  

**Interactive Bayesian Calculator**:  
```python
@widgets.interact(
    p_spam=(0.0, 1.0, 0.01), 
    p_free_spam=(0.0, 1.0, 0.01),
    p_free_nonspam=(0.0, 1.0, 0.01)
)
def bayes_calculator(p_spam=0.3, p_free_spam=0.8, p_free_nonspam=0.05):
    numerator = p_free_spam * p_spam
    denominator = numerator + p_free_nonspam * (1 - p_spam)
    p_spam_given_free = numerator / denominator
    print(f"P(Spam | 'FREE') = {p_spam_given_free:.2%}")
```

---

## 🧮 Essential Probability Functions  

### 1. Sigmoid & Friends:  

| Function | Formula | Plot | Use Case |  
|----------|---------|------|----------|  
| Sigmoid | $\sigma(z) = \frac{1}{1+e^{-z}}$ | S-shaped curve 📈 | Logistic regression, neural nets |  
| Tanh | $\tanh(z) = \frac{e^z - e^{-z}}{e^z + e^{-z}}$ | Zero-centered sigmoid | RNN hidden states |  
| ReLU | $\text{ReLU}(z) = \max(0,z)$ | Linear with cutoff | Deep learning hidden layers |  

```python
# Activation Function Comparison
z = np.linspace(-5, 5, 100)
fig = go.Figure()
fig.add_trace(go.Scatter(x=z, y=1/(1+np.exp(-z)), name="Sigmoid"))
fig.add_trace(go.Scatter(x=z, y=np.tanh(z), name="Tanh"))
fig.add_trace(go.Scatter(x=z, y=np.maximum(z,0), name="ReLU"))
fig.update_layout(title="Common Activation Functions 🎛️")
fig.show()
```

### 2. Softmax & Temperature:  

**Standard Softmax**:  
$$
\text{softmax}(z_i) = \frac{e^{z_i}}{\sum_j e^{z_j}}
$$  

**With Temperature $T$**:  
$$
\text{softmax}_T(z_i) = \frac{e^{z_i/T}}{\sum_j e^{z_j/T}}
$$  

```python
@widgets.interact(T=(0.1, 2.0))
def temp_demo(T=1.0):
    z = np.array([1.0, 2.0, 3.0])
    sm = np.exp(z/T) / np.sum(np.exp(z/T))
    print(f"Probs: {sm.round(2)}")
    print(f"Entropy: {(-sm * np.log(sm)).sum():.2f} bits")
```

**Key Insight**: Lower temperature $T$ makes the distribution "sharper" (more confident), while higher $T$ makes it "softer" (more uncertain).  

---

## 🛠️ Exercises: Train Your Probability Muscles  

**Exercise 1: COVID-19 Test Analysis 🦠**  
Given:  
- Disease prevalence: 2%  
- Test sensitivity: 95%  
- Test specificity: 98%  

Calculate:  
1. Probability someone has COVID if they test positive  
2. Probability of being healthy if test negative  

<details>
<summary>Solution</summary>

```python
# Bayes' Theorem Application
prevalence = 0.02
sensitivity = 0.95
specificity = 0.98

# P(Positive|COVID) * P(COVID) + P(Positive|Healthy) * P(Healthy)
p_positive = sensitivity * prevalence + (1 - specificity) * (1 - prevalence)
p_covid_given_positive = (sensitivity * prevalence) / p_positive

# P(Negative|Healthy) * P(Healthy) + P(Negative|COVID) * P(COVID)
p_negative = specificity * (1 - prevalence) + (1 - sensitivity) * prevalence
p_healthy_given_negative = (specificity * (1 - prevalence)) / p_negative

print(f"1. P(COVID|Positive) = {p_covid_given_positive:.2%}")
print(f"2. P(Healthy|Negative) = {p_healthy_given_negative:.2%}")
```
</details>

**Exercise 2: Expected Value in Games 🎮**  
A casino game costs \$5 to play. You roll a die:  
- Roll 6: Win \$20  
- Roll 4-5: Win \$5  
- Roll 1-3: Lose  

Calculate the expected profit. Is the game fair?  

<details>
<summary>Solution</summary>

```python
cost = 5
prob_6 = 1/6
prob_45 = 2/6
prob_123 = 3/6

expected_payout = (20 * prob_6) + (5 * prob_45) + (0 * prob_123)
expected_profit = expected_payout - cost

print(f"Expected profit: ${expected_profit:.2f}")
print("Fair game?" , "Yes" if expected_profit == 0 else "No")
```
</details>

**Exercise 3: Real-World Data Probability 🌍**  
Load the Titanic dataset:  
```python
import seaborn as sns
titanic = sns.load_dataset('titanic')
```  
Calculate:  
1. $P(\text{Survived} | \text{Female})$  
2. $P(\text{First Class} | \text{Survived})$  
3. $P(\text{Age} < 18 | \text{Survived})$  

<details>
<summary>Solution</summary>

```python
# Conditional Probabilities with Pandas
# 1. P(Survived|Female)
p_surv_female = titanic[titanic['sex'] == 'female']['survived'].mean()

# 2. P(First Class|Survived)
survived = titanic[titanic['survived'] == 1]
p_first_survived = survived['pclass'].value_counts(normalize=True)[1]

# 3. P(Age < 18 | Survived)
survived_under18 = survived[survived['age'] < 18].shape[0]
total_survived = survived.shape[0]
p_child_survived = survived_under18 / total_survived

print(f"1. P(Survived|Female) = {p_surv_female:.2%}")
print(f"2. P(First Class|Survived) = {p_first_survived:.2%}")
print(f"3. P(Age < 18|Survived) = {p_child_survived:.2%}")
```
</details>

---

## 📚 Expanded References & Learning Resources  

### Foundational Books:  
1. **"Probability Theory: The Logic of Science"** by E.T. Jaynes 🧠 - Bayesian perspective  
2. **"Introduction to Probability"** by Blitzstein & Hwang 📖 - Harvard's popular textbook  
3. **"Statistical Rethinking"** by Richard McElreath 🐍 - Bayesian stats with PyMC  

### Online Courses:  
- [MIT 6.431x: Probability - The Science of Uncertainty](https://www.edx.org/course/probability-the-science-of-uncertainty) 🎓  
- [3Blue1Brown's Probability Quincunx](https://www.3blue1brown.com/topics/probability) 🌀  

### Python Libraries:  
- `numpyro` for probabilistic programming 🔮  
- `scipy.stats` for 100+ distributions 📊  
- `plotly` for interactive visualizations 📈  

---

🌟 **Probability isn't just math - it's a superpower for rational thinking in an uncertain world!** Keep practicing with real datasets and interactive tools to build intuition. Happy calculating! 🧮✨