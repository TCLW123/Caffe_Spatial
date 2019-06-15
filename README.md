## Environment
- Ubuntu 1404
- Caffe
- Python 2.7

## How to run the code

1. Download this repo and compile: `make -j24`, see Caffe's [official guide](http://caffe.berkeleyvision.org/installation.html). Make sure you get it through. 
2. Here we show how to run the code, taking lenet5 as an example:
    - Preparation: 
        - Data: Create your mnist training and testing lmdb (either you can download [ours](https://drive.google.com/open?id=1zMbKKfOFXH3chi9xdwCPi14YfqRzC_pe)), put them in `compression_experiments/mnist/`. 
        - Pretrained model: We provide a pretrained lenet5 model in `compression_experiments/mnist/weights/baseline_lenet5.caffemodel` (test accuracy = 0.991).
    - (We have set up an experiment folder in `compression_experiments/lenet5`, where there are three files: `train.sh, solver.prototxt, train_val.prototxt`. There are some path settings in them and pruning configs in `solver.prototxt`, where we have done that for you, but you are free to change them.)
    - In your caffe root path, run `nohup  sh  compression_experiments/lenet5/train.sh  <gpu_id>  >  /dev/null  &`, then check your log at `compression_experiments/lenet5/weights`.

For vgg16, resnet50, we also provided their experiment folders in `compression_experiments`, check them out and have a try!

## Check the log

There are two logs generated during pruning: `log_<TimeID>_acc.txt` and `log_<TimeID>_prune.txt`. The former saves the logs printed by the original Caffe; the latter saves the logs printed by our added codes.

Go to the project folder, e.g., `compression_experiments/lenet5` for lenet5, then run `cat weights/*prune.txt | grep app` you will see the pruning and retraining course.

## How to check spatial_prune and kernel_reshape

   - check file: we provide a check file in 'compression_experiments/check/val_spa_lenet.py'.
   - In your caffe root path, run 'python compression_experiments/check/val_spa_lenet.py', then you will obtain the shape of kernel.

## Detailed explanation of the options in solver.prototxt

- target_reg:
- IF_eswpf:
