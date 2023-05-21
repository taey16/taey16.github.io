### Manipulating Latent vectors

In this project, we trained the StyleGAN generator and manipulated the latent space of the generator.

#### Interpolating *face identities* and corresponding *Non-Adversarial Domain Adaptation (NADA)*
We trained our own generator, i.e. a variant of StyleGAN's mapper and synthesizer, and then interpolates randomly sampled latent vectors. In addition, we applied the StyleGAN-NADA approach where driving prompts are *"character"*, *"caricature"*, *characture*, *"dc comics"*, *"marvel comics"*, and *"disney 3D"*.

[![test0](https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/stylegan/identity_stylegan_nada_thumb.png)](https://drive.google.com/file/d/1OjoZBTvdC-LYyKCw8IBT60k4ZKAIv2Uc/view?usp=sharing)
(click above and make sure full-screen mode)

#### Various Face-related attributes Manipulation
Steerable attributes we trained are geometry, lighting, age, gender, race, glasses, hat, makeup, facial expression, etc. Here we showcase various face-related attributes manipulation from our trained generator and manipulator.

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

- ,and so on ...

#### Face-Attribute Dataset Generation
The latent manipulation technique can be extended to **generate a face-attributes dataset**. For example, we can generate various face images with all wearing glasses and closing their eyes. Another example is results of generating male faces. (Red rectangles denote mis-generated images.

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/stylegan/glasses_closed_eyes.png">
<br>
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/stylegan/male_only.png">
</p>

#### Keywords:
Generative Adverserial Networks (GANs), Dataset Generation, Face Editing, Latent Manipulation, StyleGAN, StyleFlow, StyleCLIP, StyleGAN-NADA
