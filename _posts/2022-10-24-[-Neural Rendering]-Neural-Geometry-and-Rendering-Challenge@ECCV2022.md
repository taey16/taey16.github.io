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

#### Qualitative Results
Here are showcases of our novel-view synthesis (order in predicted RGB, Depth, and ROI).

[![bench](https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/bench_thumb.png)](https://drive.google.com/file/d/1XBORqxUR90m33DCLfnBTW8hJNXW4W_Z4/view?usp=share_link)
[![teddybear](https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/teddybear_thumb.png)](https://drive.google.com/file/d/16a68fUKk4bSAdcjlUbs1oX3r3kiWbFnZ/view?usp=share_link)
[![toytrain](https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/toytrain_thumb.png)](https://drive.google.com/file/d/1r_AKOPpFJJPcOle33hHel8DsoxDbHIBX/view?usp=share_link)


#### Keywords:
Neural Rendering, Neural Radiance Field (NeRF), Tensorial Radiance Field (TensoRF), Implicit Volume Rendering, Novel-View Synthesis


Check out our presentation slides: 
<a href="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NGR_CO3D_ECCV2022/NGR_CO3D_ECCV2022.pdf">InvitedTalk_winning_entry_manyview</a>, NGR-CO3D@ECCV, 2022
