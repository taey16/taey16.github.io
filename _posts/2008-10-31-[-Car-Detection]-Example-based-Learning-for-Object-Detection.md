## Example based Learning for Object Detection in Images

### Introduction
In this paper, we describe a general learning architecture for object detection especially car detection. In order to build such a system, we first perform dimension reduction
for each example by using maximizing mutual information criterion. The algorithm directly selects projection basis from examples which can minimize Bayes error. This algorithm is named as Maximizing Mutual Information(MMI) method. Given projection basis, all of examples are projected onto these basis and then trained by Support Vector Machine(SVM). This approach can be applied to any object with distinguishable patterns. In test process, we find objects in a image by using our exhaustive search algorithm which is called a Scale based Classifier Activation Map(SCAM). We applied our detection scheme into UIUC car/non-car database. In this experiment we detect 181 cars in 170 images with 200 cars. This result is competitive
comparing to others.


#### Keywords:
Feature Extraction, Dimensionalrity Reduction, Mutual Information Maximization, Object Detection

To get further details, check out our paper: <br>
<a href="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/papers/2008_example_based_learning_for_object_detection.pdf">Example based Learning for Object Detection in Images</a>, VNBA in conjunction with ACM Multimedia, 2009
