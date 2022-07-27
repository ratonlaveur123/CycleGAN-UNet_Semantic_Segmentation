# CycleGAN-UNet_Semantic_Segmentation

The purpose of this project is to perform image translation between summer and winter pictures using CycleGAN and also to perform semantic segmentation using UNet. The image data was obtained from Kaggle[1]. 

CycleGAN architecture: 

<img width="914" alt="Screen Shot 2022-07-26 at 11 04 14 PM" src="https://user-images.githubusercontent.com/72672367/181151750-48904095-800f-4f8b-8078-73856b478ac0.png">

A few highlights of the CycleGAN model: 
- The discriminator used Conv2D layer at the end to be able to output real/fake lables at region level for an image instead of a single real/fake classification. 
- Identity loss is incorporated into the model (Identity mapping means feeding images from the same domain as the generator and expecting the same output)
- Model loss is consisted of adversarial loss, identity loss as well as forward and backward cycle loss 
- Each convolutional layer has ‘“same” padding, followed by instance normalization and leaky relu activation to prevent vanishing gradient
- Model was trained for about 20 epochs and could be trained longer to improve model performance 



Here are the results of image translation:

<img width="650" alt="Screen Shot 2022-07-26 at 11 10 53 PM" src="https://user-images.githubusercontent.com/72672367/181152516-ba31aeb4-7886-4094-9e40-8f91826de9b8.png">
<img width="651" alt="Screen Shot 2022-07-26 at 11 11 20 PM" src="https://user-images.githubusercontent.com/72672367/181152557-94b7a0d0-b232-482c-bfa4-7875316ad76a.png">

The second part of the project is to perform semantic segmentation using UNet model. The image data was also obtained from Kaggle[2] and it has lables from nine different class keys. 

A few highlights of the UNet model: 
- Applied one-hot-encoding to convert a 2D image label array into one-hot format and reverse one-hot encoding to transform the one-hot format image into a 2D array with only 1 channel, where each pixel value is the classified class key 
- Applied data augmentation and preprocessing transformations on the image dataset
Applied UNet segmentation model with ‘resnet50’ pretrained encoder and ‘imagenet’ encoder weights
- UNet model is consisted of two parts: encoder and decoder. Encoder is a traditional stack of convolutional and max pooling layers. Decoder is the expansion path consisting of transposed convolutional layers along with regular convolutions. Skip connection is used at every step of the decoder by concatenating the output of the tranposed convolution layers with the feature maps from the encoder at the same level. (refer to the graph below)
- Trained UNet model for about 50 epochs but can be trained longer for even better performance

UNet architecture[3]: 

<img width="709" alt="Screen Shot 2022-07-26 at 11 17 52 PM" src="https://user-images.githubusercontent.com/72672367/181153246-6755ac53-15cb-4d91-ba01-a6de61b99a11.png">

Sample Result: 

<img width="799" alt="Screen Shot 2022-07-26 at 11 24 20 PM" src="https://user-images.githubusercontent.com/72672367/181153986-11eb2716-1606-48ff-bfca-a48311a22b1d.png">

References: 
[1] Mehul Gupta. (2021, Sep 14) Understanding CycleGANs using examples & Codes. Retrieved from https://medium.com/data-science-in-your-pocket/understanding-cyclegans-using-examples-codes-f5d6e1a47048
[2] Balraj Ashwath. UNet for Segmenting BobRoss Paintings. Retrieved from https://www.kaggle.com/code/balraj98/unet-for-segmenting-bob-ross-paintings-pytorch
[3] Harshall Lamda. (2019, Feb 17) Understanding Semantic Segmentation with UNET. Retrived from https://towardsdatascience.com/understanding-semantic-segmentation-with-unet-6be4f42d4b47


