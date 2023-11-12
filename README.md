This project has stopped working. Quandl does not provide free stock data any more. :(

# I have set up a new project that downloads stock data from Alpha Vantage https://github.com/nmharmon8/DSD. It is not integrated into this project.

# Unsupervised Stock Market Features Construction using Bidirectional Generative Adversarial Networks (BiGAN)

Check out the write up of the project and the current results -- [StockMarketGAN](https://nmharmon8.github.io/StockMarketGAN/)

## Setup

*Dependencies*:

  * [Python 2.7](https://www.python.org/download/releases/2.7/)

  * [Pandas](https://pandas.pydata.org/)

  * [Tensorflow](https://www.tensorflow.org/)

  * [scikit-learn](http://scikit-learn.org/stable/)

  * [Matplotlib](https://matplotlib.org/)

  * [XGBoost](https://github.com/dmlc/xgboost)

First clone the project.

```bash
git clone https://github.com/nmharmon8/StockMarketGAN.git
```

To set up the environment, run "source env.sh" from the root directory of the project.
This must be run  every time. 

```bash
cd StockMarketGAN
source env.sh
```

Next get a free account with [Quandl](https://www.quandl.com/) and get an API key. Export your key. This can be added to the ~/.bashrc

```bash
export QUANDL_KEY=you_key_here
```

Download the ticker data from Quandl

```bash
cd utils
python get_stock_data.py
```

The stocks can be changed by editing utils/companylist.csv.

To train a model go to the train_models directory and run the training script. 

```bash
cd ../train_models
python train_bigan_shared_weights.py
```
The model will continue to train forever. Every 100 steps it will save its weights to the models/ directory. To finish training simply kill the script. 

```bash
Ctrl+c
```

When the BiGAN is finished training the Random Forest model can be trained using the BiGAN features. The Random Forest model will load the most recently trained BiGAN from the models/ directory. 

```bash
python train_rf_bigan_shared_weights.py
```

The Random Forests script will hold out a test set.

To test your model deploy them to the deployed_models/ directory.   

```
cd ../utils
python deploy_model.py
```
Warning this will overwrite the pre-trained models.

Next, run the test script.

```
cd ../test_models
python test_bigan_rf_shared_weights.py
```
The TSNE is done on a small sample size so it will work with 4GB of RAM. If you have more RAM feel free to increase the size of the sample.

Have Fun.
# StockMarketGAN-tf2
# StockMarketGAN-tf2
