# CV & UNET multi-class image segmentation project
A Computer Vision &amp; Deep learning project on bone fracture medical data

### Dataset
I used a dataset called [FracAtlas](https://www.kaggle.com/datasets/mahmudulhasantasin/fracatlas-original-dataset/data) dataset - it is a dataset of X-Ray scans curated from the images collected from 3 major hospitals in Bangladesh. It contains 2 global labels: fractured and non-fractured bones, additionally containing fracture annotations for each fractured bone. The dataset includes 4,083 images, where 717 images with 922 instances of fractures.
This dataset could be easily used for binary segmentation with 2 classes (fractures and everything else); however, I wanted to work on multi-class segmentation with 3 classes: fractures, bones, and blank space.

### Data pre-processing
In the dataset, there is only one class - fracture, so I had to do preprocessing: I used a Li Thresholding for the bone after several experiments, generated the masks from bones and fracture classes, and combined everything (and background).

### Training and results
I used classic UNET architecture and trained it 50 epochs with batch size 16. As metrics, I chose Accuracy, loss, and meanIoU.

In testing, the results are below:
Accuracy is =  99.59%
Mean IoU is =  83%
Loss is =  02%

However, per-class IoU results are:
IoU for class 0: 99.88%

IoU for class 1: 97.92%

IoU for class 2: 25.86%

Mean IoU: 0.7455
<img width="1254" height="416" alt="image" src="https://github.com/user-attachments/assets/02a00dda-945e-43bf-bd2f-693948e632c3" />

As you can see in the results, the training accuracy is very high (99%), and the mean IOU is okay (83%), but you can see that the fracture is being segmented very poorly. There are likely 2 reasons for that: insufficient pre-processing and the amount of training data (only 574 images). You can see above that the testing label is not seen clearly, so either thresholding doesn't work well, or it is not enough. I think adding morphological transformation would have made the labels at least a bit better. 

One of the main challenges was preparing the dataset, as the original images contained only fractures. To address this, I generated bone masks using Li thresholding and separated of bone and fracture classes. Additionally, class imbalance initially caused the model to ignore fractures, which required balancing the dataset by adding weights to improve performance.

