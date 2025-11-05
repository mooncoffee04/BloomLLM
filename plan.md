Here’s a fast-track, research-grounded implementation plan for a **Domain-Aware LLM-as-a-Jury System Grading Across Bloom’s Taxonomy**—including necessary resources, design, and concrete steps for completion in 3 days. Relevant literature is referenced for context and prompt guidance.

***

## 0. **Summary**
You will build a scalable pipeline to feed student responses to a jury of LLMs, with each LLM (or prompt persona/specialized adapter) evaluating the answer specifically for one or more Bloom levels. The verdict is aggregated, with transparent rationale, for detailed formative assessment.

***

## 1. **Required Resources**

### **Datasets**
- **ASAP Automated Essay Scoring** ([Kaggle])[1]
- **RACE** (Reading Comprehension, open) or **EdNet** (for structured science/Math)
- 1000–2000 answer samples for pilot (mix simple recall, application, analysis, and creative problems)

### **Models & Libraries**
- HuggingFace Transformers, PEFT (LoRA/QLoRA), OpenAI API (for GPT-4/3.5), and at least one open-source model (Llama-3 or similar)
- pandas, numpy for data prep and scoring; matplotlib for visualization

### **Hardware**
- GPU (T4 x2 is sufficient, as previously discussed)

### **Key Reference Works**
- Huber et al., 2025 (COLING): Coverage of cognitive levels and reporting gaps[2]
- Multi-agent frameworks for education:[3][4][1]
- LLM prompt/classification for Bloom’s[5]

***

## 2. **Implementation Steps & Timeline**

### **Day 1:**
#### 1. Dataset Curation & Labeling
- Download and preprocess ASAP, RACE, or EdNet.  
- If Bloom’s levels aren’t annotated, use rules (from ) or brief crowdsourcing to assign level tags for at least 200–300 responses.[5]
- Format: `(prompt, student_response, reference_solution, bloom_labels)`.

#### 2. Jury Scaffold
- **Select LLMs:** Use 3–5 LLMs: GPT-4 (API), open-source (Llama-3, Zephyr), and any with prompt tuning capability.
- **Prompt Engineering:**
  - Design a separate prompt per Bloom’s level:
    - e.g., “Is this answer primarily showing understanding (‘Explain the main idea in your own words’)? Rate 1–5 and justify.”
  - Implement CoT rationale requirement in all prompts (as suggested in past work for transparency ).[4]

### **Day 2:**
#### 3. Jury Inference & Aggregation
- Build jury logic to send each response to each specialized prompt (per Bloom’s level) and receive scores plus rationales.
- Aggregate results per answer in a table:
  - Columns: Answer, Remember, Understand, Apply, Analyze, Evaluate, Create (1–5 each), plus rationale per column.
- Decide on voting: Majority for categorical, mean for ordinal scores.

#### 4. Post-processing and Visualization
- Generate distributions for scores per cognitive level, per answer.
- Provide a per-question verdict (“learning profile”).
- Visualize jury agreement per level (e.g., heatmaps, barplots for each Bloom’s level across the sample).

#### 5. Human Baseline (Optional)
- Sample 25–50 answers; get 1–2 educators to label for inter-rater and jury alignment (see methods in ).[1][2]

### **Day 3:**
#### 6. Report Compilation & Documentation
- Summarize design, score distributions, model agreement/disagreement, and illustrative rationales for a range of answers.
- Document prompt templates, adjudication policies, and citations.
- Compose 1–2 case studies: student progression profiles, explainability gains, and differences from single-LLM grading.
- Include references to Huber et al. (2025), DPO multi-agent (), and classifier-oriented work ().[3][5]

***

## 3. **Implementation Blueprint**

```plaintext
[Pipeline]
Student Answer → [Jury of LLMs (Prompted per Bloom’s Level)] 
→ [Score & Rationale per Bloom Level]
→ [Aggregation: per level, overall cognitive profile]
→ [Dashboard Output + Formative Feedback]
```

***

## 4. **Prompts & Adjudication Examples**

- **Remember:** “Does the answer recall or state facts? Rate 1 (not at all)–5 (fully), explain.”
- **Understand:** “Does the answer paraphrase or summarize key points?”
- **Apply:** “Does the answer correctly use knowledge in a new scenario?”
- etc.

Combine with CoT (“Because…”) explanations.

***

## 5. **Risks & Mitigations**
- **Not enough data per Bloom level:** Synthesize or relabel small subsets.
- **Interpretation ambiguity:** Use rationale fields and aggregate across jury.
- **Speed:** Batch LLM calls & use efficient inference.

***

## 6. **Deliverables**
- Pipeline code (Jupyter/notebook or script).
- Dataset with jury scores, rationales, and aggregated learning profiles.
- Short report with plots, case studies, and future work section.
- Prompt templates and documentation.

***

### **Core References to Include**
- Huber et al. 2025 (“LLMs meet Bloom’s Taxonomy”)[2]
- Li et al. 2022/2025 (“Analyzing Questions by Bloom’s Level”)[5]
- EDM/EDM 2025 Multi-agent grading frameworks[1][3]
- Tree-of-Thought ensemble[4]

***

**With this plan and referenced sources, you have an original, valuable, and actionable project—possible to fully deliver in 3 days. If you need prompt samples, notebook skeleton, or visualization tips, just ask!**

[1](https://educationaldatamining.org/EDM2025/proceedings/2025.EDM.long-papers.80/index.html)
[2](https://aclanthology.org/2025.coling-main.350.pdf)
[3](https://girt.shodhsagar.com/index.php/j/article/view/129)
[4](https://arxiv.org/abs/2502.16399)
[5](https://aclanthology.org/anthology-files/pdf/bea/2025.bea-1.42.pdf)