# Metrics

There are many different types of metrics which might be of interest, and
listing them all would be impossible. This is especially true due the highly
heterogeneous nature of the metrics that can be measured on different types of
AI assets, in addition to all possible application domains.

## Choice of metrics to be measured

The best approach is to allow the users to choose the number and types of
metrics to be collected during the benchmark execution; in practice, this
decision belongs to the users ultimately running the AI asset. It’s their
responsibility to choose the metrics they want to measure and associate them to
the AI algorithm to run.

It must also be considered “how” to measure the selected metrics; in general, it
could be as simple as preparing/developing a software module to wrap the AI
asset and collect the perform the desired measurements.  This requires a
non-trivial knowledge about the AI asset.  The complexity can be compounded by
the need to write different wrappers for different HW platforms. 

If the task might arise ethical considerations and/or involves sensitive or
protected attributes, metrics accounting for fairness and bias in the AI
software should be considered.  Another good choice is the selection of
evaluation metrics that are easy to interpret and understand, both for
researchers and stakeholders who may not have a technical background; this will
help ensure that the evaluation results are accessible and useful to a wider
audience.

To ensure fair and effective model selection, metrics need to be aligned with
application goals, considering domain-specific implications (e.g., MSE for
financial risk, MAPE for sales forecasting). Multiple metrics should be adopted
to evaluate models in a more exhaustive ways (e.g., RMSE for performance,
R-squared for explanation). To allow fairness studies, subgroup performance
should be analyzed (allowing that metrics are evaluated for fairness across
different demographic or contextual subgroups). To assess robustness, models
can be tested on simulated or out-of-sample data distributions.

### Primary versus Secondary metrics
The primary goal of benchmarking is to evaluate the performance of AI models on
a given task. Performance metrics are typically task-specific; for instance, the
accuracy is typically employed for classification tasks, and is measured as the
proportion of correct predictions out of total predictions. For tasks involving
imbalanced datasets, balancing precision and recall, the F1 score is preferred
over accuracy. For speech-to-text models, Word Error Rate (WER), namely the
error rate in transcriptions, is typically adopted. 

These metrics provide a direct measure of a model’s utility and are of utmost
interest to stakeholders who prioritize functional outcomes.  In the "Metrics"
section of benchmarking reports, performance metrics should be prominently
featured at the top of the list. This aligns with the primary interest of
stakeholders to understand the practical capabilities of a model.

While performance metrics take precedence, secondary metrics are critical for
nuanced decision-making, especially when multiple models achieve comparable
performance levels. Secondary metrics can range from environmental and resource
efficiency ones to operational metrics.

### Examples of metrics
- Performance, which strongly depend on the underlying task (e.g., accuracy or
  similar metrics could be registered in the case of ML for classification)
