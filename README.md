# Master-Thesis-Joel-Meier
The Github repository contains the following:
- The labeling, preprocessing and modeling scripts used in the thesis
- The most relevant plots used in the thesis
- This README file and a requirements.txt file to help install libraries and provie guidance
- The mid-term and final presentation slides
- The Wireshark extraction profile used for capturing the datasets

### **The code sections which actually run code and perform an action are commented at the top of the respective code box in the Juypter notebooks with: "Code Field X"**

All other code boxes only define methods or variables but do not directly execute any code.
To install the libraries needed to run the scripts, simply run:

`pip install -r requirements.txt`

Python 3.12 is required to run the code locally.

## Labeling script (dataset_labeling.ipynb):
The script requires a raw dataset with a defined path. Please note that certain parameters, such as the labeling conditions for the phone, may depend on the dataset. These variables are commented on in the code directly to know which to use and how to change them. The already labeled datasets are available in Sharepoint. Below, the code fields and their purpose are explained:

- **Code Field 0**: This field does not directly run code, but defines global variables. It is important to always re-initialize and run this before labeling a new dataset. That's why it is included here.
- **Code Field 1**: Reads the raw dataset, sets up all tracking variables/lists and assigns the labels to each row while dropping malformed packets.
- **Code Field 2**: This takes care of re-assigning the sources based on the revised labeling conditions. The parameters here need to be adjusted on the dataset. Finally, the dataframe is written to a new file.
- **Code Field 3**: Just a final evaluation check which prints the label distribution and checks against potentially existing dobule lables of source addresses.

## Modeling script (modeling.ipynb):
The script contains the loading of the labeled datasets, the preprocessing, the modeling and the analysis.
Basically, all code boxes follow a flow from top to bottom. Not all code sections need to be run, some can be skipped (like plotting learning curves).
Also, many parameters can be adjusted which is why code is extensively commented. Below, the code fields and their purpose are outlined:

- **Code Field 1**: Reads the labeled datasets, encodes dummy columns, calculates aggregate source features and stores them in a new dataframe
- **Code Field 2**: Calculates the time-based features of packet occurrences within certain time windows and appends them to the dataframes
- **Code Field 3**: Performs the column binning as well as the balancing of adjusting the maximum packet count a source address may have
- **Code Field 4**: Creates the 2:1 balanced down version of the evaluation dataset (i.e. noise to target ratio is randomly sampled to 2:1)
- **Code Field 5**: Prints the average cardinalities of columns based on the training and evaluation dataset cardinality
- **Code Field 6**: The main supervised model script, runs all models (unless commented out) including training, evaluation and plotting matrices and features
- **Code Field 7**: Plots the learning curve of the non-split training of the RF model
- **Code Field 8**: Plots the learning curve of the source-split training of the RF model
- **Code Field 9**: The main unsupervised model script, runs one model at a time to either find the best-performing model or set the parameters of the best-berforming run
- **Code Field 10**: Analysis the clustering result to get how many target devices were identified and their company_ids --> requires correct parameters, i.e. run Code Field 9 with the best-performing number of a model
- **Code Field 11**: Plot the ground truth of the cluster versus the correctly and incorrectly assigned labels
- **Code Field 12**: Plot a single target device and highlight it in the cluster
- **Code Field 13**: Plot a less dense version of Code Field 12, if the target device is not visible otherwise

