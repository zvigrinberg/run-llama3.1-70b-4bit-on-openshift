# Running Llama3.1-70b With 4 bits AWQ - Using HuggingFace TGI

## Procedure
1. Create namespace
```shell
oc new-project 70b-awq-tgi
```
2. Create Hugging Face API KEY ( you can obtain your key from [here](https://huggingface.co/docs/hub/security-tokens) )
```shell
 oc create secret generic hf-token-secret --from-literal hf-token=your_secret_hf_token_goes_here
```

3. Deploy the Model
```shell
oc create -f deployment.yaml
```

4. Example to run the model in POST RESTful API
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