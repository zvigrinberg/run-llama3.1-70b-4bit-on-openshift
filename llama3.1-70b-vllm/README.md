# Running Llama3.1-70b With 4 bits AWQ - Using vLLM inference

## Procedure
1. Create namespace
```shell
oc new-project 70b-awq
```
2. Deploy the Model
```shell
oc create -f deployment.yaml
```

**Note: You can reduce the `tensor-parallel-size` in the [`deployment.yaml`](./deployment.yaml) to value of 2 ( and also the request and limits' gpus to 2), so it will be less memory intensive,
and I also experienced more quick response using this configuration.** 