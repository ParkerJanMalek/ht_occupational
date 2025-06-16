# ht_occupational update
## Parker Malek, TSPi

This repository contains an update for ht_occupational exposure model (https://github.com/USEPA/ht_occupational)

Programs with "_new" in the names have been updated to utilized the pytensor package instead of theano (deprecated; no longer supported) and pymc instead of pymc3 package. 
This includes the requirements_new.txt that includes the packages needed to run the scripts. 

While most of the code remains the same, there are a few exceptions:

1. The pymc function *sample_posterior_predictive* no longer supports a "sample" parameter. A work around for that would be to separately select out the desired sample before feeding into the function.
2. Results of the *sample_posterior_predictive* function cannot be directly referenced. For example, a result called ppc_train cannot be referenced as ppc_train['likelihood'] but must be explicitly identified as
ppc_train.posterior_predictive['likelihood'][0]


Run load_hurdle_model_new.py to run the latests updated models (found in the model folder as .file). This should create the proper output of 1,4 dioxane and is found in the TableS2.csv output.


Below are the steps to setting up the environment (pulled from original ht_occupational readme):

## High-throughput occupational exposure modeling ##

Code to support: Minucci et al. 2023. Data-Driven Approach to Estimating Occupational Inhalation Exposure Using Workplace Compliance Data. Environmental Science and Technology. https://doi.org/10.1021/acs.est.2c08234

prerequisites: Anaconda or miniconda previously installed (Python 3.8 or higher)

1. In the Anaconda Prompt (Windows) or bash (Linux), navigate to the directory that this README is located in.

2. To install the required package in a conda virtual environment, run:

```
conda config --append channels conda-forge
conda create --name occupation theano m2w64-toolchain -y
conda activate occupation
pip install -r requirements_new.txt
```

3. Now you are ready to run the scripts. They should be run in the following order:

```
python data_processing.py

python fit_hurdle_model_new.py
```

If fit_hurdle_model.py is too slow on your system, you can optionally load pre-fit model objects. All of the same model performance metrics and predictions will be made:

```
python load_hurdle_model_new.py
```

4. Output files will appear in the `output` folder. Performance metrics will be printed in the console and also to the file `fit_hurdle_model.log`.

5. To create plots:

```
python plotting.py
```

5. To use the pre-fit model to make CDR predictions:

```
python predict_CDR.py
```