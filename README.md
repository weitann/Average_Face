# Average Face
Author: Wei Tan

### Summary of project
Celebrities' photos (a total of 13,233 photos) were downloaded from "[Faces in the Wild](http://vis-www.cs.umass.edu/lfw/)" 
and pixels are averaged to produce an "average face". 

### Recognize some of these faces?
Following are some sample photos that were included in the dataset.

![samples8](https://user-images.githubusercontent.com/42630569/52839895-6fd13300-30ac-11e9-813d-37114589def6.png)

### Average face
Using celebrities with more than 10 images in the given folder, the pixels were averaged across all the images to give an "average face".

![average](https://user-images.githubusercontent.com/42630569/52840043-ecfca800-30ac-11e9-8eaf-cb18478d80d0.png)

### Standard deviation in pixels across of images
To identify the areas that has the highest pixel difference across all images, the heatmap of the pixels is plotted. 
From the image below, we can see that the background of images has the highest standard deviation, which is expected since background can be of any color or gradient depending on where the photo was taken. In contrast, skin colors do not have much variety and has the lowest standard deviation.

![average_std](https://user-images.githubusercontent.com/42630569/52840216-698f8680-30ad-11e9-8c19-ff886b164fbe.png)

### K-Means clustering
Using k-means clustering with k=20, we identified the following 20 centroids, along with the image that is closest to that centroid.
The left column displays the centroids, while the right column displays their respective most similar image.

Do they look alike?

![colored_centroids](https://user-images.githubusercontent.com/42630569/52840456-33063b80-30ae-11e9-80db-b7f074cc9467.png)

From the above centroids and images, we observe that this clustering method causes photos with similar background colors to be clustered together, which may not be ideal. We want to focus on the faces in these images.

### Which centroid do I belong to?
Top left: my photo, Top right, my centroid
Bottom left: photo closest to my centroid, Bottom right: photo closest to my photo
![my_image](https://user-images.githubusercontent.com/42630569/52840579-985a2c80-30ae-11e9-99da-7c33ef6140ab.png)
![my_centroid](https://user-images.githubusercontent.com/42630569/52840641-bb84dc00-30ae-11e9-85e4-f862d7e566b2.png)

![my_closest_imagetocentroid](https://user-images.githubusercontent.com/42630569/52843031-b5462e00-30b5-11e9-9074-fe55646d477d.png)
![my_closest_image](https://user-images.githubusercontent.com/42630569/52843032-b70ff180-30b5-11e9-8545-0018ef9dcf1b.png)
💬

### PCA with 1 to 100 components
Next, PCA is performed to extract a selected number of components, and its effect on the % variance preserved is plotted.
To preserve around 90% of the total variance of the data, 80 components will be required.

![pca_variance_graph](https://user-images.githubusercontent.com/42630569/52840885-7ad99280-30af-11e9-9c3a-e5b80fa55d26.png)

How do the components look like? Below are the top 10 components selected.

![pca_components](https://user-images.githubusercontent.com/42630569/52841150-592cdb00-30b0-11e9-9f5d-4bdcafc896aa.png)

### Display 20 centroids after PCA with 50 components
Now let's take a look the 20 centroids created after projecting images into 50-dimensional space defined by the first 50 principal components...

![pca_centroids](https://user-images.githubusercontent.com/42630569/52841230-96916880-30b0-11e9-8489-3e20b83f17ee.png)

### Pre and post PCA comparison
Using transformed images, we can observe how images and their centroids are affect.
From the left to the right column are the original images, images after PCA, their respective nearest centroids, the transformed image closest to each centroid, and the original image closest that centroid.

![pre_post_pca](https://user-images.githubusercontent.com/42630569/52841746-eae91800-30b1-11e9-97bc-bfd3f94058a4.png)

### Deep Learning
Last but not least, [Keras InceptionV3 model](https://keras.io/applications/#inceptionv3) was implemented to observe the difference in performance compared to k-means clustering.

The model can be visualized as follows:

![imagenet_inception_module](https://user-images.githubusercontent.com/42630569/52842124-fc7eef80-30b2-11e9-9ef7-d9cc2e62d539.png)
Image via [pyimagesearch](https://www.pyimagesearch.com/2017/03/20/imagenet-vggnet-resnet-inception-xception-keras/)

And 20 centroids are produced.

![deep](https://user-images.githubusercontent.com/42630569/52842704-c6426f80-30b4-11e9-869e-039af478e1a9.png)

Testing the model on my image, the following are the images closest to my centroid, and closest to my image. Resemblance?

![my_image](https://user-images.githubusercontent.com/42630569/52840579-985a2c80-30ae-11e9-99da-7c33ef6140ab.png)
![my_2nd_centroid](https://user-images.githubusercontent.com/42630569/52842856-38b34f80-30b5-11e9-8e99-efff372a3527.png)
![my_2nd_closest](https://user-images.githubusercontent.com/42630569/52842860-3c46d680-30b5-11e9-8c0d-fde8d18edff1.png)

Looks slightly more similar than k-means clustering.
