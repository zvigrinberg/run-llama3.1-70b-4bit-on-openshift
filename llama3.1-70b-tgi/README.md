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

