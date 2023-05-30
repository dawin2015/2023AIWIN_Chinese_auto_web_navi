# 2023AIWIN_Chinese_auto_web_navi
2023AIWIN——中文网页自动导航挑战赛

比赛网页：http://ailab.aiwin.org.cn/competitions/86

得分详情：

A榜：67.670 (29)

B榜：69.200 (20)

# 主要思路
1. prompt：提高10%
2. jieba分词：提高10%

# ChatGLM-6B微调参数参考
PRE_SEQ_LEN=256
LR=2e-2

CUDA_VISIBLE_DEVICES=0 python3 main.py \
    --do_train \
    --train_file ../../label_train.json \
    --validation_file ../../label_dev.json \
    --prompt_column prompt \
    --response_column response \
    --overwrite_cache \
    --model_name_or_path THUDM/chatglm-6b \
    --output_dir output/adgen0526-chatglm-6b-pt-$PRE_SEQ_LEN-$LR \
    --overwrite_output_dir \
    --max_source_length 256 \
    --max_target_length 256 \
    --per_device_train_batch_size 1 \
    --per_device_eval_batch_size 1 \
    --gradient_accumulation_steps 16 \
    --predict_with_generate \
    --max_steps 800 \
    --logging_steps 10 \
    --save_steps 200 \
    --learning_rate $LR \
    --pre_seq_len $PRE_SEQ_LEN \
    --quantization_bit 4
