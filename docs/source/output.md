# Benchmark Output

The benchmark workflow output can vary in form.  The simplest format is a data
frame organized in a structured manner, particularly in a _tabular_ format.

The recommended solution is to have ***multiple data sets for each AI asset, and
one set for each HW resource***.
The output of the benchmarking process then is a data set identified as
  ```<asset_name>_<HW>``` where ```<asset_name>``` indicates the AI asset and
```<HW>``` indicates the HW device.

This is an example of benchmarking results, for a specific AI asset on a single
HW resource, assuming that:
- The AI asset require data as input (```input_instance```).
- The AI assets has ```N``` hyperparameters that can be configured (```HP#i```).
- ```M``` metrics are expected to be measured for each run of the AI asset.

|Input Data |HP#1 |HP#2 | ... |HP#N |Metric#1 |Metric#2 | ... |Metric#M |
|-----------|-----|-----|-----|-----|-------- |---------|-----|---------|
|Instance#1 |val1 |val2 | ... |val3 |   <?>   |   <?>   | ... |   <?>   |
|Instance#2 |val1 |val2 | ... |val3 |   <?>   |   <?>   | ... |   <?>   |
|    ...    | ... | ... | ... | ... |   ...   |   ...   | ... |   ...   |
|Instance#I |val1 |val2 | ... |val3 |   <?>   |   <?>   | ... |   <?>   |
|Instance#1 |val4 |val5 | ... |val6 |   <?>   |   <?>   | ... |   <?>   |
|Instance#2 |val4 |val5 | ... |val6 |   <?>   |   <?>   | ... |   <?>   |
|    ...    | ... | ... | ... | ... |   ...   |   ...   | ... |   ...   |
|Instance#I |val4 |val5 | ... |val6 |   <?>   |   <?>   | ... |   <?>   |
|    ...    | ... | ... | ... | ... |   ...   |   ...   | ... |   ...   |

Each row corresponds to the execution of the AI asset on a specific HW
  resource, with a particular combination of hyperparameter values (from
```HP#1``` to ```HP#N```) and fed with a particular input instance; the
remaining columns (from ```Metric#1``` to ```Metric#M```) indicate the
measurements obtained for the specific run.

The column relative to the input instance might be excluded if the metrics of
interest are not impacted by the input fed to the AI asset.  To obtain a
machine-readable representation, if there are no particular requirements, a very
basic data format such as Comma-Separated Values (CSV) file can be used.

## Metadata Companion 

To ensure reusable and understandable benchmark results, the output of the
benchmark process should be accompanied by a ***metadata companion***.

Metadata Requirement:
- Include all necessary corollary information for benchmarks to be reusable
  and understandable post-generation.
- Details to provide:
    - Specifications of the executed AI asset.
    - Hardware device used for the experiment.
    - Hyperparameter values affecting behavior.
    - Measured metrics.

Implementation:
- Provide metadata describing the benchmark and the structure of the
  corresponding dataset.
- Each data set should be accompanied by a JSON-like file descriptor

### Metadata Example

Assuming that we have run an AI asset ```<asset_name>```  using the HW platform
```<HW>```  the name of the descriptor will be ```<asset_name>_<HW>.json```.  An
example of descriptor is the following:

```
{
    name: <alg_name>, 
    HW_ID: <hw_name>, 
    input: {
        type: <input_type>,
        required: <true/false>, 
        properties: { ... }
    }
    hyperparams: [ 
    {
        hp#1_ID: <ID>,
        type: <TYPE>, 
        properties: { lb: <LB>, ub: <UB> }
    }, 
    {
        hp#2_ID: <ID>, 
        type: <TYPE>, 
        properties: { lb: <LB>, ub: <UB> }
    },
    ...   
    {
        hp#N_ID: <ID>, 
        type: <TYPE>, 
        properties: { lb: <LB>, ub: <UB> }
    }], 
	targets: [ 
    {
        metric#1_ID: <ID>, 
        type: <TYPE>, 
        properties”: { lb: <LB>, ub: <UB> }
    }, 
    {
        metric#2_ID: <ID>, 
        type: <TYPE>, 
        properties”: { lb: <LB>, ub: <UB> }
    },
    ... 
    {
        metric#M_ID: <ID>, 
        type: <TYPE>, 
        properties”: { lb: <LB>, ub: <UB> }
    }]
}
```

The descriptor starts with the name of the AI asset (```<alg_name>```) and the
HW resource (```<HW_name>```) where it was executed.  The asset is run on the HW
device with varying configurations of hyperparameters 

The first section reports the input expected by the AI asset (```“input”```).
The input is extremely dependent on the asset (e.g., images, text, tabular data,
vectors of real numbers, etc). The metadata descriptor then list all
hyperparameters that can be used to configure the AI asset (```hyperparams```)
Hyperparameters have an identifier and they are characterized by details such as
the type (string, integer, float, etc) and the lower and upper bounds
(```“LB”/“UB”```), with the latter two being optional.  

The descriptor then reports the list of the metrics measured during the
execution of the AI asset, structured similarly to the hyperparameters list
(```metrics```).



