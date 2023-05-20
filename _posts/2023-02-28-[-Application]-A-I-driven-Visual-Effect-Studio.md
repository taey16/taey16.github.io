### 3D Scene Reconstruction System for given End-User Videos.

*"Do you have any moment to remember forever? Just take a video. Our AI-powered solution brings your moment into a virtual 3D world permanently."*

Thanks to an experience participating in the NGR-CO3D challenge, we started developing an automatic AI-driven 3D scene reconstruction system for end-users. Here we describe the resulting prototype.

#### Inputs
Just take a video, and then upload it to us somthing like that:

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/car_seq.png" class="inline"/>
</p>

#### Outputs
Our solution automatically process end-user's video, and then provide an experience that browse their scenes in 3D (click below): 

Outputs: novel-view RGB, Depth, and Surface-normal

One's favorite Car
[![test5](https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/test5_thumb.png)](https://drive.google.com/file/d/13ul2QUZQqrxA7fv08BoD_UDuJmsoGGc7/view?usp=share_link)
Clothes
[![test0](https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/test0_thumb.png)](https://drive.google.com/file/d/1lkLYecAC25GBwaWyiHZb_rHGOIXVyiEX/view?usp=share_link)
Object
[![test7](https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/test7_thumb.png)](https://drive.google.com/file/d/1DPaCDI4Zn2paZ7SyyUiCvRp3XPm2AvaY/view?usp=share_link)

After train our model, we can extract a 3D mesh with the trained model like these (via marching-cube algorithm):

[![test5_mesh](https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/test5_mesh_thumb.png)](https://drive.google.com/file/d/1biIsZi_UN2SNJxQMQh6tDJdYRmQSeGsg/view?usp=share_link)
[![chair_mesh](https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/chair_mesh_thumb.png)](https://drive.google.com/file/d/13iyRp7lueqUXM7Ww3XbrfbqovyH2gyFr/view?usp=share_link)
(To render these extracted meshes, we used blender's EEVEE rendering engin.)


#### Keywords:
Neural Rendering, Neural Radiance Field (NeRF), Visual Effect Studio, 3D Reconstruction
