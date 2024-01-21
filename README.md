# Download Models
You can download the required demo models from the following link.

https://www.dropbox.com/scl/fi/dzqwrerij6kdwi3nyj87o/required_models.zip?rlkey=a9r2aa3tf72um8gltaussi0qn&dl=0


# Run
```
python demo.py --dataset cifar --tlabel 0 --model resnet18 --attack ia --device cuda:0 --size 32 --num_classes 10 --batch_size 128 --attack_type all-to-one
```

# Run on Jupyter version
A detailed introduction to each module of our code can be found in the demo.ipynb .