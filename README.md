# BTI-DBF: Towards Reliable and Efficient Backdoor Trigger Inversion via Decoupling Benign Features
This the official Pytorch implementation of our paper "[Towards Reliable and Efficient Backdoor Trigger Inversion via Decoupling Benign Features](https://openreview.net/forum?id=Tw9wemV6cb)", accepted by the ICLR 2024 (**Spotlight**). This research project is developed based on Python 3 and Pytorch.

## Requirements

To install requirements:

```setup
pip install -r requirements.txt
```
Make sure the directory follows:
```File Tree
stealingverification
├── checkpoints
│
├── datasets
│   ├── cifar10
│   └── ...
├── models 
│   
├── results
│   
```

## Pretrained Poisoned Models

>You can download the poisoned models which we have pretrained from the following link:
>[checkpoints](https://www.dropbox.com/scl/fo/m1tnyzylecimqtosr5oyv/h?rlkey=cnw876kh25gf0518ipjrbfu97&dl=0)

Our pretrained poisoned models have the following naming format:  `{dataset}-{attack}-{model}-target{tlabel}.pt.tar`. These models contain model parameters and trigger information. You can use the following code to read checkpoints and easily create backdoor samples:
```Python
import torch
from loader import Box

opt = cfg.get_arguments().parse_args()
box = Box(opt)
bd_info1, bd_info2, poisoned_model = box.get_state_dict()
testloader = box.get_dataloader(train="test", batch_size=opt.batch_size, shuffle=False)
for imgs, labels in testloader:
    backdoor_imgs = box.poisoned(imgs, bd_info1, bd_info2)
```

## Pretrain Generator
```
python pretrain.py --dataset cifar --tlabel 5 --model resnet18 --attack wanet --device cuda:0 --size 32 --num_classes 10 --batch_size 128 --attack_type all2one
```

## Inversion
```
python btidbf.py --dataset cifar --tlabel 5 --model resnet18 --attack wanet --device cuda:0 --size 32 --num_classes 10 --batch_size 128 --attack_type all2one \
--mround 20 --uround 30 --norm_bound 0.3
```
## Defense

### BTI-DBF (U)
```
python btidbfu.py --dataset cifar --tlabel 5 --model resnet18 --attack wanet --device cuda:0 --size 32 --num_classes 10 --batch_size 128 --attack_type all2one \
--mround 20 --uround 30 --norm_bound 0.3 --ul_round 30 --nround 5
```

### BTI-DBF (P)
```
python btidbfp.py --dataset cifar --tlabel 5 --model resnet18 --attack wanet --device cuda:0 --size 32 --num_classes 10 --batch_size 128 --attack_type all2one \
--mround 20 --uround 30 --norm_bound 0.3 --pur_round 30 --nround 5 --pur_norm_bound 0.05
```

## Citation
If our work or this repo is useful for your research, please cite our paper as follows:
```bibtex
@inproceedings{xu2024towards,
  title={Towards Reliable and Efficient Backdoor Trigger Inversion via Decoupling Benign Features},
  author={Xu, Xiong and Huang, Kunzhe and Li, Yiming and Qin, Zhan and Ren, Kui},
  booktitle={ICLR},
  year={2024}
}
```
