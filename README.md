# Epistemic Filter Framework

This repository presents the **Epistemic Filter Framework**, a robust system designed to evaluate the epistemic status (truthfulness, plausibility, and certainty) of textual statements. It aims to filter and categorize information based on multiple epistemic criteria, providing a nuanced understanding of a statement's reliability and associated uncertainties.

## Overview

In an era of information overload, discerning reliable information from misinformation is critical. The Epistemic Filter Framework addresses this challenge by implementing a multi-faceted approach to assess statements. It combines advanced natural language processing (NLP) techniques with logical and semantic analysis to assign an "epistemic score" to each statement, indicating its likelihood of being true, false, or uncertain. The framework also quantifies various types of uncertainty (total, epistemic, and model uncertainty) to provide a comprehensive assessment.

## Features

* **Multi-Component Epistemic Scoring:** Evaluates statements based on a combination of factors:
    * **Similarity to Trusted Knowledge:** Compares new statements against a pre-defined knowledge base of trusted information.
    * **Anti-Similarity to Falsehoods:** Checks against a collection of known false statements.
    * **Logical Coherence:** Assesses internal consistency and adherence to logical principles.
    * **Semantic Consistency:** Ensures the meaning aligns with established facts.
    * **Structural Validity:** Analyzes grammatical correctness and sentence structure.
    * **Linguistic Quality:** Measures clarity and precision of language.
    * **Confidence Score:** Incorporates a sentiment or confidence measure from an NLP model.
* **Uncertainty Quantification:** Provides a detailed breakdown of uncertainty associated with each statement's score:
    * **Total Uncertainty:** Overall variability in the score.
    * **Epistemic Uncertainty:** Uncertainty due to limited knowledge.
    * **Model Uncertainty:** Uncertainty inherent in the model's predictions.
    * **Confidence Intervals:** 95% confidence intervals for scores derived from perturbations.
* **Dynamic Knowledge Base:** Supports the management and expansion of trusted and false statements.
* **Benchmarking and Evaluation:** Includes functionalities to evaluate the framework's performance against benchmark datasets, providing metrics like accuracy, precision, recall, and F1-score.
* **Memory Bank:** Categorizes and stores statements as 'verified true', 'verified false', or 'uncertain' based on their scores and confidence levels.

## Installation

To set up the Epistemic Filter Framework, follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/sharmaraghav644/Epistemic-Filter-Framework.git](https://github.com/sharmaraghav644/Epistemic-Filter-Framework.git)
    cd Epistemic-Filter-Framework
    ```
2.  **Create a virtual environment (recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate # On Windows, use `venv\Scripts\activate`
    ```
3.  **Install dependencies:**
    The project relies on libraries such as `sentence-transformers`, `transformers`, `torch`, `numpy`, and `scikit-learn`.
    ```bash
    pip install torch transformers sentence-transformers numpy scikit-learn
    ```
    *(Note: The provided Jupyter Notebook uses `cardiffnlp/twitter-roberta-base-sentiment-latest` for sentiment analysis, which will be downloaded by the `transformers` library upon first use.)*

## Usage

The core functionality is demonstrated in the `Epistemic_Filtering_Code_POC_final(1).ipynb` notebook. Here's a high-level overview of how to use the framework:

1.  **Initialize the Epistemic Filter System:**
    ```python
    from epistemic_filter import EpistemicFilter, KnowledgeBase, UncertaintyQuantifier
    
    # Define your knowledge base
    knowledge_base_data = {
        'trusted': [
            "The Earth revolves around the Sun.",
            "Water boils at 100 degrees Celsius at standard atmospheric pressure.",
            # ... more trusted statements
        ],
        'false': [
            "The Earth is flat.",
            "Humans use only 10% of their brain capacity.",
            # ... more false statements
        ]
    }
    
    kb = KnowledgeBase(knowledge_base_data)
    filter_system = EpistemicFilter(knowledge_base=kb)
    uncertainty_quantifier = UncertaintyQuantifier(filter_system)
    ```
2.  **Compute Epistemic Scores for Statements:**
    ```python
    statement = "The Moon is made of green cheese."
    score_obj = filter_system.compute_epistemic_score(statement)
    print(f"Statement: '{statement}'")
    print(f"Final Score: {score_obj.final_score:.3f}")
    print(f"Confidence: {score_obj.confidence:.3f}")
    ```
3.  **Filter Statements:**
    ```python
    statements_to_filter = [
        "The sun is a star.",
        "A square has five sides.",
    ]
    results = filter_system.filter_statements(statements_to_filter, threshold=0.5)
    print("Accepted Statements:", results['accepted'])
    print("Rejected Statements:", results['rejected'])
    ```
4.  **Quantify Uncertainty:**
    ```python
    statement_for_uncertainty = "The Earth revolves around the Sun."
    uncertainty = uncertainty_quantifier.quantify_uncertainty(statement_for_uncertainty)
    print(f"Total Uncertainty: {uncertainty['total_uncertainty']:.3f}")
    print(f"Epistemic Uncertainty: {uncertainty['epistemic_uncertainty']:.3f}")
    print(f"Model Uncertainty: {uncertainty['model_uncertainty']:.3f}")
    print(f"95% CI: [{uncertainty['confidence_interval'][0]:.3f}, {uncertainty['confidence_interval'][1]:.3f}]")
    ```

## Results and Evaluation

The `Epistemic_Filtering_Code_POC_final(1).ipynb` notebook includes a comprehensive evaluation of the framework's performance. Key metrics and findings include:

### Overall Performance

* **Accuracy:** 0.721
* **Precision:** 0.613
* **Recall:** 1.000
* **F1 Score:** 0.760

**Confusion Matrix:**
* True Negatives (TN): 12
* False Positives (FP): 12
* False Negatives (FN): 0
* True Positives (TP): 19

### Detailed Analysis by Category

The framework was evaluated across various categories of statements, including physics, biology, mathematics, logical reasoning, and nonsensical statements.

| Dataset                 | Accuracy | Precision | Recall | F1-Score | Statements |
| :---------------------- | :------- | :-------- | :------- | :------- | :--------- |
| Scientific Facts        | 0.615    | 0.583     | 1.000    | 0.737    | 13         |
| Mathematical Statements | 0.583    | 0.545     | 1.000    | 0.706    | 12         |
| Logical Reasoning       | 0.625    | 0.571     | 1.000    | 0.727    | 8          |
| Nonsensical Statements  | 0.667    | 0.000     | 0.000    | 0.000    | 6          |

### Component Contribution Analysis

The correlation of each epistemic component with the ground truth was also analyzed:

* **Similarity:** 0.771 correlation with ground truth
* **Anti Similarity:** 0.571 correlation with ground truth
* **Logical Coherence:** 0.287 correlation with ground truth
* **Semantic Consistency:** -0.173 correlation with ground truth
* **Structural Validity:** 0.018 correlation with ground truth
* **Linguistic Quality:** 0.063 correlation with ground truth
* **Confidence:** -0.137 correlation with ground truth

## Links

* **Research Paper (Zenodo):** [Epistemic Filter Framework Paper](https://zenodo.org/records/15811822)
* **GitHub Repository:** [Epistemic Filter Framework GitHub](https://github.com/sharmaraghav644/Epistemic-Filter-Framework)

## About the Author

**Raghav Sharma**
* ORCID iD: [0009-0000-3987-0626](https://orcid.org/0009-0000-3987-0626)
* Email: sharmaraghav644@gmail.com

## Contributing

Contributions are welcome! Please refer to me at sharmaraghav644@gmail.com with your ideas.

## License

This project is open-source. Please refer to the LICENSE file in the GitHub repository for details.
