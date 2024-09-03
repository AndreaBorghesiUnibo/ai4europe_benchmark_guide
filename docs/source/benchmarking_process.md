# Benchmarking 

We define a ***benchmark*** as _the execution of an algorithm using a specific
hardware platform and under a precise configuration of hyperparameters_ (and fed
with specific input data), _while measuring some interesting metrics_.

Under this definition, running a benchmark means selecting a particular AI asset
and executing it on a specific HW device and hyperparameter configurations;
multiple benchmarking runs are needed to explore multiple HW resources and/or
configurations. The identification of the hyperparameters and targets to be
metrics are crucial for effective execution of a benchmarking suite. 

(bench_pre)=
## Preliminaries

The definition of the execution of an AI asset varies by domain. 
For instance, in the case of DNN it might refer to the training phase. In this
case, the set of hyperparameters range from the DNN topology (e.g., overall
structure of the neural network number of layers, number of nodes per layer) to
the parameters governing the DNN’s training (from the learning rate to the batch
size).

To ensure reproducible benchmarks through a systematic approach, a series of
preliminary questions to guide the benchmarking process need to be addressed.
- Which [HW resources](bench_hw) are to be used? 
    - What is the pool of devices and HW architectures available?
      High-performance and cloud computing, consumer-grade machines, embedded
systems, etc. 
    - This can be answered by taking into account the cost of the HW and the
      budget available to run the benchmarks. 
- If the AI asset’s behaviour is governed by
  [hyperparameters](bench_hp), which are the ones to be explored? How to
choose the values of such hyperparameters? 
- A vast range of potentially interesting [metrics](bench_metrics) could be
  measured – determining the useful ones depending on the scope of the
benchmark. 
    - What is the cost associated with measuring the targets? 
- Does the input [data](bench_data) feed to the AI asset impact the metrics we
  are interested in?  Some metrics might be impacted while others might be
agnostic to the input.


(bench_workflow)=
## Workflow

The benchmark workflow is composed by the following steps: 

(bench_asset)=
### AI Asset Selection
As a starting point, the AI asset to be benchmarked will have to be selected.
- Selecting an AI asset involves choosing a specific AI algorithm, such as an
  optimization model (e.g., constraint programming), an agent-based simulation,
or an ML model. For ML models, distinguish between training and inference, as
they are different AI assets. While this might seem trivial, it's crucial,
especially for non-experts, to carefully consider and clarify the algorithm of
interest to avoid confusion.

After having chose the target AI asset, it's important to provide input and
output data specifications: 
- Input Data Format - clearly specify the size and structure of the input data
  the AI software will receive.
- Output Data Format - define the expected format and structure of the output
  data the AI software will produce.

(bench_hw)=
### Hardware Resources
The pool of HW resources to be benchmarked has to be chosen, according to the
available budget and/or HW already at its own disposal.
- Choose the most suitable hardware platform for the task, such as HPC or cloud
  resources, GPU servers, compute servers, embedded devices, or IoT devices.
- The monetary budget determines the number of runs on different hardware
  platforms, considering the costs and pricing schemes (e.g., purchasing devices
for embedded systems, or calculating HPC costs based on CPU usage and duration).

(bench_hp)=
### Hyperparameters
According to the AI asset, a selection of the hyperparameters of interest must
be made.
- This can be done only by someone with sufficient knowledge about the AI asset
  to be benchmarked. 
    - Some examples: the parameters governing the agents’ behaviours in
      Agent-Based models; the number of training epochs, learning rate, number
of layers, etc., in the case of DNN training; the number of scenarios to be
considered in stochastic optimization models; the number of threads in parallel
applications, and so on.
- Additionally, a search strategy over the hyperparameters space must be
  defined, especially if multiple hyperparameters with many possible values have
to be explored
    - The issue is that the hyperparameters space tends to get very large pretty
      quickly and thus exploring it becomes a computationally challenging task,
hence the need to have an efficient search strategy able to balance exploration
and exploitation.
    - In general, common approaches are random search, grid search, Latin
      Hypercube Sampling
([LHS](https://www.jstor.org/stable/1268522?origin=crossref)), Bayesian
Optimization
([BO](https://www.sciencedirect.com/science/article/pii/S1674862X19300047)),
genetic algorithms
([GA](https://www.sciencedirect.com/science/article/pii/S1674862X19300047)),
etc.

(bench_data)=
### Datasets
If the AI asset requires data to be executed, it must be provided (for instance,
training samples for training Machine Learning models or input instances to
solve optimization problems).  Select or create appropriate datasets that
reflect the real-world scenarios and challenges relevant to your AI system or
task
- It's crucial to ensure the datasets are diverse, representative, and cover a
  wide range of possible inputs to obtain reliable benchmarking results.
- The data must be detailed described using meta-data. To ensure full
  reproducibility it is better to follow a precise
[checklist](./reproducibility_checklist.md).
- Check as well whether the available data is annotated (and whether the
  annotation process is well-documented, e.g., to better identify possible
sources of bias).A
- Consider the amount of data required to obtain trustworthy benchmarking
  results

(bench_metrics)=
### Metrics
As a final choice, the metrics to be measured must be decided, again according
to what can be relevant to the AI asset in question
- The choice of the metrics depends as well on the HW platform selected, as a
  metric that can be measured on an embedded device could be much harder
- See [Metrics](./metrics.md) for more details 

(bench_out)=
### Benchmark Output
Define the expected output format for the benchmarking process to ensure clarity
and ease of integration into downstream tasks (e.g., automated HW device
selection for AI algorithms). The output could be a simple CSV file with
accompanying metadata.

The output of the benchmark workflow can assume different shapes. The simplest
is the form of a data set (or data frame) organised in a structured format. The
first choice to be made is how to organise the results: 
- One data set per AI asset 
    - PROS: Simplifies the management and storage of the results, facilitating the
      retrieval for reuse
    - CONS: It is relatively more complicated to add new benchmarking results in
      case the same AI asset is run on a different HW platform at a later date
- Multiple data sets per asset (e.g., a different data set for each different HW
  resource where the asset has been benchmarked)
    - PROS: Adding a new resource simply means adding a new data set -- without
      interfering with already existing ones
    - CONS: Slightly more complicated management; e.g., different data sets must
      share the same structure (format) to guarantee compatibility 
- See [Output](./output.md) for more details 


