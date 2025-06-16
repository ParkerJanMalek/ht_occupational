# ht_occupational

This repository contains an update for ht_occupational exposure model (https://github.com/USEPA/ht_occupational)

Programs with "_new" in the names have been updated to utilized the pytensor package instead of theano (deprecated; no longer supported) and pymc instead of pymc3 package. 
This includes the requirements_new.txt that includes the packages needed to run the scripts. 

While most of the code remains the same, there are a few exceptions:

1.) The pymc function *sample_posterior_predictive* no longer supports a "sample" parameter. A work around for that would be to separately select out the desired sample before feeding into the function.
2.) Results of the *sample_posterior_predictive* function cannot be directly referenced. For example, a result called ppc_train cannot be referenced as ppc_train['likelihood'] but must be explicitly identified as
ppc_train.posterior_predictive['likelihood'][0]