- Latency (at different phases of the target AI application) 
- Throughput 
- Average Memory (CPU/GPU) 
- Peak Memory (CPU/GPU) 
- Memory Bandwidth (CPU/GPU) 
- Processor load (CPU/GPU/NPU) 
- Power consumption and Energy consumption
- Temperature
- FLOPs (can be used as a proxy for _computational efficiency_, a measure to
  assess the computational requirements of AI models during training and
inference
- Parameters 
- Storage 
- Performance per Watt: This metric combines raw performance with power and
  energy consumption measurements, focusing on the performance-to-energy ratio
of an AI model. Typically expressed as performance (e.g., accuracy, throughput)
per watt, it aims to maximize performance per watt for energy-efficient AI.
- Model Size (a measure of the size of AI models, such as the number of
  parameters)
- Carbon Footprint, for quantifying greenhouse gas emissions throughout the AI
  model's lifecycle, including manufacturing, training, and operation, using
metrics like CO2 equivalent emissions to assess environmental impact.

Continuous metrics are used in tasks where the model's output is a continuous
value rather than discrete categories. They quantify the magnitude of errors or
deviations between predicted and actual values, providing a more nuanced
assessment of model performance compared to classification metrics. 

It is important to keep track of multiple metrics to ensure high-quality
benchmarks. For instance, in the case of ML models, considering only the
accuracy as a metric can be misleading for a series of issues:
1. Imbalanced Datasets
    - Problem: In datasets where one class dominates (e.g., 95% positive cases,
      5% negative cases), a model can achieve high accuracy by simply predicting
the majority class (e.g., predicting all instances as positive) without learning
anything meaningful.
    - Consequence: High accuracy might mask the model's inability to correctly
      classify minority or underrepresented classes, which is critical in many
applications.

2. Failure to Capture Fairness
    - Problem: Accuracy does not consider whether the model performs equally
      well across different demographic groups (e.g., gender, ethnicity, or
age)
    - Consequence: A model might show high overall accuracy but systematically
      disadvantage specific subgroups, perpetuating bias and discrimination

3. Overlooking False Positives and False Negatives
    - Problem: Accuracy treats all misclassifications equally, ignoring the
      distinction between false positives (type I errors) and false negatives
(type II errors)
    - Consequence: This can be critical in applications like healthcare, e.g.,
      missing a diagnosis (false negative) is more severe than a false alarm; or
spam filtering, where blocking legitimate emails (false positive) might be more
disruptive than allowing spam (false negative)

4. Inadequate for Multi-Class or Multi-Label Problems
    - Problem: In tasks with multiple classes or overlapping labels, accuracy
      does not capture nuances like which classes are harder to predict or the
degree of mismatch in predictions
    - Consequence: This can lead to oversimplified evaluations and missed
      opportunities for targeted improvement

5. Neglecting Real-World Costs and Trade-Offs
    - Problem: Accuracy does not account for domain-specific costs of errors or
      decisions
    - Consequence: Models optimized purely for accuracy might be economically or
      socially suboptimal

6. Sensitivity to Thresholding
    - Problem: Accuracy depends on the classification threshold (e.g., a
      probability cutoff of 0.5). Small changes in the threshold can
dramatically affect accuracy without reflecting real performance changes
    - Consequence: This might lead to over-interpretation of small performance
      differences

7. Ignoring Model Robustness
    - Problem: Accuracy does not measure how well the model generalizes to
      unseen or noisy data, adversarial examples, or shifts in the data
distribution
    - Consequence: Models may perform well on the test data but fail in
      real-world applications

8. Lack of Interpretability
    - Problem: Accuracy does not provide insight into why a model is performing
      well or poorly
    - Consequence: This hinders debugging, improvement, and trust-building,
      particularly in high-stakes applications

### Influence of Metric Choice on Model Selection

The choice of metric for model selection can significantly influence the
outcome, as it determines which aspects of performance the model is optimized
for various aspects. For instance, the sensitivity to error types can be
considered. MSE prioritizes models that minimize large errors (important for
forecasts like energy demand or financial predictions where large deviations are
costly); conversely, MAE treats all errors equally, favoring models that balance
over- and under-prediction without emphasizing extremes

In terms of robustness to outliers, the MSE's sensitivity to outliers can lead
to models overfitting to rare, extreme data points; instead, metrics like MAE or
Huber loss (a combination of MSE and MAE) are less influenced by outliers,
producing more robust models

The interpretability and practical relevance should also be considered; MAPE is
intuitive for stakeholders since it communicates errors as percentages, making
it useful in business or finance contexts.  However, MAPE can mislead when
actual values are close to zero, leading to disproportionately high error values
The scale dependency is closely connected: metrics like MSE and MAE are
dependent on the scale of the target variable, requiring normalization or
standardization for fair comparisons across datasets; R-squared provides a
scale-independent measure, but it may not be sensitive to absolute error
magnitudes

Finally, domain-specific needs are relevant. In forecasting applications (e.g.,
weather, demand, sales), minimizing larger errors (using MSE or RMSE) might be
more critical due to operational costs. In healthcare, minimizing false
negatives or ensuring balanced predictions might prioritize MAE-like metrics.

### How Metric Choice Influences the End Result

Selecting a model based on MSE could favor models that perform well on datasets
with few outliers but may generalize poorly on skewed data distributions.
Choosing MAE could lead to a more robust model but might undervalue certain
critical edge cases. Some trade-offs are inevitable. A metric like RMSE might
produce a model that reduces large errors at the cost of increasing smaller
errors, potentially skewing practical usability. Conversely, MAE might favor a
balanced but less optimal solution for high-stakes applications.

The metric choice can illuminate model interpretation and usability: a metric
emphasizing explainability (e.g., R-squared) could lead to model selection that
aligns with stakeholder communication needs but might overlook actual prediction
performance. Metrics should be selected not to amplify bias continuous metrics
could unintentionally amplify biases if they are not evaluated across subgroups
or with fairness considerations. For example, optimizing for MSE on an
imbalanced dataset might favor dominant groups.

### Examples of different benchmarking tasks and their metrics

The following examples aim to clarify the relationship between tasks, metrics,
and model evaluation with a focus on benchmarking for selecting the best model
for specific tasks, not just training.

1. Classification Tasks
- Task: Binary Classification
    - Example: Predict whether an email is spam or not spam.
    - Metrics:
        - Accuracy: Fraction of correctly classified instances (useful for
          balanced datasets).
        - Precision: Proportion of correctly predicted positive instances among
          all predicted positives (important if false positives are costly,
e.g., in medical tests for rare diseases).
        - Recall (Sensitivity): Proportion of actual positives correctly
          identified (important if false negatives are costly, e.g., cancer
detection).
        - F1-Score: Harmonic mean of precision and recall (useful for imbalanced
          datasets).
        - ROC-AUC: Measures model’s ability to differentiate between classes
          across thresholds (useful for ranking tasks or threshold selection).

- Task: Multiclass Classification
    - Example: Classify images into categories like cats, dogs, and birds.
    - Metrics:
        - Accuracy: Fraction of correctly classified instances.
        - Macro-Averaged F1-Score: Average F1-score across all classes, treating
          each class equally (useful for imbalanced classes).
        - Confusion Matrix: Breakdown of predictions per class (identifies
          specific failure modes).

2. Regression Tasks
- Task: Predict Continuous Values
    - Example: Forecast tomorrow’s temperature in Celsius.
    - Metrics:
        - Mean Squared Error (MSE): Penalizes large deviations more than small
          ones (useful when large errors are disproportionately harmful).
        - Mean Absolute Error (MAE): Measures average magnitude of error (better
          if all errors are treated equally).
        - R-squared (R²): Indicates how much of the variance in the target
          variable is explained by the model (useful for interpretability).
        - Mean Absolute Percentage Error (MAPE): Error as a percentage of the
          true value (useful for interpretability in business forecasting).

3. Ranking and Retrieval Tasks
- Task: Information Retrieval
    - Example: Rank web pages for a search query.
    - Metrics:
        - Mean Reciprocal Rank (MRR): Evaluates how high the first relevant
          result appears in the ranking.
        - Precision@k: Fraction of relevant documents in the top k results
          (useful for top-ranked precision).
        - Normalized Discounted Cumulative Gain (NDCG): Considers both relevance
          and position of retrieved documents (higher weights for top-ranked
items).

4. Clustering Tasks
- Task: Group Similar Items
    - Example: Segment customers based on purchasing behavior.
    - Metrics:
        - Silhouette Score: Measures how similar items are within clusters
          versus between clusters (useful for internal validation).
        - Adjusted Rand Index (ARI): Compares clustering results to a ground
          truth (useful for external validation).
        - Normalized Mutual Information (NMI): Measures mutual dependence
          between predicted and true cluster assignments.

5. Natural Language Processing (NLP) Tasks
- Task: Sentiment Analysis (Binary/Multiclass Classification)
    - Example: Predict sentiment (positive, neutral, negative) of a product
      review.
    - Metrics:
        - Accuracy, Precision, Recall, F1-Score: As in classification tasks.
        - Perplexity: For language models, measures how well the model predicts
          a sample (lower is better).

- Task: Machine Translation
    - Example: Translate text from English to French.
    - Metrics:
        - BLEU (Bilingual Evaluation Understudy): Measures n-gram overlap
          between predicted and reference translations.
        - ROUGE: Similar to BLEU but also considers recall (used in
          summarization).

6. Computer Vision Tasks
- Task: Object Detection
    - Example: Detect and label objects in images (e.g., cars, pedestrians).
    - Metrics:
        - Intersection over Union (IoU): Measures overlap between predicted and
          ground truth bounding boxes.
        - Mean Average Precision (mAP): Averaged precision over multiple IoU
          thresholds (evaluates detection accuracy).

- Task: Image Segmentation
    - Example: Segment tumor regions in MRI scans.
    - Metrics:
        - Dice Coefficient: Measures overlap between predicted and true segments
          (sensitive to small errors).
        - IoU: Similar to Dice but penalizes over-segmentation.

7. Recommendation Systems
- Task: Product Recommendation
    - Example: Recommend movies to users based on their past preferences.
    - Metrics:
        - Precision@k, Recall@k: Similar to ranking metrics.
        - Hit Rate: Fraction of users for whom the relevant item appears in the
          recommendation list.
        - Coverage: Fraction of items recommended at least once (measures
          diversity).
        - Normalized Discounted Cumulative Gain (NDCG): Evaluates ranking
          quality.

8. Time Series Forecasting
- Task: Predict Future Trends
    - Example: Forecast stock prices or energy consumption.
    - Metrics:
        - MSE, MAE, RMSE: As in regression.
        - Mean Absolute Scaled Error (MASE): Scaled version of MAE that accounts
          for seasonality.
        - Symmetric Mean Absolute Percentage Error (SMAPE): A scale-independent
          metric for percentage errors.

