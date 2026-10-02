# ReAct paper reading summary

## Question
Before ReAct,the reasoning and act of the LLM is separate.
- CoT(Chain of Thought):enable a LLM give an explicit reasoning trajectory,but can not interact with the external environment.
- Act only:just give an implicit reasoning(didn't have a scratchpaper to record the detail),the model will only perform actions and unable to analyse the unsuccessful actions.
Therefore,ReAct aims to synergize reasoning and acting as the title saying.

## Methods
ReAct has a cyclical pattern that generates thoughts,performs actions,receives observations from the environment,and then use the observations to thought again and decide what to do in the next circulation/.

## Example
- ALFworld
Figure 1 (2a) 中，Act-only在完成Alfworld的任务中在做到'Take peppershaker 1 from sinkbasin 1'的时候得到了'nothing happen'的observation，但是模型无法对这个observation进行分析导致一直在重复这个action，无法推进任务。
Figure 1 (2b) 中，ReAct通过sparse reasoning是的在observation返回的时候也可以明确下一步的action
而CoT则是仅有推理没有对外界环境的交互导致只能通过内部的知识解答问题Apple Remote Figure(1b)

后续有对比实验
对比Act ReAct ReAct-IM 和BUTLER
Act:45的总得分 只有Pick2是最高
ReAct:大部分都是最高得分，也有少量的不是最高
ReAct-IM(thought只是单纯围绕当前状态重复):得分不高
BUTLER(模仿学习模型，通过105条专家轨迹进行训练):得分不高，不过有一项满分

Prompting和Finetuning实验
Prompting:把几条demonstration trajectories（table7)直接放入模型的输入中，模型根据示例模仿格式。
Finetuning:用3000条正确答案的trajectories更新模型参数

模型大小对比
大模型+少量示例->通过prompting使用ReAct
小模型+大量示例->通过finetuning学习ReAct