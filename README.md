# ArcFace
![arcface](https://user-images.githubusercontent.com/84235639/128590143-a6b9de0a-e123-409b-855c-a9ce73f28ffa.JPG)    
![arcface_eq](https://user-images.githubusercontent.com/84235639/130340815-74fedbf4-7d17-4000-851b-ad58a8ce0e3e.JPG)    
Arcface is a method of embedding feature vectors of images based on angles. Therefore, embeddings are distributed at specific angles for each class, and it is said that there is an advantage of embedding more precisely than the existing various metric learning methods. Before training, hyperparameters defined in uppercase letters in the train.py file must be specified in advance. The number of classes, batch size, and number of epochs must be entered, and the path of the data to be learned must also be entered.

    CLASS_NUM = 12
    EPOCHS = 30
    BATCH_SIZE = 16
    datagen = data_generator(DATASET_PATH = 'PATH/TO/THE/TRAIN_IMAGE/', shuffle_sel=True)
    # you can work with LFW dataset from Kaggle: https://www.kaggle.com/datasets/jessicali9530/lfw-dataset?resource=download-directory&select=lfw-deepfunneled

train.py trains the network containing the arcface algorithm, and creates a pytorch(.pt) file as the result.

    python train.py    
    
Similarly, in the test.py file, several hyperparameters must be specified in advance. The number of classes, batch size, threshold value and scaling factor should be specified. The threshold value becomes the decision threshold to be considered correct when the model's confidence is greater than or equal to this value. If you do not want to use this value, simply specify 0 to disable the function. And you can adjust the extremes of the softmax output by using a scaling factor. By dividing the input value of softmax by the corresponding factor, it is possible to obtain the effect of mitigating the output value so that it does not come out to an extreme value close to 0 or 1. It is possible to adjust the confidence, which is the output of softmax, to a reliable level through an appropriate factor for the model.

    BATCH_SIZE = 5
    THRESHOLD = 0.9
    CLASS_NUM = 12
    SCALING_FACTOR = 5 #for temperature scaling
    datagen = data_generator(DATASET_PATH = 'PATH/TO/THE/TEST_IMAGE/', shuffle_sel=True)

After specifying the value, you can evaluate the performance of the trained model by executing the test.py file.

    python test.py

# CosFace & SphereFace
![cosface_eq](https://user-images.githubusercontent.com/84235639/130340817-ea97e49e-5923-4c66-8b59-c4394f38fb56.JPG)
![sphereface_eq](https://user-images.githubusercontent.com/84235639/130340820-65bbd0a5-1bea-482b-851b-ef12a6dcfa68.JPG)  

Both cosface and sphereface are methods of creating an angular-based loss. However, the method of giving margin is different from arcface.
Cosface is a method of giving a margin to the cos value itself, not the angle, and sphereface is applied by multiplying the angle value rather than adding a margin. Distributed learning is implemented using three types of losses that give margins in different ways, which can be trained by executing the main_combine.py file. 
Also, you can check the result with test_combine.py, and you can get the result by ensemble each network.
