# SWE-QA: A Dataset and Benchmark for Complex Code Understanding

[![GitHub Pages](https://img.shields.io/badge/GitHub-Pages-blue)](https://your-username.github.io/swe-qa/)
[![Paper](https://img.shields.io/badge/Paper-PDF-red)](paper/paper.pdf)

**Anonymous submission for LREC 2026**

## Overview

This repository contains **SWE-QA**, a comprehensive dataset and benchmark for evaluating multi-hop code comprehension. The dataset includes:

- 🎯 **9,072 multiple-choice questions** for complex code understanding
- 📦 **12 Python repositories** from SWE-bench
- 🔍 **2 question categories**: Declaration-and-Call (DC) and Interacting Entities (IE)
- ⚙️ **2 experimental settings**: Oracle (clean) and Noisy Oracle (with distractors)

## Quick Links

- 🌐 **[Project Page](https://your-username.github.io/swe-qa/)** - Interactive overview with dataset details
- 📄 **[Paper](paper/paper.pdf)** - Full research paper (PDF)
- 📊 **[Dataset](datasets/)** - Download datasets and view documentation

## Repository Structure

```
.
├── index.html              # GitHub Pages project page
├── style.css               # Styling for project page
├── paper/
│   └── paper.pdf          # Research paper
├── datasets/
│   ├── README.md          # Detailed dataset documentation
│   ├── mcq_dataset.zip    # Oracle setting questions
│   ├── mcq_dataset_with_distractors.zip  # Noisy oracle setting
│   └── repos/             # Code chunks and metadata (12 repositories)
└── assets/                # Optional images and resources
```

## Datasets

### Download

- **[Oracle Questions](datasets/mcq_dataset.zip)** (9,072 questions) - Questions with only relevant code chunks
- **[Noisy Oracle Questions](datasets/mcq_dataset_with_distractors.zip)** - Questions with additional distractor chunks
- **[Code Repositories](datasets/repos/)** - Processed code chunks and entity metadata

### Repositories Included

The dataset covers 12 popular Python repositories:
- astropy
- django
- matplotlib
- seaborn
- flask
- requests
- pylint
- pytest
- xarray
- scikit-learn
- sphinx
- sympy

## Getting Started

1. **View the project page**: Visit the [GitHub Pages site](https://your-username.github.io/swe-qa/) for an interactive overview
2. **Download the datasets**: Get the question sets from the [datasets](datasets/) folder
3. **Read the documentation**: Check the [Dataset README](datasets/README.md) for detailed structure and usage information

## Dataset Structure

Each question in the dataset includes:
- **Code chunks**: Formatted code snippets with metadata
- **Question**: Natural language question about the code
- **Multiple-choice options**: 4 options (A, B, C, D)
- **Correct answer**: Ground truth label
- **Category**: DC (Declaration-and-Call) or IE (Interacting Entities)
- **Repository**: Source repository name

For detailed JSON schemas and examples, see the [Dataset README](datasets/README.md).

## Citation

If you use this dataset in your research, please cite our paper:

```bibtex
@inproceedings{swe-qa-2026,
  title={Multi-hop Code Comprehension: A Dataset and Benchmark for Complex Code Understanding},
  author={Anonymous},
  booktitle={Proceedings of LREC 2026},
  year={2026}
}
```

## GitHub Pages Setup

To enable the project page:

1. Go to your repository **Settings**
2. Navigate to **Pages** in the left sidebar
3. Under **Source**, select the **main** (or **master**) branch
4. Click **Save**
5. The site will be available at `https://your-username.github.io/repository-name/`

## License

This dataset is released for research purposes only. See paper for details.

---

© 2026 Anonymous Authors. For review purposes only.
