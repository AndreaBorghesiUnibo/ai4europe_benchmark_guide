# BonsAPPs Benchmarking Service


BonsAPPs is a service layer offering a series of modular services — such as
experimentation, model compression, optimisation, benchmarking, and deployment
on hardware and security that will increase AI usage among enterprises and small
and medium-sized enterprises (SMEs), which currently lack internal innovation
capabilities.

![BonsAPPs](./img/bonsapps.png)

 This platform primarily supports SMEs and non-tech users, helping them adopt
and optimize AI-driven solutions tailored to edge applications like healthcare,
robotics, and manufacturing.

(bonsapps_how)=
## How it works

The [benchmarking](https://bonsapps.eu/how-it-works/) component specifically
aids in assessing and comparing AI models in various edge scenarios. By
providing structured, reusable tools and resources, BonsAPPs simplifies the
model testing phase, allowing developers to evaluate AI performance under
real-world constraints like low latency and power requirements. This setup
fosters accessible, efficient AI model deployment, catering to sectors with
strict operational demands and advancing Europe’s AI adoption and
competitiveness in edge computing.

### Features

The model evaluation Allows thorough assessment of AI models across key metrics,
including latency, accuracy, and resource consumption.  The focus is on
edge-specific performance metrics, that is benchmarks models based on edge
deployment needs, including processing speed, energy efficiency, and memory
usage, making it ideal for applications in fields like healthcare and robotics.

In terms of deployment scenarios, BonsAPPs offers pre-configured benchmarking
environments that replicate typical edge computing setups, giving accurate
insights into real-world model performance.

### Supported Metrics

- Accuracy: Evaluates the predictive correctness of models.
- Latency: Measures the response time of the model when deployed at the edge.
- Resource Consumption: Tracks CPU, GPU, and memory usage, allowing users to
  optimize models for devices with limited computational resources.

### User Workflow

1. Upload Model: Users can upload models directly to the BonsAPPs platform or
  select one from the Bonseyes AI Marketplace.
2. Select Benchmark Parameters: Configure benchmarks based on desired edge
  application requirements, such as latency thresholds, target devices, or
performance metrics.
3. Run Benchmark: Initiates the benchmarking process, utilizing the BonsAPPs
  infrastructure to perform tests under pre-set configurations.
4. Review Results: Provides a comprehensive report on model performance,
  highlighting strengths and areas for improvement in the context of edge
computing needs.

### Integration with Bonseyes AI Marketplace

The benchmarking component is fully integrated with the Bonseyes AI Marketplace
(BMP), allowing users to benchmark models available in the marketplace or those
uploaded by third parties. This integration streamlines model selection,
testing, and deployment processes.


(bonsapps_doc)=
## Documentation

The documentation and the developers guidelines can be found at the following
link: [docs](https://bonseyes.gitlab.io/bonseyes-cli/pages/user_guides/ai_app_index.html)

Below, a snippet of example usage is provided. This structure highlights the
features and workflow of the BonsAPPs benchmarking component, tailored for
developers looking to assess and optimize AI models for real-world edge
computing applications.

```python
# Sample code snippet for initiating a benchmarking session on BonsAPPs platform

import bonsapps

# Load model from BMP
model = bonsapps.load_model("edge_model_01")

# Set benchmarking parameters
benchmark_params = {
    "latency": "<10ms",
    "accuracy_threshold": "95%",
    "device": "Edge-TPU"
}

# Run benchmark
results = bonsapps.run_benchmark(model, benchmark_params)

# Display results
print(results)
```
