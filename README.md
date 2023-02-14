## VITS
VITS:具有对抗学习的条件变分自动编码器，用于端到端文本到语音转换


在论文(https://arxiv.org/abs/2106.06103)
提出了VITS：具有端到端文本到语音对抗学习的条件变分自动编码器。

从已经提出了几种支持单阶段训练和并行采样的端到端文本到语音（TTS）模型，但它们的样本质量与两阶段TTS系统不匹配。在这项工作中使用了一种并行的端到端TTS方法，该方法比当前的两阶段模型生成更自然的声音音频。该方法采用变分推理，通过归一化流程和对抗训练过程进行增强，从而提高了生成建模的表达能力。同时还提出了一个随机持续时间预测器，用于从输入文本中合成具有不同节奏的语音。通过对潜在变量的不确定性建模和随机持续时间预测器，该方法表达了自然的一对多关系，其中文本输入可以以不同的音高和节奏以多种方式朗读。对LJ Speech（单个说话人数据集）的主观人类评估（平均意见得分或MOS）表明，此方法优于最好的公开可用的TTS系统，并实现了与基本事实相当的MOS。

#访问我们的演示以获取音频样本。
https://jaywalnut310.github.io/vits-demo/index.html

#我们还提供预训练模型。
https://drive.google.com/drive/folders/1ksarh-cJf3F5eKJjLVWY0X1j1qsQqiS2?usp=sharing

#TTS演示
https://colab.research.google.com/drive/1CO61pZizDj7en71NQG_aqqKdGaA_SaBf?usp=sharing

##开始

1.Python >= 3.6
2.克隆此仓库
3.安装 python 环境。请参阅https://github.com/JOETtheIV/VITS-Paimon/blob/main/requirements.txt
             您可能需要先安装 espeak ：
             
apt-get install espeak

4.下载数据集
             下载并提取 LJ 语音数据集，然后重命名或创建指向数据集文件夹的链接：
             
ln -s /path/to/LJSpeech-1.1/wavs DUMMY1

5. 对于多扬声器设置，请下载并提取 VCTK 数据集，并将 wav 文件缩减采样至 22050 Hz。然后重命名或创建指向数据集文件夹的链接：

ln -s /path/to/VCTK-Corpus/downsampled_wavs DUMMY2

6.构建单调对齐搜索并运行预处理（如果使用自己的数据集）

#Cython-version Monotonoic Alignment Search
cd monotonic_align
python setup.py build_ext --inplace

# Preprocessing (g2p) for your own datasets. Preprocessed phonemes for LJ Speech and VCTK have been already provided.
#python preprocess.py --text_index 1 --filelists filelists/ljs_audio_text_train_filelist.txt filelists/ljs_audio_text_val_filelist.txt filelists/ljs_audio_text_test_filelist.txt 
#python preprocess.py --text_index 2 --filelists filelists/vctk_audio_sid_text_train_filelist.txt filelists/vctk_audio_sid_text_val_filelist.txt filelists/vctk_audio_sid_text_test_filelist.txt

## 炼丹实例
# LJ Speech
python train.py -c configs/ljs_base.json -m ljs_base

# VCTK
python train_ms.py -c configs/vctk_base.json -m vctk_base

## 输出
https://github.com/JOETtheIV/VITS-Paimon/blob/main/inference.ipynb
