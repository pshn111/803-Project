## Dependencies

* python 3 (tested with anaconda3)
* PyTorch 1.6
* tqdm
* imageio
* scikit-image
* numpy
* matplotlib
* readline


## Datasets

* GOPRO_Large: [link](https://seungjunnah.github.io/Datasets/gopro)
* REDS: [link](https://seungjunnah.github.io/Datasets/reds)

## Usage examples

* Preparing dataset

Before running the code, put the datasets on a desired directory. By default, the data root is set as '~/Research/dataset'  
```python
group_data.add_argument('--data_root', type=str, default='~/Research/dataset', help='dataset root location')
```
Put your dataset under ```args.data_root```.

The dataset location should be like:
```bash
# GOPRO_Large dataset
~/Research/dataset/GOPRO_Large/train/GOPR0372_07_00/blur_gamma/....
# REDS dataset
~/Research/dataset/REDS/train/train_blur/000/...
```

* Example commands

```bash
# single GPU training
python main.py --n_GPUs 1 --batch_size 8 # save the results in default experiment/YYYY-MM-DD_hh-mm-ss
python main.py --n_GPUs 1 --batch_size 8 --save_dir GOPRO_L1  # save the results in experiment/GOPRO_L1

# adversarial training
python main.py --n_GPUs 1 --batch_size 8 --loss 1*L1+1*ADV
python main.py --n_GPUs 1 --batch_size 8 --loss 1*L1+3*ADV
python main.py --n_GPUs 1 --batch_size 8 --loss 1*L1+0.1*ADV

# train with GOPRO_Large dataset
python main.py --n_GPUs 1 --batch_size 8 --dataset GOPRO_Large
# train with REDS dataset (always set --do_test false)
python main.py --n_GPUs 1 --batch_size 8 --dataset REDS --do_test false --milestones 100 150 180 --end_epoch 200

# save part of the evaluation results (default)
python main.py --n_GPUs 1 --batch_size 8 --dataset GOPRO_Large --save_results part
# save no evaluation results (faster at test time)
python main.py --n_GPUs 1 --batch_size 8 --dataset GOPRO_Large --save_results none
# save all of the evaluation results
python main.py --n_GPUs 1 --batch_size 8 --dataset GOPRO_Large --save_results all
```

