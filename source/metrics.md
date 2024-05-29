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
asset and collect the perform the desired measurements. 
- This requires a non-trivial knowledge about the AI asset. 
- The complexity can be compounded by the need to write different wrappers for
  different HW platforms. 

If the task might arise ethical considerations and/or involves sensitive or
protected attributes, metrics accounting for fairness and bias in the AI
software should be considered. 

Another good choice s the selection of evaluation metrics that are easy to
interpret and understand, both for researchers and stakeholders who may not have
a technical background; this will help ensure that the evaluation results are
accessible and useful to a wider audience.

### Examples 
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
- Performance, which strongly depend on the underlying task (e.g., accuracy or
  similar metrics could be registered in the case of ML for classification)
- Performance per Watt: This metric combines raw performance with power and
  energy consumption measurements, focusing on the performance-to-energy ratio
of an AI model. Typically expressed as performance (e.g., accuracy, throughput)
per watt, it aims to maximize performance per watt for energy-efficient AI.
- Model Size (a measure of the size of AI models, such as the number of
  parameters)
- Carbon Footprint, for quantifying greenhouse gas emissions throughout the AI
  model's lifecycle, including manufacturing, training, and operation, using
metrics like CO2 equivalent emissions to assess environmental impact.



