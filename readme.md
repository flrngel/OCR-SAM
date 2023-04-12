![]()

# OCR-SAM

## 🐇 Introduction 🐙
This repository is mainly to combine the TextDetector, TextRecgonizer，[Segment Anything](https://github.com/facebookresearch/segment-anything) and other Adavanced Tech to develop some **OCR-related Application Demo**. And we provide the **[WebUI by gradio](#run-webui)** and **Colab** to make user to have better interaction.  

*Note: We will continue to update and maintain this repo, and develop more OCR-related advanced applications demo to the community. **Welcome anyones to join who have the idea and want to contribute to our repo**.*

## 📅 Updates 👀
- **2023.04.12**: Repository Release
- **2023.04.12**: Supported the [Inpainting](#🏃🏻‍♂️-run-demo-🏊‍♂️) combined with DBNet++, SAM and ControlNet.
- **2023.04.11**: Supported the [Erasing](#🏃🏻‍♂️-run-demo-🏊‍♂️) combined with DBNet++, SAM and Latent-Diffusion / Stable-Diffusion.

## 📸 Demo Zoo 🔥

This project includes:
- [x] [SAM for Text](#🏃🏻‍♂️-run-demo-🏊‍♂️): DBNet++ + SAM
![](imgs/sam_vis.png)
- [x] [Erasing](#🏃🏻‍♂️-run-demo-🏊‍♂️): DBNet++ + SAM + Latent-Diffusion / Stable Diffusion 
![](imgs/erase_vis.png)
- [x] [Inpainting](#🏃🏻‍♂️-run-demo-🏊‍♂️)


## 🚧 Installation 🛠️
### Prerequisites

- Linux | Windows
- Python 3.7
- Pytorch 1.6 or higher
- CUDA 11.3

### Environment Setup
Clone this repo:
```
git clone https://github.com/yeungchenwa/OCR-SAM.git
```
**Step 0**: Create a conda environment and activate it.
```
conda create --n ocr-sam python=3.8 -y
conda activate ocr-sam
```
**Step 1**: Install related version Pytorch following [here](https://pytorch.org/get-started/previous-versions/).

**Step 2**: Install the mmengine, mmcv, mmdet, mmcls, mmocr.
```
pip install -U openmim
mim install mmengine
mim install 'mmcv==2.0.0rc4'
mim install 'mmdet==3.0.0rc5'
mim install 'mmcls==1.0.0rc5'

# Install the mmocr from source
cd OCR-SAM
pip install -v -e .
```

**Step 3**: Prepare for the diffusers and latent-diffusion.
```
# Install the diffusers
pip install diffusers

# Install the pytorch_lightning for ldm
conda install pytorch-lightning -c conda-forge
```

## Model checkpoints

Download the checkpints to the related path (If you've done, ignore the following):
```
# mmocr ckpt
wget -O mmocr_dev/checkpoints/db_swin_mix_pretrain.pth 
wget -O mmocr_dev/checkpoints/abinet_20e_st-an_mj_20221005_012617-ead8c139.pth https://download.openmmlab.com/mmocr/textrecog/abinet/abinet_20e_st-an_mj/abinet_20e_st-an_mj_20221005_012617-ead8c139.pth

# sam ckpt, more details: https://github.com/facebookresearch/segment-anything#model-checkpoints
wget -O segment-anything-main/checkpoints/sam_vit_h_4b8939.pth https://dl.fbaipublicfiles.com/segment_anything/sam_vit_h_4b8939.pth

# ldm ckpt
wget -O latent_diffusion/checkpoints/last.ckpt https://heibox.uni-heidelberg.de/f/4d9ac7ea40c64582b7c9/?dl=1
```

## 🏃🏻‍♂️ Run Demo 🏊‍♂️

### **SAM for Text** 🧐

Run the following script:
```
python mmocr_sam.py \
    --inputs /YOUR/INPUT/IMG_PATH \ 
    --outdir /YOUR/OUTPUT_DIR \ 
    --device cuda \ 
```
- `--inputs`: the path to your input image. 
- `--outdir`: the dir to your output. 
- `--device`: the device used for inference. 

### **Erasing** 🤓

More implementation **details** are listed [here](docs/erase_details.md)

Run the following script:
```
python mmocr_sam_erase.py \ 
    --inputs /YOUR/INPUT/IMG_PATH \ 
    --outdir /YOUR/OUTPUT_DIR \ 
    --device cuda \ 
    --use_sam True \ 
    --dilate_iteration 2 \ 
    --diffusion_model \ 
    --sd_ckpt None \ 
    --img_size (512, 512) \ 
```
- `--inputs `: the path to your input image.
- `--outdir`: the dir to your output. 
- `--device`: the device used for inference. 
- `--use_sam`: whether to use sam for segment.
- `--dilate_iteration`: iter to dilate the SAM's mask.
- `--diffusion_model`: choose 'latent-diffusion' or 'stable-diffusion'.
- `--sd_ckpt`: path to the checkpoints of stable-diffusion.
- `--img_size`: image size of latent-diffusion.


### **Inpainting** 🥸
More implementation **details** are listed [here](docs/inpainting_details.md)

Run the following script:
```
python mmocr_sam_inpainting.py \
    --inputs /YOUR/INPUT/IMG_PATH \ 
    --outdir /YOUR/OUTPUT_DIR \ 
    --device cuda \ 
```
- `--inputs`: 
- `--outdir`: 
- `--device`: 

### **Run WebUI**
This repo also provides the WebUI(decided by gradio), running the following:
```
python mmocr_sam_inpainting_aoo.py
```

## 💗 Acknowledgement
- [segment-anything](https://github.com/facebookresearch/segment-anything)
- [latent-diffusion](https://github.com/CompVis/latent-diffusion)
- [mmocr](https://github.com/open-mmlab/mmocr)