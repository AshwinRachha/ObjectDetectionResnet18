# Design and Train an object detector to detect objects

You have to design and implement a Training Pipeline that can train, test and visualize the model using the dataset provided.

## Assignment Protocols

- We expect it to take ~4 hours, with an extra 15 min for clear loom explanation(s)
  - The assessment is timeboxed at 5 hours total in a single block. So please plan accordingly
- You need to use Google Collaboratory to run and edit this notebook
- You can only use Python as a programming Language
- You cannot take help from any other person
- You can use Google to search for references
- You can not search on google for design-related things, like what should be loss function, or what should be model architecture.
  - But you can use pre-trained backbones from PyTorch
- Record a 5-10 mins of code walkthrough of the work you have done. You can use Loom Platform (https://www.loom.com) to record the video.
  - Design Decisions
    - Model Design which layers and activation functions you used and why
    - Loss function, which loss functions you used and why
    - Metrics, which metrics and why
  - Any optimizations you have made to the codebase
  - How you implemented resume functionality, what were the things you thought would be needed to resume training from exact same point
  - Explain what parts of the assessment are completed and what is missing?
  - Make sure to submit the screen recording link in the submission after you are done recording
  - Please note that the free plan on Loom only allows for videos up to 5 minutes in length. As such, you may need to record two separate 5-minute videos.
- [NO SUBMISSION WILL BE ACCEPTED WITHOUT]
  - Trained best model weights
  - Visualize Function in the Notebook
  - Code Walk-through video

## Task Details
Design a Training Pipeline to train a object detector with following specs or assumptions:
- Implement & Design Model
  - You can use any backbone
    - Either from PyTorch (torhvision) or any resource online
    - But you need to design head your self (head means how you will use features of the back bone and get the desired outputs)
  - Model needs to detect one object in each image
  - Model should output following for each image passed as input:
    - Whether we have an object or not
    - Where is the object?
      - The bounding box output format should be xmin, ymin, xmax, ymax
      - It is not necessary the model is trained to output exactly this format but the visualize function which shows output should output in this format
    - Either the object is a cat or dog?
    - And which specie the object belongs to? There are in total 9 species: 
      - Cat [3 species]:
        - Abyssinian
        - Birman
        - Persian
      - Dog [6 species]
        - american_bulldog
        - american_pit_bull_terrier
        - basset_hound
        - beagle
        - chihuahua
        - pomeranian
- Implement Custom Dataloader
  - This is obvious as dataset is in a unique format any predifined dataloader wont work
  - Follow best practices of writing custom dataloaders
  - Details of the format of the dataset are defined in the Dataset Details section below
  - Add needed pre-processing that you think would help train a better model or would help as we are using pre-trained weights as starting point
  - Add augmentations that you think would help train a better model
- Implement Loss Function
  - Design and implement a loss function that can handle all of the outputs we have
  - You can use pytorch built-in loss functions
  - There are many scenarios which you need to handle, which one can understand from the dataset details and the model design
- Implement Test Function
  - The test function should be able to run the model on the validation set and output the metrics for all the outputs of the model
  - Select the metrics carefully, there are many scenarios which can change the selection of a metric
  - Keep in mind there are multiple outputs, you would need a metric for each output
  - [NOTE] You don't need to implement metrics for the bounding box output as it can take more time than provided for this assessment. But please add details of the metrics you would have implemented in your code-walk through loom video.
- Update Resume Training Functionality using the best weights
  - Current script does not have save best weights functionality
  - The code should be able to resume training from exactly same point from where the training was stopped if model weights file is passed
  - Keep in mind you can not resume training from same point by just loading weights of the model
- Implement a visualize function [Most important, without this no submission will be accepted]
  - The input of the function should be path of a folder with images and the weight file
    - Also the output folder path to save outputs
  - This function should return a dictionary of dictionaries with following details for each image:
    - {
        "has_object": True,
        "cat_or_dog": "cat",
        "specie": "persian",
        "xmin": 10,
        "ymin": 10,
        "xmax": 10,
        "ymax": 10
    }
  - And in case there is no object it should have 0 for bbox values, "NA" for "cat_or_dog" and "specie", and False for "has_object".
  - Values of the returned dictionary should be like explained above and keys should be image names including the extension ".jpg" or ".jpeg"
  - Should save output image with bounding box drawn on it, with same name input image but place in the output folder 
- Try to train the best model


## Dataset Details
The dataset has in total 1041 images. Each image has a single object which is either a cat or a dog.
- There are multiple species for both cat and dog.
- The number of images falling in each specie is as follows:
  - basset_hound: 93
  - Birman: 93
  - pomeranian: 93
  - american_pit_bull_terrier: 93
  - american_bulldog: 93
  - Abyssinian: 92
  - beagle: 93
  - Persian: 93
  - chihuahua: 93
  - empty: 142
- The dataset has two folders:
  - images
    - Inside images folder we have 986 images in .jpg folder
  - labels
    - Inside labels folder we have 899 .xml files each file with details of image labels
    - For any image that does not have a cat or dog, there is no corresponding xml file

## Deliverable
- Updated Colab Based Jupyter Notebook:
  - With all the required functionality Implemented
  - Which one can train the model without any errors
  - One should achieve same metrics (Almost same metrics) if I run training using this collab notebook
    - Set default values for everything accordingly in the notebook
  - During evaluation we will just run the notebook and use the best weights the notebook saves automatically
- Best weights you have trained
  - We will Evaluate your weights against hold-out test we have and compare results
  - We will use visualize function to generate outputs for each image
  - Upload weights in an easily downloadable location like, Dropbox, Google Drive, Github, etc
- A video code-walk through explaining your design decisions including but not limited to:
  - Model Design which layers and activation functions you used and why
  - Loss function, which loss functions you used and why
  - Metrics, which metrics and why
  - Any optimizations you have made to the codebase
  - How you implemented resume functionality, what were the things you thought would be needed to resume training from exact same point


## Evaluation Criteria
 - Design Decisions
 - Completeness: Did you include all features?
 - Correctness: Does the solution (all deliverables) work in sensible, thought-out ways?
 - Maintainability: Is the code written in a clean, maintainable way?
 - Testing: Is the solution adequately tested?
 - Documentation: Is the codebase well-documented and has proper steps to run any of the deliverables?

## Extra Points
- Add metrics for the Bounding Box Output
- Any Updates in the notebook (Bugs/Implementation Mistakes etc)

## How to submit
- Please upload the Notebook for this project to GitHub, and post a link to your repository below [repo link box, on the left of submit button].
  - Create a new GitHub repository from scratch
  - Add the final Colab/Jupyter notebook to the repository
- Please upload video and your final best weights on Google Drive or any other platform, and paste the link to the folder with both video and model in the text box just above the submit button.
- Please paste the commit Id of the latest commit of your Github Repo, which should not be later than 5 hours of time when the repo was created.
  - Please note the submission without the commit id will not be considered.

# Install Required Modules


```python
! pip install bs4 lxml kaggle
```

    Looking in indexes: https://pypi.org/simple, https://us-python.pkg.dev/colab-wheels/public/simple/
    Collecting bs4
      Downloading bs4-0.0.1.tar.gz (1.1 kB)
      Preparing metadata (setup.py) ... [?25l[?25hdone
    Requirement already satisfied: lxml in /usr/local/lib/python3.10/dist-packages (4.9.2)
    Requirement already satisfied: kaggle in /usr/local/lib/python3.10/dist-packages (1.5.13)
    Requirement already satisfied: beautifulsoup4 in /usr/local/lib/python3.10/dist-packages (from bs4) (4.11.2)
    Requirement already satisfied: six>=1.10 in /usr/local/lib/python3.10/dist-packages (from kaggle) (1.16.0)
    Requirement already satisfied: certifi in /usr/local/lib/python3.10/dist-packages (from kaggle) (2022.12.7)
    Requirement already satisfied: python-dateutil in /usr/local/lib/python3.10/dist-packages (from kaggle) (2.8.2)
    Requirement already satisfied: requests in /usr/local/lib/python3.10/dist-packages (from kaggle) (2.27.1)
    Requirement already satisfied: tqdm in /usr/local/lib/python3.10/dist-packages (from kaggle) (4.65.0)
    Requirement already satisfied: python-slugify in /usr/local/lib/python3.10/dist-packages (from kaggle) (8.0.1)
    Requirement already satisfied: urllib3 in /usr/local/lib/python3.10/dist-packages (from kaggle) (1.26.15)
    Requirement already satisfied: soupsieve>1.2 in /usr/local/lib/python3.10/dist-packages (from beautifulsoup4->bs4) (2.4.1)
    Requirement already satisfied: text-unidecode>=1.3 in /usr/local/lib/python3.10/dist-packages (from python-slugify->kaggle) (1.3)
    Requirement already satisfied: charset-normalizer~=2.0.0 in /usr/local/lib/python3.10/dist-packages (from requests->kaggle) (2.0.12)
    Requirement already satisfied: idna<4,>=2.5 in /usr/local/lib/python3.10/dist-packages (from requests->kaggle) (3.4)
    Building wheels for collected packages: bs4
      Building wheel for bs4 (setup.py) ... [?25l[?25hdone
      Created wheel for bs4: filename=bs4-0.0.1-py3-none-any.whl size=1257 sha256=72e37ce27052b0b0a8670372128d5f2f5786c1923b7c3ff38f3daa9b666b7078
      Stored in directory: /root/.cache/pip/wheels/25/42/45/b773edc52acb16cd2db4cf1a0b47117e2f69bb4eb300ed0e70
    Successfully built bs4
    Installing collected packages: bs4
    Successfully installed bs4-0.0.1


# Download Dataset from Kaggle


```python
import os
os.environ['KAGGLE_USERNAME'] = 'bilalyousaf0014'
os.environ['KAGGLE_KEY'] = '11031bc21c5e3ec23585dbe17dc4267d'
```


```python
!kaggle datasets download -d bilalyousaf0014/ml-engineer-assessment-dataset
```

    Downloading ml-engineer-assessment-dataset.zip to /content
     73% 57.0M/78.6M [00:00<00:00, 90.9MB/s]
    100% 78.6M/78.6M [00:00<00:00, 127MB/s] 



```python
! unzip /content/ml-engineer-assessment-dataset.zip
```

    Archive:  /content/ml-engineer-assessment-dataset.zip
      inflating: assessment_dataset/images/00001.jpeg  
      inflating: assessment_dataset/images/00008.jpeg  
      inflating: assessment_dataset/images/00017.jpeg  
      inflating: assessment_dataset/images/00022.jpeg  
      inflating: assessment_dataset/images/00048.jpeg  
      inflating: assessment_dataset/images/00055.jpeg  
      inflating: assessment_dataset/images/001.jpeg  
      inflating: assessment_dataset/images/1.jpeg  
      inflating: assessment_dataset/images/1001524.jpeg  
      inflating: assessment_dataset/images/1005343.jpeg  
      inflating: assessment_dataset/images/1049854.jpeg  
      inflating: assessment_dataset/images/1072860.jpeg  
      inflating: assessment_dataset/images/1120419.jpeg  
      inflating: assessment_dataset/images/1146885.jpeg  
      inflating: assessment_dataset/images/2.jpeg  
      inflating: assessment_dataset/images/3.jpeg  
      inflating: assessment_dataset/images/4.jpeg  
      inflating: assessment_dataset/images/5.jpeg  
      inflating: assessment_dataset/images/Abyssinian_10.jpg  
      inflating: assessment_dataset/images/Abyssinian_100.jpg  
      inflating: assessment_dataset/images/Abyssinian_101.jpg  
      inflating: assessment_dataset/images/Abyssinian_102.jpg  
      inflating: assessment_dataset/images/Abyssinian_103.jpg  
      inflating: assessment_dataset/images/Abyssinian_105.jpg  
      inflating: assessment_dataset/images/Abyssinian_106.jpg  
      inflating: assessment_dataset/images/Abyssinian_107.jpg  
      inflating: assessment_dataset/images/Abyssinian_108.jpg  
      inflating: assessment_dataset/images/Abyssinian_109.jpg  
      inflating: assessment_dataset/images/Abyssinian_11.jpg  
      inflating: assessment_dataset/images/Abyssinian_111.jpg  
      inflating: assessment_dataset/images/Abyssinian_112.jpg  
      inflating: assessment_dataset/images/Abyssinian_113.jpg  
      inflating: assessment_dataset/images/Abyssinian_114.jpg  
      inflating: assessment_dataset/images/Abyssinian_115.jpg  
      inflating: assessment_dataset/images/Abyssinian_116.jpg  
      inflating: assessment_dataset/images/Abyssinian_117.jpg  
      inflating: assessment_dataset/images/Abyssinian_118.jpg  
      inflating: assessment_dataset/images/Abyssinian_119.jpg  
      inflating: assessment_dataset/images/Abyssinian_12.jpg  
      inflating: assessment_dataset/images/Abyssinian_120.jpg  
      inflating: assessment_dataset/images/Abyssinian_121.jpg  
      inflating: assessment_dataset/images/Abyssinian_122.jpg  
      inflating: assessment_dataset/images/Abyssinian_123.jpg  
      inflating: assessment_dataset/images/Abyssinian_125.jpg  
      inflating: assessment_dataset/images/Abyssinian_126.jpg  
      inflating: assessment_dataset/images/Abyssinian_127.jpg  
      inflating: assessment_dataset/images/Abyssinian_128.jpg  
      inflating: assessment_dataset/images/Abyssinian_129.jpg  
      inflating: assessment_dataset/images/Abyssinian_13.jpg  
      inflating: assessment_dataset/images/Abyssinian_130.jpg  
      inflating: assessment_dataset/images/Abyssinian_131.jpg  
      inflating: assessment_dataset/images/Abyssinian_132.jpg  
      inflating: assessment_dataset/images/Abyssinian_133.jpg  
      inflating: assessment_dataset/images/Abyssinian_135.jpg  
      inflating: assessment_dataset/images/Abyssinian_136.jpg  
      inflating: assessment_dataset/images/Abyssinian_137.jpg  
      inflating: assessment_dataset/images/Abyssinian_138.jpg  
      inflating: assessment_dataset/images/Abyssinian_139.jpg  
      inflating: assessment_dataset/images/Abyssinian_14.jpg  
      inflating: assessment_dataset/images/Abyssinian_141.jpg  
      inflating: assessment_dataset/images/Abyssinian_142.jpg  
      inflating: assessment_dataset/images/Abyssinian_143.jpg  
      inflating: assessment_dataset/images/Abyssinian_144.jpg  
      inflating: assessment_dataset/images/Abyssinian_145.jpg  
      inflating: assessment_dataset/images/Abyssinian_146.jpg  
      inflating: assessment_dataset/images/Abyssinian_148.jpg  
      inflating: assessment_dataset/images/Abyssinian_149.jpg  
      inflating: assessment_dataset/images/Abyssinian_15.jpg  
      inflating: assessment_dataset/images/Abyssinian_150.jpg  
      inflating: assessment_dataset/images/Abyssinian_151.jpg  
      inflating: assessment_dataset/images/Abyssinian_152.jpg  
      inflating: assessment_dataset/images/Abyssinian_153.jpg  
      inflating: assessment_dataset/images/Abyssinian_154.jpg  
      inflating: assessment_dataset/images/Abyssinian_155.jpg  
      inflating: assessment_dataset/images/Abyssinian_156.jpg  
      inflating: assessment_dataset/images/Abyssinian_157.jpg  
      inflating: assessment_dataset/images/Abyssinian_158.jpg  
      inflating: assessment_dataset/images/Abyssinian_159.jpg  
      inflating: assessment_dataset/images/Abyssinian_16.jpg  
      inflating: assessment_dataset/images/Abyssinian_160.jpg  
      inflating: assessment_dataset/images/Abyssinian_161.jpg  
      inflating: assessment_dataset/images/Abyssinian_164.jpg  
      inflating: assessment_dataset/images/Abyssinian_165.jpg  
      inflating: assessment_dataset/images/Abyssinian_166.jpg  
      inflating: assessment_dataset/images/Abyssinian_167.jpg  
      inflating: assessment_dataset/images/Abyssinian_168.jpg  
      inflating: assessment_dataset/images/Abyssinian_169.jpg  
      inflating: assessment_dataset/images/Abyssinian_17.jpg  
      inflating: assessment_dataset/images/Abyssinian_170.jpg  
      inflating: assessment_dataset/images/Abyssinian_172.jpg  
      inflating: assessment_dataset/images/Abyssinian_173.jpg  
      inflating: assessment_dataset/images/Abyssinian_174.jpg  
      inflating: assessment_dataset/images/Abyssinian_175.jpg  
      inflating: assessment_dataset/images/Abyssinian_176.jpg  
      inflating: assessment_dataset/images/Abyssinian_177.jpg  
      inflating: assessment_dataset/images/Abyssinian_178.jpg  
      inflating: assessment_dataset/images/Abyssinian_179.jpg  
      inflating: assessment_dataset/images/Abyssinian_180.jpg  
      inflating: assessment_dataset/images/Abyssinian_181.jpg  
      inflating: assessment_dataset/images/Abyssinian_182.jpg  
      inflating: assessment_dataset/images/Abyssinian_183.jpg  
      inflating: assessment_dataset/images/Abyssinian_184.jpg  
      inflating: assessment_dataset/images/Abyssinian_185.jpg  
      inflating: assessment_dataset/images/Abyssinian_19.jpg  
      inflating: assessment_dataset/images/Abyssinian_190.jpg  
      inflating: assessment_dataset/images/Abyssinian_191.jpg  
      inflating: assessment_dataset/images/Abyssinian_192.jpg  
      inflating: assessment_dataset/images/Abyssinian_193.jpg  
      inflating: assessment_dataset/images/Abyssinian_195.jpg  
      inflating: assessment_dataset/images/Abyssinian_196.jpg  
      inflating: assessment_dataset/images/Abyssinian_197.jpg  
      inflating: assessment_dataset/images/Birman_100.jpg  
      inflating: assessment_dataset/images/Birman_101.jpg  
      inflating: assessment_dataset/images/Birman_102.jpg  
      inflating: assessment_dataset/images/Birman_103.jpg  
      inflating: assessment_dataset/images/Birman_104.jpg  
      inflating: assessment_dataset/images/Birman_105.jpg  
      inflating: assessment_dataset/images/Birman_106.jpg  
      inflating: assessment_dataset/images/Birman_107.jpg  
      inflating: assessment_dataset/images/Birman_108.jpg  
      inflating: assessment_dataset/images/Birman_109.jpg  
      inflating: assessment_dataset/images/Birman_110.jpg  
      inflating: assessment_dataset/images/Birman_111.jpg  
      inflating: assessment_dataset/images/Birman_112.jpg  
      inflating: assessment_dataset/images/Birman_113.jpg  
      inflating: assessment_dataset/images/Birman_114.jpg  
      inflating: assessment_dataset/images/Birman_115.jpg  
      inflating: assessment_dataset/images/Birman_116.jpg  
      inflating: assessment_dataset/images/Birman_117.jpg  
      inflating: assessment_dataset/images/Birman_118.jpg  
      inflating: assessment_dataset/images/Birman_119.jpg  
      inflating: assessment_dataset/images/Birman_120.jpg  
      inflating: assessment_dataset/images/Birman_121.jpg  
      inflating: assessment_dataset/images/Birman_122.jpg  
      inflating: assessment_dataset/images/Birman_123.jpg  
      inflating: assessment_dataset/images/Birman_124.jpg  
      inflating: assessment_dataset/images/Birman_125.jpg  
      inflating: assessment_dataset/images/Birman_126.jpg  
      inflating: assessment_dataset/images/Birman_127.jpg  
      inflating: assessment_dataset/images/Birman_128.jpg  
      inflating: assessment_dataset/images/Birman_129.jpg  
      inflating: assessment_dataset/images/Birman_130.jpg  
      inflating: assessment_dataset/images/Birman_131.jpg  
      inflating: assessment_dataset/images/Birman_132.jpg  
      inflating: assessment_dataset/images/Birman_133.jpg  
      inflating: assessment_dataset/images/Birman_134.jpg  
      inflating: assessment_dataset/images/Birman_135.jpg  
      inflating: assessment_dataset/images/Birman_136.jpg  
      inflating: assessment_dataset/images/Birman_137.jpg  
      inflating: assessment_dataset/images/Birman_138.jpg  
      inflating: assessment_dataset/images/Birman_139.jpg  
      inflating: assessment_dataset/images/Birman_140.jpg  
      inflating: assessment_dataset/images/Birman_141.jpg  
      inflating: assessment_dataset/images/Birman_142.jpg  
      inflating: assessment_dataset/images/Birman_143.jpg  
      inflating: assessment_dataset/images/Birman_144.jpg  
      inflating: assessment_dataset/images/Birman_145.jpg  
      inflating: assessment_dataset/images/Birman_146.jpg  
      inflating: assessment_dataset/images/Birman_147.jpg  
      inflating: assessment_dataset/images/Birman_148.jpg  
      inflating: assessment_dataset/images/Birman_149.jpg  
      inflating: assessment_dataset/images/Birman_150.jpg  
      inflating: assessment_dataset/images/Birman_151.jpg  
      inflating: assessment_dataset/images/Birman_152.jpg  
      inflating: assessment_dataset/images/Birman_153.jpg  
      inflating: assessment_dataset/images/Birman_154.jpg  
      inflating: assessment_dataset/images/Birman_155.jpg  
      inflating: assessment_dataset/images/Birman_156.jpg  
      inflating: assessment_dataset/images/Birman_157.jpg  
      inflating: assessment_dataset/images/Birman_158.jpg  
      inflating: assessment_dataset/images/Birman_159.jpg  
      inflating: assessment_dataset/images/Birman_16.jpg  
      inflating: assessment_dataset/images/Birman_160.jpg  
      inflating: assessment_dataset/images/Birman_161.jpg  
      inflating: assessment_dataset/images/Birman_162.jpg  
      inflating: assessment_dataset/images/Birman_163.jpg  
      inflating: assessment_dataset/images/Birman_164.jpg  
      inflating: assessment_dataset/images/Birman_165.jpg  
      inflating: assessment_dataset/images/Birman_166.jpg  
      inflating: assessment_dataset/images/Birman_167.jpg  
      inflating: assessment_dataset/images/Birman_168.jpg  
      inflating: assessment_dataset/images/Birman_169.jpg  
      inflating: assessment_dataset/images/Birman_17.jpg  
      inflating: assessment_dataset/images/Birman_170.jpg  
      inflating: assessment_dataset/images/Birman_171.jpg  
      inflating: assessment_dataset/images/Birman_172.jpg  
      inflating: assessment_dataset/images/Birman_173.jpg  
      inflating: assessment_dataset/images/Birman_174.jpg  
      inflating: assessment_dataset/images/Birman_175.jpg  
      inflating: assessment_dataset/images/Birman_176.jpg  
      inflating: assessment_dataset/images/Birman_177.jpg  
      inflating: assessment_dataset/images/Birman_178.jpg  
      inflating: assessment_dataset/images/Birman_179.jpg  
      inflating: assessment_dataset/images/Birman_18.jpg  
      inflating: assessment_dataset/images/Birman_180.jpg  
      inflating: assessment_dataset/images/Birman_181.jpg  
      inflating: assessment_dataset/images/Birman_182.jpg  
      inflating: assessment_dataset/images/Birman_183.jpg  
      inflating: assessment_dataset/images/Birman_184.jpg  
      inflating: assessment_dataset/images/Birman_185.jpg  
      inflating: assessment_dataset/images/Birman_186.jpg  
      inflating: assessment_dataset/images/Birman_187.jpg  
      inflating: assessment_dataset/images/Birman_188.jpg  
      inflating: assessment_dataset/images/Birman_189.jpg  
      inflating: assessment_dataset/images/Birman_190.jpg  
      inflating: assessment_dataset/images/Cars0.png  
      inflating: assessment_dataset/images/Cars144.png  
      inflating: assessment_dataset/images/Persian_100.jpg  
      inflating: assessment_dataset/images/Persian_101.jpg  
      inflating: assessment_dataset/images/Persian_102.jpg  
      inflating: assessment_dataset/images/Persian_103.jpg  
      inflating: assessment_dataset/images/Persian_104.jpg  
      inflating: assessment_dataset/images/Persian_105.jpg  
      inflating: assessment_dataset/images/Persian_106.jpg  
      inflating: assessment_dataset/images/Persian_107.jpg  
      inflating: assessment_dataset/images/Persian_108.jpg  
      inflating: assessment_dataset/images/Persian_111.jpg  
      inflating: assessment_dataset/images/Persian_112.jpg  
      inflating: assessment_dataset/images/Persian_114.jpg  
      inflating: assessment_dataset/images/Persian_115.jpg  
      inflating: assessment_dataset/images/Persian_116.jpg  
      inflating: assessment_dataset/images/Persian_117.jpg  
      inflating: assessment_dataset/images/Persian_118.jpg  
      inflating: assessment_dataset/images/Persian_120.jpg  
      inflating: assessment_dataset/images/Persian_121.jpg  
      inflating: assessment_dataset/images/Persian_122.jpg  
      inflating: assessment_dataset/images/Persian_123.jpg  
      inflating: assessment_dataset/images/Persian_125.jpg  
      inflating: assessment_dataset/images/Persian_126.jpg  
      inflating: assessment_dataset/images/Persian_128.jpg  
      inflating: assessment_dataset/images/Persian_129.jpg  
      inflating: assessment_dataset/images/Persian_131.jpg  
      inflating: assessment_dataset/images/Persian_132.jpg  
      inflating: assessment_dataset/images/Persian_133.jpg  
      inflating: assessment_dataset/images/Persian_134.jpg  
      inflating: assessment_dataset/images/Persian_135.jpg  
      inflating: assessment_dataset/images/Persian_136.jpg  
      inflating: assessment_dataset/images/Persian_137.jpg  
      inflating: assessment_dataset/images/Persian_138.jpg  
      inflating: assessment_dataset/images/Persian_139.jpg  
      inflating: assessment_dataset/images/Persian_140.jpg  
      inflating: assessment_dataset/images/Persian_141.jpg  
      inflating: assessment_dataset/images/Persian_143.jpg  
      inflating: assessment_dataset/images/Persian_144.jpg  
      inflating: assessment_dataset/images/Persian_145.jpg  
      inflating: assessment_dataset/images/Persian_147.jpg  
      inflating: assessment_dataset/images/Persian_149.jpg  
      inflating: assessment_dataset/images/Persian_15.jpg  
      inflating: assessment_dataset/images/Persian_150.jpg  
      inflating: assessment_dataset/images/Persian_152.jpg  
      inflating: assessment_dataset/images/Persian_153.jpg  
      inflating: assessment_dataset/images/Persian_155.jpg  
      inflating: assessment_dataset/images/Persian_156.jpg  
      inflating: assessment_dataset/images/Persian_158.jpg  
      inflating: assessment_dataset/images/Persian_159.jpg  
      inflating: assessment_dataset/images/Persian_16.jpg  
      inflating: assessment_dataset/images/Persian_160.jpg  
      inflating: assessment_dataset/images/Persian_161.jpg  
      inflating: assessment_dataset/images/Persian_162.jpg  
      inflating: assessment_dataset/images/Persian_163.jpg  
      inflating: assessment_dataset/images/Persian_164.jpg  
      inflating: assessment_dataset/images/Persian_165.jpg  
      inflating: assessment_dataset/images/Persian_166.jpg  
      inflating: assessment_dataset/images/Persian_168.jpg  
      inflating: assessment_dataset/images/Persian_169.jpg  
      inflating: assessment_dataset/images/Persian_17.jpg  
      inflating: assessment_dataset/images/Persian_170.jpg  
      inflating: assessment_dataset/images/Persian_171.jpg  
      inflating: assessment_dataset/images/Persian_172.jpg  
      inflating: assessment_dataset/images/Persian_173.jpg  
      inflating: assessment_dataset/images/Persian_174.jpg  
      inflating: assessment_dataset/images/Persian_175.jpg  
      inflating: assessment_dataset/images/Persian_176.jpg  
      inflating: assessment_dataset/images/Persian_179.jpg  
      inflating: assessment_dataset/images/Persian_18.jpg  
      inflating: assessment_dataset/images/Persian_180.jpg  
      inflating: assessment_dataset/images/Persian_181.jpg  
      inflating: assessment_dataset/images/Persian_182.jpg  
      inflating: assessment_dataset/images/Persian_183.jpg  
      inflating: assessment_dataset/images/Persian_184.jpg  
      inflating: assessment_dataset/images/Persian_185.jpg  
      inflating: assessment_dataset/images/Persian_186.jpg  
      inflating: assessment_dataset/images/Persian_187.jpg  
      inflating: assessment_dataset/images/Persian_188.jpg  
      inflating: assessment_dataset/images/Persian_189.jpg  
      inflating: assessment_dataset/images/Persian_19.jpg  
      inflating: assessment_dataset/images/Persian_190.jpg  
      inflating: assessment_dataset/images/Persian_191.jpg  
      inflating: assessment_dataset/images/Persian_192.jpg  
      inflating: assessment_dataset/images/Persian_193.jpg  
      inflating: assessment_dataset/images/Persian_194.jpg  
      inflating: assessment_dataset/images/Persian_195.jpg  
      inflating: assessment_dataset/images/Persian_196.jpg  
      inflating: assessment_dataset/images/Persian_197.jpg  
      inflating: assessment_dataset/images/Persian_20.jpg  
      inflating: assessment_dataset/images/Persian_200.jpg  
      inflating: assessment_dataset/images/Persian_201.jpg  
      inflating: assessment_dataset/images/Persian_202.jpg  
      inflating: assessment_dataset/images/Persian_206.jpg  
      inflating: assessment_dataset/images/Persian_213.jpg  
      inflating: assessment_dataset/images/Persian_217.jpg  
      inflating: assessment_dataset/images/american_bulldog_10.jpg  
      inflating: assessment_dataset/images/american_bulldog_100.jpg  
      inflating: assessment_dataset/images/american_bulldog_101.jpg  
      inflating: assessment_dataset/images/american_bulldog_103.jpg  
      inflating: assessment_dataset/images/american_bulldog_104.jpg  
      inflating: assessment_dataset/images/american_bulldog_105.jpg  
      inflating: assessment_dataset/images/american_bulldog_106.jpg  
      inflating: assessment_dataset/images/american_bulldog_107.jpg  
      inflating: assessment_dataset/images/american_bulldog_109.jpg  
      inflating: assessment_dataset/images/american_bulldog_11.jpg  
      inflating: assessment_dataset/images/american_bulldog_110.jpg  
      inflating: assessment_dataset/images/american_bulldog_111.jpg  
      inflating: assessment_dataset/images/american_bulldog_112.jpg  
      inflating: assessment_dataset/images/american_bulldog_113.jpg  
      inflating: assessment_dataset/images/american_bulldog_115.jpg  
      inflating: assessment_dataset/images/american_bulldog_116.jpg  
      inflating: assessment_dataset/images/american_bulldog_117.jpg  
      inflating: assessment_dataset/images/american_bulldog_118.jpg  
      inflating: assessment_dataset/images/american_bulldog_119.jpg  
      inflating: assessment_dataset/images/american_bulldog_12.jpg  
      inflating: assessment_dataset/images/american_bulldog_121.jpg  
      inflating: assessment_dataset/images/american_bulldog_122.jpg  
      inflating: assessment_dataset/images/american_bulldog_123.jpg  
      inflating: assessment_dataset/images/american_bulldog_124.jpg  
      inflating: assessment_dataset/images/american_bulldog_125.jpg  
      inflating: assessment_dataset/images/american_bulldog_127.jpg  
      inflating: assessment_dataset/images/american_bulldog_128.jpg  
      inflating: assessment_dataset/images/american_bulldog_129.jpg  
      inflating: assessment_dataset/images/american_bulldog_13.jpg  
      inflating: assessment_dataset/images/american_bulldog_130.jpg  
      inflating: assessment_dataset/images/american_bulldog_131.jpg  
      inflating: assessment_dataset/images/american_bulldog_132.jpg  
      inflating: assessment_dataset/images/american_bulldog_133.jpg  
      inflating: assessment_dataset/images/american_bulldog_134.jpg  
      inflating: assessment_dataset/images/american_bulldog_135.jpg  
      inflating: assessment_dataset/images/american_bulldog_136.jpg  
      inflating: assessment_dataset/images/american_bulldog_137.jpg  
      inflating: assessment_dataset/images/american_bulldog_138.jpg  
      inflating: assessment_dataset/images/american_bulldog_139.jpg  
      inflating: assessment_dataset/images/american_bulldog_14.jpg  
      inflating: assessment_dataset/images/american_bulldog_140.jpg  
      inflating: assessment_dataset/images/american_bulldog_141.jpg  
      inflating: assessment_dataset/images/american_bulldog_142.jpg  
      inflating: assessment_dataset/images/american_bulldog_143.jpg  
      inflating: assessment_dataset/images/american_bulldog_144.jpg  
      inflating: assessment_dataset/images/american_bulldog_146.jpg  
      inflating: assessment_dataset/images/american_bulldog_147.jpg  
      inflating: assessment_dataset/images/american_bulldog_148.jpg  
      inflating: assessment_dataset/images/american_bulldog_149.jpg  
      inflating: assessment_dataset/images/american_bulldog_150.jpg  
      inflating: assessment_dataset/images/american_bulldog_151.jpg  
      inflating: assessment_dataset/images/american_bulldog_152.jpg  
      inflating: assessment_dataset/images/american_bulldog_153.jpg  
      inflating: assessment_dataset/images/american_bulldog_158.jpg  
      inflating: assessment_dataset/images/american_bulldog_16.jpg  
      inflating: assessment_dataset/images/american_bulldog_161.jpg  
      inflating: assessment_dataset/images/american_bulldog_164.jpg  
      inflating: assessment_dataset/images/american_bulldog_166.jpg  
      inflating: assessment_dataset/images/american_bulldog_167.jpg  
      inflating: assessment_dataset/images/american_bulldog_168.jpg  
      inflating: assessment_dataset/images/american_bulldog_169.jpg  
      inflating: assessment_dataset/images/american_bulldog_171.jpg  
      inflating: assessment_dataset/images/american_bulldog_172.jpg  
      inflating: assessment_dataset/images/american_bulldog_173.jpg  
      inflating: assessment_dataset/images/american_bulldog_174.jpg  
      inflating: assessment_dataset/images/american_bulldog_175.jpg  
      inflating: assessment_dataset/images/american_bulldog_176.jpg  
      inflating: assessment_dataset/images/american_bulldog_177.jpg  
      inflating: assessment_dataset/images/american_bulldog_178.jpg  
      inflating: assessment_dataset/images/american_bulldog_179.jpg  
      inflating: assessment_dataset/images/american_bulldog_18.jpg  
      inflating: assessment_dataset/images/american_bulldog_180.jpg  
      inflating: assessment_dataset/images/american_bulldog_181.jpg  
      inflating: assessment_dataset/images/american_bulldog_182.jpg  
      inflating: assessment_dataset/images/american_bulldog_183.jpg  
      inflating: assessment_dataset/images/american_bulldog_184.jpg  
      inflating: assessment_dataset/images/american_bulldog_185.jpg  
      inflating: assessment_dataset/images/american_bulldog_186.jpg  
      inflating: assessment_dataset/images/american_bulldog_187.jpg  
      inflating: assessment_dataset/images/american_bulldog_188.jpg  
      inflating: assessment_dataset/images/american_bulldog_189.jpg  
      inflating: assessment_dataset/images/american_bulldog_19.jpg  
      inflating: assessment_dataset/images/american_bulldog_190.jpg  
      inflating: assessment_dataset/images/american_bulldog_191.jpg  
      inflating: assessment_dataset/images/american_bulldog_192.jpg  
      inflating: assessment_dataset/images/american_bulldog_193.jpg  
      inflating: assessment_dataset/images/american_bulldog_194.jpg  
      inflating: assessment_dataset/images/american_bulldog_196.jpg  
      inflating: assessment_dataset/images/american_bulldog_197.jpg  
      inflating: assessment_dataset/images/american_bulldog_198.jpg  
      inflating: assessment_dataset/images/american_bulldog_199.jpg  
      inflating: assessment_dataset/images/american_bulldog_200.jpg  
      inflating: assessment_dataset/images/american_bulldog_201.jpg  
      inflating: assessment_dataset/images/american_bulldog_202.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_100.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_101.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_102.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_103.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_104.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_105.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_106.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_107.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_108.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_109.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_110.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_111.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_112.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_113.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_114.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_115.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_116.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_117.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_118.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_119.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_120.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_121.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_122.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_123.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_124.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_125.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_126.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_127.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_128.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_129.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_130.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_131.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_132.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_133.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_134.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_135.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_136.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_137.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_138.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_139.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_140.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_141.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_142.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_143.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_144.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_145.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_146.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_147.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_148.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_149.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_150.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_151.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_152.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_153.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_154.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_155.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_156.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_157.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_158.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_159.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_16.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_160.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_161.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_162.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_163.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_164.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_165.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_166.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_167.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_168.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_169.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_17.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_170.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_171.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_172.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_173.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_174.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_175.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_176.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_177.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_178.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_179.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_18.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_180.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_181.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_182.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_183.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_184.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_185.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_186.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_187.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_188.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_189.jpg  
      inflating: assessment_dataset/images/american_pit_bull_terrier_190.jpg  
      inflating: assessment_dataset/images/basset_hound_100.jpg  
      inflating: assessment_dataset/images/basset_hound_101.jpg  
      inflating: assessment_dataset/images/basset_hound_102.jpg  
      inflating: assessment_dataset/images/basset_hound_103.jpg  
      inflating: assessment_dataset/images/basset_hound_104.jpg  
      inflating: assessment_dataset/images/basset_hound_105.jpg  
      inflating: assessment_dataset/images/basset_hound_106.jpg  
      inflating: assessment_dataset/images/basset_hound_107.jpg  
      inflating: assessment_dataset/images/basset_hound_108.jpg  
      inflating: assessment_dataset/images/basset_hound_109.jpg  
      inflating: assessment_dataset/images/basset_hound_110.jpg  
      inflating: assessment_dataset/images/basset_hound_111.jpg  
      inflating: assessment_dataset/images/basset_hound_112.jpg  
      inflating: assessment_dataset/images/basset_hound_113.jpg  
      inflating: assessment_dataset/images/basset_hound_114.jpg  
      inflating: assessment_dataset/images/basset_hound_115.jpg  
      inflating: assessment_dataset/images/basset_hound_116.jpg  
      inflating: assessment_dataset/images/basset_hound_117.jpg  
      inflating: assessment_dataset/images/basset_hound_118.jpg  
      inflating: assessment_dataset/images/basset_hound_119.jpg  
      inflating: assessment_dataset/images/basset_hound_120.jpg  
      inflating: assessment_dataset/images/basset_hound_121.jpg  
      inflating: assessment_dataset/images/basset_hound_122.jpg  
      inflating: assessment_dataset/images/basset_hound_123.jpg  
      inflating: assessment_dataset/images/basset_hound_124.jpg  
      inflating: assessment_dataset/images/basset_hound_125.jpg  
      inflating: assessment_dataset/images/basset_hound_126.jpg  
      inflating: assessment_dataset/images/basset_hound_127.jpg  
      inflating: assessment_dataset/images/basset_hound_128.jpg  
      inflating: assessment_dataset/images/basset_hound_129.jpg  
      inflating: assessment_dataset/images/basset_hound_130.jpg  
      inflating: assessment_dataset/images/basset_hound_131.jpg  
      inflating: assessment_dataset/images/basset_hound_132.jpg  
      inflating: assessment_dataset/images/basset_hound_133.jpg  
      inflating: assessment_dataset/images/basset_hound_134.jpg  
      inflating: assessment_dataset/images/basset_hound_135.jpg  
      inflating: assessment_dataset/images/basset_hound_136.jpg  
      inflating: assessment_dataset/images/basset_hound_137.jpg  
      inflating: assessment_dataset/images/basset_hound_138.jpg  
      inflating: assessment_dataset/images/basset_hound_139.jpg  
      inflating: assessment_dataset/images/basset_hound_140.jpg  
      inflating: assessment_dataset/images/basset_hound_141.jpg  
      inflating: assessment_dataset/images/basset_hound_142.jpg  
      inflating: assessment_dataset/images/basset_hound_143.jpg  
      inflating: assessment_dataset/images/basset_hound_144.jpg  
      inflating: assessment_dataset/images/basset_hound_145.jpg  
      inflating: assessment_dataset/images/basset_hound_146.jpg  
      inflating: assessment_dataset/images/basset_hound_147.jpg  
      inflating: assessment_dataset/images/basset_hound_148.jpg  
      inflating: assessment_dataset/images/basset_hound_149.jpg  
      inflating: assessment_dataset/images/basset_hound_150.jpg  
      inflating: assessment_dataset/images/basset_hound_151.jpg  
      inflating: assessment_dataset/images/basset_hound_152.jpg  
      inflating: assessment_dataset/images/basset_hound_153.jpg  
      inflating: assessment_dataset/images/basset_hound_154.jpg  
      inflating: assessment_dataset/images/basset_hound_155.jpg  
      inflating: assessment_dataset/images/basset_hound_156.jpg  
      inflating: assessment_dataset/images/basset_hound_157.jpg  
      inflating: assessment_dataset/images/basset_hound_158.jpg  
      inflating: assessment_dataset/images/basset_hound_159.jpg  
      inflating: assessment_dataset/images/basset_hound_16.jpg  
      inflating: assessment_dataset/images/basset_hound_160.jpg  
      inflating: assessment_dataset/images/basset_hound_161.jpg  
      inflating: assessment_dataset/images/basset_hound_162.jpg  
      inflating: assessment_dataset/images/basset_hound_163.jpg  
      inflating: assessment_dataset/images/basset_hound_164.jpg  
      inflating: assessment_dataset/images/basset_hound_165.jpg  
      inflating: assessment_dataset/images/basset_hound_166.jpg  
      inflating: assessment_dataset/images/basset_hound_167.jpg  
      inflating: assessment_dataset/images/basset_hound_168.jpg  
      inflating: assessment_dataset/images/basset_hound_169.jpg  
      inflating: assessment_dataset/images/basset_hound_17.jpg  
      inflating: assessment_dataset/images/basset_hound_170.jpg  
      inflating: assessment_dataset/images/basset_hound_171.jpg  
      inflating: assessment_dataset/images/basset_hound_172.jpg  
      inflating: assessment_dataset/images/basset_hound_173.jpg  
      inflating: assessment_dataset/images/basset_hound_174.jpg  
      inflating: assessment_dataset/images/basset_hound_175.jpg  
      inflating: assessment_dataset/images/basset_hound_176.jpg  
      inflating: assessment_dataset/images/basset_hound_177.jpg  
      inflating: assessment_dataset/images/basset_hound_178.jpg  
      inflating: assessment_dataset/images/basset_hound_179.jpg  
      inflating: assessment_dataset/images/basset_hound_18.jpg  
      inflating: assessment_dataset/images/basset_hound_180.jpg  
      inflating: assessment_dataset/images/basset_hound_181.jpg  
      inflating: assessment_dataset/images/basset_hound_182.jpg  
      inflating: assessment_dataset/images/basset_hound_183.jpg  
      inflating: assessment_dataset/images/basset_hound_184.jpg  
      inflating: assessment_dataset/images/basset_hound_185.jpg  
      inflating: assessment_dataset/images/basset_hound_186.jpg  
      inflating: assessment_dataset/images/basset_hound_187.jpg  
      inflating: assessment_dataset/images/basset_hound_188.jpg  
      inflating: assessment_dataset/images/basset_hound_189.jpg  
      inflating: assessment_dataset/images/basset_hound_190.jpg  
      inflating: assessment_dataset/images/beagle_100.jpg  
      inflating: assessment_dataset/images/beagle_101.jpg  
      inflating: assessment_dataset/images/beagle_102.jpg  
      inflating: assessment_dataset/images/beagle_103.jpg  
      inflating: assessment_dataset/images/beagle_104.jpg  
      inflating: assessment_dataset/images/beagle_105.jpg  
      inflating: assessment_dataset/images/beagle_107.jpg  
      inflating: assessment_dataset/images/beagle_108.jpg  
      inflating: assessment_dataset/images/beagle_109.jpg  
      inflating: assessment_dataset/images/beagle_110.jpg  
      inflating: assessment_dataset/images/beagle_111.jpg  
      inflating: assessment_dataset/images/beagle_112.jpg  
      inflating: assessment_dataset/images/beagle_113.jpg  
      inflating: assessment_dataset/images/beagle_114.jpg  
      inflating: assessment_dataset/images/beagle_115.jpg  
      inflating: assessment_dataset/images/beagle_116.jpg  
      inflating: assessment_dataset/images/beagle_117.jpg  
      inflating: assessment_dataset/images/beagle_118.jpg  
      inflating: assessment_dataset/images/beagle_119.jpg  
      inflating: assessment_dataset/images/beagle_120.jpg  
      inflating: assessment_dataset/images/beagle_121.jpg  
      inflating: assessment_dataset/images/beagle_122.jpg  
      inflating: assessment_dataset/images/beagle_123.jpg  
      inflating: assessment_dataset/images/beagle_124.jpg  
      inflating: assessment_dataset/images/beagle_125.jpg  
      inflating: assessment_dataset/images/beagle_126.jpg  
      inflating: assessment_dataset/images/beagle_127.jpg  
      inflating: assessment_dataset/images/beagle_128.jpg  
      inflating: assessment_dataset/images/beagle_129.jpg  
      inflating: assessment_dataset/images/beagle_130.jpg  
      inflating: assessment_dataset/images/beagle_131.jpg  
      inflating: assessment_dataset/images/beagle_133.jpg  
      inflating: assessment_dataset/images/beagle_134.jpg  
      inflating: assessment_dataset/images/beagle_135.jpg  
      inflating: assessment_dataset/images/beagle_136.jpg  
      inflating: assessment_dataset/images/beagle_137.jpg  
      inflating: assessment_dataset/images/beagle_138.jpg  
      inflating: assessment_dataset/images/beagle_139.jpg  
      inflating: assessment_dataset/images/beagle_140.jpg  
      inflating: assessment_dataset/images/beagle_141.jpg  
      inflating: assessment_dataset/images/beagle_142.jpg  
      inflating: assessment_dataset/images/beagle_143.jpg  
      inflating: assessment_dataset/images/beagle_144.jpg  
      inflating: assessment_dataset/images/beagle_145.jpg  
      inflating: assessment_dataset/images/beagle_146.jpg  
      inflating: assessment_dataset/images/beagle_147.jpg  
      inflating: assessment_dataset/images/beagle_148.jpg  
      inflating: assessment_dataset/images/beagle_149.jpg  
      inflating: assessment_dataset/images/beagle_150.jpg  
      inflating: assessment_dataset/images/beagle_151.jpg  
      inflating: assessment_dataset/images/beagle_152.jpg  
      inflating: assessment_dataset/images/beagle_153.jpg  
      inflating: assessment_dataset/images/beagle_154.jpg  
      inflating: assessment_dataset/images/beagle_155.jpg  
      inflating: assessment_dataset/images/beagle_156.jpg  
      inflating: assessment_dataset/images/beagle_157.jpg  
      inflating: assessment_dataset/images/beagle_158.jpg  
      inflating: assessment_dataset/images/beagle_160.jpg  
      inflating: assessment_dataset/images/beagle_161.jpg  
      inflating: assessment_dataset/images/beagle_162.jpg  
      inflating: assessment_dataset/images/beagle_163.jpg  
      inflating: assessment_dataset/images/beagle_164.jpg  
      inflating: assessment_dataset/images/beagle_165.jpg  
      inflating: assessment_dataset/images/beagle_166.jpg  
      inflating: assessment_dataset/images/beagle_167.jpg  
      inflating: assessment_dataset/images/beagle_168.jpg  
      inflating: assessment_dataset/images/beagle_169.jpg  
      inflating: assessment_dataset/images/beagle_17.jpg  
      inflating: assessment_dataset/images/beagle_170.jpg  
      inflating: assessment_dataset/images/beagle_171.jpg  
      inflating: assessment_dataset/images/beagle_172.jpg  
      inflating: assessment_dataset/images/beagle_173.jpg  
      inflating: assessment_dataset/images/beagle_174.jpg  
      inflating: assessment_dataset/images/beagle_175.jpg  
      inflating: assessment_dataset/images/beagle_176.jpg  
      inflating: assessment_dataset/images/beagle_177.jpg  
      inflating: assessment_dataset/images/beagle_178.jpg  
      inflating: assessment_dataset/images/beagle_179.jpg  
      inflating: assessment_dataset/images/beagle_18.jpg  
      inflating: assessment_dataset/images/beagle_180.jpg  
      inflating: assessment_dataset/images/beagle_181.jpg  
      inflating: assessment_dataset/images/beagle_182.jpg  
      inflating: assessment_dataset/images/beagle_183.jpg  
      inflating: assessment_dataset/images/beagle_184.jpg  
      inflating: assessment_dataset/images/beagle_185.jpg  
      inflating: assessment_dataset/images/beagle_186.jpg  
      inflating: assessment_dataset/images/beagle_187.jpg  
      inflating: assessment_dataset/images/beagle_188.jpg  
      inflating: assessment_dataset/images/beagle_189.jpg  
      inflating: assessment_dataset/images/beagle_190.jpg  
      inflating: assessment_dataset/images/beagle_191.jpg  
      inflating: assessment_dataset/images/beagle_192.jpg  
      inflating: assessment_dataset/images/beagle_193.jpg  
      inflating: assessment_dataset/images/beagle_194.jpg  
      inflating: assessment_dataset/images/chihuahua_100.jpg  
      inflating: assessment_dataset/images/chihuahua_101.jpg  
      inflating: assessment_dataset/images/chihuahua_102.jpg  
      inflating: assessment_dataset/images/chihuahua_103.jpg  
      inflating: assessment_dataset/images/chihuahua_104.jpg  
      inflating: assessment_dataset/images/chihuahua_105.jpg  
      inflating: assessment_dataset/images/chihuahua_106.jpg  
      inflating: assessment_dataset/images/chihuahua_107.jpg  
      inflating: assessment_dataset/images/chihuahua_108.jpg  
      inflating: assessment_dataset/images/chihuahua_109.jpg  
      inflating: assessment_dataset/images/chihuahua_110.jpg  
      inflating: assessment_dataset/images/chihuahua_111.jpg  
      inflating: assessment_dataset/images/chihuahua_112.jpg  
      inflating: assessment_dataset/images/chihuahua_113.jpg  
      inflating: assessment_dataset/images/chihuahua_114.jpg  
      inflating: assessment_dataset/images/chihuahua_115.jpg  
      inflating: assessment_dataset/images/chihuahua_116.jpg  
      inflating: assessment_dataset/images/chihuahua_117.jpg  
      inflating: assessment_dataset/images/chihuahua_118.jpg  
      inflating: assessment_dataset/images/chihuahua_119.jpg  
      inflating: assessment_dataset/images/chihuahua_120.jpg  
      inflating: assessment_dataset/images/chihuahua_121.jpg  
      inflating: assessment_dataset/images/chihuahua_122.jpg  
      inflating: assessment_dataset/images/chihuahua_123.jpg  
      inflating: assessment_dataset/images/chihuahua_124.jpg  
      inflating: assessment_dataset/images/chihuahua_125.jpg  
      inflating: assessment_dataset/images/chihuahua_126.jpg  
      inflating: assessment_dataset/images/chihuahua_127.jpg  
      inflating: assessment_dataset/images/chihuahua_128.jpg  
      inflating: assessment_dataset/images/chihuahua_129.jpg  
      inflating: assessment_dataset/images/chihuahua_130.jpg  
      inflating: assessment_dataset/images/chihuahua_131.jpg  
      inflating: assessment_dataset/images/chihuahua_132.jpg  
      inflating: assessment_dataset/images/chihuahua_133.jpg  
      inflating: assessment_dataset/images/chihuahua_134.jpg  
      inflating: assessment_dataset/images/chihuahua_135.jpg  
      inflating: assessment_dataset/images/chihuahua_136.jpg  
      inflating: assessment_dataset/images/chihuahua_137.jpg  
      inflating: assessment_dataset/images/chihuahua_138.jpg  
      inflating: assessment_dataset/images/chihuahua_139.jpg  
      inflating: assessment_dataset/images/chihuahua_140.jpg  
      inflating: assessment_dataset/images/chihuahua_141.jpg  
      inflating: assessment_dataset/images/chihuahua_142.jpg  
      inflating: assessment_dataset/images/chihuahua_143.jpg  
      inflating: assessment_dataset/images/chihuahua_144.jpg  
      inflating: assessment_dataset/images/chihuahua_145.jpg  
      inflating: assessment_dataset/images/chihuahua_146.jpg  
      inflating: assessment_dataset/images/chihuahua_147.jpg  
      inflating: assessment_dataset/images/chihuahua_148.jpg  
      inflating: assessment_dataset/images/chihuahua_149.jpg  
      inflating: assessment_dataset/images/chihuahua_150.jpg  
      inflating: assessment_dataset/images/chihuahua_151.jpg  
      inflating: assessment_dataset/images/chihuahua_152.jpg  
      inflating: assessment_dataset/images/chihuahua_153.jpg  
      inflating: assessment_dataset/images/chihuahua_154.jpg  
      inflating: assessment_dataset/images/chihuahua_155.jpg  
      inflating: assessment_dataset/images/chihuahua_156.jpg  
      inflating: assessment_dataset/images/chihuahua_157.jpg  
      inflating: assessment_dataset/images/chihuahua_158.jpg  
      inflating: assessment_dataset/images/chihuahua_159.jpg  
      inflating: assessment_dataset/images/chihuahua_16.jpg  
      inflating: assessment_dataset/images/chihuahua_160.jpg  
      inflating: assessment_dataset/images/chihuahua_161.jpg  
      inflating: assessment_dataset/images/chihuahua_162.jpg  
      inflating: assessment_dataset/images/chihuahua_163.jpg  
      inflating: assessment_dataset/images/chihuahua_164.jpg  
      inflating: assessment_dataset/images/chihuahua_165.jpg  
      inflating: assessment_dataset/images/chihuahua_166.jpg  
      inflating: assessment_dataset/images/chihuahua_167.jpg  
      inflating: assessment_dataset/images/chihuahua_168.jpg  
      inflating: assessment_dataset/images/chihuahua_169.jpg  
      inflating: assessment_dataset/images/chihuahua_17.jpg  
      inflating: assessment_dataset/images/chihuahua_170.jpg  
      inflating: assessment_dataset/images/chihuahua_171.jpg  
      inflating: assessment_dataset/images/chihuahua_172.jpg  
      inflating: assessment_dataset/images/chihuahua_173.jpg  
      inflating: assessment_dataset/images/chihuahua_174.jpg  
      inflating: assessment_dataset/images/chihuahua_175.jpg  
      inflating: assessment_dataset/images/chihuahua_176.jpg  
      inflating: assessment_dataset/images/chihuahua_177.jpg  
      inflating: assessment_dataset/images/chihuahua_178.jpg  
      inflating: assessment_dataset/images/chihuahua_179.jpg  
      inflating: assessment_dataset/images/chihuahua_18.jpg  
      inflating: assessment_dataset/images/chihuahua_180.jpg  
      inflating: assessment_dataset/images/chihuahua_181.jpg  
      inflating: assessment_dataset/images/chihuahua_182.jpg  
      inflating: assessment_dataset/images/chihuahua_183.jpg  
      inflating: assessment_dataset/images/chihuahua_184.jpg  
      inflating: assessment_dataset/images/chihuahua_185.jpg  
      inflating: assessment_dataset/images/chihuahua_186.jpg  
      inflating: assessment_dataset/images/chihuahua_187.jpg  
      inflating: assessment_dataset/images/chihuahua_188.jpg  
      inflating: assessment_dataset/images/chihuahua_189.jpg  
      inflating: assessment_dataset/images/chihuahua_190.jpg  
      inflating: assessment_dataset/images/n01440764_tench.jpeg  
      inflating: assessment_dataset/images/n01443537_goldfish.jpeg  
      inflating: assessment_dataset/images/n01491361_tiger_shark.jpeg  
      inflating: assessment_dataset/images/n01629819_European_fire_salamander.jpeg  
      inflating: assessment_dataset/images/n01630670_common_newt.jpeg  
      inflating: assessment_dataset/images/n01631663_eft.jpeg  
      inflating: assessment_dataset/images/n01632458_spotted_salamander.jpeg  
      inflating: assessment_dataset/images/n01632777_axolotl.jpeg  
      inflating: assessment_dataset/images/n01641577_bullfrog.jpeg  
      inflating: assessment_dataset/images/n01644373_tree_frog.jpeg  
      inflating: assessment_dataset/images/n01644900_tailed_frog.jpeg  
      inflating: assessment_dataset/images/n01664065_loggerhead.jpeg  
      inflating: assessment_dataset/images/n01665541_leatherback_turtle.jpeg  
      inflating: assessment_dataset/images/n01667114_mud_turtle.jpeg  
      inflating: assessment_dataset/images/n01675722_banded_gecko.jpeg  
      inflating: assessment_dataset/images/n01677366_common_iguana.jpeg  
      inflating: assessment_dataset/images/n01682714_American_chameleon.jpeg  
      inflating: assessment_dataset/images/n01685808_whiptail.jpeg  
      inflating: assessment_dataset/images/n01687978_agama.jpeg  
      inflating: assessment_dataset/images/n01688243_frilled_lizard.jpeg  
      inflating: assessment_dataset/images/n01689811_alligator_lizard.jpeg  
      inflating: assessment_dataset/images/n01692333_Gila_monster.jpeg  
      inflating: assessment_dataset/images/n01693334_green_lizard.jpeg  
      inflating: assessment_dataset/images/n01694178_African_chameleon.jpeg  
      inflating: assessment_dataset/images/n01695060_Komodo_dragon.jpeg  
      inflating: assessment_dataset/images/n01697457_African_crocodile.jpeg  
      inflating: assessment_dataset/images/n01698640_American_alligator.jpeg  
      inflating: assessment_dataset/images/n01704323_triceratops.jpeg  
      inflating: assessment_dataset/images/n01728572_thunder_snake.jpeg  
      inflating: assessment_dataset/images/n01728920_ringneck_snake.jpeg  
      inflating: assessment_dataset/images/n01729322_hognose_snake.jpeg  
      inflating: assessment_dataset/images/n01729977_green_snake.jpeg  
      inflating: assessment_dataset/images/n01734418_king_snake.jpeg  
      inflating: assessment_dataset/images/n01735189_garter_snake.jpeg  
      inflating: assessment_dataset/images/n01737021_water_snake.jpeg  
      inflating: assessment_dataset/images/n01739381_vine_snake.jpeg  
      inflating: assessment_dataset/images/n01740131_night_snake.jpeg  
      inflating: assessment_dataset/images/n01742172_boa_constrictor.jpeg  
      inflating: assessment_dataset/images/n01744401_rock_python.jpeg  
      inflating: assessment_dataset/images/n01748264_Indian_cobra.jpeg  
      inflating: assessment_dataset/images/n01749939_green_mamba.jpeg  
      inflating: assessment_dataset/images/n01751748_sea_snake.jpeg  
      inflating: assessment_dataset/images/n01753488_horned_viper.jpeg  
      inflating: assessment_dataset/images/n01755581_diamondback.jpeg  
      inflating: assessment_dataset/images/n01756291_sidewinder.jpeg  
      inflating: assessment_dataset/images/n01768244_trilobite.jpeg  
      inflating: assessment_dataset/images/n01770081_harvestman.jpeg  
      inflating: assessment_dataset/images/n01770393_scorpion.jpeg  
      inflating: assessment_dataset/images/n01773157_black_and_gold_garden_spider.jpeg  
      inflating: assessment_dataset/images/n01773549_barn_spider.jpeg  
      inflating: assessment_dataset/images/n01773797_garden_spider.jpeg  
      inflating: assessment_dataset/images/n01774384_black_widow.jpeg  
      inflating: assessment_dataset/images/n01774750_tarantula.jpeg  
      inflating: assessment_dataset/images/n01775062_wolf_spider.jpeg  
      inflating: assessment_dataset/images/n01776313_tick.jpeg  
      inflating: assessment_dataset/images/n01784675_centipede.jpeg  
      inflating: assessment_dataset/images/n01795545_black_grouse.jpeg  
      inflating: assessment_dataset/images/n01796340_ptarmigan.jpeg  
      inflating: assessment_dataset/images/n01797886_ruffed_grouse.jpeg  
      inflating: assessment_dataset/images/n01798484_prairie_chicken.jpeg  
      inflating: assessment_dataset/images/n01806143_peacock.jpeg  
      inflating: assessment_dataset/images/n01806567_quail.jpeg  
      inflating: assessment_dataset/images/n01807496_partridge.jpeg  
      inflating: assessment_dataset/images/n01817953_African_grey.jpeg  
      inflating: assessment_dataset/images/n01818515_macaw.jpeg  
      inflating: assessment_dataset/images/n01819313_sulphur-crested_cockatoo.jpeg  
      inflating: assessment_dataset/images/n01820546_lorikeet.jpeg  
      inflating: assessment_dataset/images/n01824575_coucal.jpeg  
      inflating: assessment_dataset/images/n01828970_bee_eater.jpeg  
      inflating: assessment_dataset/images/n01829413_hornbill.jpeg  
      inflating: assessment_dataset/images/n01833805_hummingbird.jpeg  
      inflating: assessment_dataset/images/n01843065_jacamar.jpeg  
      inflating: assessment_dataset/images/n01843383_toucan.jpeg  
      inflating: assessment_dataset/images/n01847000_drake.jpeg  
      inflating: assessment_dataset/images/n01855032_red-breasted_merganser.jpeg  
      inflating: assessment_dataset/images/n01855672_goose.jpeg  
      inflating: assessment_dataset/images/n01860187_black_swan.jpeg  
      inflating: assessment_dataset/images/n01872401_echidna.jpeg  
      inflating: assessment_dataset/images/n01873310_platypus.jpeg  
      inflating: assessment_dataset/images/n01877812_wallaby.jpeg  
      inflating: assessment_dataset/images/n01882714_koala.jpeg  
      inflating: assessment_dataset/images/n01883070_wombat.jpeg  
      inflating: assessment_dataset/images/n01910747_jellyfish.jpeg  
      inflating: assessment_dataset/images/n01914609_sea_anemone.jpeg  
      inflating: assessment_dataset/images/n01917289_brain_coral.jpeg  
      inflating: assessment_dataset/images/n01924916_flatworm.jpeg  
      inflating: assessment_dataset/images/n01930112_nematode.jpeg  
      inflating: assessment_dataset/images/n01943899_conch.jpeg  
      inflating: assessment_dataset/images/n01944390_snail.jpeg  
      inflating: assessment_dataset/images/n01945685_slug.jpeg  
      inflating: assessment_dataset/images/n01950731_sea_slug.jpeg  
      inflating: assessment_dataset/images/n01955084_chiton.jpeg  
      inflating: assessment_dataset/images/n01968897_chambered_nautilus.jpeg  
      inflating: assessment_dataset/images/n01978287_Dungeness_crab.jpeg  
      inflating: assessment_dataset/images/n01978455_rock_crab.jpeg  
      inflating: assessment_dataset/images/n01980166_fiddler_crab.jpeg  
      inflating: assessment_dataset/images/n01981276_king_crab.jpeg  
      inflating: assessment_dataset/images/n01983481_American_lobster.jpeg  
      inflating: assessment_dataset/images/n01984695_spiny_lobster.jpeg  
      inflating: assessment_dataset/images/n01985128_crayfish.jpeg  
      inflating: assessment_dataset/images/n01986214_hermit_crab.jpeg  
      inflating: assessment_dataset/images/n01990800_isopod.jpeg  
      inflating: assessment_dataset/images/n02002556_white_stork.jpeg  
      inflating: assessment_dataset/images/n02002724_black_stork.jpeg  
      inflating: assessment_dataset/images/n02006656_spoonbill.jpeg  
      inflating: assessment_dataset/images/n02007558_flamingo.jpeg  
      inflating: assessment_dataset/images/n02009229_little_blue_heron.jpeg  
      inflating: assessment_dataset/images/n02009912_American_egret.jpeg  
      inflating: assessment_dataset/images/n02011460_bittern.jpeg  
      inflating: assessment_dataset/images/n02012849_crane.jpeg  
      inflating: assessment_dataset/images/n02013706_limpkin.jpeg  
      inflating: assessment_dataset/images/n02017213_European_gallinule.jpeg  
      inflating: assessment_dataset/images/n02018207_American_coot.jpeg  
      inflating: assessment_dataset/images/n02018795_bustard.jpeg  
      inflating: assessment_dataset/images/n02025239_ruddy_turnstone.jpeg  
      inflating: assessment_dataset/images/n02027492_red-backed_sandpiper.jpeg  
      inflating: assessment_dataset/images/n02028035_redshank.jpeg  
      inflating: assessment_dataset/images/n02033041_dowitcher.jpeg  
      inflating: assessment_dataset/images/n02037110_oystercatcher.jpeg  
      inflating: assessment_dataset/images/n02051845_pelican.jpeg  
      inflating: assessment_dataset/images/n02056570_king_penguin.jpeg  
      inflating: assessment_dataset/images/pomeranian_100.jpg  
      inflating: assessment_dataset/images/pomeranian_101.jpg  
      inflating: assessment_dataset/images/pomeranian_102.jpg  
      inflating: assessment_dataset/images/pomeranian_103.jpg  
      inflating: assessment_dataset/images/pomeranian_104.jpg  
      inflating: assessment_dataset/images/pomeranian_105.jpg  
      inflating: assessment_dataset/images/pomeranian_106.jpg  
      inflating: assessment_dataset/images/pomeranian_107.jpg  
      inflating: assessment_dataset/images/pomeranian_108.jpg  
      inflating: assessment_dataset/images/pomeranian_109.jpg  
      inflating: assessment_dataset/images/pomeranian_110.jpg  
      inflating: assessment_dataset/images/pomeranian_111.jpg  
      inflating: assessment_dataset/images/pomeranian_112.jpg  
      inflating: assessment_dataset/images/pomeranian_113.jpg  
      inflating: assessment_dataset/images/pomeranian_114.jpg  
      inflating: assessment_dataset/images/pomeranian_115.jpg  
      inflating: assessment_dataset/images/pomeranian_116.jpg  
      inflating: assessment_dataset/images/pomeranian_117.jpg  
      inflating: assessment_dataset/images/pomeranian_118.jpg  
      inflating: assessment_dataset/images/pomeranian_119.jpg  
      inflating: assessment_dataset/images/pomeranian_120.jpg  
      inflating: assessment_dataset/images/pomeranian_121.jpg  
      inflating: assessment_dataset/images/pomeranian_122.jpg  
      inflating: assessment_dataset/images/pomeranian_123.jpg  
      inflating: assessment_dataset/images/pomeranian_124.jpg  
      inflating: assessment_dataset/images/pomeranian_125.jpg  
      inflating: assessment_dataset/images/pomeranian_126.jpg  
      inflating: assessment_dataset/images/pomeranian_127.jpg  
      inflating: assessment_dataset/images/pomeranian_128.jpg  
      inflating: assessment_dataset/images/pomeranian_129.jpg  
      inflating: assessment_dataset/images/pomeranian_130.jpg  
      inflating: assessment_dataset/images/pomeranian_131.jpg  
      inflating: assessment_dataset/images/pomeranian_132.jpg  
      inflating: assessment_dataset/images/pomeranian_133.jpg  
      inflating: assessment_dataset/images/pomeranian_134.jpg  
      inflating: assessment_dataset/images/pomeranian_135.jpg  
      inflating: assessment_dataset/images/pomeranian_136.jpg  
      inflating: assessment_dataset/images/pomeranian_137.jpg  
      inflating: assessment_dataset/images/pomeranian_138.jpg  
      inflating: assessment_dataset/images/pomeranian_139.jpg  
      inflating: assessment_dataset/images/pomeranian_140.jpg  
      inflating: assessment_dataset/images/pomeranian_141.jpg  
      inflating: assessment_dataset/images/pomeranian_142.jpg  
      inflating: assessment_dataset/images/pomeranian_143.jpg  
      inflating: assessment_dataset/images/pomeranian_144.jpg  
      inflating: assessment_dataset/images/pomeranian_145.jpg  
      inflating: assessment_dataset/images/pomeranian_146.jpg  
      inflating: assessment_dataset/images/pomeranian_147.jpg  
      inflating: assessment_dataset/images/pomeranian_148.jpg  
      inflating: assessment_dataset/images/pomeranian_149.jpg  
      inflating: assessment_dataset/images/pomeranian_150.jpg  
      inflating: assessment_dataset/images/pomeranian_151.jpg  
      inflating: assessment_dataset/images/pomeranian_152.jpg  
      inflating: assessment_dataset/images/pomeranian_153.jpg  
      inflating: assessment_dataset/images/pomeranian_154.jpg  
      inflating: assessment_dataset/images/pomeranian_155.jpg  
      inflating: assessment_dataset/images/pomeranian_156.jpg  
      inflating: assessment_dataset/images/pomeranian_157.jpg  
      inflating: assessment_dataset/images/pomeranian_158.jpg  
      inflating: assessment_dataset/images/pomeranian_159.jpg  
      inflating: assessment_dataset/images/pomeranian_16.jpg  
      inflating: assessment_dataset/images/pomeranian_160.jpg  
      inflating: assessment_dataset/images/pomeranian_161.jpg  
      inflating: assessment_dataset/images/pomeranian_162.jpg  
      inflating: assessment_dataset/images/pomeranian_163.jpg  
      inflating: assessment_dataset/images/pomeranian_164.jpg  
      inflating: assessment_dataset/images/pomeranian_165.jpg  
      inflating: assessment_dataset/images/pomeranian_166.jpg  
      inflating: assessment_dataset/images/pomeranian_167.jpg  
      inflating: assessment_dataset/images/pomeranian_168.jpg  
      inflating: assessment_dataset/images/pomeranian_169.jpg  
      inflating: assessment_dataset/images/pomeranian_17.jpg  
      inflating: assessment_dataset/images/pomeranian_170.jpg  
      inflating: assessment_dataset/images/pomeranian_171.jpg  
      inflating: assessment_dataset/images/pomeranian_172.jpg  
      inflating: assessment_dataset/images/pomeranian_173.jpg  
      inflating: assessment_dataset/images/pomeranian_174.jpg  
      inflating: assessment_dataset/images/pomeranian_175.jpg  
      inflating: assessment_dataset/images/pomeranian_176.jpg  
      inflating: assessment_dataset/images/pomeranian_177.jpg  
      inflating: assessment_dataset/images/pomeranian_178.jpg  
      inflating: assessment_dataset/images/pomeranian_179.jpg  
      inflating: assessment_dataset/images/pomeranian_18.jpg  
      inflating: assessment_dataset/images/pomeranian_180.jpg  
      inflating: assessment_dataset/images/pomeranian_181.jpg  
      inflating: assessment_dataset/images/pomeranian_182.jpg  
      inflating: assessment_dataset/images/pomeranian_183.jpg  
      inflating: assessment_dataset/images/pomeranian_184.jpg  
      inflating: assessment_dataset/images/pomeranian_185.jpg  
      inflating: assessment_dataset/images/pomeranian_186.jpg  
      inflating: assessment_dataset/images/pomeranian_187.jpg  
      inflating: assessment_dataset/images/pomeranian_188.jpg  
      inflating: assessment_dataset/images/pomeranian_189.jpg  
      inflating: assessment_dataset/images/pomeranian_190.jpg  
      inflating: assessment_dataset/labels/Abyssinian_10.xml  
      inflating: assessment_dataset/labels/Abyssinian_100.xml  
      inflating: assessment_dataset/labels/Abyssinian_101.xml  
      inflating: assessment_dataset/labels/Abyssinian_102.xml  
      inflating: assessment_dataset/labels/Abyssinian_103.xml  
      inflating: assessment_dataset/labels/Abyssinian_105.xml  
      inflating: assessment_dataset/labels/Abyssinian_106.xml  
      inflating: assessment_dataset/labels/Abyssinian_107.xml  
      inflating: assessment_dataset/labels/Abyssinian_108.xml  
      inflating: assessment_dataset/labels/Abyssinian_109.xml  
      inflating: assessment_dataset/labels/Abyssinian_11.xml  
      inflating: assessment_dataset/labels/Abyssinian_111.xml  
      inflating: assessment_dataset/labels/Abyssinian_112.xml  
      inflating: assessment_dataset/labels/Abyssinian_113.xml  
      inflating: assessment_dataset/labels/Abyssinian_114.xml  
      inflating: assessment_dataset/labels/Abyssinian_115.xml  
      inflating: assessment_dataset/labels/Abyssinian_116.xml  
      inflating: assessment_dataset/labels/Abyssinian_117.xml  
      inflating: assessment_dataset/labels/Abyssinian_118.xml  
      inflating: assessment_dataset/labels/Abyssinian_119.xml  
      inflating: assessment_dataset/labels/Abyssinian_12.xml  
      inflating: assessment_dataset/labels/Abyssinian_120.xml  
      inflating: assessment_dataset/labels/Abyssinian_121.xml  
      inflating: assessment_dataset/labels/Abyssinian_122.xml  
      inflating: assessment_dataset/labels/Abyssinian_123.xml  
      inflating: assessment_dataset/labels/Abyssinian_125.xml  
      inflating: assessment_dataset/labels/Abyssinian_126.xml  
      inflating: assessment_dataset/labels/Abyssinian_127.xml  
      inflating: assessment_dataset/labels/Abyssinian_128.xml  
      inflating: assessment_dataset/labels/Abyssinian_129.xml  
      inflating: assessment_dataset/labels/Abyssinian_13.xml  
      inflating: assessment_dataset/labels/Abyssinian_130.xml  
      inflating: assessment_dataset/labels/Abyssinian_131.xml  
      inflating: assessment_dataset/labels/Abyssinian_132.xml  
      inflating: assessment_dataset/labels/Abyssinian_133.xml  
      inflating: assessment_dataset/labels/Abyssinian_135.xml  
      inflating: assessment_dataset/labels/Abyssinian_136.xml  
      inflating: assessment_dataset/labels/Abyssinian_137.xml  
      inflating: assessment_dataset/labels/Abyssinian_138.xml  
      inflating: assessment_dataset/labels/Abyssinian_139.xml  
      inflating: assessment_dataset/labels/Abyssinian_14.xml  
      inflating: assessment_dataset/labels/Abyssinian_141.xml  
      inflating: assessment_dataset/labels/Abyssinian_142.xml  
      inflating: assessment_dataset/labels/Abyssinian_143.xml  
      inflating: assessment_dataset/labels/Abyssinian_144.xml  
      inflating: assessment_dataset/labels/Abyssinian_145.xml  
      inflating: assessment_dataset/labels/Abyssinian_146.xml  
      inflating: assessment_dataset/labels/Abyssinian_148.xml  
      inflating: assessment_dataset/labels/Abyssinian_149.xml  
      inflating: assessment_dataset/labels/Abyssinian_15.xml  
      inflating: assessment_dataset/labels/Abyssinian_150.xml  
      inflating: assessment_dataset/labels/Abyssinian_151.xml  
      inflating: assessment_dataset/labels/Abyssinian_152.xml  
      inflating: assessment_dataset/labels/Abyssinian_153.xml  
      inflating: assessment_dataset/labels/Abyssinian_154.xml  
      inflating: assessment_dataset/labels/Abyssinian_155.xml  
      inflating: assessment_dataset/labels/Abyssinian_156.xml  
      inflating: assessment_dataset/labels/Abyssinian_157.xml  
      inflating: assessment_dataset/labels/Abyssinian_158.xml  
      inflating: assessment_dataset/labels/Abyssinian_159.xml  
      inflating: assessment_dataset/labels/Abyssinian_16.xml  
      inflating: assessment_dataset/labels/Abyssinian_160.xml  
      inflating: assessment_dataset/labels/Abyssinian_161.xml  
      inflating: assessment_dataset/labels/Abyssinian_164.xml  
      inflating: assessment_dataset/labels/Abyssinian_165.xml  
      inflating: assessment_dataset/labels/Abyssinian_166.xml  
      inflating: assessment_dataset/labels/Abyssinian_167.xml  
      inflating: assessment_dataset/labels/Abyssinian_168.xml  
      inflating: assessment_dataset/labels/Abyssinian_169.xml  
      inflating: assessment_dataset/labels/Abyssinian_17.xml  
      inflating: assessment_dataset/labels/Abyssinian_170.xml  
      inflating: assessment_dataset/labels/Abyssinian_172.xml  
      inflating: assessment_dataset/labels/Abyssinian_173.xml  
      inflating: assessment_dataset/labels/Abyssinian_174.xml  
      inflating: assessment_dataset/labels/Abyssinian_175.xml  
      inflating: assessment_dataset/labels/Abyssinian_176.xml  
      inflating: assessment_dataset/labels/Abyssinian_177.xml  
      inflating: assessment_dataset/labels/Abyssinian_178.xml  
      inflating: assessment_dataset/labels/Abyssinian_179.xml  
      inflating: assessment_dataset/labels/Abyssinian_180.xml  
      inflating: assessment_dataset/labels/Abyssinian_181.xml  
      inflating: assessment_dataset/labels/Abyssinian_182.xml  
      inflating: assessment_dataset/labels/Abyssinian_183.xml  
      inflating: assessment_dataset/labels/Abyssinian_184.xml  
      inflating: assessment_dataset/labels/Abyssinian_185.xml  
      inflating: assessment_dataset/labels/Abyssinian_19.xml  
      inflating: assessment_dataset/labels/Abyssinian_190.xml  
      inflating: assessment_dataset/labels/Abyssinian_191.xml  
      inflating: assessment_dataset/labels/Abyssinian_192.xml  
      inflating: assessment_dataset/labels/Abyssinian_193.xml  
      inflating: assessment_dataset/labels/Abyssinian_195.xml  
      inflating: assessment_dataset/labels/Abyssinian_196.xml  
      inflating: assessment_dataset/labels/Abyssinian_197.xml  
      inflating: assessment_dataset/labels/Birman_100.xml  
      inflating: assessment_dataset/labels/Birman_101.xml  
      inflating: assessment_dataset/labels/Birman_102.xml  
      inflating: assessment_dataset/labels/Birman_103.xml  
      inflating: assessment_dataset/labels/Birman_104.xml  
      inflating: assessment_dataset/labels/Birman_105.xml  
      inflating: assessment_dataset/labels/Birman_106.xml  
      inflating: assessment_dataset/labels/Birman_107.xml  
      inflating: assessment_dataset/labels/Birman_108.xml  
      inflating: assessment_dataset/labels/Birman_109.xml  
      inflating: assessment_dataset/labels/Birman_110.xml  
      inflating: assessment_dataset/labels/Birman_111.xml  
      inflating: assessment_dataset/labels/Birman_112.xml  
      inflating: assessment_dataset/labels/Birman_113.xml  
      inflating: assessment_dataset/labels/Birman_114.xml  
      inflating: assessment_dataset/labels/Birman_115.xml  
      inflating: assessment_dataset/labels/Birman_116.xml  
      inflating: assessment_dataset/labels/Birman_117.xml  
      inflating: assessment_dataset/labels/Birman_118.xml  
      inflating: assessment_dataset/labels/Birman_119.xml  
      inflating: assessment_dataset/labels/Birman_120.xml  
      inflating: assessment_dataset/labels/Birman_121.xml  
      inflating: assessment_dataset/labels/Birman_122.xml  
      inflating: assessment_dataset/labels/Birman_123.xml  
      inflating: assessment_dataset/labels/Birman_124.xml  
      inflating: assessment_dataset/labels/Birman_125.xml  
      inflating: assessment_dataset/labels/Birman_126.xml  
      inflating: assessment_dataset/labels/Birman_127.xml  
      inflating: assessment_dataset/labels/Birman_128.xml  
      inflating: assessment_dataset/labels/Birman_129.xml  
      inflating: assessment_dataset/labels/Birman_130.xml  
      inflating: assessment_dataset/labels/Birman_131.xml  
      inflating: assessment_dataset/labels/Birman_132.xml  
      inflating: assessment_dataset/labels/Birman_133.xml  
      inflating: assessment_dataset/labels/Birman_134.xml  
      inflating: assessment_dataset/labels/Birman_135.xml  
      inflating: assessment_dataset/labels/Birman_136.xml  
      inflating: assessment_dataset/labels/Birman_137.xml  
      inflating: assessment_dataset/labels/Birman_138.xml  
      inflating: assessment_dataset/labels/Birman_139.xml  
      inflating: assessment_dataset/labels/Birman_140.xml  
      inflating: assessment_dataset/labels/Birman_141.xml  
      inflating: assessment_dataset/labels/Birman_142.xml  
      inflating: assessment_dataset/labels/Birman_143.xml  
      inflating: assessment_dataset/labels/Birman_144.xml  
      inflating: assessment_dataset/labels/Birman_145.xml  
      inflating: assessment_dataset/labels/Birman_146.xml  
      inflating: assessment_dataset/labels/Birman_147.xml  
      inflating: assessment_dataset/labels/Birman_148.xml  
      inflating: assessment_dataset/labels/Birman_149.xml  
      inflating: assessment_dataset/labels/Birman_150.xml  
      inflating: assessment_dataset/labels/Birman_151.xml  
      inflating: assessment_dataset/labels/Birman_152.xml  
      inflating: assessment_dataset/labels/Birman_153.xml  
      inflating: assessment_dataset/labels/Birman_154.xml  
      inflating: assessment_dataset/labels/Birman_155.xml  
      inflating: assessment_dataset/labels/Birman_156.xml  
      inflating: assessment_dataset/labels/Birman_157.xml  
      inflating: assessment_dataset/labels/Birman_158.xml  
      inflating: assessment_dataset/labels/Birman_159.xml  
      inflating: assessment_dataset/labels/Birman_16.xml  
      inflating: assessment_dataset/labels/Birman_160.xml  
      inflating: assessment_dataset/labels/Birman_161.xml  
      inflating: assessment_dataset/labels/Birman_162.xml  
      inflating: assessment_dataset/labels/Birman_163.xml  
      inflating: assessment_dataset/labels/Birman_164.xml  
      inflating: assessment_dataset/labels/Birman_165.xml  
      inflating: assessment_dataset/labels/Birman_166.xml  
      inflating: assessment_dataset/labels/Birman_167.xml  
      inflating: assessment_dataset/labels/Birman_168.xml  
      inflating: assessment_dataset/labels/Birman_169.xml  
      inflating: assessment_dataset/labels/Birman_17.xml  
      inflating: assessment_dataset/labels/Birman_170.xml  
      inflating: assessment_dataset/labels/Birman_171.xml  
      inflating: assessment_dataset/labels/Birman_172.xml  
      inflating: assessment_dataset/labels/Birman_173.xml  
      inflating: assessment_dataset/labels/Birman_174.xml  
      inflating: assessment_dataset/labels/Birman_175.xml  
      inflating: assessment_dataset/labels/Birman_176.xml  
      inflating: assessment_dataset/labels/Birman_177.xml  
      inflating: assessment_dataset/labels/Birman_178.xml  
      inflating: assessment_dataset/labels/Birman_179.xml  
      inflating: assessment_dataset/labels/Birman_18.xml  
      inflating: assessment_dataset/labels/Birman_180.xml  
      inflating: assessment_dataset/labels/Birman_181.xml  
      inflating: assessment_dataset/labels/Birman_182.xml  
      inflating: assessment_dataset/labels/Birman_183.xml  
      inflating: assessment_dataset/labels/Birman_184.xml  
      inflating: assessment_dataset/labels/Birman_185.xml  
      inflating: assessment_dataset/labels/Birman_186.xml  
      inflating: assessment_dataset/labels/Birman_187.xml  
      inflating: assessment_dataset/labels/Birman_188.xml  
      inflating: assessment_dataset/labels/Birman_189.xml  
      inflating: assessment_dataset/labels/Birman_190.xml  
      inflating: assessment_dataset/labels/Persian_100.xml  
      inflating: assessment_dataset/labels/Persian_101.xml  
      inflating: assessment_dataset/labels/Persian_102.xml  
      inflating: assessment_dataset/labels/Persian_103.xml  
      inflating: assessment_dataset/labels/Persian_104.xml  
      inflating: assessment_dataset/labels/Persian_105.xml  
      inflating: assessment_dataset/labels/Persian_106.xml  
      inflating: assessment_dataset/labels/Persian_107.xml  
      inflating: assessment_dataset/labels/Persian_108.xml  
      inflating: assessment_dataset/labels/Persian_111.xml  
      inflating: assessment_dataset/labels/Persian_112.xml  
      inflating: assessment_dataset/labels/Persian_114.xml  
      inflating: assessment_dataset/labels/Persian_115.xml  
      inflating: assessment_dataset/labels/Persian_116.xml  
      inflating: assessment_dataset/labels/Persian_117.xml  
      inflating: assessment_dataset/labels/Persian_118.xml  
      inflating: assessment_dataset/labels/Persian_120.xml  
      inflating: assessment_dataset/labels/Persian_121.xml  
      inflating: assessment_dataset/labels/Persian_122.xml  
      inflating: assessment_dataset/labels/Persian_123.xml  
      inflating: assessment_dataset/labels/Persian_125.xml  
      inflating: assessment_dataset/labels/Persian_126.xml  
      inflating: assessment_dataset/labels/Persian_128.xml  
      inflating: assessment_dataset/labels/Persian_129.xml  
      inflating: assessment_dataset/labels/Persian_131.xml  
      inflating: assessment_dataset/labels/Persian_132.xml  
      inflating: assessment_dataset/labels/Persian_133.xml  
      inflating: assessment_dataset/labels/Persian_134.xml  
      inflating: assessment_dataset/labels/Persian_135.xml  
      inflating: assessment_dataset/labels/Persian_136.xml  
      inflating: assessment_dataset/labels/Persian_137.xml  
      inflating: assessment_dataset/labels/Persian_138.xml  
      inflating: assessment_dataset/labels/Persian_139.xml  
      inflating: assessment_dataset/labels/Persian_140.xml  
      inflating: assessment_dataset/labels/Persian_141.xml  
      inflating: assessment_dataset/labels/Persian_143.xml  
      inflating: assessment_dataset/labels/Persian_144.xml  
      inflating: assessment_dataset/labels/Persian_145.xml  
      inflating: assessment_dataset/labels/Persian_147.xml  
      inflating: assessment_dataset/labels/Persian_149.xml  
      inflating: assessment_dataset/labels/Persian_15.xml  
      inflating: assessment_dataset/labels/Persian_150.xml  
      inflating: assessment_dataset/labels/Persian_152.xml  
      inflating: assessment_dataset/labels/Persian_153.xml  
      inflating: assessment_dataset/labels/Persian_155.xml  
      inflating: assessment_dataset/labels/Persian_156.xml  
      inflating: assessment_dataset/labels/Persian_158.xml  
      inflating: assessment_dataset/labels/Persian_159.xml  
      inflating: assessment_dataset/labels/Persian_16.xml  
      inflating: assessment_dataset/labels/Persian_160.xml  
      inflating: assessment_dataset/labels/Persian_161.xml  
      inflating: assessment_dataset/labels/Persian_162.xml  
      inflating: assessment_dataset/labels/Persian_163.xml  
      inflating: assessment_dataset/labels/Persian_164.xml  
      inflating: assessment_dataset/labels/Persian_165.xml  
      inflating: assessment_dataset/labels/Persian_166.xml  
      inflating: assessment_dataset/labels/Persian_168.xml  
      inflating: assessment_dataset/labels/Persian_169.xml  
      inflating: assessment_dataset/labels/Persian_17.xml  
      inflating: assessment_dataset/labels/Persian_170.xml  
      inflating: assessment_dataset/labels/Persian_171.xml  
      inflating: assessment_dataset/labels/Persian_172.xml  
      inflating: assessment_dataset/labels/Persian_173.xml  
      inflating: assessment_dataset/labels/Persian_174.xml  
      inflating: assessment_dataset/labels/Persian_175.xml  
      inflating: assessment_dataset/labels/Persian_176.xml  
      inflating: assessment_dataset/labels/Persian_179.xml  
      inflating: assessment_dataset/labels/Persian_18.xml  
      inflating: assessment_dataset/labels/Persian_180.xml  
      inflating: assessment_dataset/labels/Persian_181.xml  
      inflating: assessment_dataset/labels/Persian_182.xml  
      inflating: assessment_dataset/labels/Persian_183.xml  
      inflating: assessment_dataset/labels/Persian_184.xml  
      inflating: assessment_dataset/labels/Persian_185.xml  
      inflating: assessment_dataset/labels/Persian_186.xml  
      inflating: assessment_dataset/labels/Persian_187.xml  
      inflating: assessment_dataset/labels/Persian_188.xml  
      inflating: assessment_dataset/labels/Persian_189.xml  
      inflating: assessment_dataset/labels/Persian_19.xml  
      inflating: assessment_dataset/labels/Persian_190.xml  
      inflating: assessment_dataset/labels/Persian_191.xml  
      inflating: assessment_dataset/labels/Persian_192.xml  
      inflating: assessment_dataset/labels/Persian_193.xml  
      inflating: assessment_dataset/labels/Persian_194.xml  
      inflating: assessment_dataset/labels/Persian_195.xml  
      inflating: assessment_dataset/labels/Persian_196.xml  
      inflating: assessment_dataset/labels/Persian_197.xml  
      inflating: assessment_dataset/labels/Persian_20.xml  
      inflating: assessment_dataset/labels/Persian_200.xml  
      inflating: assessment_dataset/labels/Persian_201.xml  
      inflating: assessment_dataset/labels/Persian_202.xml  
      inflating: assessment_dataset/labels/Persian_206.xml  
      inflating: assessment_dataset/labels/Persian_213.xml  
      inflating: assessment_dataset/labels/Persian_217.xml  
      inflating: assessment_dataset/labels/american_bulldog_10.xml  
      inflating: assessment_dataset/labels/american_bulldog_100.xml  
      inflating: assessment_dataset/labels/american_bulldog_101.xml  
      inflating: assessment_dataset/labels/american_bulldog_103.xml  
      inflating: assessment_dataset/labels/american_bulldog_104.xml  
      inflating: assessment_dataset/labels/american_bulldog_105.xml  
      inflating: assessment_dataset/labels/american_bulldog_106.xml  
      inflating: assessment_dataset/labels/american_bulldog_107.xml  
      inflating: assessment_dataset/labels/american_bulldog_109.xml  
      inflating: assessment_dataset/labels/american_bulldog_11.xml  
      inflating: assessment_dataset/labels/american_bulldog_110.xml  
      inflating: assessment_dataset/labels/american_bulldog_111.xml  
      inflating: assessment_dataset/labels/american_bulldog_112.xml  
      inflating: assessment_dataset/labels/american_bulldog_113.xml  
      inflating: assessment_dataset/labels/american_bulldog_115.xml  
      inflating: assessment_dataset/labels/american_bulldog_116.xml  
      inflating: assessment_dataset/labels/american_bulldog_117.xml  
      inflating: assessment_dataset/labels/american_bulldog_118.xml  
      inflating: assessment_dataset/labels/american_bulldog_119.xml  
      inflating: assessment_dataset/labels/american_bulldog_12.xml  
      inflating: assessment_dataset/labels/american_bulldog_121.xml  
      inflating: assessment_dataset/labels/american_bulldog_122.xml  
      inflating: assessment_dataset/labels/american_bulldog_123.xml  
      inflating: assessment_dataset/labels/american_bulldog_124.xml  
      inflating: assessment_dataset/labels/american_bulldog_125.xml  
      inflating: assessment_dataset/labels/american_bulldog_127.xml  
      inflating: assessment_dataset/labels/american_bulldog_128.xml  
      inflating: assessment_dataset/labels/american_bulldog_129.xml  
      inflating: assessment_dataset/labels/american_bulldog_13.xml  
      inflating: assessment_dataset/labels/american_bulldog_130.xml  
      inflating: assessment_dataset/labels/american_bulldog_131.xml  
      inflating: assessment_dataset/labels/american_bulldog_132.xml  
      inflating: assessment_dataset/labels/american_bulldog_133.xml  
      inflating: assessment_dataset/labels/american_bulldog_134.xml  
      inflating: assessment_dataset/labels/american_bulldog_135.xml  
      inflating: assessment_dataset/labels/american_bulldog_136.xml  
      inflating: assessment_dataset/labels/american_bulldog_137.xml  
      inflating: assessment_dataset/labels/american_bulldog_138.xml  
      inflating: assessment_dataset/labels/american_bulldog_139.xml  
      inflating: assessment_dataset/labels/american_bulldog_14.xml  
      inflating: assessment_dataset/labels/american_bulldog_140.xml  
      inflating: assessment_dataset/labels/american_bulldog_141.xml  
      inflating: assessment_dataset/labels/american_bulldog_142.xml  
      inflating: assessment_dataset/labels/american_bulldog_143.xml  
      inflating: assessment_dataset/labels/american_bulldog_144.xml  
      inflating: assessment_dataset/labels/american_bulldog_146.xml  
      inflating: assessment_dataset/labels/american_bulldog_147.xml  
      inflating: assessment_dataset/labels/american_bulldog_148.xml  
      inflating: assessment_dataset/labels/american_bulldog_149.xml  
      inflating: assessment_dataset/labels/american_bulldog_150.xml  
      inflating: assessment_dataset/labels/american_bulldog_151.xml  
      inflating: assessment_dataset/labels/american_bulldog_152.xml  
      inflating: assessment_dataset/labels/american_bulldog_153.xml  
      inflating: assessment_dataset/labels/american_bulldog_158.xml  
      inflating: assessment_dataset/labels/american_bulldog_16.xml  
      inflating: assessment_dataset/labels/american_bulldog_161.xml  
      inflating: assessment_dataset/labels/american_bulldog_164.xml  
      inflating: assessment_dataset/labels/american_bulldog_166.xml  
      inflating: assessment_dataset/labels/american_bulldog_167.xml  
      inflating: assessment_dataset/labels/american_bulldog_168.xml  
      inflating: assessment_dataset/labels/american_bulldog_169.xml  
      inflating: assessment_dataset/labels/american_bulldog_171.xml  
      inflating: assessment_dataset/labels/american_bulldog_172.xml  
      inflating: assessment_dataset/labels/american_bulldog_173.xml  
      inflating: assessment_dataset/labels/american_bulldog_174.xml  
      inflating: assessment_dataset/labels/american_bulldog_175.xml  
      inflating: assessment_dataset/labels/american_bulldog_176.xml  
      inflating: assessment_dataset/labels/american_bulldog_177.xml  
      inflating: assessment_dataset/labels/american_bulldog_178.xml  
      inflating: assessment_dataset/labels/american_bulldog_179.xml  
      inflating: assessment_dataset/labels/american_bulldog_18.xml  
      inflating: assessment_dataset/labels/american_bulldog_180.xml  
      inflating: assessment_dataset/labels/american_bulldog_181.xml  
      inflating: assessment_dataset/labels/american_bulldog_182.xml  
      inflating: assessment_dataset/labels/american_bulldog_183.xml  
      inflating: assessment_dataset/labels/american_bulldog_184.xml  
      inflating: assessment_dataset/labels/american_bulldog_185.xml  
      inflating: assessment_dataset/labels/american_bulldog_186.xml  
      inflating: assessment_dataset/labels/american_bulldog_187.xml  
      inflating: assessment_dataset/labels/american_bulldog_188.xml  
      inflating: assessment_dataset/labels/american_bulldog_189.xml  
      inflating: assessment_dataset/labels/american_bulldog_19.xml  
      inflating: assessment_dataset/labels/american_bulldog_190.xml  
      inflating: assessment_dataset/labels/american_bulldog_191.xml  
      inflating: assessment_dataset/labels/american_bulldog_192.xml  
      inflating: assessment_dataset/labels/american_bulldog_193.xml  
      inflating: assessment_dataset/labels/american_bulldog_194.xml  
      inflating: assessment_dataset/labels/american_bulldog_196.xml  
      inflating: assessment_dataset/labels/american_bulldog_197.xml  
      inflating: assessment_dataset/labels/american_bulldog_198.xml  
      inflating: assessment_dataset/labels/american_bulldog_199.xml  
      inflating: assessment_dataset/labels/american_bulldog_200.xml  
      inflating: assessment_dataset/labels/american_bulldog_201.xml  
      inflating: assessment_dataset/labels/american_bulldog_202.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_100.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_101.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_102.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_103.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_104.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_105.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_106.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_107.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_108.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_109.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_110.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_111.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_112.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_113.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_114.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_115.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_116.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_117.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_118.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_119.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_120.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_121.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_122.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_123.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_124.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_125.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_126.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_127.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_128.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_129.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_130.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_131.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_132.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_133.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_134.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_135.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_136.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_137.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_138.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_139.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_140.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_141.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_142.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_143.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_144.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_145.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_146.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_147.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_148.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_149.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_150.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_151.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_152.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_153.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_154.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_155.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_156.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_157.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_158.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_159.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_16.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_160.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_161.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_162.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_163.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_164.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_165.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_166.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_167.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_168.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_169.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_17.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_170.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_171.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_172.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_173.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_174.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_175.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_176.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_177.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_178.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_179.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_18.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_180.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_181.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_182.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_183.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_184.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_185.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_186.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_187.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_188.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_189.xml  
      inflating: assessment_dataset/labels/american_pit_bull_terrier_190.xml  
      inflating: assessment_dataset/labels/basset_hound_100.xml  
      inflating: assessment_dataset/labels/basset_hound_101.xml  
      inflating: assessment_dataset/labels/basset_hound_102.xml  
      inflating: assessment_dataset/labels/basset_hound_103.xml  
      inflating: assessment_dataset/labels/basset_hound_104.xml  
      inflating: assessment_dataset/labels/basset_hound_105.xml  
      inflating: assessment_dataset/labels/basset_hound_106.xml  
      inflating: assessment_dataset/labels/basset_hound_107.xml  
      inflating: assessment_dataset/labels/basset_hound_108.xml  
      inflating: assessment_dataset/labels/basset_hound_109.xml  
      inflating: assessment_dataset/labels/basset_hound_110.xml  
      inflating: assessment_dataset/labels/basset_hound_111.xml  
      inflating: assessment_dataset/labels/basset_hound_112.xml  
      inflating: assessment_dataset/labels/basset_hound_113.xml  
      inflating: assessment_dataset/labels/basset_hound_114.xml  
      inflating: assessment_dataset/labels/basset_hound_115.xml  
      inflating: assessment_dataset/labels/basset_hound_116.xml  
      inflating: assessment_dataset/labels/basset_hound_117.xml  
      inflating: assessment_dataset/labels/basset_hound_118.xml  
      inflating: assessment_dataset/labels/basset_hound_119.xml  
      inflating: assessment_dataset/labels/basset_hound_120.xml  
      inflating: assessment_dataset/labels/basset_hound_121.xml  
      inflating: assessment_dataset/labels/basset_hound_122.xml  
      inflating: assessment_dataset/labels/basset_hound_123.xml  
      inflating: assessment_dataset/labels/basset_hound_124.xml  
      inflating: assessment_dataset/labels/basset_hound_125.xml  
      inflating: assessment_dataset/labels/basset_hound_126.xml  
      inflating: assessment_dataset/labels/basset_hound_127.xml  
      inflating: assessment_dataset/labels/basset_hound_128.xml  
      inflating: assessment_dataset/labels/basset_hound_129.xml  
      inflating: assessment_dataset/labels/basset_hound_130.xml  
      inflating: assessment_dataset/labels/basset_hound_131.xml  
      inflating: assessment_dataset/labels/basset_hound_132.xml  
      inflating: assessment_dataset/labels/basset_hound_133.xml  
      inflating: assessment_dataset/labels/basset_hound_134.xml  
      inflating: assessment_dataset/labels/basset_hound_135.xml  
      inflating: assessment_dataset/labels/basset_hound_136.xml  
      inflating: assessment_dataset/labels/basset_hound_137.xml  
      inflating: assessment_dataset/labels/basset_hound_138.xml  
      inflating: assessment_dataset/labels/basset_hound_139.xml  
      inflating: assessment_dataset/labels/basset_hound_140.xml  
      inflating: assessment_dataset/labels/basset_hound_141.xml  
      inflating: assessment_dataset/labels/basset_hound_142.xml  
      inflating: assessment_dataset/labels/basset_hound_143.xml  
      inflating: assessment_dataset/labels/basset_hound_144.xml  
      inflating: assessment_dataset/labels/basset_hound_145.xml  
      inflating: assessment_dataset/labels/basset_hound_146.xml  
      inflating: assessment_dataset/labels/basset_hound_147.xml  
      inflating: assessment_dataset/labels/basset_hound_148.xml  
      inflating: assessment_dataset/labels/basset_hound_149.xml  
      inflating: assessment_dataset/labels/basset_hound_150.xml  
      inflating: assessment_dataset/labels/basset_hound_151.xml  
      inflating: assessment_dataset/labels/basset_hound_152.xml  
      inflating: assessment_dataset/labels/basset_hound_153.xml  
      inflating: assessment_dataset/labels/basset_hound_154.xml  
      inflating: assessment_dataset/labels/basset_hound_155.xml  
      inflating: assessment_dataset/labels/basset_hound_156.xml  
      inflating: assessment_dataset/labels/basset_hound_157.xml  
      inflating: assessment_dataset/labels/basset_hound_158.xml  
      inflating: assessment_dataset/labels/basset_hound_159.xml  
      inflating: assessment_dataset/labels/basset_hound_16.xml  
      inflating: assessment_dataset/labels/basset_hound_160.xml  
      inflating: assessment_dataset/labels/basset_hound_161.xml  
      inflating: assessment_dataset/labels/basset_hound_162.xml  
      inflating: assessment_dataset/labels/basset_hound_163.xml  
      inflating: assessment_dataset/labels/basset_hound_164.xml  
      inflating: assessment_dataset/labels/basset_hound_165.xml  
      inflating: assessment_dataset/labels/basset_hound_166.xml  
      inflating: assessment_dataset/labels/basset_hound_167.xml  
      inflating: assessment_dataset/labels/basset_hound_168.xml  
      inflating: assessment_dataset/labels/basset_hound_169.xml  
      inflating: assessment_dataset/labels/basset_hound_17.xml  
      inflating: assessment_dataset/labels/basset_hound_170.xml  
      inflating: assessment_dataset/labels/basset_hound_171.xml  
      inflating: assessment_dataset/labels/basset_hound_172.xml  
      inflating: assessment_dataset/labels/basset_hound_173.xml  
      inflating: assessment_dataset/labels/basset_hound_174.xml  
      inflating: assessment_dataset/labels/basset_hound_175.xml  
      inflating: assessment_dataset/labels/basset_hound_176.xml  
      inflating: assessment_dataset/labels/basset_hound_177.xml  
      inflating: assessment_dataset/labels/basset_hound_178.xml  
      inflating: assessment_dataset/labels/basset_hound_179.xml  
      inflating: assessment_dataset/labels/basset_hound_18.xml  
      inflating: assessment_dataset/labels/basset_hound_180.xml  
      inflating: assessment_dataset/labels/basset_hound_181.xml  
      inflating: assessment_dataset/labels/basset_hound_182.xml  
      inflating: assessment_dataset/labels/basset_hound_183.xml  
      inflating: assessment_dataset/labels/basset_hound_184.xml  
      inflating: assessment_dataset/labels/basset_hound_185.xml  
      inflating: assessment_dataset/labels/basset_hound_186.xml  
      inflating: assessment_dataset/labels/basset_hound_187.xml  
      inflating: assessment_dataset/labels/basset_hound_188.xml  
      inflating: assessment_dataset/labels/basset_hound_189.xml  
      inflating: assessment_dataset/labels/basset_hound_190.xml  
      inflating: assessment_dataset/labels/beagle_100.xml  
      inflating: assessment_dataset/labels/beagle_101.xml  
      inflating: assessment_dataset/labels/beagle_102.xml  
      inflating: assessment_dataset/labels/beagle_103.xml  
      inflating: assessment_dataset/labels/beagle_104.xml  
      inflating: assessment_dataset/labels/beagle_105.xml  
      inflating: assessment_dataset/labels/beagle_107.xml  
      inflating: assessment_dataset/labels/beagle_108.xml  
      inflating: assessment_dataset/labels/beagle_109.xml  
      inflating: assessment_dataset/labels/beagle_110.xml  
      inflating: assessment_dataset/labels/beagle_111.xml  
      inflating: assessment_dataset/labels/beagle_112.xml  
      inflating: assessment_dataset/labels/beagle_113.xml  
      inflating: assessment_dataset/labels/beagle_114.xml  
      inflating: assessment_dataset/labels/beagle_115.xml  
      inflating: assessment_dataset/labels/beagle_116.xml  
      inflating: assessment_dataset/labels/beagle_117.xml  
      inflating: assessment_dataset/labels/beagle_118.xml  
      inflating: assessment_dataset/labels/beagle_119.xml  
      inflating: assessment_dataset/labels/beagle_120.xml  
      inflating: assessment_dataset/labels/beagle_121.xml  
      inflating: assessment_dataset/labels/beagle_122.xml  
      inflating: assessment_dataset/labels/beagle_123.xml  
      inflating: assessment_dataset/labels/beagle_124.xml  
      inflating: assessment_dataset/labels/beagle_125.xml  
      inflating: assessment_dataset/labels/beagle_126.xml  
      inflating: assessment_dataset/labels/beagle_127.xml  
      inflating: assessment_dataset/labels/beagle_128.xml  
      inflating: assessment_dataset/labels/beagle_129.xml  
      inflating: assessment_dataset/labels/beagle_130.xml  
      inflating: assessment_dataset/labels/beagle_131.xml  
      inflating: assessment_dataset/labels/beagle_133.xml  
      inflating: assessment_dataset/labels/beagle_134.xml  
      inflating: assessment_dataset/labels/beagle_135.xml  
      inflating: assessment_dataset/labels/beagle_136.xml  
      inflating: assessment_dataset/labels/beagle_137.xml  
      inflating: assessment_dataset/labels/beagle_138.xml  
      inflating: assessment_dataset/labels/beagle_139.xml  
      inflating: assessment_dataset/labels/beagle_140.xml  
      inflating: assessment_dataset/labels/beagle_141.xml  
      inflating: assessment_dataset/labels/beagle_142.xml  
      inflating: assessment_dataset/labels/beagle_143.xml  
      inflating: assessment_dataset/labels/beagle_144.xml  
      inflating: assessment_dataset/labels/beagle_145.xml  
      inflating: assessment_dataset/labels/beagle_146.xml  
      inflating: assessment_dataset/labels/beagle_147.xml  
      inflating: assessment_dataset/labels/beagle_148.xml  
      inflating: assessment_dataset/labels/beagle_149.xml  
      inflating: assessment_dataset/labels/beagle_150.xml  
      inflating: assessment_dataset/labels/beagle_151.xml  
      inflating: assessment_dataset/labels/beagle_152.xml  
      inflating: assessment_dataset/labels/beagle_153.xml  
      inflating: assessment_dataset/labels/beagle_154.xml  
      inflating: assessment_dataset/labels/beagle_155.xml  
      inflating: assessment_dataset/labels/beagle_156.xml  
      inflating: assessment_dataset/labels/beagle_157.xml  
      inflating: assessment_dataset/labels/beagle_158.xml  
      inflating: assessment_dataset/labels/beagle_160.xml  
      inflating: assessment_dataset/labels/beagle_161.xml  
      inflating: assessment_dataset/labels/beagle_162.xml  
      inflating: assessment_dataset/labels/beagle_163.xml  
      inflating: assessment_dataset/labels/beagle_164.xml  
      inflating: assessment_dataset/labels/beagle_165.xml  
      inflating: assessment_dataset/labels/beagle_166.xml  
      inflating: assessment_dataset/labels/beagle_167.xml  
      inflating: assessment_dataset/labels/beagle_168.xml  
      inflating: assessment_dataset/labels/beagle_169.xml  
      inflating: assessment_dataset/labels/beagle_17.xml  
      inflating: assessment_dataset/labels/beagle_170.xml  
      inflating: assessment_dataset/labels/beagle_171.xml  
      inflating: assessment_dataset/labels/beagle_172.xml  
      inflating: assessment_dataset/labels/beagle_173.xml  
      inflating: assessment_dataset/labels/beagle_174.xml  
      inflating: assessment_dataset/labels/beagle_175.xml  
      inflating: assessment_dataset/labels/beagle_176.xml  
      inflating: assessment_dataset/labels/beagle_177.xml  
      inflating: assessment_dataset/labels/beagle_178.xml  
      inflating: assessment_dataset/labels/beagle_179.xml  
      inflating: assessment_dataset/labels/beagle_18.xml  
      inflating: assessment_dataset/labels/beagle_180.xml  
      inflating: assessment_dataset/labels/beagle_181.xml  
      inflating: assessment_dataset/labels/beagle_182.xml  
      inflating: assessment_dataset/labels/beagle_183.xml  
      inflating: assessment_dataset/labels/beagle_184.xml  
      inflating: assessment_dataset/labels/beagle_185.xml  
      inflating: assessment_dataset/labels/beagle_186.xml  
      inflating: assessment_dataset/labels/beagle_187.xml  
      inflating: assessment_dataset/labels/beagle_188.xml  
      inflating: assessment_dataset/labels/beagle_189.xml  
      inflating: assessment_dataset/labels/beagle_190.xml  
      inflating: assessment_dataset/labels/beagle_191.xml  
      inflating: assessment_dataset/labels/beagle_192.xml  
      inflating: assessment_dataset/labels/beagle_193.xml  
      inflating: assessment_dataset/labels/beagle_194.xml  
      inflating: assessment_dataset/labels/chihuahua_100.xml  
      inflating: assessment_dataset/labels/chihuahua_101.xml  
      inflating: assessment_dataset/labels/chihuahua_102.xml  
      inflating: assessment_dataset/labels/chihuahua_103.xml  
      inflating: assessment_dataset/labels/chihuahua_104.xml  
      inflating: assessment_dataset/labels/chihuahua_105.xml  
      inflating: assessment_dataset/labels/chihuahua_106.xml  
      inflating: assessment_dataset/labels/chihuahua_107.xml  
      inflating: assessment_dataset/labels/chihuahua_108.xml  
      inflating: assessment_dataset/labels/chihuahua_109.xml  
      inflating: assessment_dataset/labels/chihuahua_110.xml  
      inflating: assessment_dataset/labels/chihuahua_111.xml  
      inflating: assessment_dataset/labels/chihuahua_112.xml  
      inflating: assessment_dataset/labels/chihuahua_113.xml  
      inflating: assessment_dataset/labels/chihuahua_114.xml  
      inflating: assessment_dataset/labels/chihuahua_115.xml  
      inflating: assessment_dataset/labels/chihuahua_116.xml  
      inflating: assessment_dataset/labels/chihuahua_117.xml  
      inflating: assessment_dataset/labels/chihuahua_118.xml  
      inflating: assessment_dataset/labels/chihuahua_119.xml  
      inflating: assessment_dataset/labels/chihuahua_120.xml  
      inflating: assessment_dataset/labels/chihuahua_121.xml  
      inflating: assessment_dataset/labels/chihuahua_122.xml  
      inflating: assessment_dataset/labels/chihuahua_123.xml  
      inflating: assessment_dataset/labels/chihuahua_124.xml  
      inflating: assessment_dataset/labels/chihuahua_125.xml  
      inflating: assessment_dataset/labels/chihuahua_126.xml  
      inflating: assessment_dataset/labels/chihuahua_127.xml  
      inflating: assessment_dataset/labels/chihuahua_128.xml  
      inflating: assessment_dataset/labels/chihuahua_129.xml  
      inflating: assessment_dataset/labels/chihuahua_130.xml  
      inflating: assessment_dataset/labels/chihuahua_131.xml  
      inflating: assessment_dataset/labels/chihuahua_132.xml  
      inflating: assessment_dataset/labels/chihuahua_133.xml  
      inflating: assessment_dataset/labels/chihuahua_134.xml  
      inflating: assessment_dataset/labels/chihuahua_135.xml  
      inflating: assessment_dataset/labels/chihuahua_136.xml  
      inflating: assessment_dataset/labels/chihuahua_137.xml  
      inflating: assessment_dataset/labels/chihuahua_138.xml  
      inflating: assessment_dataset/labels/chihuahua_139.xml  
      inflating: assessment_dataset/labels/chihuahua_140.xml  
      inflating: assessment_dataset/labels/chihuahua_141.xml  
      inflating: assessment_dataset/labels/chihuahua_142.xml  
      inflating: assessment_dataset/labels/chihuahua_143.xml  
      inflating: assessment_dataset/labels/chihuahua_144.xml  
      inflating: assessment_dataset/labels/chihuahua_145.xml  
      inflating: assessment_dataset/labels/chihuahua_146.xml  
      inflating: assessment_dataset/labels/chihuahua_147.xml  
      inflating: assessment_dataset/labels/chihuahua_148.xml  
      inflating: assessment_dataset/labels/chihuahua_149.xml  
      inflating: assessment_dataset/labels/chihuahua_150.xml  
      inflating: assessment_dataset/labels/chihuahua_151.xml  
      inflating: assessment_dataset/labels/chihuahua_152.xml  
      inflating: assessment_dataset/labels/chihuahua_153.xml  
      inflating: assessment_dataset/labels/chihuahua_154.xml  
      inflating: assessment_dataset/labels/chihuahua_155.xml  
      inflating: assessment_dataset/labels/chihuahua_156.xml  
      inflating: assessment_dataset/labels/chihuahua_157.xml  
      inflating: assessment_dataset/labels/chihuahua_158.xml  
      inflating: assessment_dataset/labels/chihuahua_159.xml  
      inflating: assessment_dataset/labels/chihuahua_16.xml  
      inflating: assessment_dataset/labels/chihuahua_160.xml  
      inflating: assessment_dataset/labels/chihuahua_161.xml  
      inflating: assessment_dataset/labels/chihuahua_162.xml  
      inflating: assessment_dataset/labels/chihuahua_163.xml  
      inflating: assessment_dataset/labels/chihuahua_164.xml  
      inflating: assessment_dataset/labels/chihuahua_165.xml  
      inflating: assessment_dataset/labels/chihuahua_166.xml  
      inflating: assessment_dataset/labels/chihuahua_167.xml  
      inflating: assessment_dataset/labels/chihuahua_168.xml  
      inflating: assessment_dataset/labels/chihuahua_169.xml  
      inflating: assessment_dataset/labels/chihuahua_17.xml  
      inflating: assessment_dataset/labels/chihuahua_170.xml  
      inflating: assessment_dataset/labels/chihuahua_171.xml  
      inflating: assessment_dataset/labels/chihuahua_172.xml  
      inflating: assessment_dataset/labels/chihuahua_173.xml  
      inflating: assessment_dataset/labels/chihuahua_174.xml  
      inflating: assessment_dataset/labels/chihuahua_175.xml  
      inflating: assessment_dataset/labels/chihuahua_176.xml  
      inflating: assessment_dataset/labels/chihuahua_177.xml  
      inflating: assessment_dataset/labels/chihuahua_178.xml  
      inflating: assessment_dataset/labels/chihuahua_179.xml  
      inflating: assessment_dataset/labels/chihuahua_18.xml  
      inflating: assessment_dataset/labels/chihuahua_180.xml  
      inflating: assessment_dataset/labels/chihuahua_181.xml  
      inflating: assessment_dataset/labels/chihuahua_182.xml  
      inflating: assessment_dataset/labels/chihuahua_183.xml  
      inflating: assessment_dataset/labels/chihuahua_184.xml  
      inflating: assessment_dataset/labels/chihuahua_185.xml  
      inflating: assessment_dataset/labels/chihuahua_186.xml  
      inflating: assessment_dataset/labels/chihuahua_187.xml  
      inflating: assessment_dataset/labels/chihuahua_188.xml  
      inflating: assessment_dataset/labels/chihuahua_189.xml  
      inflating: assessment_dataset/labels/chihuahua_190.xml  
      inflating: assessment_dataset/labels/pomeranian_100.xml  
      inflating: assessment_dataset/labels/pomeranian_101.xml  
      inflating: assessment_dataset/labels/pomeranian_102.xml  
      inflating: assessment_dataset/labels/pomeranian_103.xml  
      inflating: assessment_dataset/labels/pomeranian_104.xml  
      inflating: assessment_dataset/labels/pomeranian_105.xml  
      inflating: assessment_dataset/labels/pomeranian_106.xml  
      inflating: assessment_dataset/labels/pomeranian_107.xml  
      inflating: assessment_dataset/labels/pomeranian_108.xml  
      inflating: assessment_dataset/labels/pomeranian_109.xml  
      inflating: assessment_dataset/labels/pomeranian_110.xml  
      inflating: assessment_dataset/labels/pomeranian_111.xml  
      inflating: assessment_dataset/labels/pomeranian_112.xml  
      inflating: assessment_dataset/labels/pomeranian_113.xml  
      inflating: assessment_dataset/labels/pomeranian_114.xml  
      inflating: assessment_dataset/labels/pomeranian_115.xml  
      inflating: assessment_dataset/labels/pomeranian_116.xml  
      inflating: assessment_dataset/labels/pomeranian_117.xml  
      inflating: assessment_dataset/labels/pomeranian_118.xml  
      inflating: assessment_dataset/labels/pomeranian_119.xml  
      inflating: assessment_dataset/labels/pomeranian_120.xml  
      inflating: assessment_dataset/labels/pomeranian_121.xml  
      inflating: assessment_dataset/labels/pomeranian_122.xml  
      inflating: assessment_dataset/labels/pomeranian_123.xml  
      inflating: assessment_dataset/labels/pomeranian_124.xml  
      inflating: assessment_dataset/labels/pomeranian_125.xml  
      inflating: assessment_dataset/labels/pomeranian_126.xml  
      inflating: assessment_dataset/labels/pomeranian_127.xml  
      inflating: assessment_dataset/labels/pomeranian_128.xml  
      inflating: assessment_dataset/labels/pomeranian_129.xml  
      inflating: assessment_dataset/labels/pomeranian_130.xml  
      inflating: assessment_dataset/labels/pomeranian_131.xml  
      inflating: assessment_dataset/labels/pomeranian_132.xml  
      inflating: assessment_dataset/labels/pomeranian_133.xml  
      inflating: assessment_dataset/labels/pomeranian_134.xml  
      inflating: assessment_dataset/labels/pomeranian_135.xml  
      inflating: assessment_dataset/labels/pomeranian_136.xml  
      inflating: assessment_dataset/labels/pomeranian_137.xml  
      inflating: assessment_dataset/labels/pomeranian_138.xml  
      inflating: assessment_dataset/labels/pomeranian_139.xml  
      inflating: assessment_dataset/labels/pomeranian_140.xml  
      inflating: assessment_dataset/labels/pomeranian_141.xml  
      inflating: assessment_dataset/labels/pomeranian_142.xml  
      inflating: assessment_dataset/labels/pomeranian_143.xml  
      inflating: assessment_dataset/labels/pomeranian_144.xml  
      inflating: assessment_dataset/labels/pomeranian_145.xml  
      inflating: assessment_dataset/labels/pomeranian_146.xml  
      inflating: assessment_dataset/labels/pomeranian_147.xml  
      inflating: assessment_dataset/labels/pomeranian_148.xml  
      inflating: assessment_dataset/labels/pomeranian_149.xml  
      inflating: assessment_dataset/labels/pomeranian_150.xml  
      inflating: assessment_dataset/labels/pomeranian_151.xml  
      inflating: assessment_dataset/labels/pomeranian_152.xml  
      inflating: assessment_dataset/labels/pomeranian_153.xml  
      inflating: assessment_dataset/labels/pomeranian_154.xml  
      inflating: assessment_dataset/labels/pomeranian_155.xml  
      inflating: assessment_dataset/labels/pomeranian_156.xml  
      inflating: assessment_dataset/labels/pomeranian_157.xml  
      inflating: assessment_dataset/labels/pomeranian_158.xml  
      inflating: assessment_dataset/labels/pomeranian_159.xml  
      inflating: assessment_dataset/labels/pomeranian_16.xml  
      inflating: assessment_dataset/labels/pomeranian_160.xml  
      inflating: assessment_dataset/labels/pomeranian_161.xml  
      inflating: assessment_dataset/labels/pomeranian_162.xml  
      inflating: assessment_dataset/labels/pomeranian_163.xml  
      inflating: assessment_dataset/labels/pomeranian_164.xml  
      inflating: assessment_dataset/labels/pomeranian_165.xml  
      inflating: assessment_dataset/labels/pomeranian_166.xml  
      inflating: assessment_dataset/labels/pomeranian_167.xml  
      inflating: assessment_dataset/labels/pomeranian_168.xml  
      inflating: assessment_dataset/labels/pomeranian_169.xml  
      inflating: assessment_dataset/labels/pomeranian_17.xml  
      inflating: assessment_dataset/labels/pomeranian_170.xml  
      inflating: assessment_dataset/labels/pomeranian_171.xml  
      inflating: assessment_dataset/labels/pomeranian_172.xml  
      inflating: assessment_dataset/labels/pomeranian_173.xml  
      inflating: assessment_dataset/labels/pomeranian_174.xml  
      inflating: assessment_dataset/labels/pomeranian_175.xml  
      inflating: assessment_dataset/labels/pomeranian_176.xml  
      inflating: assessment_dataset/labels/pomeranian_177.xml  
      inflating: assessment_dataset/labels/pomeranian_178.xml  
      inflating: assessment_dataset/labels/pomeranian_179.xml  
      inflating: assessment_dataset/labels/pomeranian_18.xml  
      inflating: assessment_dataset/labels/pomeranian_180.xml  
      inflating: assessment_dataset/labels/pomeranian_181.xml  
      inflating: assessment_dataset/labels/pomeranian_182.xml  
      inflating: assessment_dataset/labels/pomeranian_183.xml  
      inflating: assessment_dataset/labels/pomeranian_184.xml  
      inflating: assessment_dataset/labels/pomeranian_185.xml  
      inflating: assessment_dataset/labels/pomeranian_186.xml  
      inflating: assessment_dataset/labels/pomeranian_187.xml  
      inflating: assessment_dataset/labels/pomeranian_188.xml  
      inflating: assessment_dataset/labels/pomeranian_189.xml  
      inflating: assessment_dataset/labels/pomeranian_190.xml  
      inflating: assessment_dataset/train_list.npy  
      inflating: assessment_dataset/val_list.npy  


# MODEL IMPLEMENTATION:


```python
import os
import torch
import torch.nn as nn
import numpy as np

from torchvision.models import resnet18, ResNet18_Weights
```


```python
class Model(nn.Module):

  def __init__(self, num_species=10):
    super(Model, self).__init__()

    # Pretrained ResNet18 as backbone
    pretrained_model = resnet18(pretrained=True)
    self.backbone = nn.Sequential(*list(pretrained_model.children())[:-2])

    # Output size of the backbone
    backbone_out_features = 512

    # Adjust the output of the backbone with a linear layer
    self.adjust = nn.Linear(25088, backbone_out_features)

    # Whether image has an object or not (binary classification)
    self.have_object = nn.Linear(backbone_out_features, 2)

    # Whether the object is a cat or a dog (binary classification)
    self.cat_or_dog = nn.Linear(backbone_out_features, 2)

    # Species of the object (multi-class classification)
    self.specie = nn.Linear(backbone_out_features, num_species)

    # Bounding box regression (xmin, ymin, xmax, ymax)
    self.bbox = nn.Linear(backbone_out_features, 4)

  def forward(self, input):
    out_backbone = self.backbone(input)
    out_backbone = out_backbone.view(out_backbone.size(0), -1)  # Flattening the output of backbone

    # Adjust the output size
    out_backbone = self.adjust(out_backbone)

    # Forward pass through the custom head
    bbox = self.bbox(out_backbone)
    object_ = self.have_object(out_backbone)
    cat_or_dog = self.cat_or_dog(out_backbone)
    specie = self.specie(out_backbone)

    return {
        "bbox": bbox,
        "object": object_,
        "cat_or_dog": cat_or_dog,
        "specie": specie
    }

```

# CUSTOM DATALOADER IMPLEMENTATION


```python
train_list = np.load('/content/assessment_dataset/train_list.npy', allow_pickle=True).tolist()
val_list = np.load('/content/assessment_dataset/val_list.npy', allow_pickle=True).tolist()
```


```python
from bs4 import BeautifulSoup

def read_xml_file(path):
    with open(path, 'r') as f:
        data = f.read()
    bs_data = BeautifulSoup(data, 'xml')
    return {
        "cat_or_dog": bs_data.find("name").text,
        "xmin": int(bs_data.find("xmin").text),
        "ymin": int(bs_data.find("ymin").text),
        "xmax": int(bs_data.find("xmax").text),
        "ymax": int(bs_data.find("ymax").text),
        "specie": "_".join(path.split(os.sep)[-1].split("_")[:-1])
    }
```


```python
from sklearn.preprocessing import LabelEncoder, OneHotEncoder

# List of species
species_list = ['american_bulldog', 'Birman', 'Birman', 'Persian', 'Birman', 'american_pit_bull_terrier', 'beagle', 'american_pit_bull_terrier', 0, 'american_pit_bull_terrier', 'Persian', 'beagle', 0, 'Birman', 'basset_hound', 'Persian', 'Abyssinian', 0, 'Birman', 'beagle', 'american_bulldog', 'chihuahua', 0, 'american_pit_bull_terrier', 'chihuahua', 'basset_hound', 'american_bulldog', 'beagle', 'beagle', 0, 'Abyssinian', 'basset_hound']

# Replace 0 with 'None' or any placeholder for no-species
species_list = ['None' if species == 0 else species for species in species_list]

# Use LabelEncoder to convert species to integers
label_encoder = LabelEncoder()
integer_encoded = label_encoder.fit_transform(species_list)

# Use OneHotEncoder to convert integers to one-hot vectors
onehot_encoder = OneHotEncoder(sparse=False)
integer_encoded = integer_encoded.reshape(len(integer_encoded), 1)
onehot_encoded = onehot_encoder.fit_transform(integer_encoded)
```

    /usr/local/lib/python3.10/dist-packages/sklearn/preprocessing/_encoders.py:868: FutureWarning: `sparse` was renamed to `sparse_output` in version 1.2 and will be removed in 1.4. `sparse_output` is ignored unless you leave `sparse` to its default value.
      warnings.warn(



```python
from PIL import Image

import torchvision.transforms as transforms

class CustomDataset():

    def __init__(self, dataset_path, images_list, train=False):
        self.dataset_path = dataset_path
        self.images_data = []
        self.preprocess = transforms.Compose([
            transforms.Resize((224, 224)),
            transforms.ToTensor(),
            transforms.Normalize(mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225]),
        ])
        all_species =  ['american_bulldog', 'Birman', 'Birman', 'Persian', 'Birman', 'american_pit_bull_terrier', 'beagle', 'american_pit_bull_terrier', 0, 'american_pit_bull_terrier', 'Persian', 'beagle', 0, 'Birman', 'basset_hound', 'Persian', 'Abyssinian', 0, 'Birman', 'beagle', 'american_bulldog', 'chihuahua', 0, 'american_pit_bull_terrier', 'chihuahua', 'basset_hound', 'american_bulldog', 'beagle', 'beagle', 0, 'Abyssinian', 'basset_hound']
        all_species.append('unknown')  # Add 'unknown' category during fitting
        self.label_encoder = LabelEncoder()
        self.label_encoder.fit(all_species)
        
        if train:
            self.preprocess = transforms.Compose([
                transforms.RandomResizedCrop(224),
                transforms.RandomHorizontalFlip(),
                transforms.ToTensor(),
                transforms.Normalize(mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225]),
            ])
        
        image_folder_path = os.path.join(dataset_path, "images")
        label_folder_path = os.path.join(dataset_path, "labels")

        for path in os.listdir(image_folder_path):
            name = path.split(os.sep)[-1].split(".")[0]
            if name in images_list:
                image_path = os.path.join(image_folder_path, path)
                xml_path = os.path.join(label_folder_path, name + ".xml")
                xml_data = read_xml_file(xml_path) if os.path.exists(xml_path) else None
                self.images_data.append((image_path, xml_data))

    def __len__(self):
        return len(self.images_data)

    def __getitem__(self, index):
      image_path, xml_data = self.images_data[index]
      image = Image.open(image_path).convert("RGB")
      image = self.preprocess(image)
      
      label = {
          "bbox": torch.tensor([0, 0, 0, 0], dtype = torch.float),
          "object": 0,
          "cat_or_dog": 0,
          "specie": self.label_encoder.transform(['unknown'])[0]  # 'unknown' is now the default species
      }
      if xml_data:
          # Get the species or 'unknown' if the species is not known
          specie = xml_data["specie"] if xml_data["specie"] in self.label_encoder.classes_ else 'unknown'
          label = {
              "bbox": torch.tensor([xml_data["xmin"], xml_data["ymin"], xml_data["xmax"], xml_data["ymax"]], dtype=torch.float),
              "object": 1,
              "cat_or_dog": 0 if xml_data["cat_or_dog"] == "cat" else 1,
              "specie": self.label_encoder.transform([specie])[0]
          }
      
      return image, label



```

# TRAINING LOOP IMPLEMENTATION

## Initializations


```python
from torch.utils.data import DataLoader
```


```python
training_dataset = CustomDataset("/content/assessment_dataset", images_list=train_list)
training_loader = torch.utils.data.DataLoader(training_dataset, batch_size=32, shuffle=True)
for batch in training_loader:
    print(batch)
    break
```

    [tensor([[[[-0.9363, -0.9877, -1.0390,  ...,  0.3652,  0.4679,  0.2796],
              [-0.9705, -1.0562, -1.1760,  ...,  0.2624,  0.2453,  0.1768],
              [-1.0562, -1.1418, -1.2617,  ..., -0.1828, -0.0629,  0.0056],
              ...,
              [ 0.7248,  0.6734,  0.4508,  ..., -0.5082,  0.3309,  0.1254],
              [ 0.3138,  0.4337,  0.4851,  ..., -0.4739,  0.2282,  0.2111],
              [-0.1828, -0.0116,  0.2282,  ..., -0.8335, -0.1314,  0.1254]],
    
             [[ 0.1702,  0.1176,  0.0651,  ...,  0.3627,  0.5028,  0.2052],
              [ 0.1352,  0.0476, -0.0749,  ...,  0.1702,  0.1702,  0.0126],
              [ 0.0126, -0.0749, -0.1975,  ..., -0.2150, -0.1975, -0.2675],
              ...,
              [ 0.6954,  0.7829,  0.5903,  ...,  0.0651,  0.7304,  0.5028],
              [ 0.2577,  0.5378,  0.6429,  ..., -0.0049,  0.5728,  0.5378],
              [-0.2675,  0.0476,  0.3978,  ..., -0.4601,  0.1001,  0.3627]],
    
             [[ 0.1128,  0.0779,  0.0082,  ...,  0.1128,  0.3916,  0.1651],
              [ 0.0431, -0.0615, -0.1835,  ..., -0.0790,  0.0431, -0.0615],
              [-0.1312, -0.2184, -0.3404,  ..., -0.5147, -0.3927, -0.3927],
              ...,
              [ 0.4091,  0.6008,  0.5136,  ..., -0.3230,  0.6879,  0.4439],
              [ 0.0953,  0.3568,  0.5136,  ..., -0.3230,  0.6182,  0.5136],
              [-0.3404, -0.0790,  0.1999,  ..., -0.7587,  0.1128,  0.2696]]],


​    
            [[[-0.6109, -0.6109, -0.6281,  ..., -0.6452, -0.6794, -0.6452],
              [-0.6109, -0.5938, -0.5938,  ..., -0.6452, -0.6452, -0.6452],
              [-0.5938, -0.5938, -0.5938,  ..., -0.6109, -0.6109, -0.6452],
              ...,
              [ 0.1254,  0.1426,  0.1083,  ..., -0.7822, -0.7993, -0.7650],
              [ 0.1426,  0.1254,  0.1254,  ..., -0.7137, -0.7650, -0.7479],
              [ 0.1426,  0.1083,  0.1426,  ..., -0.6281, -0.7137, -0.7822]],
    
             [[-0.6877, -0.6877, -0.7052,  ..., -0.7227, -0.7577, -0.7227],
              [-0.6877, -0.6702, -0.6702,  ..., -0.7227, -0.7227, -0.7227],
              [-0.6702, -0.6702, -0.6702,  ..., -0.6877, -0.6877, -0.7227],
              ...,
              [ 0.3627,  0.3803,  0.3452,  ..., -0.7927, -0.8102, -0.7752],
              [ 0.3803,  0.3627,  0.3627,  ..., -0.7227, -0.7752, -0.7577],
              [ 0.3803,  0.3452,  0.3803,  ..., -0.6352, -0.7227, -0.7927]],
    
             [[-1.0376, -0.9853, -1.0027,  ..., -1.0201, -1.0550, -1.0201],
              [-0.9853, -0.9504, -0.9504,  ..., -1.0201, -1.0201, -1.0201],
              [-1.0027, -0.9853, -0.9678,  ..., -0.9853, -0.9853, -1.0201],
              ...,
              [ 0.5485,  0.5659,  0.5311,  ..., -0.8458, -0.8633, -0.8284],
              [ 0.5659,  0.5485,  0.5485,  ..., -0.7761, -0.8284, -0.8110],
              [ 0.5659,  0.5311,  0.5659,  ..., -0.6890, -0.7761, -0.8458]]],


​    
            [[[-2.1008, -2.1179, -2.1179,  ..., -0.0458, -0.1143, -0.0972],
              [-2.1179, -2.1179, -2.1008,  ..., -0.0801, -0.0972, -0.0629],
              [-2.1179, -2.1179, -2.1008,  ..., -0.0972, -0.0801, -0.0972],
              ...,
              [-2.0323, -2.0494, -2.0665,  ..., -0.7822, -0.7137, -0.7822],
              [-2.0494, -2.0837, -2.0837,  ..., -0.7308, -0.7308, -0.7993],
              [-2.0665, -1.9980, -2.0323,  ..., -0.6623, -0.8164, -0.8507]],
    
             [[-1.9307, -1.9307, -1.9482,  ...,  0.2227,  0.1527,  0.1702],
              [-1.9482, -1.9307, -1.9132,  ...,  0.1702,  0.1702,  0.2052],
              [-1.9482, -1.9482, -1.9307,  ...,  0.1702,  0.1877,  0.1702],
              ...,
              [-1.6681, -1.7381, -1.8081,  ..., -0.5126, -0.4951, -0.5651],
              [-1.6856, -1.7731, -1.8256,  ..., -0.5301, -0.4776, -0.5476],
              [-1.7031, -1.6856, -1.7206,  ..., -0.4776, -0.5651, -0.5651]],
    
             [[-1.7696, -1.7696, -1.7870,  ...,  0.2173,  0.1825,  0.1999],
              [-1.7870, -1.7696, -1.7522,  ...,  0.1999,  0.1999,  0.2348],
              [-1.7870, -1.7870, -1.7696,  ...,  0.2348,  0.2173,  0.1999],
              ...,
              [-1.3164, -1.4384, -1.5430,  ..., -0.4450, -0.4624, -0.5495],
              [-1.3164, -1.4384, -1.5256,  ..., -0.4798, -0.4450, -0.5147],
              [-1.3339, -1.3164, -1.4210,  ..., -0.4624, -0.5147, -0.4973]]],


​    
            ...,


​    
            [[[-2.0665, -2.0665, -2.0665,  ..., -1.3473, -1.3130, -1.2617],
              [-2.0665, -2.0665, -2.0665,  ..., -1.2959, -1.2617, -1.2103],
              [-2.0665, -2.0665, -2.0665,  ..., -1.1932, -1.1247, -1.0733],
              ...,
              [-1.7583, -1.6727, -1.6213,  ..., -2.0152, -2.0152, -2.0152],
              [-1.7925, -1.7069, -1.6555,  ..., -1.9638, -1.9809, -1.9809],
              [-1.8268, -1.7412, -1.6898,  ..., -1.9467, -1.9467, -1.9467]],
    
             [[-1.9132, -1.9132, -1.9132,  ..., -1.6155, -1.5805, -1.5280],
              [-1.9132, -1.9132, -1.9132,  ..., -1.5805, -1.5455, -1.4930],
              [-1.9132, -1.9132, -1.9132,  ..., -1.5105, -1.4755, -1.4230],
              ...,
              [-1.4580, -1.3704, -1.3179,  ..., -1.7906, -1.7906, -1.7906],
              [-1.4930, -1.4055, -1.3529,  ..., -1.7381, -1.7556, -1.7556],
              [-1.5280, -1.4405, -1.3880,  ..., -1.7206, -1.7206, -1.7206]],
    
             [[-1.6999, -1.6999, -1.6999,  ..., -1.4036, -1.3687, -1.3164],
              [-1.6999, -1.6999, -1.6999,  ..., -1.3687, -1.3339, -1.2816],
              [-1.6999, -1.6999, -1.6999,  ..., -1.2641, -1.2293, -1.1770],
              ...,
              [-1.2641, -1.1770, -1.1247,  ..., -1.1596, -1.1596, -1.1596],
              [-1.2990, -1.2119, -1.1596,  ..., -1.1073, -1.1247, -1.1247],
              [-1.3339, -1.2467, -1.1944,  ..., -1.0898, -1.0898, -1.0898]]],


​    
            [[[-1.3302, -1.1932, -1.0733,  ...,  0.8961,  1.2728,  1.6667],
              [-1.4329, -1.2617, -0.9877,  ...,  0.8618,  1.2385,  1.6495],
              [-1.3130, -1.2959, -1.0390,  ...,  0.8447,  1.2557,  1.6838],
              ...,
              [-0.4568, -0.6109, -0.7993,  ..., -0.1657, -1.0733, -0.8849],
              [-0.0801, -0.1828, -0.6794,  ...,  0.1426, -0.8507, -0.6109],
              [ 0.0227, -0.1143, -0.1657,  ...,  0.1597, -1.0390, -0.1143]],
    
             [[-1.2479, -1.0903, -0.9853,  ...,  0.7479,  1.0805,  1.5007],
              [-1.3529, -1.1604, -0.8803,  ...,  0.7129,  1.0630,  1.4832],
              [-1.2479, -1.2129, -0.9503,  ...,  0.6954,  1.0805,  1.5182],
              ...,
              [-0.4951, -0.6352, -0.8452,  ..., -0.0224, -1.0378, -0.8452],
              [-0.0924, -0.1975, -0.7227,  ...,  0.2227, -0.8452, -0.5651],
              [-0.0224, -0.1275, -0.2150,  ...,  0.2927, -0.9853,  0.0651]],
    
             [[-0.8981, -0.6193, -0.5495,  ...,  0.7925,  1.1237,  1.4722],
              [-1.0201, -0.7761, -0.4624,  ...,  0.7751,  1.0888,  1.4548],
              [-0.9504, -0.8633, -0.5147,  ...,  0.7576,  1.1062,  1.4897],
              ...,
              [-0.2707, -0.4798, -0.7413,  ..., -0.6018, -0.6890, -0.3927],
              [ 0.0431,  0.0953, -0.5321,  ..., -0.1138, -0.5495, -0.2532],
              [ 0.0779,  0.1651, -0.0267,  ..., -0.3230, -0.6890, -0.3055]]],


​    
            [[[ 2.2489,  2.2489,  2.2489,  ...,  2.2489,  2.2489,  2.2489],
              [ 2.2489,  2.2489,  2.2489,  ...,  2.2489,  2.2489,  2.2489],
              [ 2.2489,  2.2489,  2.2489,  ...,  2.2489,  2.2489,  2.2489],
              ...,
              [-0.7822, -0.4568, -0.5082,  ..., -1.1247, -1.2959, -1.4158],
              [-0.7993, -0.5767, -0.7308,  ..., -1.3473, -1.3644, -1.4329],
              [-0.9020, -0.4739, -0.8164,  ..., -1.3815, -1.3473, -1.4500]],
    
             [[ 2.4286,  2.4286,  2.4286,  ...,  2.4286,  2.4286,  2.4286],
              [ 2.4286,  2.4286,  2.4286,  ...,  2.4286,  2.4286,  2.4286],
              [ 2.4286,  2.4286,  2.4286,  ...,  2.4286,  2.4286,  2.4286],
              ...,
              [-0.6702, -0.7227, -0.8627,  ..., -1.2304, -1.1604, -1.2479],
              [-0.6877, -0.7577, -1.0378,  ..., -1.1954, -1.2129, -1.2829],
              [-1.0028, -0.7752, -1.1429,  ..., -1.3704, -1.3354, -1.3704]],
    
             [[ 2.6400,  2.6400,  2.6400,  ...,  2.6400,  2.6400,  2.6400],
              [ 2.6400,  2.6400,  2.6400,  ...,  2.6400,  2.6400,  2.6400],
              [ 2.6400,  2.6400,  2.6400,  ...,  2.6400,  2.6400,  2.6400],
              ...,
              [-1.4210, -1.1421, -1.1596,  ..., -1.5081, -1.5256, -1.5081],
              [-1.3687, -1.1596, -1.2990,  ..., -1.4559, -1.5081, -1.5081],
              [-1.4036, -1.0550, -1.4036,  ..., -1.4733, -1.4384, -1.4733]]]]), {'bbox': tensor([[  0.,   0.,   0.,   0.],
            [ 60.,  16., 290., 244.],
            [169.,  74., 333., 212.],
            [297.,  79., 351., 149.],
            [136.,  56., 305., 213.],
            [235., 239., 486., 458.],
            [ 90.,  72., 171., 155.],
            [109.,   1., 233., 135.],
            [204., 105., 290., 202.],
            [  0.,   0.,   0.,   0.],
            [  0.,   0.,   0.,   0.],
            [156.,  20., 228.,  81.],
            [148.,  86., 336., 238.],
            [154.,  38., 336., 238.],
            [112.,   4., 196.,  92.],
            [  0.,   0.,   0.,   0.],
            [ 31.,  31., 104., 119.],
            [  0.,   0.,   0.,   0.],
            [ 20.,  78., 375., 379.],
            [ 66.,  23., 168., 131.],
            [ 28.,   8., 101.,  89.],
            [103.,  69., 194., 144.],
            [ 89.,  25., 209., 133.],
            [115., 124., 300., 330.],
            [  0.,   0.,   0.,   0.],
            [  0.,   0.,   0.,   0.],
            [183.,  76., 265., 201.],
            [152.,  37., 293., 167.],
            [ 65.,  16., 243., 175.],
            [ 28.,   1., 155., 143.],
            [244.,  76., 370., 179.],
            [142.,  47., 351., 231.]]), 'object': tensor([0, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 1, 1, 1, 1, 0, 1, 0, 1, 1, 1, 1, 1, 1,
            0, 0, 1, 1, 1, 1, 1, 1]), 'cat_or_dog': tensor([0, 0, 0, 1, 1, 1, 1, 1, 1, 0, 0, 1, 1, 0, 1, 0, 1, 0, 1, 1, 0, 1, 1, 1,
            0, 0, 1, 1, 0, 1, 1, 1]), 'specie': tensor([9, 3, 2, 9, 6, 4, 5, 8, 4, 9, 9, 5, 7, 1, 8, 9, 8, 9, 4, 9, 1, 8, 5, 6,
            9, 9, 9, 4, 1, 9, 6, 6])}]



```python
from tqdm.notebook import tqdm
```


```python
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
```


```python
def train(epochs, model_weights):

  # Initialize Model and Optimizer
  model = Model()
  optimizer = optim.Adam(model.parameters())

  # Initialize Loss Functions
  have_object_loss = nn.CrossEntropyLoss()
  specie_loss = nn.CrossEntropyLoss()
  cat_or_dog_loss = nn.CrossEntropyLoss()
  bbox_loss = nn.MSELoss()

  training_dataset = CustomDataset("/content/assessment_dataset", images_list=train_list)
  training_loader = DataLoader(training_dataset, batch_size=32, shuffle=True, num_workers=4)

  if torch.cuda.is_available():
    model = model.cuda()

  def train_one_epoch(epoch_index, tb_writer):
      running_loss = 0.
      last_loss = 0.

      model.train()

      # Here, we use enumerate(training_loader) instead of
      # iter(training_loader) so that we can track the batch
      # index and do some intra-epoch reporting
      for i, data in enumerate(training_loader):
          # Every data instance is an input + label pair
          inputs, labels = data
          inputs = inputs.to(device)
          for key in labels:
              labels[key] = labels[key].to(device)

          optimizer.zero_grad()

          # Make predictions for this batch
          outputs = model(inputs)

          # Compute the loss and its gradients
          loss_object = have_object_loss(outputs["object"], labels["object"])
          loss_specie = specie_loss(outputs["specie"], labels["specie"])
          loss_cat_or_dog = cat_or_dog_loss(outputs["cat_or_dog"], labels["cat_or_dog"])
          loss_bbox = bbox_loss(outputs["bbox"], labels["bbox"])
          
          # Consolidate all individual losses
          loss = loss_object + loss_specie + loss_cat_or_dog + loss_bbox

          loss.backward()
          optimizer.step()

          # Gather data and report
          running_loss += loss.item()
          if i % 10 == 0:
              last_loss = running_loss / 10 # loss per batch
              running_loss = 0.
      return last_loss

  def test(model):
    model.eval()

    metric_object = torchmetrics.Accuracy(num_classes=2, average='micro', mdmc_average='global', task="binary").to(device)
    metric_cat_or_dog = torchmetrics.Accuracy(num_classes=2, average='micro', mdmc_average='global', task="binary").to(device)
    metric_specie = torchmetrics.Accuracy(num_classes=10, average='micro', mdmc_average='global', task="multiclass").to(device)
    metric_bbox = torchmetrics.MeanAbsoluteError().to(device)

    val_dataset = CustomDataset("/content/assessment_dataset", images_list=val_list)
    val_loader = torch.utils.data.DataLoader(val_dataset, batch_size=32)

    for i, data in tqdm(enumerate(val_loader)):
        inputs, labels = data
        if torch.cuda.is_available():
            inputs = inputs.cuda()
            for key in labels:
                labels[key] = labels[key].to(device)

        # Make predictions for this batch
        with torch.no_grad():
            outputs = model(inputs)

        predicted_object = torch.argmax(outputs["object"], dim=1)
        predicted_cat_or_dog = torch.argmax(outputs["cat_or_dog"], dim=1)
        predicted_specie = torch.argmax(outputs["specie"], dim=1)

        metric_object(predicted_object, labels["object"])
        metric_cat_or_dog(predicted_cat_or_dog, labels["cat_or_dog"])
        metric_specie(predicted_specie, labels["specie"])
        metric_bbox(outputs["bbox"], labels["bbox"])

    score_object = metric_object.compute()
    score_cat_or_dog = metric_cat_or_dog.compute()
    score_specie = metric_specie.compute()
    score_bbox = metric_bbox.compute()

    return score_object, score_cat_or_dog, score_specie, score_bbox



    
  for i in range(epochs):
    epoch_loss = train_one_epoch(i, None)
    print(f' Epoch {i} Loss : {epoch_loss}')

    torch.save(model.state_dict(), "model.pth")
    metrics = test(model)
    print(metrics)

```


```python
import torch
import torch.optim as optim
import torchmetrics
```


```python
epochs = 30  # Set the number of epochs
model_weights = None  # Set this to the path of model weights if you want to continue training from previously saved weights

# Start the training process
train(epochs, model_weights)

```

    /usr/local/lib/python3.10/dist-packages/torchvision/models/_utils.py:208: UserWarning: The parameter 'pretrained' is deprecated since 0.13 and may be removed in the future, please use 'weights' instead.
      warnings.warn(
    /usr/local/lib/python3.10/dist-packages/torchvision/models/_utils.py:223: UserWarning: Arguments other than a weight enum or `None` for 'weights' are deprecated since 0.13 and may be removed in the future. The current behavior is equivalent to passing `weights=ResNet18_Weights.IMAGENET1K_V1`. You can also use `weights=ResNet18_Weights.DEFAULT` to get the most up-to-date weights.
      warnings.warn(msg)
    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 0 Loss : 8171.389892578125



    0it [00:00, ?it/s]


    (tensor(0.8608, device='cuda:0'), tensor(0.5928, device='cuda:0'), tensor(0.1082, device='cuda:0'), tensor(224.7715, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 1 Loss : 5391.212158203125



    0it [00:00, ?it/s]


    (tensor(0.8402, device='cuda:0'), tensor(0.6804, device='cuda:0'), tensor(0.1701, device='cuda:0'), tensor(57.7630, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 2 Loss : 3449.299658203125



    0it [00:00, ?it/s]


    (tensor(0.9639, device='cuda:0'), tensor(0.4485, device='cuda:0'), tensor(0.3557, device='cuda:0'), tensor(66.1513, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 3 Loss : 2737.6340576171874



    0it [00:00, ?it/s]


    (tensor(0.9536, device='cuda:0'), tensor(0.4536, device='cuda:0'), tensor(0.2835, device='cuda:0'), tensor(42.2595, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 4 Loss : 3977.6148315429687



    0it [00:00, ?it/s]


    (tensor(0.9485, device='cuda:0'), tensor(0.4845, device='cuda:0'), tensor(0.3351, device='cuda:0'), tensor(38.0805, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 5 Loss : 1630.0474487304687



    0it [00:00, ?it/s]


    (tensor(0.9794, device='cuda:0'), tensor(0.7732, device='cuda:0'), tensor(0.3660, device='cuda:0'), tensor(37.9987, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 6 Loss : 1361.9340759277343



    0it [00:00, ?it/s]


    (tensor(0.9536, device='cuda:0'), tensor(0.4278, device='cuda:0'), tensor(0.3299, device='cuda:0'), tensor(39.6305, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 7 Loss : 905.9114929199219



    0it [00:00, ?it/s]


    (tensor(0.9794, device='cuda:0'), tensor(0.7784, device='cuda:0'), tensor(0.3247, device='cuda:0'), tensor(32.6547, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 8 Loss : 777.1705993652344



    0it [00:00, ?it/s]


    (tensor(0.9588, device='cuda:0'), tensor(0.7371, device='cuda:0'), tensor(0.3351, device='cuda:0'), tensor(38.0315, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 9 Loss : 1039.4549102783203



    0it [00:00, ?it/s]


    (tensor(0.9742, device='cuda:0'), tensor(0.8454, device='cuda:0'), tensor(0.3505, device='cuda:0'), tensor(33.7756, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 10 Loss : 1632.3771240234375



    0it [00:00, ?it/s]


    (tensor(0.9742, device='cuda:0'), tensor(0.8557, device='cuda:0'), tensor(0.3144, device='cuda:0'), tensor(40.9971, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 11 Loss : 972.1351257324219



    0it [00:00, ?it/s]


    (tensor(0.9691, device='cuda:0'), tensor(0.7526, device='cuda:0'), tensor(0.4021, device='cuda:0'), tensor(32.7424, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 12 Loss : 1090.1743530273438



    0it [00:00, ?it/s]


    (tensor(0.9485, device='cuda:0'), tensor(0.8247, device='cuda:0'), tensor(0.3969, device='cuda:0'), tensor(30.8369, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 13 Loss : 658.3907958984375



    0it [00:00, ?it/s]


    (tensor(0.9742, device='cuda:0'), tensor(0.8299, device='cuda:0'), tensor(0.3814, device='cuda:0'), tensor(29.2859, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 14 Loss : 724.2850799560547



    0it [00:00, ?it/s]


    (tensor(0.9691, device='cuda:0'), tensor(0.8402, device='cuda:0'), tensor(0.3454, device='cuda:0'), tensor(32.7917, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 15 Loss : 1161.784976196289



    0it [00:00, ?it/s]


    (tensor(0.9330, device='cuda:0'), tensor(0.7629, device='cuda:0'), tensor(0.3454, device='cuda:0'), tensor(39.7505, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 16 Loss : 1071.117413330078



    0it [00:00, ?it/s]


    (tensor(0.9588, device='cuda:0'), tensor(0.8247, device='cuda:0'), tensor(0.3247, device='cuda:0'), tensor(33.5242, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 17 Loss : 984.894189453125



    0it [00:00, ?it/s]


    (tensor(0.9691, device='cuda:0'), tensor(0.7938, device='cuda:0'), tensor(0.2835, device='cuda:0'), tensor(34.5743, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 18 Loss : 957.6609375



    0it [00:00, ?it/s]


    (tensor(0.9794, device='cuda:0'), tensor(0.7474, device='cuda:0'), tensor(0.3711, device='cuda:0'), tensor(40.8665, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 19 Loss : 726.6043823242187



    0it [00:00, ?it/s]


    (tensor(0.9742, device='cuda:0'), tensor(0.7268, device='cuda:0'), tensor(0.4330, device='cuda:0'), tensor(29.4098, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 20 Loss : 639.893832397461



    0it [00:00, ?it/s]


    (tensor(0.9742, device='cuda:0'), tensor(0.6598, device='cuda:0'), tensor(0.4381, device='cuda:0'), tensor(27.1055, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 21 Loss : 414.34313507080077



    0it [00:00, ?it/s]


    (tensor(0.9742, device='cuda:0'), tensor(0.8351, device='cuda:0'), tensor(0.4021, device='cuda:0'), tensor(25.2148, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 22 Loss : 280.23120269775393



    0it [00:00, ?it/s]


    (tensor(0.9639, device='cuda:0'), tensor(0.7938, device='cuda:0'), tensor(0.4124, device='cuda:0'), tensor(25.3277, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 23 Loss : 318.01119232177734



    0it [00:00, ?it/s]


    (tensor(0.9742, device='cuda:0'), tensor(0.8299, device='cuda:0'), tensor(0.3814, device='cuda:0'), tensor(26.3586, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 24 Loss : 212.05134963989258



    0it [00:00, ?it/s]


    (tensor(0.9742, device='cuda:0'), tensor(0.7165, device='cuda:0'), tensor(0.4278, device='cuda:0'), tensor(26.1501, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 25 Loss : 192.6232063293457



    0it [00:00, ?it/s]


    (tensor(0.9742, device='cuda:0'), tensor(0.8299, device='cuda:0'), tensor(0.4278, device='cuda:0'), tensor(27.0893, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 26 Loss : 253.8660903930664



    0it [00:00, ?it/s]


    (tensor(0.9742, device='cuda:0'), tensor(0.8299, device='cuda:0'), tensor(0.4639, device='cuda:0'), tensor(27.4750, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 27 Loss : 153.20695571899415



    0it [00:00, ?it/s]


    (tensor(0.9742, device='cuda:0'), tensor(0.8454, device='cuda:0'), tensor(0.3247, device='cuda:0'), tensor(25.4001, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 28 Loss : 228.38826446533204



    0it [00:00, ?it/s]


    (tensor(0.9691, device='cuda:0'), tensor(0.8247, device='cuda:0'), tensor(0.2990, device='cuda:0'), tensor(25.7139, device='cuda:0'))


    /usr/local/lib/python3.10/dist-packages/torch/utils/data/dataloader.py:560: UserWarning: This DataLoader will create 4 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
      warnings.warn(_create_warning_msg(


     Epoch 29 Loss : 344.0905601501465



    0it [00:00, ?it/s]


    (tensor(0.9691, device='cuda:0'), tensor(0.8144, device='cuda:0'), tensor(0.4536, device='cuda:0'), tensor(26.4411, device='cuda:0'))



```python
preprocess = transforms.Compose([
    transforms.Resize((224, 224)),
    transforms.ToTensor(),
    transforms.Normalize(mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225])
])
```


```python
all_species =  ['american_bulldog', 'Birman', 'Birman', 'Persian', 'Birman', 'american_pit_bull_terrier', 'beagle', 'american_pit_bull_terrier', 0, 'american_pit_bull_terrier', 'Persian', 'beagle', 0, 'Birman', 'basset_hound', 'Persian', 'Abyssinian', 0, 'Birman', 'beagle', 'american_bulldog', 'chihuahua', 0, 'american_pit_bull_terrier', 'chihuahua', 'basset_hound', 'american_bulldog', 'beagle', 'beagle', 0, 'Abyssinian', 'basset_hound']
all_species.append('unknown')  # Add 'unknown' category during fitting
label_encoder = LabelEncoder()
label_encoder.fit(all_species)
```




<style>#sk-container-id-1 {color: black;background-color: white;}#sk-container-id-1 pre{padding: 0;}#sk-container-id-1 div.sk-toggleable {background-color: white;}#sk-container-id-1 label.sk-toggleable__label {cursor: pointer;display: block;width: 100%;margin-bottom: 0;padding: 0.3em;box-sizing: border-box;text-align: center;}#sk-container-id-1 label.sk-toggleable__label-arrow:before {content: "â–¸";float: left;margin-right: 0.25em;color: #696969;}#sk-container-id-1 label.sk-toggleable__label-arrow:hover:before {color: black;}#sk-container-id-1 div.sk-estimator:hover label.sk-toggleable__label-arrow:before {color: black;}#sk-container-id-1 div.sk-toggleable__content {max-height: 0;max-width: 0;overflow: hidden;text-align: left;background-color: #f0f8ff;}#sk-container-id-1 div.sk-toggleable__content pre {margin: 0.2em;color: black;border-radius: 0.25em;background-color: #f0f8ff;}#sk-container-id-1 input.sk-toggleable__control:checked~div.sk-toggleable__content {max-height: 200px;max-width: 100%;overflow: auto;}#sk-container-id-1 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {content: "â–¾";}#sk-container-id-1 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 input.sk-hidden--visually {border: 0;clip: rect(1px 1px 1px 1px);clip: rect(1px, 1px, 1px, 1px);height: 1px;margin: -1px;overflow: hidden;padding: 0;position: absolute;width: 1px;}#sk-container-id-1 div.sk-estimator {font-family: monospace;background-color: #f0f8ff;border: 1px dotted black;border-radius: 0.25em;box-sizing: border-box;margin-bottom: 0.5em;}#sk-container-id-1 div.sk-estimator:hover {background-color: #d4ebff;}#sk-container-id-1 div.sk-parallel-item::after {content: "";width: 100%;border-bottom: 1px solid gray;flex-grow: 1;}#sk-container-id-1 div.sk-label:hover label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 div.sk-serial::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: 0;}#sk-container-id-1 div.sk-serial {display: flex;flex-direction: column;align-items: center;background-color: white;padding-right: 0.2em;padding-left: 0.2em;position: relative;}#sk-container-id-1 div.sk-item {position: relative;z-index: 1;}#sk-container-id-1 div.sk-parallel {display: flex;align-items: stretch;justify-content: center;background-color: white;position: relative;}#sk-container-id-1 div.sk-item::before, #sk-container-id-1 div.sk-parallel-item::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: -1;}#sk-container-id-1 div.sk-parallel-item {display: flex;flex-direction: column;z-index: 1;position: relative;background-color: white;}#sk-container-id-1 div.sk-parallel-item:first-child::after {align-self: flex-end;width: 50%;}#sk-container-id-1 div.sk-parallel-item:last-child::after {align-self: flex-start;width: 50%;}#sk-container-id-1 div.sk-parallel-item:only-child::after {width: 0;}#sk-container-id-1 div.sk-dashed-wrapped {border: 1px dashed gray;margin: 0 0.4em 0.5em 0.4em;box-sizing: border-box;padding-bottom: 0.4em;background-color: white;}#sk-container-id-1 div.sk-label label {font-family: monospace;font-weight: bold;display: inline-block;line-height: 1.2em;}#sk-container-id-1 div.sk-label-container {text-align: center;}#sk-container-id-1 div.sk-container {/* jupyter's `normalize.less` sets `[hidden] { display: none; }` but bootstrap.min.css set `[hidden] { display: none !important; }` so we also need the `!important` here to be able to override the default hidden behavior on the sphinx rendered scikit-learn.org. See: https://github.com/scikit-learn/scikit-learn/issues/21755 */display: inline-block !important;position: relative;}#sk-container-id-1 div.sk-text-repr-fallback {display: none;}</style><div id="sk-container-id-1" class="sk-top-container"><div class="sk-text-repr-fallback"><pre>LabelEncoder()</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br />On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class="sk-container" hidden><div class="sk-item"><div class="sk-estimator sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-1" type="checkbox" checked><label for="sk-estimator-id-1" class="sk-toggleable__label sk-toggleable__label-arrow">LabelEncoder</label><div class="sk-toggleable__content"><pre>LabelEncoder()</pre></div></div></div></div></div>




```python
from PIL import ImageDraw

def visualize(model_weights, image_folder_path, output_folder="output"):

    model = Model()
    model.load_state_dict(torch.load(model_weights))
    model.eval()

    # Create the output folder if it doesn't exist
    os.makedirs(output_folder, exist_ok=True)

    # Define the preprocessing transformation
    preprocess = transforms.Compose([
        transforms.Resize((224, 224)),
        transforms.ToTensor(),
        transforms.Normalize(mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225])
    ])

    # Get the list of image files in the folder
    image_files = os.listdir(image_folder_path)

    results = {}

    for image_file in image_files:
        image_path = os.path.join(image_folder_path, image_file)
        image_name = os.path.splitext(image_file)[0]

        try:
            image = Image.open(image_path)
        except:
            continue

        # Preprocess the image
        image_tensor = preprocess(image).unsqueeze(0)

        # Make predictions using the model
        with torch.no_grad():
            output = model(image_tensor)

        # Extract the predicted values
        bbox = output["bbox"][0]
        object_pred = output["object"][0]
        cat_or_dog_pred = output["cat_or_dog"][0]
        specie_pred = output["specie"][0]

        # Decode the predictions
        has_object = bool(torch.argmax(object_pred).item())
        cat_or_dog = "cat" if torch.argmax(cat_or_dog_pred).item() == 0 else "dog"
        specie_idx = torch.argmax(specie_pred).item()
        specie = label_encoder.inverse_transform([specie_idx])[0]

        # Convert the bounding box predictions to integers
        xmin, ymin, xmax, ymax = map(int, bbox.tolist())

        # Prepare the result dictionary
        result = {
            "has_object": has_object,
            "cat_or_dog": cat_or_dog,
            "specie": specie,
            "xmin": xmin,
            "ymin": ymin,
            "xmax": xmax,
            "ymax": ymax
        }

        results[image_file] = result

        # Draw the bounding box on the image
        draw = ImageDraw.Draw(image)
        draw.rectangle([(xmin, ymin), (xmax, ymax)], outline="red", width=2)

        # Save the annotated image
        output_path = os.path.join(output_folder, image_file)
        image.save(output_path)

    return results

```


```python
model_weights = "/content/model.pth"
image_folder_path = "/content/assessment_dataset/images"
output_folder = "output"

results = visualize(model_weights, image_folder_path, output_folder)
```


```python
from PIL import ImageDraw

def visualize(model_weights, image_folder_path, output_folder="output"):

    model = Model()
    model.load_state_dict(torch.load(model_weights))
    model.eval()

    # Create the output folder if it doesn't exist
    os.makedirs(output_folder, exist_ok=True)

    # Define the preprocessing transformation
    preprocess = transforms.Compose([
        transforms.Resize((224, 224)),
        transforms.ToTensor(),
        transforms.Normalize(mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225])
    ])

    # Get the list of image files in the folder
    image_files = os.listdir(image_folder_path)

    results = {}

    for image_file in image_files:
        image_path = os.path.join(image_folder_path, image_file)
        image_name = os.path.splitext(image_file)[0]

        try:
            image = Image.open(image_path)
        except:
            continue

        # Preprocess the image
        image_tensor = preprocess(image).unsqueeze(0)

        # Make predictions using the model
        with torch.no_grad():
            output = model(image_tensor)

        # Extract the predicted values
        bbox = output["bbox"][0]
        object_pred = output["object"][0]
        cat_or_dog_pred = output["cat_or_dog"][0]
        specie_pred = output["specie"][0]

        # Decode the predictions
        has_object = bool(torch.argmax(object_pred).item())
        cat_or_dog = "cat" if torch.argmax(cat_or_dog_pred).item() == 0 else "dog"
        specie_idx = torch.argmax(specie_pred).item()
        specie = label_encoder.inverse_transform([specie_idx])[0]

        # Convert the bounding box predictions to integers
        xmin, ymin, xmax, ymax = map(int, bbox.tolist())

        # Prepare the result dictionary
        result = {
            "has_object": has_object,
            "cat_or_dog": cat_or_dog,
            "specie": specie,
            "xmin": xmin,
            "ymin": ymin,
            "xmax": xmax,
            "ymax": ymax
        }

        results[image_file] = result

        # Draw the bounding box on the image
        draw = ImageDraw.Draw(image)
        draw.rectangle([(xmin, ymin), (xmax, ymax)], outline="red", width=2)

        # Write the species label on the bounding box
        label_text = f"{specie} ({cat_or_dog})"
        label_width, label_height = draw.textsize(label_text)
        label_position = (xmin, ymin - label_height - 5)
        draw.rectangle([(label_position[0], label_position[1]), (label_position[0] + label_width, label_position[1] + label_height)], fill="red")
        draw.text(label_position, label_text, fill="white")

        # Save the annotated image
        output_path = os.path.join(output_folder, image_file)
        image.save(output_path)

    return results

```


```python
model_weights = "/content/model.pth"
image_folder_path = "/content/assessment_dataset/images"
output_folder = "output"

results = visualize(model_weights, image_folder_path, output_folder)
```

    /usr/local/lib/python3.10/dist-packages/torchvision/models/_utils.py:208: UserWarning: The parameter 'pretrained' is deprecated since 0.13 and may be removed in the future, please use 'weights' instead.
      warnings.warn(
    /usr/local/lib/python3.10/dist-packages/torchvision/models/_utils.py:223: UserWarning: Arguments other than a weight enum or `None` for 'weights' are deprecated since 0.13 and may be removed in the future. The current behavior is equivalent to passing `weights=ResNet18_Weights.IMAGENET1K_V1`. You can also use `weights=ResNet18_Weights.DEFAULT` to get the most up-to-date weights.
      warnings.warn(msg)



```python
from PIL import Image, ImageDraw
import matplotlib.pyplot as plt

# Get the list of image files
image_files = os.listdir(image_folder_path)[:10]  # Select the first 10 images

# Create a subplot with 2 rows and 5 columns
fig, axs = plt.subplots(2, 5, figsize=(15, 6))

# Iterate over the image files
for i, image_file in enumerate(image_files):
    # Load the image
    image_path = os.path.join(image_folder_path, image_file)
    image = Image.open(image_path)

    # Load the corresponding result
    result = results[image_file]

    # Create a copy of the image to draw on
    draw_image = image.copy()
    draw = ImageDraw.Draw(draw_image)

    # Draw the bounding box if an object is detected
    if result["has_object"]:
        xmin, ymin, xmax, ymax = result["xmin"], result["ymin"], result["xmax"], result["ymax"]
        draw.rectangle([(xmin, ymin), (xmax, ymax)], outline="red", width=2)

        # Write the species label on the bounding box
        label_text = f"{result['specie']} ({result['cat_or_dog']})"
        label_width, label_height = draw.textsize(label_text)
        label_position = (xmin, ymin - label_height - 5)
        draw.rectangle([(label_position[0], label_position[1]), (label_position[0] + label_width, label_position[1] + label_height)], fill="red")
        draw.text(label_position, label_text, fill="white")

    # Display the image with bounding boxes
    axs[i // 5, i % 5].imshow(draw_image)
    axs[i // 5, i % 5].axis('off')

# Show the plot
plt.tight_layout()
plt.show()

```


​    
![png](ML_Engineer_Take_Home_Assessment_files/ML_Engineer_Take_Home_Assessment_30_0.png)
​    



```python

```
