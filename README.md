# Using AI to Address Taiwan’s Waste Classification and Recycling Management

## Project Description

This project aims to develop an AI model tailored specifically for waste classification in Taiwan. Existing AI models from other countries often lack specificity for the unique types of waste commonly found in Taiwan and do not align with Taiwanese waste classification regulations. Taiwan’s recycling rate has reached an impressive 60% as of 2022, however, without a correct and precise classification at the source, recycled materials would be downgraded or treated as garbage upon reaching recycling plants. To address this issue, we have curated a comprehensive dataset composed of images of various waste items collected in Taipei, and combined with other external sources. We utilized a Convolutional Neural Network (CNN) implemented with TensorFlow and Keras to identify and classify images of waste found in Taiwan, also providing clear instructions on their appropriate disposal methods.

## Getting Started

* Prerequisites
  - Ensure you have a Google account to access Google Colab.

* Prepare Data 
  - Download `original_data` and `preprocessed_data` using the following link: https://drive.google.com/drive/folders/1-1xCiUErjF-nEyUobdbqsEdGfIY-ZnoZ

* Running on Google Colab
  - Open Google Colab
  - Navigate to Google Colab in your web browser.
  - open the **model_Trash_Classifier.ipynb** by clicking the link below: https://colab.research.google.com/drive/1bs236qO3KR6_YBC5Hy3vBbrgmuBYXb46?usp=sharing
  - Make a copy and run our project on the copy

By following these steps, you can easily set up and run your project on Google Colab.

* Install Dependencies<br/>
  - Prerequisites: make sure you have the following software and libraries installed:<br/>
TensorFlow, Keras (part of TensorFlow),scikit-learn, PIL (Python Imaging Library), SciPy, NumPy, Matplotlib, PyTorch, Torchvision<br/><br/>
- Install and verify required Python libraries:<br/>
```
import tensorflow as tf
#import tensorflow.contrib.keras as keras
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Conv2D, Flatten, Dropout, MaxPooling2D
from tensorflow.keras.preprocessing.image import ImageDataGenerator
from sklearn.metrics import classification_report,confusion_matrix
from PIL import Image
from pathlib import Path
import scipy
import os
import numpy as np
import matplotlib.pyplot as plt
from torchvision.datasets import ImageFolder
import torchvision.transforms as T

print("Done with library declaration, Current version of Tensorflow is: ", tf.__version__)
```


## File Structure
The folders 'original_images' and 'processed_images' serve as examples. For the complete dataset, please visit the Google drive at https://drive.google.com/drive/folders/1-1xCiUErjF-nEyUobdbqsEdGfIY-ZnoZ.

* Train(orignal_images): 5112
  (contains 6 classes)
  -  一般垃圾 1074
  -  一般資源回收 1398
  -  保麗龍 496
  -  紙容器 376
  -  塑膠袋 1300
  -  廢紙 468
 
* Test(processed_images): 5112
  (contains 6 classes)
  -  一般垃圾 1074
  -  一般資源回收 1398
  -  保麗龍 496
  -  紙容器 376
  -  塑膠袋 1300
  -  廢紙 468

## Analysis

To address the specific needs of waste classification in Taiwan, we employed a convolutional neural network (CNN) architecture. The key steps in our analysis included:<br/>

- Data Collection and Preprocessing: We collected images of waste from various sources, focusing on six categories of garbage in Taiwan: cardboard, glass, metal, paper, plastic, and trash. Each image was resized to 32x32 pixels and converted to tensors for neural network processing.<br/>
```
IMG_HEIGHT = 32
IMG_WIDTH = 32
batch_size = 32
```
- Model Architecture: We built a CNN using the Sequential API in Keras. The model included convolutional layers to extract features from the images, pooling layers to reduce spatial dimensions, and fully connected layers to perform the final classification. <br/>
```
# 構建神經網絡模型
model = Sequential()

# 卷積層和池化層
model.add(Conv2D(32, kernel_size=(3,3), padding='same', input_shape=(IMG_HEIGHT, IMG_WIDTH, 3), activation='relu'))
model.add(MaxPooling2D(pool_size=2))

model.add(Conv2D(64, kernel_size=(3,3), padding='same', activation='relu'))
model.add(MaxPooling2D(pool_size=2))

model.add(Conv2D(32, kernel_size=(3,3), padding='same', activation='relu'))
model.add(MaxPooling2D(pool_size=2))

# 平坦層和全連接層
model.add(Flatten())

model.add(Dense(64, activation='relu'))
model.add(Dropout(0.2))
model.add(Dense(32, activation='relu'))
model.add(Dropout(0.2))
model.add(Dense(6, activation='softmax'))  # 輸出層為 6 個類別
```

