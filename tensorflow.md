# Introduction to TensorFlow
*[Ashkan Mirzaee](https://ashki23.github.io/index.html)*

[TensorFlow](https://www.tensorflow.org/) is an end-to-end open source
platform for machine learning. It has a comprehensive, flexible
ecosystem of tools, libraries and community resources that lets
researchers push the state-of-the-art in ML and developers easily build
and deploy ML powered applications.

  - [TensorFlow Guide](https://www.tensorflow.org/guide)

This document will cover how to install TensorFlow (TF) by using
Anaconda and run a toy example in Python. Make sure review
[Anaconda](python-env.html#miniconda) to learn how to create and
maintain Conda virtual environments.

-----

## TensorFlow environment

We have two options for using TensorFlow (TF), one is using CPUs for the
computational tasks and the other one is using GPU resources. Depends on
your workflow and identity of your calculations, you might choose any of
these methods.

To use TF with CPU resources, use the following to create the
environment (env) and install TF:

``` bash
conda create --name tensorflow-env tensorflow
```

And use the following to install TF for GPUs:

``` bash
conda create --name tensorflow-gpu-env tensorflow-gpu
```

Note that `tensorflow-gpu` includes `cudatoolkit` and `cudnn` in
addition to TF. Also in a HPC system, you need to request resources and
load `miniconda3` module first.

## A simple example

After creating the preferred env, we can use Python to run TF. The
following is a simple example from TensorFlow
[tutorials](https://www.tensorflow.org/tutorials/quickstart/beginner).
This example uses [the MNIST
database](http://yann.lecun.com/exdb/mnist/) and *Keras* to run a
pattern recognition training task on images of handwritten digits.

Create a Python file called `minist.py` including the following scripts
(from [here](https://www.tensorflow.org/tutorials/quickstart/beginner)):

``` python
import tensorflow as tf
mnist = tf.keras.datasets.mnist

(x_train, y_train),(x_test, y_test) = mnist.load_data()
x_train, x_test = x_train / 255.0, x_test / 255.0

model = tf.keras.models.Sequential([
  tf.keras.layers.Flatten(input_shape=(28, 28)),
  tf.keras.layers.Dense(128, activation='relu'),
  tf.keras.layers.Dropout(0.2),
  tf.keras.layers.Dense(10, activation='softmax')
])

model.compile(optimizer='adam',
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])

model.fit(x_train, y_train, epochs=5)
model.evaluate(x_test, y_test)
```

To run the above code with CPUs, we can use:

``` bash
conda activate tensorflow-env
python3 minist.py
```

Also, if you have created `tensorflow-gpu-env` environment, you can use
the following to run this job with a GPU.

``` bash
conda activate tensorflow-gpu-env
python3 minist.py
```

Note that in an HPC system with [Slum](cluster.html#slurm) scheduler, we
can use a sbatch file, called `tf-gpu.sh`, such that:

``` bash
#!/bin/bash

#SBATCH -p gpu-partition # modify partition's name
#SBATCH --gres gpu:1
#SBATCH --mem 16G
#SBATCH -n 4
#SBATCH -N 1

module load miniconda3
conda activate tensorflow-gpu-env

python3 minist.py
```

To submit the job to a GPU partition by running `sbatch tf-gpu.sh`.
Slurm out file will show the outputs.

---

Copyright 2018-2023, [Ashkan Mirzaee](https://ashki23.github.io/index.html) | Content is available under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | Sourcecode licensed under [GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)
