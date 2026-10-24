# LeakageLab

**Independent experimental ML research project** investigating how feature-selection leakage can affect machine-learning evaluation.

## Research question
How does fitting feature selection before the train/test split affect test accuracy, and how does candidate-feature count influence the observed effect?

## Key recorded results

### Synthetic experiments
| Candidate features | Correct mean accuracy | Leaky mean accuracy | Gap (percentage points) |
|---:|---:|---:|---:|
| 20 | 49.5% | 53.1% | 3.587 |
| 100 | 51.4% | 59.0% | 7.667 |
| 500 | 50.2% | 62.9% | 12.667 |

### Real dataset
- Breast Cancer Wisconsin Diagnostic: 569 observations, 30 features
- Five features selected; 50 repeated stratified train/test splits
- Correct mean accuracy: 93.1%; leaky mean accuracy: 93.5%
- Mean difference: 0.363 percentage points; median: 0.0
- Standard deviation of paired differences: 1.082 percentage points
- Leaky higher / equal / lower: 6 / 44 / 0

These are the values observed in the initial project run. Re-running the notebook may produce slightly different values. Use fresh output when reporting a new run.

## Method
**Correct:** split first, fit feature selection only on training data, train, and evaluate on held-out data.

**Leaky (demonstration only):** fit feature selection using all rows and labels before splitting. Test labels then influence feature selection, compromising the independence of test evaluation.

## Main finding
Under the tested synthetic conditions, the leaky workflow had higher mean accuracy, with a larger gap as candidate feature count increased. On the real dataset, the average gap was much smaller. The effect depends on the data and experimental setting; this does not show leakage always improves accuracy.

## Limitations
1. Synthetic features and labels are independent random variables.
2. Only one feature selector and one classifier were tested.
3. Only one real dataset was evaluated.
4. Accuracy alone does not capture every dimension of model quality.
5. The 50 real-data splits reuse the same observations and are not independent datasets.
6. Statistical conclusions from these repeated splits should be interpreted cautiously.

## Files
- `LeakageLab.ipynb`: experiments, explanations, tables and figures
- `figures/`: recorded-results figure
- `results/`: CSV summaries
- `requirements.txt`: Python dependencies

## Run
Install dependencies with `pip install -r requirements.txt`, then open `LeakageLab.ipynb` in Jupyter or Google Colab and run all cells.

The intentionally leaky workflow is for education only, not production evaluation. The breast cancer dataset is a machine-learning benchmark and not for medical decision-making.
