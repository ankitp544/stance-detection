Hoaxbait
========

The Fake News Detection App is a single, end-to-end system consisting of lexical
as well as similarity features fed through a multi-layer perceptron (MLP) with
one hidden layer.

Although relatively simple in nature, the model performs on par with more
elaborate, ensemble-based systems of other teams.

The features extracted from the headline and article body pairs consist of three
overarching elements only:

-   A bag-of-words term frequency (BoW-TF) vector of the headline

-   A BoW-TF vector of the body

-   The cosine similarity of term frequency-inverse document frequency (TF-IDF)
    vectors of the headline and body

A schematic overview of the setup is provided below. Further detailed
information can be found in a [short paper](http://arxiv.org/abs/1707.03264) on
arXiv.

 

Reproducibility
---------------

Rather than providing seed values and requiring the model to be retrained, the
repository contains relevant scripts and the TensorFlow model trained as part of
the submission.

The submission can easily be reproduced by loading this model using the
`pred.py` script to make the predictions on the relevant test set.

Alternatively, as suggested by the organizers of the competition, the validity
of the submission can be checked by also using the `pred.py` script to train the
model with different seeds and evaluating the mean performance of the system.

Getting started
---------------

To get started, simply download the files in this repository to a local
directory.

### Prerequisites

The model was developed, trained and tested using the following:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Python==3.5.2
NumPy==1.11.3
scikit-learn==0.18.1
TensorFlow==0.12.1
Flask==0.12.2
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Please note that compatibility of the saved model with newer versions of
`TensorFlow` has not been checked. Accordingly, please use the `TensorFlow`
version listed above.

### Running

Other than ensuring the dependencies are in place, no separate installation is
required.

Simply execute the `app.py` file once the repository has been saved locally and
open localhost:5000 to access the application

Reproducing the submission
--------------------------

The `pred.py` script can be run in two different modes: 'load' or 'train'. Upon
running the `pred.py` file, the user is requested to input the desired mode.

Execution of the `pred.py` file in 'load' mode entails the following:

-   The train set will be loaded from `train_stances.csv` and `train_bodies.csv`
    using the corresponding `FNCData` class defined in `util.py`.

-   The test set will be loaded from `test_stances_unlabeled.csv` and
    `train_bodies.csv` using the same `FNCData` class. Please note that
    `test_stances_unlabeled.csv` corresponds to the second, amended release of
    the file.

-   The train and test sets are then respectively processed by the
    `pipeline_train` and `pipeline_test` functions defined in `util.py`.

-   The `TensorFlow` model saved in the `model` directory is then loaded in
    place of the model definition in `pred.py`. The associated `load_model`
    function can be found in `util.py`.

-   The model is then used to predict the labels on the processed test set.

-   The predictions are then saved in a `predictions_test.csv` file in the top
    level of the local directory. The corresponding `save_predictions` function
    is defined in `util.py`. The predictions made are equivalent to those
    submitted during the competition.

Execution of the `pred.py` file in 'train' mode encompasses steps identical to
those outlined above with the exception of the model being trained as opposed to
loaded from file. In this case, the predictions will obviously not be identical
to those submitted during the competition.

The file name for the predictions can be changed in section '\# Set file names'
at the top of `pred.py`, if required.

Please note that the predictions are saved in chronological order with respect
to the `test_stances_unlabeled.csv` file, however, only the predictions are
saved and not combined with the `Headline` and `Body ID` fields of the source
file.

Team members
------------

-   Anirudh Jain

-   Shril Kumar

-   Ajeet Singh

-   Rishabh Thukral

-   Madhavan Venkatesh
