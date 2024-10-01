![image](https://github.com/user-attachments/assets/3bde3832-699f-4f73-9e9e-62fd7643dee9)
# Stable-Diffusion---Image-to-Prompts
本次竞赛的目标是扭转生成文本到图像模型的典型方向：我们能否创建一个模型，在给定生成的图像的情况下预测文本提示，而不是从文本提示生成图像？您将对包含由 Stable Diffusion 2.0 生成的各种对的数据集进行预测，以了解潜在关系的可逆性。(prompt, image)

首先，在数据预处理阶段，由于缺少训练数据且测试数据完全封闭，我们使用了DiffusionDB数据集，过滤掉文本相似度高于0.8的数据，构建验证集。

然后，利用开源数据集和预训练语言模型生成大量文本指令，并同样进行相似度过滤，最后使用Stable Diffusion 2.0模型生成对应的图片数据集。

在训练阶段，采用OpenCLIP的预训练模型，并自定义了预处理器。为了提高训练效率，选择冻结大约3/4的模型层数，并将图像尺寸缩小以适应训练需求。

模型评估时，使用与训练阶段相同的数据处理步骤，并以平均cosine similarity作为评估指标。

最终，模型在16000张测试图像上取得了0.61144的cosine similarity，成绩位列国际排名Top 4%，并获得了银牌。