- Training and Evaluation: The model was trained on a dataset split into training and validation sets. Metrics such as test accuracy, test loss, and the confusion matrix were used to evaluate the model.<br/><br/>

From our analysis, we gained several key insights:<br/>
- Model Accuracy: The final test accuracy of 72.21% demonstrates that our model performs well in classifying various types of waste according to Taiwan's specific categories. This level of accuracy indicates that the model can effectively support waste sorting processes.<br/>
![3549E8C4-EE2F-4F13-9737-D5292898FA3D_1_201_a](https://github.com/bbswan/GroupD_Taiwan-Waste-Classifier/assets/172978438/55eeb087-4839-46a6-969d-3283bb9835bf=250x250)

- Error Analysis: The confusion matrix and classification report highlighted specific categories where the model performed exceptionally well, such as general recycling, styrofoam, paper, and plastic bags. However, it also revealed areas where improvements are needed.<br/>
![F2140EDE-3F9A-4385-AFAA-E548FB8966C1_1_201_a](https://github.com/bbswan/GroupD_Taiwan-Waste-Classifier/assets/172978438/8861cb91-afb3-4725-b22a-6407729f5266)


## Results

The developed AI model tailored for waste classification in Taiwan achieved a final test accuracy of 72.21% and test loss of 1.36, demonstrating great performance on unseen data. The model excels in predicting categories like general recycling, styrofoam, and plastic bags while maintaining high accuracy across other waste types. For each input waste image, the model provides the classified label (e.g., Trash, Recyclable - Paper) and a recommendation on the appropriate disposal method and collection schedule.

By enabling precise waste classification at the source, the model addresses Taiwan's need for accurate identification aligned with local waste types and regulations. This can prevent the downgrading of recyclable materials and ensure proper recycling practices, leading to an increase in recycling rates, reduction in landfill use, and lower processing costs at recycling facilities, contributing to Taiwan's environmental sustainability and circular economy efforts.

Future work could involve **expanding the dataset** and categories, improving accuracy with **transfer learning** , and integrating the model into existing waste management systems or user-friendly applications to facilitate broader adoption and impact for all residents in Taiwan.

## Contributors

- 謝宜蓁 Coding, project discussion, content research + writing
- 鄒宸萱 Coding, project discussion, project presentation, content research + writing
- 韋欣 Dataset collection, project methodology discussion, booth poster design
- 胡裔婕 Project ideation, dataset collection, presentation slide design
- 李聖悅 Dataset collection, project methodology discussion, project presentation
- 葉可彤 Dataset collection

## Acknowledgments

We would like to express our sincere gratitude to the following individuals for their invaluable contributions to this project:

Pien, Chung-Pei (Professor): We are deeply grateful to professor Pien for providing guidance and mentorship throughout the project. Your expertise and insights were instrumental in shaping our approach and ensuring the success of this project.

Ian Huang (Teaching Assistant): We are very grateful to Ian for his unwavering support and guidance throughout the coding process, answering any questions we raised. 

The Kaggle Community: We would like to acknowledge the open-source community and the valuable resources they have created, which served as the foundation for our work. Specifically, we utilized some datasets from other creators for an increased accuracy.

## References

Dataset sources (for non-Taiwanese trash):<br/>
https://www.kaggle.com/datasets/mostafaabla/garbage-classification <br/>
https://www.kaggle.com/datasets/ashwinshrivastav/most-common-recyclable-and-nonrecyclable-objects <br/>
https://www.kaggle.com/code/farzadnekouei/imbalanced-garbage-classification-resnet50 <br/><br/>
  
Research sources:<br/>
https://news.pts.org.tw/article/488630 <br/>
https://www.nyckel.com/pretrained-classifiers/recycling-identifier/ <br/>
https://www.taiwanwatch.org.tw/node/1385 <br/>
