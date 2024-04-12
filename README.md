# MD-NeRF
MD-NeRF is a framework that guarantees the consistency of 3D geometry and appearance from the principle of defocus blur formation. MD-NeRF proposes the Defocus Modelling Approach (DMA), which is a new method to simulate an defocus scene When the view is fixed, DMA considers that the pixels are rendered by multiple rays emitted from the same light source. In addition, DM-NeRF proposes a new Multi-view Panning Algorithm (MPA), where MPA simulates the motion of the light source by applying small pans to the center of the camera in different views to produce a blurring effect similar to that found in real photography. MD-NeRF enhances the capture of complex scene details with the combination of DMA and MPA including texture and detail information. Our experimental results validate that MD-NeRF produces significant improvements in peak Signal-to-Noise Ratio (PSNR), Structural Similarity Indexing Measure (SSIM), and Learned Perceptual Image Patch Similarity (LPIPS).
## Quick Start
### 1.Install environment
```
git clone https://github.com/luckhui0505/MP-NeRF.git
cd MP-NeRF
pip install -r requirements.txt
```
### 2. Download dataset
There are total of 31 scenes used in the paper. We mainly focus on camera motion blur and defocus blur, so we use 5 synthetic scenes and 10 real world scenes for each blur type. We also include one case of object motion blur. You can download all the data in [here](https://hkustconnect-my.sharepoint.com/personal/lmaag_connect_ust_hk/_layouts/15/onedrive.aspx?id=%2Fpersonal%2Flmaag%5Fconnect%5Fust%5Fhk%2FDocuments%2Fshare%2FCVPR2022%2Fdeblurnerf%5Fdataset&ga=1).
### 3. Setting parameters
Changing the data path and log path in the configs/demo_blurfactory.txt
### 4. Execute
python3 run_nerf.py --config configs/demo_blurfactory.txt
## Method Overview
![image](https://github.com/luckhui0505/MD-NeRF/blob/master/framework.jpg) 
Overall architecture of MD-NeRF. Structure (a) presents the algorithm flow of the Multi-view Panning Algorithm (MPA), generating the translation of the camera center. Here, I denotes the batch of image information, N represents the sparsity of the blur kernel, and D denotes the dimensionality of the ray vectors, typically 2. Structure (b) illustrates the loss function, which is derived from the color differences at N sparse positions. Structure (c) depicts the Defocus Modeling Approach (DMA), which yields the directional offsets of N rays.
## Comparison of Experimental Results
![image](https://github.com/luckhui0505/MD-NeRF/blob/master/result.png) 
Quantitative results. We bolded the best result in the metric.
## Some Notes
### GPU Memory
We train our model on a RTX3090 GPU with 24GB GPU memory. If you have less memory, setting N_rand to a smaller value, or use multiple GPUs.
### Multiple GPUs
you can simply set <mark> num_gpu = <num_gpu> <mark> to use multiple gpus. It is implemented using <mark> torch.nn.DataParallel <mark>. We've optimized the code to reduce the data transfering in each iteration, but it may still suffer from low GPU usable if you use too much GPU.
## Acknowledge
This source code is derived from the famous pytorch reimplementation of NeRF, nerf-pytorch, Deblur-NeRF. We appreciate the effort of the contributor to that repository.


