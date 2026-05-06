# dead-heat-analysis
Parimutuel horse racing betting strategy using Monte Carlo simulation, Normal distribution fitting, and Kelly Criterion bet sizing to identify and exploit market inefficiencies across 500 historical races.
# 🐴 Dead Heat — Parimutuel Betting Strategy

> Identifying market inefficiencies in a parimutuel horse racing betting market using statistical modelling, Monte Carlo simulation, and Kelly Criterion bet sizing.

---

## 📌 Project Overview

This project analyses 500 historical horse races to estimate each horse's **true win probability** using distribution fitting and Monte Carlo simulation. These estimates are then compared against the **market-implied probabilities** (pool fractions) to identify positive expected value (EV) bets. Final bet sizes are determined using the **Kelly Criterion**.

The strategy was submitted to a simulated parimutuel betting competition where performance is scored as **average profit per race across 10,000 simulations**.

---

## 🧠 Key Concepts Used

| Concept | Description |
|---|---|
| **Parimutuel Betting** | All bets go into a shared pool; winners split the pool proportionally |
| **Expected Value (EV)** | `EV = p × (0.85 / f) − 1` where `p` = true win prob, `f` = pool fraction |
| **Monte Carlo Simulation** | Simulated 100,000 races by sampling from fitted Normal distributions |
| **Kelly Criterion** | Optimal bet sizing formula to maximise long-run growth |
| **Favourite-Longshot Bias** | Market tendency to overbet underdogs — exploited here |

---

## 📁 Project Structure

```
dead-heat-betting/
│
├── race_data.csv           # 500 historical races with finish times
├── dead_heat_analysis.ipynb  # Full analysis notebook
└── README.md
```

---

## 🔬 Methodology

### Step 1 — Exploratory Data Analysis
- Loaded 500 races with finishing times (in seconds) for 8 horses
- Calculated empirical win rates directly from historical data
- Examined mean and standard deviation of each horse's finishing times

### Step 2 — Distribution Fitting
- Fitted a **Normal distribution** to each horse's finishing times
- Parameters: mean μ and standard deviation σ per horse

### Step 3 — Monte Carlo Simulation
- Simulated **100,000 races** by sampling from each horse's fitted distribution
- Winner = horse with lowest sampled time in each simulation
- Derived stable estimates of true win probability `p_i` for each horse

### Step 4 — Edge Detection
Compared true probabilities against market pool fractions:

| Horse | True P(win) | Market Implied | EV |
|---|---|---|---|
| Shadowfax | 32.4% | 8.0% | **+2.44** ✅ |
| Morningstar | 32.1% | 11.0% | **+1.48** ✅ |
| Iron Duke | 13.8% | 9.0% | **+0.31** ✅ |
| Red Tide | 6.9% | 13.0% | −0.55 ❌ |
| Gallant Fox | 5.6% | 14.0% | −0.66 ❌ |
| Blue Streak | 4.1% | 15.0% | −0.77 ❌ |
| Copper Prince | 2.8% | 14.0% | −0.83 ❌ |
| Last Chance | 2.3% | 16.0% | −0.88 ❌ |

**Finding:** The market severely overestimates the bottom 5 horses and underestimates the top 3 — a classic reverse favourite-longshot bias.

### Step 5 — Kelly Criterion Bet Sizing
Used **quarter-Kelly** (25% of full Kelly) to account for model uncertainty:

```
Kelly fraction = (p × b − (1 − p)) / b
where b = net odds = 0.85 / f − 1
```

| Horse | Stake (£) |
|---|---|
| Shadowfax | £634 |
| Morningstar | £549 |
| Iron Duke | £90 |
| All others | £0 |
| **Total** | **£1,273** |

---

## 📊 Results

- Only bet on horses with **positive EV**
- Conservative quarter-Kelly sizing protects against variance
- Total stake: ~£1,273 out of £10,000 bankroll
- Expected positive average profit per race based on the identified edges

---

## 🛠️ Tech Stack

- **Python 3**
- **Pandas** — data loading and manipulation
- **NumPy** — numerical computation and simulation
- **SciPy** — distribution fitting
- **Matplotlib / Seaborn** — visualisation
- **Jupyter Notebook** — interactive analysis environment

---

## 🚀 How to Run

```bash
# Clone the repo
git clone https://github.com/yourusername/dead-heat-betting.git
cd dead-heat-betting

# Install dependencies
pip install pandas numpy scipy matplotlib seaborn jupyter

# Launch the notebook
jupyter notebook dead_heat_analysis.ipynb
```

---

## 📚 Background Reading

- [Parimutuel Betting — Wikipedia](https://en.wikipedia.org/wiki/Parimutuel_betting)
- [Kelly Criterion — Wikipedia](https://en.wikipedia.org/wiki/Kelly_criterion)
- [Favourite-Longshot Bias — Wikipedia](https://en.wikipedia.org/wiki/Favourite-longshot_bias)

---

## 👤 Author

**Your Name**
[LinkedIn](https://linkedin.com/in/yourprofile) · [GitHub](https://github.com/yourusername)
