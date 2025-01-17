# Why Benchmarking? 

A robust _benchmarking strategy_ for AI involves a systematic approach to
discovering, mapping, evaluating, and comparing AI models, algorithms, and
systems against emerging industry standards and research developments. This kind
on initiative aims to gain insights into AI technologies' performance,
efficiency, and effectiveness, identifying areas for improvement.
By implementing such strategic initiative, organizations can better understand
and enhance their AI technologies' performance across diverse and evolving
hardware environments.

## Motivations

Comparing AI assets and results across research papers and techniques is needed
to ***fairly*** compare assets.  Assessing the performance of a variety of AI
models with the goal of selecting the best model for a specific task can be only
performed if the corresponding benchmarks have been executed.  Additionally,
benchmarking activities provide valuable insights, driving improvements and
informed decision-making to enhance AI system performance and competitiveness.

## Relevance

As AI becomes more prevalent across various domains,
  understanding AI tools and algorithms' behavior on different computing
resources is crucial. Benchmarking characterizes how AI
algorithms perform across various hardware platforms and configurations,
offering a comprehensive understanding of their behavior.

The effort is complicated by AI assets' variability in behavior based on
numerous hyperparameters and performance differences on heterogeneous hardware
devices. A possible way out is using AI itself to build and train ML models;
the datasets obtained through benchmarking can be used used to guide the
creation of new models. This concept is often named
[AutoML](https://www.automl.org/automl/).

## Challenges

AI applications now run across a wide range of hardware, from cloud and
high-performance computing (HPC) resources to embedded and low-power systems;
this requires to evaluate AI models over a wider spectrum of hardware resources.
Additionally, there has been a remarkable device diversification: the increasing
capacity and performance of embedded devices enable them to perform
sophisticated AI tasks, including new applications in computer vision and speech
recognition.

The availability of open-source data for training AI models (especially
data-driven models such as ML and DL approaches) is crucial. AI model training,
especially for tasks like computer vision and speech recognition, relies on
machine learning algorithms and extensive open-source datasets created by
researchers.

A very significant issue is posed by the lack of standardised and easy
benchmarking does not allow understanding when AI algorithms actually work.

### Task-specific Evaluations and Large-Language Models

As AI models continue to evolve, particularly with the rise of general-purpose
foundation models, task-specific evaluation poses unique challenges. The
variability in model behavior due to hyperparameters, heterogeneous hardware
performance, and preparation techniques makes benchmarking increasingly complex.
Large enterprises often focus on specific business tasks, such as classifying
customer calls, as highlighted in recent research. Some specific challenges are
illustrated below.

***Foundation models***  are designed to solve a wide range of tasks and require
specialized preparation techniques (e.g., prompt engineering,
retrieval-augmented generation) to perform optimally on specific tasks.  The
diversity in preparation methods and use cases introduces variability in
benchmarking results, complicating comparisons. Metrics such as accuracy on
standardized tasks (e.g., Massive Multitask Language Understanding (MMLU) or
text summarization) provide useful insights but often fail to capture the
performance nuances required for domain-specific applications.

Enterprises may benefit from designing purpose-specific tests tailored to their
unique requirements rather than relying solely on standardized evaluations.  For
example, benchmarking models for customer call classification might involve
metrics like classification accuracy, latency under deployment conditions, and
robustness to noisy input data.

To manage complexity, benchmarking efforts could limit the scope to a subset of
models tested in zero-shot scenarios.  However, given the significant
performance improvements achievable through task-specific preparation, such an
approach might overlook the model’s true potential.  Instead, prioritizing a
balance between zero-shot benchmarking and task-specific fine-tuning evaluations
ensures both generalizability and relevance.

Quantifying large foundation models to operate on standard hardware introduces
additional benchmarking variables, such as variations in speed, memory
requirements, and power usage.  Evaluations must account for these factors,
particularly when models are deployed in resource-constrained environments.



