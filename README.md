# Easy-CoT: Extensible Dataset for Diverse CoT Reasoning On Small Language Models

## Grading
See paper result in the last output cells of code/result.ipynb (I ran out of compute on colab and had to switch to kaggle to run these).

## Instruction
To run experiment on an unseen complex reasoning dataset (one that has question-answer data), first produce base dataset using [Fine-tune-CoT](https://github.com/itsnamgyu/reasoning-teacher), then run our method run_auto_cot() to produce the Easy-CoT dataset, then run finetune_model() to tune gpt2-small on this generated dataset, and finally use test_all() to evaluate.

## Directories
### code/
The easy_cot.ipynb notebook has the following APIs are avaliable for use: 
- run_auto_cot(dataset, task, save_dir, *hyperparams): apply auto-cot on base dataset to generate easy_cot dataset corresponding to the task and dump in save_dir. Note that since the base dataset is the output of teacher model from Fine-tune-CoT.

- finetune_model(task, model_dir): fine-tune gpt2-small on Easy-CoT data of provided task, save the fine-tuned model in model_dir.
  
- test_all(task, model_dir): run two baselines (auto-cot and fine-tune-cot) and easy-cot experiment on the test set for task, output average accuracy over three runs for each. The fine-tuned-model should be in model_dir.

### easy_cot/
Contains our main Easy-CoT dataset. See generation process in paper. Each subdirectory of easy_cot has a name corresponding to the base dataset that it was generated from, and contains two files: data.json (containing output of fine-tune-cot applied on base dataset) and demos.json (containing output of auto-cot applied on data.json).

### finetuned_model/
All fine-tuned models from our experiment can be downloaded [here](https://drive.google.com/drive/folders/1FnIW-2SayX6KT6YGN6IL_8gQyiLiFY23?usp=drive_link). There are six models in total, one for each base dataset.

### datasets/
Contains the six base datasets on complex reasoning tasks used to generate our easy_cot dataset.

- fine_tune_cot/: completed data generated by teacher model in fine-tune-cot, courtesy of [Ho et al.](https://github.com/itsnamgyu/reasoning-teacher)

- zero_shot_cot/: raw data for complex reasoning task benchmarks, courtesy of [Kojima et al.](https://github.com/kojima-takeshi188/zero_shot_cot/tree/main/dataset). Not directly used in our experiment but was used to produce the fine_tune_cot/ dataset

