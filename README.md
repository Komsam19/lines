# dataset

# Running on Local Machine

In main directory (dataset) folder open cmd and make a new environment, activate this environment and then install all these libraries in current environment. 

eg: 
- install required python and pip and then 
- python --version
- pip --verison (to verify installation)
- pip install virtualenv
- virtualenv lines (making virtual environment by 'lines' name)
- lines\Scripts\activate (by this command activate this environment)
After activation now you can install all requirements in this environment. 

Requirements:
- Python 3.6.7 (You can download this version by this link: https://www.python.org/ftp/python/3.6.7/python-3.6.7-amd64.exe)
- Pandas 0.22.0
- Matplotlib 2.2.2
- Argparse
- Pickle5
- Opencv-python 3.4.0.14
- xlrd 1.2.0
- scikit-image
- Tensorflow v1.6.0 (If got error against protobuf then do this: 
				1. pip uninstall protobuf
				2. pip install protobuf==3.14.0
				3. Now install tensorflow (pip install tensorflow=1.6.0)	

Now make this directory structure. 

# Directory structure
<pre>
dataset/
  -- PUCIT_OHUL
    -- train_lines/
    -- test_lines/
    -- train_lables_v2.xlsx
    -- test_lables_v2.xlsx
    -- generate_pickle_files.py <=== this file will read the PUCIT_OHUL dataset and populate the 'data/' folder with 7 pickle files (see below))
           Usage: python generate_pickle_files.py --valid_inds
    -- vocabulary.txt <=== will be generated by generate_pickle_files.py
    -- vocabulary_unicode.txt <=== will be generated by generate_pickle_files.py
data/PUCIT_OHUL/
  -- train_lines.pkl
  -- valid_lines.pkl
  -- test_lines.pkl
  -- train_labels.pkl
  -- valid_labels.pkl
  -- test_labels.pkl
  -- vocabulary_unicode.pkl
results/
  -- valid_predicted.txt
  -- valid_target.txt
  -- valid_wer.wer
  -- test_predicted.txt
  -- test_target.txt
  -- test_wer.wer
  -- log.txt
chekpoints/
  -- cp-NUM-ACCURACY.ckpt  <== checkpoint files
models/
  -- current_best_model.ckpt  <== checkpoint file for currently best performing model on validation set
</pre>

# How to train on dataset

PUCIT Offline Handwritten Urdu Lines (PUCIT-OHUL) Dataset and Ground Truth files: http://faculty.pucit.edu.pk/nazarkhan/work/urdu_ohtr/pucit_ohul_dataset.html
   
# How to train on dataset
1. Place all training line images in the folder "train_lines"
2. Place all testing line images in the folder "test_lines"
3. Place all training ground-truth labels in the file "train_labels_v2.xlsx" using 2 columns. Column 1 contains image name/number. Column 2 contains the ground-truth label of the text contained in the image.
4. Place all testing ground-truth labels in the file "test_labels_v2.xlsx" using 2 columns. Column 1 contains image name/number. Column 2 contains the ground-truth label of the text contained in the image.
5. Run "generate_pickle_files.py" after specifying validation indices (if required). This will place all training, testing and validation images and labels in pickle format in the 'data/PUCIT_OHUL/' folder.
6. For training, set mode="train", and run "CALText.py". This will place the trained model(s) in 'models/' folder.
7. For testing, set mode="test", set path of the model to be used and run "CALText.py".
8. For Contextual Attention, set alpha_reg=1, while training.
9. For Contextual Attention Localization, set alpha_reg=0, while testing.

Now place these commands in current environment cmd. 

First you generate all pickle files by using this command: 

- python generate_pickle_files.py (make sure you should have in same directory where this file exists)

For train use this command:
- python CALText.py --mode=train --dataset=PUCIT_OHUL --alpha_reg=1
  
For test use this command: 
- python CALText.py --mode=test --dataset=PUCIT_OHUL --alpha_reg=0
