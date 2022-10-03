# Cable-Segmentation
This work is part of my student research project at the University of Stuttgart IFF and Fraunhofer IPA, which is about 3D position determination of cables based on 3D point cloud segmentation in disassembly processes.
This repo is about routines for point cloud analysis using pointnet2 and stratified transformer.

# Install
* Environment: Ubuntu 20.04.4 LTS, PyTorch 1.8.1, CUDA 10.1 and Python 3.8.13
* Pytorch related libraries: torch_cluster 1.5.9, torch-sparse 0.6.12, torch_geometric 1.7.0, torch_points3d 1.3.0, torch_points_kernels 0.6.10, torch_scatter 2.0.8

# Datasets Preparation
The dataset consists of 20 scenes containing wires and cables at Fraunhofer IPA Vision Lab and test field. Please refer to the steps for S3DIS preprocessing in https://github.com/yanx27/Pointnet_Pointnet2_pytorch.

# PointNet++
* Training
```
python3 train_semseg.py --model pointnet2_sem_seg --test_area 1 2 --log_dir 12
```
* Test
```
python test_semseg.py --log_dir 12 --test_areas 1 2 --visual
```

# Stratified Transformer
* Training
```
python3 train.py --config config/stratified_transformer_train_val_test.yaml
```
* Test
```
python3 test.py --config config/stratified_transformer_train_val_test.yaml
```
* Trained Models (Cross-Validation) saved in path `trained_models/`.

# Cable Segmentation Routines
1. 3D point cloud acquisition (3D (XYZ) + color (RGB)).
2. export point cloud to `data_root` in format `.pcd`.
3. modify the `data_root` in `config/stratified_transformer_cable_segmentation.yaml` and run `python3 cable_segmentation.py --config config/stratified_transformer_cable_segmentation.yaml`.

