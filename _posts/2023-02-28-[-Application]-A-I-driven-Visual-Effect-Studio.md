### 3D Scene Reconstruction System for given End-User Videos.

*"Do you have any moment to remember forever? Just take a video. Our AI-powered solution brings your moment into a virtual 3D world permanently."*

Thanks to an experience participating in the NGR-CO3D challenge, we started developing an automatic AI-driven 3D scene reconstruction system for end-users. Here we describe the resulting prototype.

#### Inputs
Just take a video, and then upload it to us something like that:

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/car_seq.png" class="inline"/>
</p>

#### Outputs
Our solution automatically processes end-users videos, and then provides an experience where the end-users browse their scenes in 3D (click below): 

Order in novel-view RGB, Depth, and Surface-normal

One's favorite Car
[![test5](https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/test5_thumb.png)](https://drive.google.com/file/d/13ul2QUZQqrxA7fv08BoD_UDuJmsoGGc7/view?usp=share_link)
Clothes
[![test0](https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/test0_thumb.png)](https://drive.google.com/file/d/1lkLYecAC25GBwaWyiHZb_rHGOIXVyiEX/view?usp=share_link)
Object
[![test7](https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/test7_thumb.png)](https://drive.google.com/file/d/1DPaCDI4Zn2paZ7SyyUiCvRp3XPm2AvaY/view?usp=share_link)

After finishing train our model, we can extract a 3D mesh (via marching-cube algorithm):

[![test5_mesh](https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/test5_mesh_thumb.png)](https://drive.google.com/file/d/1biIsZi_UN2SNJxQMQh6tDJdYRmQSeGsg/view?usp=share_link)
[![chair_mesh](https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/chair_mesh_thumb.png)](https://drive.google.com/file/d/13iyRp7lueqUXM7Ww3XbrfbqovyH2gyFr/view?usp=share_link)
[![mic_mesh](https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/mic_thumb.png)](https://drive.google.com/file/d/1SwMl1DWMnUuWHq8yjyyITXe3QmTsLNLj/view?usp=share_link)
(To render these extracted meshes, we used blender's EEVEE rendering engin.)

#### System Building Blocks
Our system consists of major three stages i.e. 1) Automatic Dataset Building, 2) Training, and 3) Eval.
- Automatic Dataset Building<br>
-- Our solution splits an input video into N number of frames and then executes an off-the-shelf Structure-from-Motion (SfM) package (COLMAP in our case) to estimate camera-to-world pose parameters, i.e., camera intrinsic (focal length, principle point, and distortion) and extrinsic (camera rotation and translation). <br>
-- Miscellaneous information is also acquired by pre-trained vision networks, e.g., semantic segmentation mask, face parsing mask, etc. 
- Train<br>
-- Our Implicit Neural Network is trained for the train datasets built by the previous stage.
- Eval<br>
-- Given a trained implicit renderer, ray-sampler, and train dataset, we compose a virtual camera trajectory for novel-view synthesis off-line.

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/building_block.png" class="inline"/>
</p>


#### Keywords:
Neural Rendering, Neural Radiance Field (NeRF), Visual Effect Studio, 3D Reconstruction
