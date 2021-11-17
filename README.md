# chaii 4th place solution
This is the source code of the 4th place solution of the [chaii - Hindi and Tamil Question Answering](https://www.kaggle.com/c/chaii-hindi-and-tamil-question-answering) competition at kaggle.

Our solution write-up: https://www.kaggle.com/c/chaii-hindi-and-tamil-question-answering/discussion/287911.

Inference kernel: https://www.kaggle.com/zacchaeus/chaii-infer-blend-postpro-4models.

Dataset we made (not involved in the final submission): [hi/ta parsed wiki] (https://www.kaggle.com/zacchaeus/chaii-tfds-wiki), [SQuAD 2.0 in Tamil] (https://www.kaggle.com/zacchaeus/chaii-tfds-wiki), [cleaned chaii dataset] (https://www.kaggle.com/zacchaeus/chaiitrain0917)
## The training pipeline:
- `pip install -r requirements.txt`
- Finetune RemBERT, InfoXLM, Muril, XLM-R on SQuAD 2.0 with `finetune.py`.
An example of finetuning Muril, same for the others.
```
python finetune.py
--model_checkpoint google/muril-large-cased \
--train_path /gpfsnyu/scratch/yw3642/chaii/input/squad2/train-v2.0.json \
--max_length 512 \
--doc_stride 128 \
--epochs 3 \
--batch_size 4 \
--accumulation_steps 8 \
--lr 1e-5 \
--weight_decay 0.01 \
--warmup_ratio 0.2 \
--seed 42 \
--dropout 0.1
```
- Train 5 folds on the chaii dataset with `train-cv.py`. OR Train with all data with `train-all.py`.
