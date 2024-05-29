# API

## Configuration files

| Endpoint                           | Request Type | Description                                                      |
|------------------------------------|--------------|------------------------------------------------------------------|
| `/configs`                         | GET          | Get list of available configuration files                        |
| `/configs/<algorithm>/<hw>`        | GET          | Retrieve the config (JSON) for the (algorithm, hw) couple        |
| `/configs/<algorithm>/<hw>`        | POST         | Upload/overwrite the config (JSON) for the (algorithm, hw) couple|
| `/configs/<algorithm>/<hw>`        | DELETE       | Delete the config (JSON) for the (algorithm, hw) couple          |
| `/configs/<algorithm>/<hw>/input`  | GET          | Retrieve the input-dependent config (JSON)                       |
| `/configs/<algorithm>/<hw>/input`  | POST         | Upload/overwrite the input-dependent config (JSON)               |
| `/configs/<algorithm>/<hw>/input`  | DELETE       | Delete the input-dependent config (JSON)                         |

## Datasets

| Endpoint                           | Request Type | Description                                                      |
|------------------------------------|--------------|------------------------------------------------------------------|
| `/datasets`                        | GET          | Get list of available datasets                                   |
| `/datasets/<algorithm>/<hw>`       | GET          | Retrieve the dataset (CSV) for the (algorithm, hw) couple        |
| `/datasets/<algorithm>/<hw>`       | POST         | Upload/overwrite the dataset (CSV) for the (algorithm, hw) couple|
| `/datasets/<algorithm>/<hw>`       | DELETE       | Delete the dataset (CSV) for the (algorithm, hw) couple          |
| `/datasets/<algorithm>/<hw>/input` | GET          | Retrieve the input-dependent dataset (CSV)                       |
| `/datasets/<algorithm>/<hw>/input` | POST         | Upload/overwrite the input-dependent dataset (CSV)               |
| `/datasets/<algorithm>/<hw>/input` | DELETE       | Delete the input-dependent dataset (CSV)                         |

## Hardware platforms (WIP)

| Endpoint                           | Request Type | Description                                                      |
|------------------------------------|--------------|------------------------------------------------------------------|
| `/hw_info`                         | GET          | Retrieve the CSV containing hardware platforms information        |
| `/hw_info`                         | POST         | Upload/overwrite the CSV containing hardware platforms information|
| `/hw_info`                         | DELETE       | Remove the CSV containing hardware platforms information          |

## Examples
### Response for `/config` (GET):
```
{
"configs":{
    "input-dependent":[
        {"algorithm":"anticipate", "hw":"pc"},
        {"algorithm":"contingency", "hw":"pc"},
        {"algorithm":"toyalgstr", "hw":"vm"},
        ...
    ],
    "input-independent":[
        {"algorithm":"3D-face-landmarks", "hw":"imx8m-nano"},
        {"algorithm":"3D-face-landmarks", "hw":"jetson-nano2"},
        {"algorithm":"3D-face-landmarks", "hw":"jetson-xav-agx"},
        { "algorithm":"3D-face-landmarks","hw":"rpi3"},
        ...
    ]
}
}
```

### cURL examples
#### Download (GET)
```bash
# configs
curl localhost:5333/configs/algo1/hw1
# datasets
curl localhost:5333/datasets/algo1/hw1
# HW info
curl localhost:5333/hw_info
```
#### Upload (POST)
```bash
# configs
curl -X POST -F 'file=@test_config.json' localhost:5333/configs/algo1/hw1
# datasets
curl -X POST -F 'file=@test_dataset.csv' localhost:5333/datasets/algo1/hw1
# HW info
curl -X POST -F 'file=@test_hw_info.csv' localhost:5333/hw_info
```
#### Delete (DELETE)
```bash
# configs
curl -X DELETE localhost:5333/configs/algo1/hw1
# datasets
curl -X DELETE localhost:5333/datasets/algo1/hw1
# HW info
curl -X DELETE localhost:5333/hw_info
```

