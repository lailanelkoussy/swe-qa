# SWE-QA: A Dataset and Benchmark for Complex Code Understanding

**Anonymous submission for LREC 2026**

This repository contains the dataset, code chunks, and metadata for our paper "Multi-hop Code Comprehension: A Dataset and Benchmark for Complex Code Understanding."

## Dataset Overview

- **9,072 multiple-choice questions** for multi-hop code comprehension
- **12 Python repositories** from SWE-bench
- **2 question categories**: Declaration-and-Call (DC) and Interacting Entities (IE)
- **2 experimental settings**: Oracle (clean) and Noisy Oracle (with distractors)

## Repository Structure

```
.
├── mcq_dataset.zip                          # Oracle setting questions
├── mcq_dataset_with_distractors.zip         # Noisy oracle setting questions
├── repo/                                     # Source code chunks and metadata
│   ├── astropy.zip
│   ├── django.zip
│   ├── matplotlib.zip
│   ├── seaborn.zip
│   ├── flask.zip
│   ├── requests.zip
│   ├── pylint.zip
│   ├── pytest.zip
│   ├── xarray.zip
│   ├── scikit-learn.zip
│   ├── sphinx.zip
│   └── sympy.zip
└── README.md                                 # This file
```

## Dataset Files

### `mcq_dataset.zip` (Oracle Setting)

Contains questions with only relevant code chunks (Experimental Setting 1).

**JSON Structure:**
```json
{
  "code": "# Formatted code as provided to models\nclass Example:\n    ...",
  "chunks": [
    {
      "content": "class Example:\n    def method(self):\n        ...",
      "file_path": "lib/package/module.py",
      "chunk_index": 0,
      "chunk_id": "chunk_uuid",
      "declared_entities": [...],
      "called_entities": [...]
    }
  ],
  "question": "How does the Example class handle...?",
  "options": {
    "A": "Option A text...",
    "B": "Option B text...",
    "C": "Option C text...",
    "D": "Option D text..."
  },
  "correct_answer": "C",
  "category": "entity_declaration_call_specific",
  "repo": "matplotlib_matplotlib",
  "entities": ["Example"]
}
```

**Total:** 9,072 questions
- **Declaration-and-Call (DC):** 4,584 questions
- **Interacting Entities (IE):** 4,488 questions

### `mcq_dataset_with_distractors.zip` (Noisy Oracle Setting)

Same structure as `mcq_dataset.zip`, but `chunks` array includes additional distractor chunks that are plausible but irrelevant (Experimental Setting 3).

### `repo/` Directory

Contains processed code chunks and entity metadata for each repository.

**JSON Structure (per repository):**
```json
[
  {
    "id": "chunk_uuid",
    "content": "def function_name(param1, param2):\n    ...",
    "file_path": "src/module/file.py",
    "order_in_file": 0,
    "declared_entities": [
      {
        "name": "function_name",
        "type": "function",
        "dtype": "None"
      }
    ],
    "called_entities": [
      {
        "name": "helper_function",
        "type": "function"
      }
    ]
  }
]
```

## Field Descriptions

### Question Fields

| Field | Type | Description |
|-------|------|-------------|
| `code` | `str` | Formatted code string as provided to language models |
| `chunks` | `list[dict]` | List of code chunk objects with metadata |
| `question` | `str` | The multiple-choice question text |
| `options` | `dict` | Multiple-choice options (keys: "A", "B", "C", "D") |
| `correct_answer` | `str` | Letter of the correct answer ("A", "B", "C", or "D") |
| `category` | `str` | Question type: `"entity_declaration_call_specific"` or `"interacting_entities"` |
| `repo` | `str` | Repository name (e.g., `"matplotlib_matplotlib"`) |
| `entities` | `list[str]` | Entity name(s) the question focuses on (1-2 entities) |

### Chunk Fields

| Field | Type | Description |
|-------|------|-------------|
| `id` | `str` | Unique chunk identifier |
| `content` | `str` | Source code text of the chunk |
| `file_path` | `str` | Relative path to source file in repository |
| `order_in_file` | `int` | Relative position of chunk within file |
| `declared_entities` | `list[dict]` | Entities defined in this chunk |
| `called_entities` | `list[dict]` | Entities invoked in this chunk |

### Entity Fields

| Field | Type | Description |
|-------|------|-------------|
| `name` | `str` | Entity identifier (function/class/variable name) |
| `type` | `str` | Entity type: `"function"`, `"class"`, `"method"`, `"variable"`, `"constant"` |
| `dtype` | `str` | Inferred data type (for declared entities only) |

## Dataset Statistics

| Repository | Questions | DC Questions | IE Questions | Code Chunks |
|------------|-----------|--------------|--------------|-------------|
| astropy_astropy | 974 | 484 | 490 | 19425 |
| django_django | 1032 | 519 | 513 | 26382 |
| marshmallow-code_marshmallow |753 | 271 | 482 | 729 |
| matplotlib_matplotlib | 983 | 488 | 495 | 13202 |
| mwaskom_seaborn | 395 | 239 | 156 | 2410 |
| pallets_flask | 157 | 99 | 58 | 816 |
| psf_requests | 128 | 80 | 48 | 519 |
| pylint-dev_pylint | 978 | 493 | 485 | 6395 |
| pytest-dev_pytest | 792 | 460 | 332 | 4746 |
| pydata_xarray | 959 | 477 | 482 | 9216 |
| scikit-learn_scikit-learn | 939 | 475 | 464 | 20744 |
| sphinx-doc_sphinx | 982 | 499 | 483 | 7087 |
| **Total** | **9,072** | **4,584** | **4,488** | **111671** |


## Experimental Settings

### Setting 1: Oracle Question Answering
- Use `mcq_dataset.zip`
- Only relevant chunks provided
- Measures pure comprehension ability
- Upper bound on performance

### Setting 2: Retrieval-Based Evaluation
- Use chunks from `repo/` directory
- Embed all chunks with a code embedding model
- Retrieve top-k chunks for each question
- Measures retrieval quality (NDCG@k, Precision@k)

### Setting 3: Noisy Oracle Comprehension
- Use `mcq_dataset_with_distractors.zip`
- Relevant chunks + plausible distractors
- Simulates imperfect retrieval
- Tests robustness to noise

##  Baseline Results

See our paper for detailed results. Best performance:

| Model | Setting 1 (Oracle) | Setting 3 (Noisy) |
|-------|-------------------|-------------------|
| Llama-3.3-70B-Instruct | 74.41% | 74.31% |
| gemma-3-4b-it | 72.00% | 70.63% |
| Qwen3-4B-Instruct | 70.05% | 68.79% |

**Key Findings:**
- Dense models outperform MoE by 10-13 points
- DC questions easier than IE questions (5-15 point gap)
- Minimal degradation under retrieval noise
- Performance scales with model size (plateau below 3B parameters)


---

**Note:** This is an anonymous submission for LREC 2026. Author information and permanent URLs will be added upon acceptance.
