# Use Pytorch to train your own facial keypoint model to detect face
## https://medium.com/@patrickhk/use-pytorch-to-train-your-own-facial-keypoint-model-to-detect-face-1c9203ab85ac

### Dataset
Youtube Faces Dataset is used for training, total 3462 training images and 2308 testing images. Also we need a CSV file containing the annotations of the facial keypoints of the above face images. Remember to use pandas to read the CSV file and reshape into proper (x,y) coordinate format for our model.<br/>

### Visualize data
We can write a helper function to read the x,y coordinate and use maplotlib to write the scatter points over the original images, such as
![p1](https://cdn-images-1.medium.com/max/800/1*JU2ZY7TmadHS1PLlWq9EGA.png)<br/>

### Preprocessing/ transformation
Preprocessing/transformation is a must-do step for image data. Common preprocessing includes rescaling, normalizing, random cropping, flipping..etc <br/>

Pytorch and Keras both have their ready-to-use transformation class their we can import easier. However in this udacity project we write our own class, i guess the purpose is want us getting familiarized with customized class.<br/>
![p2](https://cdn-images-1.medium.com/max/800/1*muDzI7OXb-AcOnKx5eyWcg.png)<br/>
### Build the CNN model
I choose to build my own CNN model from scratch. I apply total 8 convolution layers and 3 fully connected layers. I apply maxpooling layer with stride=2 every 2 convolution layers, then the batch normalization layer. Dropout layers are added in between the FC layers.<br/>

Honestly there is no “model answer” for CNN model architecture, just trial and error. It is a good practice to apply batch norm and drop out layer…etc<br/>

If you want to go quicker you may considering using pre-trained model.<br/>

![p3](https://cdn-images-1.medium.com/max/800/1*rQJ_woX5R1FtbUHIOvc3gw.png)<br/>
### Hyper parameter for training
I always use Adam optimizer, my first choice.<br/>

Batch size=16 this is the max my GPU can afford.<br/>

Learning rate 0.01 to 0.001, depend on number of epoch. When I observe the validation loss is getting flatted, I lower the lr.<br/>
### Result
In the original udacity project we are not required to calculate validation loss so the dataset didnt contain validation set. I myself think a validation set is very important in training therefore I use the test set as validation set and build the code to track the validation loss.<br/>

I find other unseen images to test the result of the model.<br/>
![p4](https://cdn-images-1.medium.com/max/800/1*HFATChg0Bd1ZWOGqBdOLDA.png)<br/>
The actual epoch I trained was over 30+ but I didnt record the loss data during the first 15–20 epochs. Since this project is for my own interest only, I don’t plan to re-run again just to get all the tracking. (Notice it is a good practice to keep all the records about the epoch, lr and loss data…etc)<br/>

Generally both the training loss and validation loss are decreasing with the last 15 epochs and without sign of overfitting. However when epoch=8 the validation loss was abnormally high, then return to normal.<br/>


![p5](https://cdn-images-1.medium.com/max/800/1*K3AAi-Up2CpCYKMZtcokYw.png)<br/>
![p6](https://cdn-images-1.medium.com/max/800/1*soZpvZ5WSp3vsfrRf3muNw.png)<br/>
From the above comparison we can see our model can predict facial keypoints quite well after training.<br/>
### Let combine with other computer vision skills

![p7](https://cdn-images-1.medium.com/max/800/1*gicQHKIkkP07arA3DQSV-Q.png)<br/>
I apply Harr features to detect all the faces in the image because it is fast. (there are many better options such as HOG..etc) . Then I use cv2.rectangle to draw box over the coordinate.<br/>
![p8](https://cdn-images-1.medium.com/max/800/1*gWa5Y4TmFwDt7ZUChgQlPA.png)<br/>

Write a custom function to select the face area only (ROI), remember to normalize and convert to torch tensor before pass into our trained model.<br/>
![p8](https://cdn-images-1.medium.com/max/800/1*gMjlIzvrl75D6RVgmp8pRg.png)<br/>
This is the final result, can see our CNN model can predict the facial keypoints of the Averager actors quite well!

-------------------------------------------------------------------------------------------------------------------------------------
### More about me
[[:pencil:My Medium]](https://medium.com/@patrickhk)<br/>
[[:house_with_garden:My Website]](https://www.fiyeroleung.com/)<br/>
[[:space_invader:	My Github]](https://github.com/fiyero)<br/>
