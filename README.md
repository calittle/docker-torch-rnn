# docker-torch-rnn
Based on work by:
   https://github.com/crisbal/docker-torch-rnn - Crisbal
   https://github.com/jcjohnson/torch-rnn - JCJohnson

## Available tags

* `crisbal/torch-rnn:latest`
    * Based on `nvidia/cuda:7.5`
    * Allows usage of torch-rnn in GPU mode (Cuda 7.5 support)
    * Run with nvidia-docker https://github.com/NVIDIA/nvidia-docker
    
## How to

More details here: https://github.com/jcjohnson/torch-rnn#usage

1. Install nvidia-docker
    * https://github.com/NVIDIA/nvidia-docker
2. Start bash in the container
    * `nvidia-docker run -ti calittle/torch-rnn bash`
3. Preprocess the sample data

    ```
    python scripts/preprocess.py \
    --input_txt data/tiny-shakespeare.txt \
    --output_h5 data/tiny-shakespeare.h5 \
    --output_json data/tiny-shakespeare.json
    ```

4. Train 
    
    ```
    th train.lua \
    -input_h5 data/tiny-shakespeare.h5 \
    -input_json data/tiny-shakespeare.json
    ```

5. Sample
Note: checkpoint files are named with Epoch (XXX) and Validation Loss (YYY). 
Normally you'll want to use a checkpoint file with the lowest value for validation loss,
but perhaps not.

    * `th sample.lua -checkpoint cv/checkpoint_10000_epoch-XXX_YYY.t7 -length 2000`
