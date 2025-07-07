# Qwen3-高效微调

---1. 数学垂域
---2. 法律垂域

---详细步骤：
1. 任务：增强Qwen3 (unsloth-bnb-4bit)的数学推理能力。
2. 主要方法：使用LoRA高效微调，基于Unsloth平台，以及模型性能评估框架EvalScope和模型调度框架VLLM，最终使用wandb
记录模型微调时的权重变化。
3. 微调数据集构建：为了Qwen3能够在提升数学能力的同时，保留混合推理的性能，我们在微调数据集中加入如普通对话数据集
FineTome以及带有推理字段的数学类数据集OpenMathReasoning，并以1：3的比对以上普通文本问答数据集和COT数学数据
集进行拼接。
4. 微调数据集清洗：对于COT数据集中筛选出“problem”和“generated_solution”字段，并以字典的格式分别拼接
在“user”和“assistant”上；最后使用Qwen3的tokenizer.apply_chat_template()提示器模板进行转换为<|im_start|>user
格式模型数据集。
5. 微调训练流程：首先对model进行LoRA层参数注入，
