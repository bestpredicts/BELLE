# 1.5M中文数据集

**1.5M**中文数据集包含数个由BELLE项目产生的不同指令类型、不同领域的子集。


## 字段
各子集使用统一的字段
```
instruction: 指令
input: 输入
output: 输出
```

## 局限性和使用限制
我们要求开发者仅将我们开源的代码、数据、模型及后续衍生物用于研究目的，不得用于商业，以及其他会对社会带来危害的用途。

由于数据是由*ChatGPT*生成的，未经严格验证，在事实性和其他方面还存在一些不足。因此，在使用此数据集时，请务必注意甄别。

本数据集不代表任何一方的立场、利益或想法，无关任何团体的任何类型的主张。因使用本数据集带来的任何损害、纠纷，本项目的开发者不承担任何责任。


## 子集
1. [zh_seed_tasks.jsonl](https://github.com/LianjiaTech/BELLE/blob/main/1.5M/zh_seed_tasks.json)：包含175个种子任务。
2. [0.5M生成的数据](https://huggingface.co/datasets/BelleGroup/train_0.5M_CN) ： 为了方便模型训练，huggingface开源数据将原始生成文件中的"instruction"、"input"字段合并成"input"字段，"output"字段修改为"target"字段。
3. [1M生成的数据](https://huggingface.co/datasets/BelleGroup/train_1M_CN)：生成方式与0.5M数据集相同，在后处理中去掉了一些质量不高的数据，例如自称`GPT模型`的数据、由于input不完善导致模型无法回答的数据，以及指令是中文但input或target是英文的数据。


## 数据生成
沿用Alpaca的方式：
```
pip install -r requirements.txt
export OPENAI_API_KEY=YOUR_API_KEY
python 1.5M/generate_instruction.py generate_instruction_following_data
```

默认使用`Completion` API，模型`text-davinci-003`。如果想使用`Chat` API并使用`gpt-3.5-turbo`模型，可通过参数控制：

```
python 1.5M/generate_instruction.py generate_instruction_following_data \
    --api=chat --model_name=gpt-3.5-turbo
```

输出文件在`Belle.train.json`，可以人工筛选后再使用。


***


# The 1.5M Chinese Dataset

The **1.5M** Chinese dataset is composed of subsets spanning multiple (instruction) types and multiple fields.


## Schema
All subsets follow the same schema:
```
instruction: the instruction
input: the input
output: the expected output
```


## Limitation and Usage Limits
We require developers only use the open-sourced code, data, model and any other artifacts generated via this project for research purposes. Commercial use and other potential harmful use cases are not allowed.

Since this dataset was generated by *ChatGPT* and was not strictly verified, it still has shortcomings regarding factuality and other aspects. When using this dataset, careful inspection is needed.

This dataset does not represent anyone's ground, interest or thought, and is not related to any kind of claim of any groups. The developers of this project do not assume any responsibility to potential harm inflicted by using this dataset and project.


## Subsets
1. [zh_seed_tasks.jsonl](https://github.com/LianjiaTech/BELLE/blob/main/1.5M/zh_seed_tasks.json) contains 175 seed tasks
2. [0.5M generated data](https://huggingface.co/datasets/BelleGroup/train_0.5M_CN)：To facilitate model training, Hugging Face open-sourced data that merged the "instruction" and "input" fields in the original generation file into a single "input" field, and renamed the "output" field as the "target" field.
3. [1M generated data](https://huggingface.co/datasets/BelleGroup/train_1M_CN). Same generation pipeline as 0.5M dataset, removed lower-quality items in postprocessing, e.g. items regarding `GPT model`, bad items because of incomplete/invalid input, items with Chinese instructionb but English input or target.


## Data Generation Process
Following Alpaca:
```
pip install -r requirements.txt
export OPENAI_API_KEY=YOUR_API_KEY
python 1.5M/generate_instruction.py generate_instruction_following_data
```

Uses the `Completion` API and `text-davinci-003` model by default. To use `Chat` API and `gpt-3.5-turbo` model, just change the arguments:

```
python 1.5M/generate_instruction.py generate_instruction_following_data \
    --api=chat --model_name=gpt-3.5-turbo
```

Generated instructions are in `Belle.train.json`, you can check manually before using it.
