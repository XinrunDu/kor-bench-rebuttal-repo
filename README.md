<h2 align="center" style="font-size: 2.5em; font-weight: bold; color: #2c3e50;">
  KOR-Bench: Benchmarking Language Models<br>
  on Knowledge-Orthogonal Reasoning Tasks
</h2>

This repository contains the evaluation code for the paper "KOR-Bench: Benchmarking Language Models on Knowledge-Orthogonal Reasoning Tasks".

---

## 🔔 Introduction


<p align="center">
  <img src="images/KOR-overview.png" alt="KOR-Bench Overview" style="width: 400px;"> 
</p>


**Knowledge-Orthogonal Reasoning Benchmark (KOR-Bench)** is designed to evaluate models' intrinsic reasoning and planning abilities while minimizing interference from pretrained knowledge. It introduces new rules that are independent of prior knowledge, allowing for a more accurate assessment of how models adapt to novel rule-driven tasks. KOR-Bench consists of five task categories: **Operation**, **Logic**, **Cipher**, **Puzzle**, and **Counterfactual**. Leading models, such as **Claude-3.5-Sonnet** and **GPT-4o**, score around **58%** on this challenging benchmark.

---


## 🏆 Mini-Leaderboard

| Chat Models                       | Overall |
|-----------------------------------|---------|
| **_Claude-3.5-Sonnet(2024-06-20)_**   | **58.96**   |
| _Gpt-4o(2024-05-13)_              | 58.00   |
| Meta-Llama-3.1-405B-Instruct      | 55.36   |
| Qwen2.5-32B-Instruct              | 54.72   |
| _Gpt-4-Turbo(2024-04-09)_         | 53.52   |
| Mistral-Large-Instruct-2407       | 53.12   |
| Qwen2.5-72B-Instruct              | 52.16   |
| Meta-Llama-3.1-70B-Instruct       | 50.00   |
| _Yi-Large_                        | 50.00   |
| Qwen2.5-14B-Instruct              | 49.36   |
| Meta-Llama-3-70B-Instruct         | 49.20   |
| _Doubao-Pro-128k(2024-06-28)_     | 48.08   |
| DeepSeek-V2.5                     | 47.76   |
| Qwen2-72B-Instruct                | 47.04   |
| Gemma-2-27b-It                    | 44.48   |
| Phi-3.5-MoE-Instruct              | 43.92   |
| _Gemini-1.5-Pro-001_              | 43.36   |
| Gemma-2-9b-It                     | 41.60   |
| Yi-1.5-34B-Chat                   | 39.76   |
| Phi-3.5-mini-Instruct             | 39.04   |
| Qwen2.5-7B-Instruct               | 38.56   |
| Meta-Llama-3.1-8B-Instruct        | 37.20   |
| Yi-1.5-9B-Chat                    | 35.20   |
| Meta-Llama-3-8B-Instruct          | 32.80   |
| C4ai-Command-R-Plus-08-2024       | 32.72   |
| Yi-1.5-6B-Chat                    | 32.48   |
| C4ai-Command-R-08-2024            | 31.12   |
| Qwen2-7B-Instruct                 | 30.72   |
| Gemma-2-2b-It                     | 24.32   |
| Mistral-7B-Instruct-v0.3          | 24.16   |
| Qwen2.5-1.5B-Instruct             | 20.40   |
| OLMo-7B-0724-Instruct-hf          | 18.48   |
| MAP-Neo-7B-Instruct-v0.1          | 18.16   |
| Qwen2-1.5B-Instruct               | 14.32   |
| Qwen2.5-0.5B-Instruct             | 9.04    |
| Qwen2-0.5B-Instruct               | 3.52    |
---
| Base Models                       | Overall |
|-----------------------------------|---------|
| **Meta-Llama-3.1-405B**               | **39.68**   |
| Qwen2.5-32B                       | 37.28   |
| Qwen2.5-72B                       | 37.28   |
| Meta-Llama-3-70B                  | 35.20   |
| Qwen2-72B                         | 34.32   |
| Meta-Llama-3.1-70B                | 33.84   |
| Gemma-2-27b                       | 33.36   |
| Qwen2.5-14B                       | 33.28   |
| Yi-1.5-34B                        | 30.08   |
| Yi-1.5-9B                         | 29.20   |
| Qwen2.5-7B                        | 28.80   |
| Qwen2-7B                          | 27.44   |
| Meta-Llama-3.1-8B                 | 26.00   |
| Gemma-2-9b                        | 25.52   |
| Meta-Llama-3-8B                   | 24.96   |
| Mistral-7B-v0.1                   | 21.60   |
| Yi-1.5-6B                         | 20.88   |
| MAP-Neo-7B                        | 15.60   |
| Qwen2.5-1.5B                      | 15.12   |
| OLMo-7B-0724-hf                   | 14.80   |
| Gemma-2-2b                        | 13.20   |
| Qwen2-1.5B                        | 12.32   |
| Qwen2-0.5B                        | 9.92    |
| Qwen2.5-0.5B                      | 9.12    |

