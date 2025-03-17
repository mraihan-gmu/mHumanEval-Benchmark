## Step 1: Setup Environment

Create and activate a clean, isolated environment to ensure reliable test results:

```bash
# Using conda (recommended)
conda create -n mhumaneval python=3.8
conda activate mhumaneval

# OR using venv
python -m venv mhumaneval-env
# On Windows
mhumaneval-env\Scripts\activate
# On macOS/Linux
source mhumaneval-env/bin/activate
```

## Step 2: Install Dependencies

Install the required dependencies:

```bash
pip install -r requirements.txt
```

## Step 3: Download Benchmark Files

1. Download the appropriate benchmark file(s) for your evaluation:
   - For natural language-specific benchmarks, use files in the `mHumanEval-{NL}` directory
   - For programming language-specific benchmarks, use files in the `mHumanEval-{PL}` directory

2. Place the benchmark file(s) in your working directory or a subdirectory.

## Step 4: Evaluate Your Model

1. Start Jupyter notebook:
   ```bash
   jupyter notebook
   ```

2. Open `evaluate.ipynb` from the file browser.

3. Update the configuration variables at the top of the notebook:

   ```python
   # Configuration variables (customize these)
   CSV_FILE_NAME = 'mHumanEval-ben_Beng.csv'  # The CSV file to evaluate
   JSON_FILE_NAME = 'mHumanEval-ben_Beng.json'  # The JSON file to evaluate
   SOLUTION_COLUMN = 'model_solution'  # IMPORTANT: Change this to the column name that contains your model's solutions
   ```

   - The `SOLUTION_COLUMN` variable is particularly important - it must match the exact column name in your CSV/JSON file that contains the code solutions you want to evaluate
   - By default, it's set to `canonical_solution` (the reference solutions)

4. Run the notebook cell. The entire evaluation process will run automatically when you execute the cell.

## Step 5: Interpret Results

The evaluation produces:

1. **Console output** with a summary of results including:
   - Natural Language (NL) and Programming Language (PL) information
   - Pass@1 score percentage
   - Visual breakdown of passed and failed tests
   - Execution time

2. **Results file** (`evaluation_results.txt`) with detailed information:
   - List of all passed tasks
   - Details on failed, error, and timeout tasks
   - Exact error messages for debugging

Example output:
```
=============================================================
✨ HUMANEVAL BENCHMARK EVALUATION SUMMARY ✨
=============================================================
🌐 Natural Language (NL): ben_Beng
💻 Programming Language (PL): python
📊 Pass@1 Score: 95.73%
⏱️ Execution Time: 28.45 seconds
-------------------------------------------------------------
📈 Results Breakdown:
  ✅ Passed:   157/164 ( 95.73%) 🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩
  ❌ Failed:     4/164 (  2.44%) 🟥
  ⏱️ Timeouts:   2/164 (  1.22%) 🟨
  ⚠️ Errors:     1/164 (  0.61%) 🟧
=============================================================
```

## Evaluating Different Models

To evaluate different models or solutions:

1. Make sure your benchmark file includes the model's solutions in a separate column (e.g., `gpt4_solutions`, `llama_solutions`, etc.)

2. Update the `SOLUTION_COLUMN` variable to match your column name:

   ```python
   SOLUTION_COLUMN = 'gpt4_solutions'  # Replace with your model's solution column
   ```

## Evaluating Multiple Benchmarks

To evaluate multiple benchmarks sequentially, run the notebook multiple times with different file names:

1. Update the file names:
   ```python
   CSV_FILE_NAME = 'mHumanEval-hin_Deva.csv'
   JSON_FILE_NAME = 'mHumanEval-hin_Deva.json'
   ```

2. Run the cell again to evaluate the new benchmark.

3. Repeat for each language or programming language benchmark you want to evaluate.

## Troubleshooting

- **File not found errors**: Ensure the benchmark file is in the correct location and has the expected name.
- **Column not found errors**: Verify the column names in your benchmark file match the `SOLUTION_COLUMN` value exactly (case-sensitive).
- **Execution timeouts**: Increase the timeout value in the code if legitimate solutions are timing out.
- **Python compatibility issues**: Ensure you're using Python 3.6+ and have installed all dependencies.
