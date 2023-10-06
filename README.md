# uncertainty_quant_peract

1. Create and activate a virtual environment
   ```
   # use virtualenv to create and activate the environment
   virtualenv -p $(which python3.8) --system-site-packages peract_env  
   source peract_env/bin/activate
   pip install --upgrade pip

   # update all submodules
   git submodule update --init --recursive
   ```
2. After cloning all submodules, install PyRep, RLBench, YARR accordingly in the submodule according to instructions in [Perceiver-Actor](https://github.com/peract/peract).
  
   Note you don't need to ```git clone``` the packages in the installation instructions again, they have been included in the submodules and have been heavily modified to add support for the uncertainty aware action selection strategy method.


3. Add path shortcut and PYTHONPATH
   
   ```
   cd path/to/uncertainty_quant_peract/peract_reliability
   export PERACT_ROOT=$(pwd)

   export PYTHONPATH=/path/to/uncertainty_quant_peract/YARR/
   export PYTHONPATH=/path/to/uncertainty_quant_peract
   ```

4. Download ckpts for Perceiver-Actor
   
   Download a [pre-trained PerAct checkpoint](https://github.com/peract/peract/releases/download/v1.0.0/peract_600k.zip) trained with 100 demos per task (18 tasks in total):
   ```bash
   cd $PERACT_ROOT
   sh scripts/quickstart_download.sh
   ```
5. Download data used for confidence calibration
   
   Download the **val** folder in [pre-generated RLBench demonstrations](https://drive.google.com/drive/folders/0B2LlLwoO3nfZfkFqMEhXWkxBdjJNNndGYl9uUDQwS1pfNkNHSzFDNGwzd1NnTmlpZXR1bVE?resourcekey=0-jRw5RaXEYRLe2W6aNrNFEQ&usp=share_link) for confidence calibration, we recommend using [rclone](https://rclone.org/drive/) for the validation set
6. Download data used for task evaluation
   
   You can use ```bash data_gen.sh``` to generate the evaluation set, you can also parallelize it to speed up the process. Please make sure you have enough disk space before the data generation, the entire evaluation set takes ~98G.
   **We will upload the data we generated for evaluation in this paper soon**
7. Run temperature scaling calibration on calibration data
    Now you can start ```bash temperature_training.sh``` for the temperature calibration process.
   **We also provide the pre-trained temperature scaler in here**
9. Run task evaluation on evaluation data
    ```bash rollout_safe_load_temp.sh```
    
