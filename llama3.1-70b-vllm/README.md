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

3. Example to run the model in POST RESTful API
```shell
export LLM_SERVICE_URL=http://$(oc get route -n 70b-awq -o=jsonpath='{...host}' | awk '{print $1}')
curl -X POST -H "Content-Type: application/json" ${LLM_SERVICE_URL}/v1/chat/completions \
  -d '{ "model": "hugging-quants/Meta-Llama-3.1-70B-Instruct-AWQ-INT4", \                                                                  
        "messages": [{"role": "user", "content": "What is Openshift?"}], \
        "temperature": 0, \ 
        "top_p": 0.01, \ 
        "max_tokens": 1024, \ 
        "stream": false}'
```

**Note: You can enlarge the `tensor-parallel-size` in the [`deployment.yaml`](./deployment.yaml) to value of 4 ( and also the request and limits' gpus to 4), so it increase redundancy and free memory margins ( especially KV Cache memory),
But personally I also experienced more quicker response using 2 GPU replicas, so this is better also in terms of memory usage and that you don't really need more than this probably** 
