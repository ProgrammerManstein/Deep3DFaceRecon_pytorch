# Install
Unzip the Deep3DFaceRecon_pytorch.zip. It has included everything we need for the project. 
Use the [jupyter notebook](https://github.com/ProgrammerManstein/Deep3DFaceRecon_pytorch/blob/master/notebook/3dre.ipynb) to install the project.
You can find some help from [the origin project](https://github.com/sicxu/Deep3DFaceRecon_pytorch).  
# Prepare prerequisite models
Our method uses Basel Face Model 2009 (BFM09) to represent 3d faces. Get access to BFM09 using this [link](https://drive.google.com/file/d/1bw5Xf8C12pWmcMhNEu6PtsYVZkVucEN6/view?usp=sharing). After getting the access, download "01_MorphableModel.mat". In addition, we use an Expression Basis provided by Guo et al.. Download the Expression Basis (Exp_Pca.bin) using this link ([google drive](https://drive.google.com/file/d/1bw5Xf8C12pWmcMhNEu6PtsYVZkVucEN6/view?usp=sharing)). Organize all files into the following structure:  
Deep3DFaceRecon_pytorch  
│  
└─── BFM  
    │  
    └─── 01_MorphableModel.mat  
    │  
    └─── Exp_Pca.bin  
    |  
    └─── ...  
We provide a model trained on a combination of CelebA, LFW, 300WLP, IJB-A, LS3D-W, and FFHQ datasets. Download the pre-trained model using this link ([google drive](https://faces.dmi.unibas.ch/bfm/main.php?nav=1-2&id=downloads)) and organize the directory into the following structure:  
Deep3DFaceRecon_pytorch  
│  
└─── checkpoints  
    │  
    └─── <model_name>  
        │  
        └─── epoch_20.pth  
	
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
