### Manipulating Latent vectors

In this project, we trained StyleGAN generator and manipulated the latent space of the generator.

#### Interplolating *face identities* and corresponding *Non Adverserial Domain Adeptation (NADA)*
We trained our own generator, i.e. a variant of StyleGAN's mapper and synthesizer, and then interpolates randomly sampled latent vectors. In addition, we applied StyleGAN-NADA apporach whose driving prompts are *"character"*, *"caricature"*, *characture*, *"dc comics"*, *"marvel comics"*, and *"disney 3D"*.

[![test0](https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/stylegan/identity_stylegan_nada_thumb.png)](https://drive.google.com/file/d/1OjoZBTvdC-LYyKCw8IBT60k4ZKAIv2Uc/view?usp=sharing)
(click above and make sure full-screen mode)

#### Various Face-related attributes Manipulation
Here we showcase various face-related attributes manipulation from our trained generator.
- Geometry (Yaw, Pitch)

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/stylegan/yaw.gif" width="512" height="256">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/stylegan/pitch.gif" width="512" height="256">
</p>

- Re-lighting (Light location, strength)

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/stylegan/lightlocation.gif" width="512" height="256">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/stylegan/lightstrength.gif" width="512" height="256">
</p>

- Aging

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/stylegan/age.gif" width="512" height="256">
</p>

- Eye Closing 

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/stylegan/closed_eyes.gif" width="512" height="256">
</p>

- Beard

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/stylegan/beard.gif" width="512" height="256">
</p>

- Expressions

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/stylegan/smile.gif" width="512" height="256">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/stylegan/angry.gif" width="512" height="256">
</p>

- Makeup

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/stylegan/makeup.png" width="512" height="256">
</p>

#### Face-Attribute Dataset Generation
The latent manipulation technique can be extended to generate **face-attributes dataset**. For example, we can generate various face images with all wearing glasses and closing their eyes. Other example is results of generating male's faces. (Red rectangles denote mis-generated images.

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/stylegan/glasses_closed_eyes.png">
<br>
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/stylegan/male_only.png">
</p>
