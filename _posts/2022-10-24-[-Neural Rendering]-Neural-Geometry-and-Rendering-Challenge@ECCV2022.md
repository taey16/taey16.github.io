### Neural Geometry and Rendering (NGR): Advances and the Common Objects in 3D (CO3D) Challenge @ECCV2022

We took part in the NGR-CO3D challenge hosted by ECCV2022. As a result, we placed the **winning entry** for the *"manyview"*-reconstruction track. 

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/CO3D_Multiview_centificate.png" class="inline"/>
</p>

#### Task Definition
Given a sequence of RGB images, ROI-masks and camera-poses, one's algorithm outputs appearance (RGB), depth-map (D), and ROI-mask (A) for a given test camera poses for 88 video sequences in total.

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/task_def.png" class="inline"/>
</p>

#### Our Apporach
We employed a simple ensemble representation of an object with the NeRF and TensoRF. To prevent overfitting phenomena, per-sample-entropy, L1-sparsity, and total-variation loss were applied. 

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/approach.png" class="inline"/>
</p>


#### Quantitative Results
Until the evaluation server shutdown, we slightly but granularly imporved the performance of our method.

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/quantitative_result.png" class="inline"/>
</p>
