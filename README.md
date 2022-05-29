# Deep Learning Classification

Participation to the [Bird Challenge Classification](https://www.kaggle.com/competitions/mva-recvis-2021/data) 

![alt text](https://github.com/danielAmar02/CV_Classification/blob/main/pres.png)

For the data, please click [here](https://www.di.ens.fr/willow/teaching/recvis18orig/assignment3/bird_dataset.zip). 

## Few Insights

Trainging/Validation dataset : 1000 pictures of birds to classify in 20 classes
Test Dataset : 200 pictures of birds
Accuracy on the test dataset : 89% accuracy


# Method 

First of all, the main problem we are facing here is that we are lacking of data and thus the risk of overfitting is very high. 

We first work on a classical 4 layers CNN but it barely outperformed the random baseline of 10% and gave a 15% accuracy on the training dataset.

![alt text](https://github.com/danielAmar02/CV_Classification/blob/main/loss_init.png)


We then used data augmentation which reduced overfitting and I reached a 30% accuracy.

![alt text](https://github.com/danielAmar02/CV_Classification/blob/main/loss_dataaug.png)


The major improvement I made was to used a pre-trained model on ImageNet (I used **VGG16** and **ResNet**) which gave a 78% with the data augmentation. I also used an interesting idea developped by Francois Chollet (Keras founder) in his book Deep Learning with Python  which recommand to unfreeze "a few of the top layers of a frozen model base used for feature extraction, and jointly training both the newly added part of the model (in this  case the fully connected classifier) and these top layers". This allows to improve (although not significatively) the classification up to 80-82%. All of this allows me to really improve the overfitting.


![alt text](https://github.com/danielAmar02/CV_Classification/blob/main/loss_resnet.png)



Lastly, I realized that maybe some of the pictures were difficult to classify because of the environment (see example below). I tried to use the pretrained image segmentation model **Mask R-CNN trained on the COCO dataset** which allows to focus on the birds and then to reach a final 89% accuracy.

![alt text](https://github.com/danielAmar02/CV_Classification/blob/main/difficult.png)


## Ideas to improve classification

As a conclusion, I would like to speak about other ideas I had that may improve the classification task : 
- First of all, I believe there is still lot of room for hyperparameters improvement
- Secondly, I noticed that my model was behaving well except for 2 species (mixing class 0 and class 16). An extra model (0 vs 16) could be implemented in order ot improve the prediction for these two species.

![alt text](https://github.com/danielAmar02/CV_Classification/blob/main/confusion_matrix.png)
