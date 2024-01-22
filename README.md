# Towards Reliable and Efficient Backdoor Trigger Inversion via Decoupling Benign Features

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

## Download Poisoned Models

>You can download the poisoned models which we have pretrained from the following link:
>[checkpoints](https://www.dropbox.com/scl/fo/m1tnyzylecimqtosr5oyv/h?rlkey=cnw876kh25gf0518ipjrbfu97&dl=0)

## Pretrain Generator
```
python pretrain.py --dataset cifar --tlabel 5 --model resnet18 --attack wanet --device cuda:0 --size 32 --num_classes 10 --batch_size 128 --attack_type all2one
```

## BTI-DBF
```
python btidbf.py --dataset cifar --tlabel 5 --model resnet18 --attack wanet --device cuda:0 --size 32 --num_classes 10 --batch_size 128 --attack_type all2one \
--mround 20 --uround 30 --norm_bound 0.3
```

## BTI-DBF (U)
```
python btidbfu.py --dataset cifar --tlabel 5 --model resnet18 --attack wanet --device cuda:0 --size 32 --num_classes 10 --batch_size 128 --attack_type all2one \
--mround 20 --uround 30 --norm_bound 0.3 --ul_round 30 --nround 5
```