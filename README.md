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

