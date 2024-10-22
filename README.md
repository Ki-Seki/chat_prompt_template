# Chat Prompt Templates

Collection of Basic Prompt Templates for Various Chat LLMs | Chat LLM 的基础提示模板集合

**Motivation**: The basic prompt template will significantly affect the effectiveness of instruction following. Models of different architectures may use different prompt templates during training. However, at present, these templates can be challenging to locate; sometimes they are embedded in example codes, hidden within GitHub issues, or occasionally found in official blogs...

**动机**: 基础提示模板会显著影响指令跟随的效果。不同架构的模型在训练时可能使用不同的提示模板。然而，目前这些模板往往难以找到；有时它们嵌入在示例代码中，有时隐藏在 GitHub 问题中，有时偶尔在官方博客中发现...

> [!Note]
> [Chat Markup Language](https://github.com/MicrosoftDocs/azure-docs/blob/main/articles/ai-services/openai/includes/chat-markup-language.md) is the mainstream, eg. [HuggingFace's transformers](https://github.com/huggingface/transformers/blob/76a33a10923ccc1074917f6b6a1e719e626b7dc9/src/transformers/tokenization_utils_base.py#L1847-L1865), [OpenAI's tiktoken](https://github.com/openai/tiktoken/blob/db5bda9fc93b3171db6c4afea329394e6b6d31ca/README.md?plain=1#L91-L92).
>
> [Chat Markup Language](https://github.com/MicrosoftDocs/azure-docs/blob/main/articles/ai-services/openai/includes/chat-markup-language.md) 是主流格式，例如 [HuggingFace's transformers](https://github.com/huggingface/transformers/blob/76a33a10923ccc1074917f6b6a1e719e626b7dc9/src/transformers/tokenization_utils_base.py#L1847-L1865), [OpenAI's tiktoken](https://github.com/openai/tiktoken/blob/db5bda9fc93b3171db6c4afea329394e6b6d31ca/README.md?plain=1#L91-L92)。

(Alphabetical order by architecture)

（按架构名称的字典序排列）

## Baichuan Prompt Template

```python
template = """<reserved_195>{query}<reserved_196>"""
```

* References:
  * https://huggingface.co/baichuan-inc/Baichuan2-13B-Chat/blob/main/generation_config.json
  * https://github.com/baichuan-inc/Baichuan2/issues/227
* Model Site: https://huggingface.co/baichuan-inc

## ChatGLM3 Prompt Template

```python
template = """<|system|>
You are ChatGLM3, a large language model trained by Zhipu.AI. Follow the user's instructions carefully. Respond using markdown.
<|user|>
{query}
<|assistant|>
"""
```

* References:
  * https://github.com/THUDM/ChatGLM3/blob/main/PROMPT_en.md
* Model Site: https://huggingface.co/THUDM/chatglm3-6b
* Note: If no special template is provided, the instruction following still works very well.

## Gemma Prompt Template

```python
template = """<bos><start_of_turn>user
{query}<end_of_turn>
<start_of_turn>model"""
```

* References:
  * https://huggingface.co/google/gemma-2b-it
* Model Site: https://huggingface.co/google/gemma-2b-it
* Note: Gemma does not have a system field

## InternLM2 Prompt Template

```python
template = """<|im_start|>system
You are a helpful assistant.<|im_end|>
<|im_start|>user
{query}<|im_end|>
<|im_start|>assistant
"""
```

* References:
  * https://huggingface.co/internlm/internlm-chat-20b/blob/main/modeling_internlm.py
* Model Site: https://huggingface.co/internlm/internlm-chat-20b

## LLaMA2 Prompt Template

```python
template = """<s>[INST] <<SYS>>
You are a helpful, respectful and honest assistant.
<</SYS>> {query} [/INST] Sure, I'd be happy to help. Here is the answer:"""
```

* References:
  * https://huggingface.co/blog/llama2#how-to-prompt-llama-2
  * https://www.reddit.com/r/LocalLLaMA/comments/16x4733/how_to_stop_llama_2_13b_from_starting_each/
* Model Site: https://huggingface.co/meta-llama/Llama-2-13b-chat
* Note: `Sure, I'd be happy to help. Here is the answer:` avoids verbose model outputs.

## Phi-2 Prompt Template

```python
template = """Instruct: {query}\nOutput:"""
# or template = """Alice: {query}\nBob:"""
```

* References:
  * https://huggingface.co/microsoft/phi-2
* Model Site: https://huggingface.co/microsoft/phi-2

## Qwen Prompt Template

```python
template = """<|im_start|>system
You are a helpful assistant.<|im_end|>
<|im_start|>user
{query}<|im_end|>
<|im_start|>assistant
"""
```

* References:
  * https://github.com/QwenLM/Qwen/blob/5aa84bdfd3237b37f01bc88cd49b3279b9a71d0b/examples/vllm_wrapper.py#L32
  * https://github.com/vllm-project/vllm/issues/901
* Model Site: https://huggingface.co/Qwen/Qwen-7B-Chat
* Note: Qwen will output special tokens like `<|im_end|>` or `<|endoftext|>`, you can remove texts after them or use `stop` parameter like:

```python
# Using vLLM interface
payload = json.dumps({
    "prompt": query,
    "n": 1,
    "stop": ["<|endoftext|>", "<|im_end|>"],
})

```

## Yi Prompt Template

```python
template = """<|im_start|>system
{system_message}<|im_end|>
<|im_start|>user
{prompt}<|im_end|>
<|im_start|>assistant"""
```

* References:
  * https://github.com/01-ai/Yi/pull/177/files
  * https://huggingface.co/01-ai/Yi-34B-Chat/blob/main/tokenizer_config.json#L60
* Model Site: https://huggingface.co/01-ai/Yi-34B-Chat

## Meta Llama3 Instruct Prompt Template

```python
template = """<|begin_of_text|><|start_header_id|>system<|end_header_id|>

You are a helpful AI assistant.<|eot_id|><|start_header_id|>user<|end_header_id|>

{query}<|eot_id|><|start_header_id|>assistant<|end_header_id|>
"""
```

* References: https://llama.meta.com/docs/model-cards-and-prompt-formats/meta-llama-3/#llama-3-instruct
* Model Site: https://huggingface.co/meta-llama/Meta-Llama-3.1-8B-Instruct
* Note: 
  * Newlines (0x0A) are part of the prompt format, for clarity in the examples, they have been represented as actual new lines.
  * The model expects the assistant header at the end of the prompt to start completing it.

## XXX Prompt Template

```python
template = 
```

* References:
* Model Site: 
* Note: 
