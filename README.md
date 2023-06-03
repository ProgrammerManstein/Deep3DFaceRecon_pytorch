# Install
Unzip the Deep3DFaceRecon_pytorch.zip  
Use the [jupyter notebook]([https://www.baidu.com/](https://github.com/ProgrammerManstein/Deep3DFaceRecon_pytorch/blob/master/notebook/3dre.ipynb))to install the project.
You can find some help from [the origin project](https://github.com/sicxu/Deep3DFaceRecon_pytorch)  
# Test with custom images  
To reconstruct 3d faces from test images, organize the test image folder as follows:  

```  
Deep3DFaceRecon_pytorch  
│  
└─── <folder_to_test_images>  
    │  
    └─── *.jpg/*.png  
    |  
    └─── detections  
        |  
	└─── *.txt  
    
```
The *.jpg/*.png files are test images. The *.txt files are detected 5 facial landmarks with a shape of 5x2, and have the same name as the corresponding images. Check ./datasets/examples for a reference.  

Then, run the test script:  

# get reconstruction results of your custom images  

```
python test.py --name=<model_name> --epoch=20 --img_folder=<folder_to_test_images>  
```

# get reconstruction results of example images  
```
python test.py --name=<model_name> --epoch=20 --img_folder=./datasets/examples  
```
Following #108, if you don't have OpenGL environment, you can simply add "--use_opengl False" to use CUDA context. Make sure you have updated the nvdiffrast to the latest version.  

Results will be saved into ./checkpoints/<model_name>/results/<folder_to_test_images>, which contain the following files:  

```
*.png	A combination of cropped input image, reconstructed image, and visualization of projected landmarks.  
*.obj	Reconstructed 3d face mesh with predicted color (texture+illumination) in the world coordinate space. Best viewed in Meshlab.  
*.mat	Predicted 257-dimensional coefficients and 68 projected 2d facial landmarks. Best viewed in Matlab.  
```
