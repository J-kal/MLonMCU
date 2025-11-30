# MLonMCU

To run demo:

```
python demo_test.py --checkpoint-path weight_path --cpu --video video_path
```


Command to download the validation dataset on Mac:

Create the `coco/` folder at top level inside the submodule and paste the following commands. Unzip those folders later.

```
/bin/zsh -lc 'cd .../MLonMCU/lightweight-human-pose-estimation.pytorch && cd coco && curl -LO http://images.cocodataset.org/annotations/annotations_trainval2017.zip'
```

```
/bin/zsh -lc 'cd .../MLonMCU/lightweight-human-pose-estimation.pytorch/coco && curl -LO http://images.cocodataset.org/zips/val2017.zip'
```


Command to run the validation script (Assuming you have the model weights, labels, and images in the expected folders - coco for labels and images, pre_model for model_weights):
```
python val.py \                    
  --labels coco/val_subset.json \                          
  --images-folder coco/val2017 \      
  --checkpoint-path pre_model/checkpoint_iter_370000.pth \
  --cpu
```

Commands to run a quick smoke test for the training script on CPU (fine-tuning on the existing weights):
1. Make a tiny subset from validation group and prepare labels
```
python scripts/make_val_subset.py \
  --labels coco/annotations/person_keypoints_val2017.json \
  --output-name coco/val_subset_10.json \
  --num-images 10
```

```
python scripts/prepare_train_labels.py \
  --labels coco/val_subset_10.json \
  --output-name coco/prepared_train_annotation_10.pkl \
  --net-input-size 368
```

2. Train for 4 epochs. Do not expect any reasonable improvement with this (it is just a smoke test to verify the script and all new changes in it on CPU).
```
python train.py \
  --train-images-folder coco/val2017 \
  --prepared-train-labels coco/prepared_train_annotation_10.pkl \
  --val-labels coco/val_subset_10.json \
  --val-images-folder coco/val2017 \
  --checkpoint-path pre_model/checkpoint_iter_370000.pth \
  --weights-only \
  --batch-size 2 \
  --num-workers 0 \
  --log-after 1 \
  --checkpoint-after 10 \
  --val-after 10 \
  --experiment-name smoke_cpu \
  --epochs 4 \
  --cpu
```


