# Reproducibility in Benchmarking: Challenges and Opportunities 

Reproducibility refers to achieving consistent outcomes when repeating
experiments. While definitions vary, ACM proposed unifying key terms:
repeatability (consistent results within the same team and setup),
reproducibility (consistent results across different teams under similar
conditions), and replicability (comparable results under different conditions or
equipment).

Many AI studies have been found to be irreproducible, primarily due to
methodological flaws and insufficient consideration of the variability
introduced by algorithms or their implementations. A significant contributing
factor is the absence of a theoretical framework that connects experimental
design choices to their potential impact on research conclusions. Without such a
framework, it becomes challenging for practitioners and researchers to
critically assess experimental results and clearly articulate the limitations of
their studies. This gap also complicates the ability of independent researchers
to systematically identify and attribute the causes of reproducibility failures.
See [Gundersen2022](https://arxiv.org/abs/2204.07610/) for more information
about reproducibility challenges.

Integrity and trust in scientific research heavily depend on the reproducibility
of results. In computer science, many scientific conferences and journals have
recognized the importance of reproducibility and implemented initiatives to
strengthen it. These initiatives involve not only the traditional peer-review
process but also an additional reproducibility review. This extra layer ensures
that the computational experiments presented in research papers can be
independently replicated and validated.

## Challenges in Reproducibility

Replicating computational experiments poses numerous challenges, particularly
those related to hardware resources. One of the foremost challenges is
determining how and where the necessary hardware resources for reproducibility
testing are provided. Practical experience in reproducibility efforts highlights
the critical need for both authors and reproducibility reviewers to have access
to a shared computational infrastructure. Such shared infrastructure simplifies
the process of configuring and executing computational artifacts, reducing the
technical and logistical burdens often associated with reproducibility efforts.

## Existing Solutions and Limitations

Public initiatives like **ChameleonCloud** in the United States have emerged to
support open science and reproducibility efforts. ChameleonCloud has played a
significant role in providing computational resources for reproducibility
evaluations at major scientific conferences, such as ICPP23 and SC23. These
evaluations have substantial hardware demands:

- **ICPP23**: 15 submissions assessed, requiring a total of 150–270 hours of CPU
  time per submission.
- **SC23**: 61 submissions assessed, collectively consuming over 20,000 CPU
  hours.

Platforms like ChameleonCloud are designed to balance the needs of large-scale
experiments and hardware diversity. They offer resources ranging from various
GPU technologies and FPGAs to advanced storage hierarchies (HDDs, SSDs, and
NVRAM) and diverse processor architectures, including x86 and ARM. However,
certain circumstances limit the full utilization of such platforms for
reproducibility purposes:

1. **Resource Scale**: Submissions requiring massive computational resources
   (e.g., over 10,000 cores) may exceed the capacity of shared platforms.
2. **Specialized Hardware Requirements**: Unique configurations or access to
   supercomputers often fall outside the scope of general-purpose
reproducibility platforms.
3. **Complex Configurations**: Highly specialized SLURM setups or other advanced
   system configurations may demand impractical levels of system administration.

These limitations are exacerbated at large-scale conferences, such as **ECAI**,
where over 1,000 papers are accepted annually. Each paper may require
reproducibility testing, creating immense challenges in terms of both scale and
hardware diversity.

## The Path Forward: Federated Computing Infrastructures

To address these challenges, the benchmarking community must adopt federated
computing infrastructures that integrate multiple hardware providers. These
infrastructures should be designed to:

1. **Accommodate Diverse Hardware Needs**: Ensure access to specialized and
   varied hardware configurations, including GPUs, FPGAs, and non-x86
architectures.
2. **Support Large-Scale Evaluations**: Provide scalable solutions capable of
   handling thousands of reproducibility assessments efficiently.
3. **Facilitate Sharing Policies**: Develop policies and frameworks for resource
   sharing that align with the needs of researchers, authors, and reviewers.
4. **Enable Flexible Business Models**: Incorporate diverse funding and
   operational models to support a wide range of reproducibility efforts.

By leveraging federated infrastructures, the reproducibility process can become
more inclusive and adaptable, ensuring that computational experiments are
accessible, verifiable, and trustworthy across diverse research domains and
hardware ecosystems.

## Reproducible Benchmarks in the AIoD Platform

[REANA](https://reana.io/)(Reproducible Analyses) is an open-source
computational platform designed to enhance the reproducibility of research data
analyses by automating and managing computational workflows. It supports popular
workflow languages like CWL (Common Workflow Language) and YAML, enabling users
to define and execute workflows across diverse computing infrastructures, such
as local machines, HPC clusters, and cloud platforms. REANA emphasizes
portability, scalability, and collaboration, simplifying the reproduction and
sharing of analyses while
promoting knowledge exchange within the research community.

For AI research and development, REANA provides a structured framework to manage
and reproduce computational experiments as workflows. In a field where
reproducibility and transparency are critical, REANA enables the seamless
creation, execution, and sharing of complex AI workflows, such as machine
learning pipelines, model training, and experiment configurations. Its robust
support for workflow automation ensures consistency across environments, while
its collaborative features facilitate peer review and the sharing of
reproducible experiments. By addressing key challenges in reproducibility, REANA
helps accelerate innovation and foster trust in AI research.

In AI4Europe, REANA is used to facilitate the creation of reproducible
benchmarks through ad hoc services. The Research and Innovation AI Lab
([RAIL](https://rail.aiod.eu/)) is an example of a specific service built on top
of the AI on Demand platform. RAIL is a tool that enables AI practitioners to
explore and use AI assets directly in AIoD in a lightweight and flexible way. It
is a web application consisting of three parts: a frontend implemented in the
Angular 2 framework, a backend implemented in FastAPI, and a NoSQL database
MongoDB. RAIL allows AI practitioners to work with AIoD AI assets, explore,
search, compare, and create experiments that are reproducible and reusable. RAIL
relies on REANA as workflow execution engine.

### REANA as a Reproducibility Tool

REANA is specifically designed to address reproducibility challenges in
computational research. It provides a robust framework for running, sharing, and
verifying data analysis workflows. Below, I explain its features and the steps
to use REANA for running reproducible benchmarks, with a focus on benchmarking
insights.

Workflows in REANA are defined using standard languages like CWL, Yadage,
Snakemake, or REANA Serial.  These definitions include all steps, dependencies,
and parameters, ensuring workflows are portable and consistent.
REANA runs workflows inside Docker containers.  Containers encapsulate all
software dependencies, ensuring the same environment is used across different
systems and runs.

REANA allows input datasets to be versioned and stored in a controlled manner.
Supports integration with external storage systems (e.g., S3, HTTP servers, or
databases).

In terms of version control, workflow definitions and configurations can be
stored in Git, allowing users to track changes and revert to previous versions.
This enables reproducibility across different versions of the workflow or
datasets.
REANA runs workflows on Kubernetes clusters, ensuring consistent performance
regardless of the computational resources available locally; this aspect makes
large-scale benchmarking feasible by distributing tasks across multiple nodes,
increasing scalability.

REANA stores logs, outputs, and metadata for each run.
It provides a unique identifier for every workflow execution, ensuring
results can be traced back to the exact configuration and dataset used.
Finally, workflows and configurations can be easily exported and shared with
collaborators, enabling independent verification of results.

## Data Reproducibility Checklist

Datasets are among the potential outcome of a benchmarking activity. For the
sake of trustworthiness, the provider of the data should declare a series of
metadata accompanying any dataset upon its publication.

In practice, dataset providers should undergo the following checklist, ideally
providing the metadata required by each item in the list:
- ***Data Provenance***: it is crucial to include information about the dataset's
  origin, such as its source, data collection methods, and the timeframe in
which the data was collected. This metadata enables users to assess the
reliability and credibility of the dataset.
- ***Data Collection Methods***: detailed documentation on the procedures used to
  collect the data, including any instruments or tools employed, allows users to
evaluate the accuracy and potential biases present in the dataset.
- ***Sampling Techniques***: if the dataset is a sample of a larger population, it
  would be helpful to describe the sampling methods used, such as random
sampling, stratified sampling, or convenience sampling. This information would
assist users in understanding the representativeness of the data.
- ***Data Preprocessing***: including a description of any preprocessing steps applied
  to the data, such as cleaning, filtering, or transformation, serve to help
users understand how the raw data was processed and any potential impact on the
final dataset.
- ***Variables and Definitions***: clear definitions and descriptions of the variables
  present in the dataset, including their units of measurement, data types, and
possible values, would enable users to correctly interpret and analyze the data.
- ***Missing Data Handling***: the method used to treat missing or incomplete data
  (whether through imputation, exclusion, or other methods) needs to be clearly
stated. This information let users inspect any potential biases or
limitations resulting from missing data.
- ***Data Quality Measures***: it is important to document the metrics used to measure
  quality of the dataset (e.g., accuracy, completeness, consistency); this
allows to assess the reliability of the data.
- ***Privacy and Ethical Considerations***: it is paramount to provide the information
  regarding any privacy or ethical considerations associated with the dataset,
such as anonymization techniques used, consent procedures, or adherence to data
protection regulations. This serves to more easily ensure compliance with legal
and ethical standards.
- ***Versioning and Updates***: If the dataset undergoes changes or updates, the
  version information and a changelog to track modifications need to be
included. This helps understanding the evolution of the data over time (and to
roughly assess if any compatibility issue has to be taken into account).
- ***Licensing and Usage Terms***: stating the licensing terms of the dataset is
  fundamental, as to indicate users' rights and obligations when working with
the data; any limitation on data usage, redistribution or modification needs to
be included.

