## Installation

#### Environment

You can directly use the conda environment for [Stable Diffusion](https://github.com/CompVis/stable-diffusion) or [DDNM](https://github.com/wyhuai/DDNM). You can find configuration instructions in their GitHub links.

#### Pre-trained model

- human face diffusion model provided by [Google drive](https://drive.google.com/drive/folders/1cSCTaBtnL7OIKXT4SVME88Vtk4uDd_u4)
- The original checkpoint is from [SDEdit](https://github.com/ermongroup/SDEdit), which has been expired.
  - place the model in this directory `./exp/logs/celeba/celeba_hq.ckpt`
- unconditional [guided diffusion model](https://github.com/openai/guided-diffusion)
  - place the model in this directory `./exp/logs/imagenet/256x256_diffusion_uncond.pt`
- [CLIP](https://github.com/openai/CLIP)
  - The model will automatically download.
- [face parsing model](https://drive.google.com/open?id=154JgKpzCPW82qINcVieuPH3fZ2e0P812)
  - place the model in this directory `./functions/face_parsing/79999_iter.pth`
- [sketch model](https://drive.google.com/drive/folders/1Srf-WYUixK0wiUddc9y3pNKHHno5PN6R)
  - place the model in this directory `./functions/anime2sketch/netG.pth`

## Quick Start

Just run `bash run.sh`, you will get the results.

The explanation of useful options:

- `-i` is the folder name of the results.
- `-s` is the sampling method with different conditions, we support `	clip_ddim | parse_ddim | sketch_ddim | clip_ddim_i | parse_ddim_i |    `
- `--doc` for human face model, choose `celeba_hq`; for ImageNet model, choose `imagenet`
- `--timesteps` the number of sampling times, we use 100 as default setting.
- `--seed` you can choose your seeds to make results different!
  - `--model_type` for human face model, choose `"face"`; for ImageNet model, choose `"imagenet"`
- `--prompt` is the text prompt for CLIP condition control
- `--batch_size` control the number of generated images
- `--ref_path` is the path of reference image

Examples:
294.jpg can be replaced by any other images in the image folder. The prompts can also be changed. 
For FreeDoM method, please using the following commands (The hyperparameters are copied from FreeDoM's github):
'''python main.py -i clip_face -s clip_ddim --doc celeba_hq --timesteps 100 --seed 1234 --model_type "face" --prompt "a black asian" --batch_size 1'''

'''python main.py -i seg_face -s parse_ddim --doc celeba_hq --timesteps 100 --rho_scale 0.2 --seed 1234 --stop 200 --ref_path ./images/294.jpg --batch_size 1'''

'''python main.py -i sketch_face -s sketch_ddim --doc celeba_hq --timesteps 100 --rho_scale 20.0 --seed 1234 --stop 100 --ref_path ./images/294.jpg --batch_size 1'''

'''python main.py -i clip_imagenet -s clip_ddim --doc imagenet --timesteps 100 --seed 1234 --model_type "imagenet" --prompt "an elepant on the roof" --batch_size 1'''


For the improved methods (ours), please using the following commands:
'''python main.py -i seg_face_i -s parse_ddim_i --doc celeba_hq --timesteps 100 --rho_scale 2 --seed 1234 --stop 200 --ref_path ./images/294.jpg --batch_size 1'''

'''python main.py -i sketch_face_i -s sketch_ddim_i --doc celeba_hq --timesteps 100 --rho_scale 0.002 --seed 1234 --stop 100 --ref_path ./images/294.jpg --batch_size 1'''

'''python main.py -i clip_face_i -s clip_ddim_i --doc celeba_hq --rho_scale 0.001 --timesteps 100 --seed 1234 --model_type "face" --prompt "a black asian" --batch_size 1'''

'''python main.py -i clip_imagenet_i -s clip_ddim_i --doc imagenet --timesteps 100 --seed 1234 --model_type "imagenet" --prompt "an elepant on the roof" --batch_size 1 --rho_scale 2'''




