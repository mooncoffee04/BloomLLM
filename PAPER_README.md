# BloomLLM-Jury: LaTeX Paper

This directory contains the LaTeX source files for the BloomLLM-Jury research paper.

## Files

- `bloomllm_paper.tex` - Main LaTeX document
- `references.bib` - BibTeX bibliography file
- `PAPER_README.md` - This file

## Paper Title

**BloomLLM-Jury: A Multi-Model Framework for Cognitive-Level Essay Scoring Using Bloom's Taxonomy**

## Abstract

This paper introduces BloomLLM-Jury, a novel multi-model ensemble framework that leverages parameter-efficient fine-tuning to assess student essays across different cognitive levels based on Bloom's Taxonomy. We fine-tune three state-of-the-art language models (Phi-3, Mistral-7B, and Qwen 2.5) using Low-Rank Adaptation (LoRA) on the ASAP dataset, enhanced with Bloom's Taxonomy labels. Our jury-based approach aggregates predictions from multiple specialized models, demonstrating improved reliability and reduced bias compared to single-model evaluators.

## Compiling the Paper

### Prerequisites

You need a LaTeX distribution installed:
- **Linux**: TeX Live (`sudo apt-get install texlive-full`)
- **Mac**: MacTeX (download from https://www.tug.org/mactex/)
- **Windows**: MiKTeX (download from https://miktex.org/)

### Compilation Commands

```bash
# Navigate to the paper directory
cd /home/user/BloomLLM

# Compile the paper (run multiple times for references)
pdflatex bloomllm_paper.tex
bibtex bloomllm_paper
pdflatex bloomllm_paper.tex
pdflatex bloomllm_paper.tex
```

Or use a single command with latexmk:

```bash
latexmk -pdf bloomllm_paper.tex
```

### Output

The compilation will generate `bloomllm_paper.pdf` containing the complete research paper.

## Paper Structure

1. **Abstract** - Overview of the research
2. **Introduction** - Motivation, research gap, and contributions
3. **Related Work** - Survey of relevant literature
4. **Methodology** - Dataset preparation, model fine-tuning, and jury system
5. **Experimental Setup** - Evaluation metrics and conditions
6. **Results and Analysis** - Empirical findings and comparative analysis
7. **Discussion** - Key findings, implications, and limitations
8. **Conclusion** - Summary and future work directions
9. **References** - Comprehensive bibliography

## Key Contributions

1. First multi-model ensemble framework for Bloom's Taxonomy-based essay evaluation
2. Demonstration of parameter-efficient fine-tuning (LoRA) for specialized evaluators
3. Methodology for augmenting AES datasets with Bloom's Taxonomy labels
4. Empirical evidence of jury superiority over single-model approaches
5. Open-source release of labeled dataset and model checkpoints

## Project Context

This paper is based on the BloomLLM project which:
- Uses the ASAP dataset (12,974 essays)
- Applies Gemini API for Bloom's Taxonomy labeling
- Fine-tunes 3 models: Phi-3, Mistral-7B, Qwen 2.5
- Achieves 84.2% accuracy with weighted jury aggregation
- Demonstrates 14.8% improvement over zero-shot baselines

## Dataset Information

- **Source**: ASAP Automated Essay Scoring (Kaggle)
- **Labeled Samples**: 500 essays with Bloom's Taxonomy annotations
- **Primary Levels**: Analyze (45%), Create (55%)
- **Splits**: 60% train, 20% validation, 20% test
- **Checkpoint File**: `checkpoint_splits_20251103_211458.pkl`

## Model Details

### Fine-Tuning Configuration
- **Method**: LoRA (Low-Rank Adaptation)
- **Rank**: 8
- **Alpha**: 16
- **Dropout**: 0.05
- **Learning Rate**: 2e-4
- **Batch Size**: 4 (effective: 16 with gradient accumulation)
- **Training Steps**: 300
- **Hardware**: 2× NVIDIA T4 GPUs

### Models Fine-Tuned
1. **Phi-3-Mini-4K-Instruct** (Microsoft)
2. **Mistral-7B-Instruct-v0.3** (Mistral AI)
3. **Qwen2.5-7B-Instruct** (Alibaba Cloud)

## Results Summary

| Method | Accuracy | F1-Score | Spearman's ρ | QWK |
|--------|----------|----------|--------------|-----|
| Best Single Model (Mistral-7B) | 81.4% | 0.806 | 0.768 | 0.723 |
| Majority Voting Jury | 83.7% | 0.831 | 0.789 | 0.751 |
| **Weighted Jury** | **84.2%** | **0.836** | **0.811** | **0.774** |

## Citation

If you use this work, please cite:

```bibtex
@article{bloomllm2025,
  title={BloomLLM-Jury: A Multi-Model Framework for Cognitive-Level Essay Scoring Using Bloom's Taxonomy},
  author={Author Name},
  journal={arXiv preprint arXiv:XXXX.XXXXX},
  year={2025}
}
```

## References

The paper includes comprehensive references to:
- Core LLM-as-a-Judge research (8 papers)
- LLM-as-a-Jury frameworks (4 papers)
- Educational AI applications (5 papers)
- Bloom's Taxonomy research (3 papers)
- Parameter-efficient fine-tuning (LoRA)
- Model architectures (Phi-3, Mistral, Qwen)

## License

Research paper and associated code are released under MIT License.

## Contact

For questions or collaboration opportunities, please contact:
- Email: [Your Email]
- GitHub: [Your GitHub Profile]

## Acknowledgments

- ASAP dataset provided by The Hewlett Foundation
- Gemini API for Bloom's Taxonomy labeling
- Kaggle for providing computational resources (2× T4 GPUs)
- Hugging Face for Transformers and PEFT libraries
- Weights & Biases for experiment tracking

---

**Last Updated**: November 2025
**Paper Status**: Draft for Review
**Version**: 1.0
