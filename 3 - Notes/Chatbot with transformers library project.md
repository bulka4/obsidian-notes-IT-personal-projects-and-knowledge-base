Tags: [[_My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
In this project, we:
- Create a chatbot using the `transformers` library. 
- Test different models, how they response to questions.
- Use CPUs to run those chatbots (tried to use a GPU, there is a code for that, but we didn't have NVIDIA drivers prepared to do so).

Some models which we were testing takes huge amount of time to generate a response and we were cancelling the generation of a response before we got it.

There was no model which would give reasonable answers and run quickly on an average CPU.
# Code repository
The repository with code for this project is here - [github.com](https://github.com/bulka4/chatbot_with_transformers_library).
# Environment preparation to run the code
- Install pytorch with cuda (maybe cuda is not needed):
```
pip3 install torch torchvision torchaudio --index-url [https://download.pytorch.org/whl/cu118](https://download.pytorch.org/whl/cu118)
```
- for using the ‘TheBloke/sqlcoder-GPTQ’ model:
```
pip3 install auto-gptq --extra-index-url https://huggingface.github.io/autogptq-index/whl/cu118/
```
- Install transformers:
```
pip install git+https://github.com/huggingface/transformers.git@main
```
- Install optimum:
```
pip install --upgrade optimum
```
# Code notes
- In order to get rid of the error `addmm_impl_cpu_" not implemented for 'Half`, we need to use this argument in this function:
```
	AutoModelForCausalLM.from_pretrained(
		torch_dtype=torch.float32
	)
```
- models are saved in the `C:/users/<username>/.cache/huggingface/hub`