## Visual Clothes Search

### Introduction
We build a large-scale visual search system that finds similar clothe-images given a fashion item. Defining similarity among arbitrary fashion-products is remains a challenging problem, even there is no exact ground truth. To address this, we define more than 90 fashion-related attributes, and a combination of these attributes can represent thousands of unique fashion styles. Fashion attributes are one of the ingredients to define semantic similarity among fashion product images. Given an image and corresponding multi annotations, for the first time, we design such a multi-label classification as a vision-language sequence generation task. We employ our variant of the Inception-v3 network and the LSTM which is responsible for the vision encoder and language decoder, respectively. To build our system at scale, these fashion attributes are again used to build an inverted indexing scheme. In addition to these fashion attributes for semantic similarity, we extract color and appearance features in a region of interest (ROI) of a fashion item for visual similarity.

### Quantative Results

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/fashion/fashion_result0.png">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/fashion/fashion_result1.png">
</p>

Much more examples including qualitative results are described in our paper.


#### Keywords:
Multi-label Classification, Vision-Encoder/Language-Decoder, Sequence (Sentence) Generation, Inception Network, LSTM, Fashion Search

Check out our paper for further details: <br>
<a href="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/papers/2016_fashion.pdf">Visual Fashion-Product Search at SK Planet</a>, CoRR abs/1609.07859, 2016
