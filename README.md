# deep-fashion-retrieval
Simple image retrieval algorithm on [deep-fashion dataset](http://mmlab.ie.cuhk.edu.hk/projects/DeepFashion/AttributePrediction.html) with pytorch

![Capture](resources/Capture.PNG)

### Dependencies
- Python (Compatible with 2 and 3)
- [Pytorch](http://pytorch.org/)
- Torchvision
- PIL

[Anaconda](https://www.anaconda.com/download/) is recommended.

### Training
1. Download dataset from [DeepFashion: Attribute Prediction](http://mmlab.ie.cuhk.edu.hk/projects/DeepFashion/AttributePrediction.html)
2. Unzip all files and set `DATASET_BASE` in `config.py`
3. Run `train.py`

The models will be saved to `DATASET_BASE/models`.

Model: ResNet50 - (Linear 1024 to 512) - (Linear 512 to 20), the 512-dim vector is regarded as images' identical features.

Loss: CrossEntropyLoss + TripletMarginLoss * 0.5

### Generating feature databases
- Feature extraction
    - Set `DUMPED_MODEL` in `config.py` as trained model
    - Run `scripts/feature_extractor.py`
    
    The feature will be saved to `DATASET_BASE/features`
- Accelerating querying by clustering
    - Seems no need to do this... A naive query on the database with 139,709 features cost about 0.12 sec. 

### Query with a picture
- Run `retrieval.py img_path`, for example:

    `python retrieval.py img/Sheer_Pleated-Front_Blouse/img_00000005.jpg`.
    
### Time cost
- 2.854 sec for loading model, 
- 0.078 sec for loading feature database, 
- 0.519 sec for extracting feature of given image, 
- 0.122 sec for doing query(139,709 features)

### Environment
- Intel(R) Core(TM) i7-4790K CPU @ 4.00GHz with 32GB RAM
- GeForce GTX TITAN X with CUDA 7.5
- Ubuntu 14.04
- Pytorch 0.2.0_4

### Future works
- Add web support
- Add more models and fuse them
- Consider color when calculating similarity
