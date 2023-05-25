<!--
How to use LaTeX in Markdown
https://www.fabriziomusacchio.com/blog/2021-08-10-How_to_use_LaTeX_in_Markdown/
<script
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"
  type="text/javascript">
</script>
-->
<script type="text/javascript"
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS_CHTML">
</script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [['$','$'], ['\\(','\\)']],
      processEscapes: true},
      jax: ["input/TeX","input/MathML","input/AsciiMath","output/CommonHTML"],
      extensions: ["tex2jax.js","mml2jax.js","asciimath2jax.js","MathMenu.js","MathZoom.js","AssistiveMML.js", "[Contrib]/a11y/accessibility-menu.js"],
      TeX: {
      extensions: ["AMSmath.js","AMSsymbols.js","noErrors.js","noUndefined.js"],
      equationNumbers: {
      autoNumber: "AMS"
      }
    }
  });
</script>

#### NeR-NeRF: 3D Head Swap for Fully Controllable 3D Human Generation (Submitted)

#### Introduction
Modeling 3D face and body research are essential components to realize a controllable 3D virtual avatar. However, there is no attempt to bridge the gap between them. Specifically, The domain of 3D body modeling focuses on controlling the skeleton of our body but is limited to controlling (representing) facial details, e.g., the fidelity of faces, facial expressions, etc. The objective of this paper is to integrate two separate research domains - constructing the controllable human head and body models - to create a 3D human model that is fully controllable.

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/NeR_NeRF/NeR_NeRF_results.png">
</p>
Results of our apporach.

*Note that this work is under review. Feel free to email me for details*

#### Keywords:
Neural Radiance Fields (NeRF), Generative Radiance Fields, Deformable Radiance Fields, 3D-aware GANs, 3D Inversion, Controllable Full-Body Avatar Generation
