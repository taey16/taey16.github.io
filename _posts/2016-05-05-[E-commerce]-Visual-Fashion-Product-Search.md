## Visual Clothes Search

### Introduction
We build a large-scale visual search system which finds similar product images given a fashion item. Defining similarity among arbitrary fashion-products is still remains a challenging problem, even there is no exact ground-truth. To resolve this problem, we define more than 90 fashion-related attributes, and combination of these attributes can represent thousands of unique fashion-styles. The fashion attributes are one of the ingredients to define semantic similarity among fashion product images. Given image and corresponding multi annotations, for the first time, we design such an multi-label classification as a vision-language sequence generation task. We employ our variant of the Inception-v3 network and the LSTM for dealing with vision-encoder and language-decoder, respectively. To build our system at scale, these fashion-attributes are again used to build an inverted indexing scheme. In addition to these fashion-attributes for semantic similarity, we extract colour and appearance features in a region-ofinterest (ROI) of a fashion item for visual similarity.


#### Keywords:
Multi-label Classification, Vision-Language, Sequence Generation, Fashion Search

Check out our paper for further details: <br>
[Visual Fashion-Product Search at SK Planet](https://github.com/taey16/taey16.github.io/blob/main/assets/papers/2016_fashion.pdf), CoRR abs/1609.07859, 2016
