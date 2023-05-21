### Masked Face Recognition (MFR) Challenge & Workshop, ICCV2021

We entered the MFR@ICCV2021 challenge and achieved **2nd place** for the *Main task of WebFace260M track*.<br>
Ref.: <a href="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/papers/2021_MFR_WebFace260M_track_report.pdf">Masked Face Recognition Challenge: The WebFace260M Track Report</a>, ICCV, 2021

#### Task Definition
Given the train-dataset, i.e., WebFace260M, one's algorithm has to learn a good representation of face images wearing a mask as well as non-masked. An uploaded model is evaluated on the test set consisting of more than 3.3 billion pairs of a combination of masked and non-masked face images. The evaluation metric is TPR@FPR1e-5.

#### Apporoach

##### Large-Scale Multi-node/Multi-gpu Distributed Training
The WebFace260M dataset is composed of more than 2 million classes, and 0.26 billion face images. To train on this dataset, it is infeasible to train with a plain cross-entropy loss, due to its a huge amount of classes. To address this, we employed Model-Parallelism for the classification head, and Multi-Node, Multi-GPU Distributed Data Parallelism for the feature-extraction network, respectively (See bolow). 

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/MFR_ICCV2021/ddp_mp.png" class="inline"/>
</p>

For further speed-up and the highest peak memory reduction during training, the micro-batching, checkpoing, automatic mixed precision, and ZeRO optimizer, etc. were utilized, if necessary.

##### Feature Distillation
To improve face recognition performance, we adopted the feature distillation method. Specifically, we first trained a teacher network (our ResNet1200 network) in advance. and conduct to train our student network with a convex combination of the supervised cross entropy loss and unsupervised teacher distillation loss. Performaces of train-scratch (denoted as red)  and train-distill (denoted as blue) are shown below.

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/MFR_ICCV2021/distill_vs_scratch.png" class="inline"/>
</p>

#### Results
Finally, we achieved **2nd place** for the *Main task of the WebFace260M track*. <br>
Ref.: https://competitions.codalab.org/competitions/32478#results

#### Keywords:
(Masked) Face Recognition, Distillation, ArcFace, CosFace, Multi-Node Distributed Training

#### Check out for furthers
Tech Note: <a href="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/MFR_ICCV2021/MFR_ICCV2021_Report_ethan.pdf">Technical Details of our submissions of MFR-ICCV2021 Challenge, WebFace260M Track</a> <br>
Slide: <a href="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/MFR_ICCV2021/MFR_ICCV2021_Slide_ethan.pdf">InvitedTalk_slide_workshop</a>, MFR Challenge & Workshop, ICCV, 2021