**Note:** Models marked with an underscore (_) are closed-source.


## ⚙️ Installation 

To install the required packages, run:

```bash
# Prepare repository and environment
pip install -r requirements.txt
```

---
## 🔍 Inference
You can directly perform inference on `<MODEL_NAME>` using the following command:

```bash
export PYTHONPATH=$(pwd)

python infer/infer.py --config <CONFIG_PATH> --split <TASKS> --mode <MODE> --model_name <MODEL_NAME> --output_dir <OUTPUT_DIR> --batch_size <BATCH_SIZE> --use_accel
```

Example:
```bash
export PYTHONPATH=$(pwd)

python infer/infer.py --config config/config.yaml --split logic cipher counterfactual operation puzzle --mode zero-shot --model_name Yi-1.5-6B-Chat --output_dir results --batch_size 250 --use_accel
```

*More examples can be found in the shell scripts of this repository.* 🔗

#### 📜Parameter Explanations for Inference Script 

- **`--config`**: Path to the configuration file.
- **`--split`**: Specify the task categories for evaluation.  
  Available options include:
  - `logic`
  - `cipher`
  - `counterfactual`
  - `operation`
  - `puzzle`
  
  Multiple categories can be selected at once, separated by spaces.
  
- **`--mode`**: Choose from different evaluation modes (`zero-shot`, `three-shot`, etc.).  Default is to evaluate all modes.

- **`--infer_limit`**: Limit the number of problems processed during inference to save costs during API debugging. Defaults to unlimited.

- **`--use_accel`**: Enables acceleration options for faster inference.

- **`--num_workers`**: Set the number of concurrent processes (use for API calls; set to 1 for local models).

- **`--batch_size`**: Set the batch size for local model inference (set to 1 for API calls).


#### 📝 Notes 

- During inference, a temporary file `.jsonl.tmp` will be saved. If the inference is unexpectedly interrupted, you can directly rerun the command to resume from the last checkpoint.
  
- After inference is complete, check the `response` field in the saved JSONL file in `output_dir`. This field should typically be of string type; if it is of dict type, the `error` field will contain error information. You can rerun the command to re-infer any issues that caused errors.


#### 🛠️ Run Custom Model 

- **`--model_name`**: This parameter must align with the filenames in the `infer/models` directory.  We have some built-in models available for direct selection.

- **Adding a Custom Model**:  
  If you want to add a **custom model** for testing, follow these steps:
  1. Refer to the files in the `infer/models` directory.
  2. Create and add a new `.py` file for your model.
  3. Update the configuration in [`__init__.py`](infer/models/__init__.py).

-  For more details, please check the documentation of the specific model you are adding.


---

## ⭐ Evaluation

After you finish inference and confirm there are no error messages, please run the answer parsing and evaluation pipeline as follows: 
```bash
export PYTHONPATH=$(pwd)

python eval/eval.py <source_folder> <target_root_folder> <csv_file>

# example:
python eval/eval.py results/0923_main eval/results/0923_main eval/results_0923_main.csv
```
Detailed evaluation results can be found in the `target_root_folder`.

