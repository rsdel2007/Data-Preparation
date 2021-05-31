# Data-Preparation

- I have collected some differently coloured cones by scraping google images. I have uploaded data on [google drive](https://drive.google.com/drive/u/2/folders/1Ny0qUTbB0KxCktouF8KFxD9Hj7_VjL5W). Some images were repeated, and some were useless, i.e., I had to filter the images manually. Finally, there are about ~1100 images. For now, I have resized the image size into 224 x 224, but I will be resizing later while training the model as per the algorithm's requirements ([models](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2_detection_zoo.md)).
- The next part was to annotate all the images. For this, I had to create bounding boxes for each image in the data manually. I used [labelimg](https://github.com/tzutalin/labelImg) for this task. After each step, I got a ```.xml``` file for each image that contains labels and coordinates of the bounding box in Pascal-VOC format(Since I will be using SSD/Faster RCNN).
- I used ```xml_to_csv.py``` to convert the labels into ```CSV``` format. Now labels are ready to use.
- Further, I will be generating ```tfrecords``` and the ```label map```, which will complete the dataset preparation.

- Generated ```tfrecord``` using TensorFlow Object Detection API.<br>
First step was to install [TensorFlow Models repository](https://github.com/tensorflow/models) in conda environment. Then created a folder ```annotations``` which contains ```train``` and ```test``` folder, such that images and .xml files for training & testing are stored in ```train``` and ```test``` folder respectively. <br>
Then a ```labelmap``` was required, that namely maps each used labels to an integer values. Here, only 1 label is used.<br>
Then I wrote a script ```generate_tfrecord.py``` using the instructions provided by [TensorFlow](https://www.tensorflow.org/tutorials/load_data/tfrecord) to generate tfrecord for each image in the csv file.<br>
Final step is to run the following command in the same conda environment:<br>
```python generate_tfrecord.py -x /train -l /label_map.pbtxt -o /train.record```<br>
```python generate_tfrecord.py -x /test -l /label_map.pbtxt -o [/test.record```<br>
These will generate two files ```train.record``` and ```test.record```. These will be used to train the detection model.
