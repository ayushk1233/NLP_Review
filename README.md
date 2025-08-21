# NLP_Review
Project Overview

This project demonstrates an end-to-end sentiment analysis workflow using a public dataset and pretrained language models. The focus is on dataset preparation, prompt engineering, model evaluation, and reflection on limitations. The work highlights how different prompt styles influence LLM behavior and how pretrained models perform under real-world constraints.

1. Dataset & Preprocessing

Dataset Used: IMDb Movie Reviews Dataset (50,000 reviews)
.

Reason for Choice: Balanced dataset (25k positive, 25k negative), widely used in sentiment tasks, and suitable for experimentation under resource constraints.

Preprocessing Steps:

Lowercasing all text.

Removing HTML tags, punctuation, and stopwords.

Tokenization applied for cleaner model input.

Visual Insights:

Class distribution: Evenly balanced.

Word cloud: Frequent sentiment-rich words like movie, film, good, bad.

2. Prompt Engineering & Model Interaction

A pretrained Hugging Face DistilBERT sentiment analysis pipeline was used. Three prompt styles were tested:

Prompt Style	Example	Observed Output
Direct Classification	“Classify the sentiment of this review: The movie had amazing visuals but the story was too slow and boring.”	NEGATIVE
Few-Shot Example	“This movie was great → Positive, I hated the film → Negative. Now classify: The movie had amazing visuals but the story was too slow and boring.”	NEGATIVE (confidence ~0.98)
Explanation Request	“Analyze this review and explain whether it is positive or negative: The movie had amazing visuals but the story was too slow and boring.”	NEGATIVE + rationale (“positive visuals, weak storyline”)

👉 Insight: Prompt design affects confidence scores and output richness (label-only vs. explanation).

3. Model Evaluation

Evaluation on 1,000 reviews:

Accuracy: 0.795 (~80%)

Precision: 0.81

Recall: 0.80

F1 Score: 0.79

Custom Samples:

Positive: “I absolutely loved this movie, it was fantastic!” → POSITIVE (0.9999) ✅

Negative: “Worst film I’ve ever seen, total waste of time.” → NEGATIVE (0.9998) ✅

Mixed: “The visuals were stunning, but the plot was boring.” → NEGATIVE (0.9982) ❌ (classified as fully negative, missing nuance).

👉 While pretrained DistilBERT performed strongly, it struggled with mixed/neutral cases, which is consistent with dataset limitations (binary labels only).

4. Troubleshooting & Reflection

Issue Observed: The model shows bias toward strong binary sentiment, leading to errors on nuanced reviews.

Reason: IMDb dataset is strictly binary (positive/negative), which trains the model to avoid “neutral” outputs.

Potential Improvements:

Fine-tune on a dataset with a neutral/mixed class (e.g., Amazon 3-class reviews).

Use instruction-tuned models for better reasoning.

Apply data augmentation to improve generalization.

Resource Constraints: Due to limited compute, full fine-tuning was not performed. Instead, pretrained models were used with prompt variations and evaluation on a 1k-sample subset. This approach balances practicality with meaningful insights.

Conclusion

This project demonstrates:

Competence in dataset preparation and text preprocessing.

Awareness of prompt engineering and its real-world effects.

Ability to evaluate pretrained models with standard metrics.

Critical reflection on limitations and bias issues.

Although constrained by resources, the work shows an end-to-end understanding of applied NLP workflows and clear thinking about trade-offs in model performance.
