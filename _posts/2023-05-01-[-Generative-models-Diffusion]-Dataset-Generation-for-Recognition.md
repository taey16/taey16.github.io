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

### Identity-Preserving Face-Recognition Dataset Generation via Conditional Diffusion Probabilistic Models (Ongoing)

#### Introduction
As far as all of we know, discriminative models always required large amount of labeled data in general. The deep learning success in previous decay is also based on labor-intensive currated annotations and crawled images for training. Nowadays, there exist few research works to overcoming a need for composing a training dataset manually, but their success is limited. We got started to ice-breaking such a limitation. Our hypothesis is that if we can generate a sample from $$ p_{\theta}(x) $$ without error, then performance of a trained discriminative model on synthetically generated samples meets that of the counterpart model trained on a real data. By referring current notable improvement to mimic sampling on true distribution with Diffusion Probabilistic Model (DPM), we adopted the DPM to generate training dataset for recognition. 

#### Latent Variable Models (LVMs), and Diffusion Probabilistic Models (DPMs)
Inspired by the diffusion (Brownian motion) as a natural phenomenon in themodynamics, the diffusion process can be modelled as finding a posterior as the time-introducing LVMs, 

\begin{align}
\label{diffusionforward}
q(x_{T}, x_{t-1}, \cdots, x_{1}, x_{0}).
\end{align}

The diffusion process is a special case of the Probablistic Graphical Model (PGM), where distribution of the latent variable is known, such that 

\begin{align}
\label{samplelatent}
x_T \sim \mathcal{N}(\mathbf{0}, \mathbf{I}).
\end{align}

Note that distributions of $$ x_0, x_T $$ are known in this case, we can easily compute a sample in the (forward) diffusion process at time $$ t $$ such that:

\begin{align}
\label{computediffusionforward}
    q(x_{t+1}|x_{T}, x_0) = \sqrt{\bar{\alpha}_t} x_0 + \sqrt{1 - \bar{\alpha}_t}x_T,
\end{align}

where $$ \alpha_t $$ is a constant at $$ t $$, induced by a beta-scheduler (*"linear scheduler"* as a common choice). Inherited by the PGM, the reverse diffusion process (the generation process parameterized by $$ \theta $$), which finds a likelihood,

$$ q_{\theta}(x_0|x_1, x_2, \cdots, x_T) $$ 

can be tractable. To solve this reverse process, Denoising Diffusion Probabilistic Model (DDPM) proposes the $$ q_{\theta} $$ as a $$ \epsilon $$-predictor so that a procedure in training is to be dramatically simple (under the markov property):

$$
\begin{equation}
\label{ddpmobjectives}
L_{\text{simple}} := 
    E_{t, x_0, x_T} \Big [ \|| 
        x_T - \epsilon_{\theta}(
            \underbrace{\sqrt{\bar{\alpha}_t} x_0 + \sqrt{1 - \bar{\alpha}_t}x_T}_{\text{The output of the (forward) diffusion process}}, t
        ) 
    \||^2 \Big ].
\end{equation}
$$

In Eq.[$$\ref{ddpmobjectives} $$], an input to the $\epsilon_{\theta}$ is already acquired in computing the diffusion process (as Eq.[$$ \ref{computediffusionforward} $$]).
<!--
In Eq.($$\ref{ddpm} $$), $$ x_0, t $$ are a randomly selected sample and time, respectively. $$ x_T $$ was sampled in the diffusion process in advance so that we can compute an input to our $\epsilon_{\theta}$ straightforwardly.
-->

#### Sampling $$ q_{\theta}(x_0|x_1, \cdots, x_T) \approx p(x_0) $$
First, we sample a latent variable $$ x_T $$ as Eq.[$$ \ref{samplelatent} $$]. To mimic $$ p(x_0) $$, Authors of DDPM derives followings:

$$
\begin{equation} \label{ddpmsample}
q(x_{t-1}|x_t, x_0) = 
    \underbrace{
        \frac{\sqrt{\bar{\alpha}_{t-1} \beta_t}}{1 - \bar{\alpha}_t} x_0 + \frac{\sqrt{\alpha_t} (1 - \bar{\alpha}_{t-1} ) } { 1 - \bar{\alpha}_t } x_t
    }_{\mu_t(x_t, x_0)} + 
    \underbrace{
        \frac{1 - \bar{\alpha}_{t-1}}{1 - \bar{\alpha}_t} \beta_t \mathcal{N}(0, \mathbf{I})
    }_{\Sigma_t},
\end{equation}
$$

which means that if we know $$ x_0 $$, computing $$ x_{t-1} $$ of Eq.[$$\ref{ddpmsample}$$] is tractable via reparameterization trick. The authors of DDMP describe to approximate $$ x_0 $$ such that:

<p align="center">
$$
\begin{equation} \label{approxx0}
    x_0 \approx \frac{x_t - \sqrt{1 - \bar{\alpha}_t}\epsilon_{\theta}(x_t)}{\sqrt{\bar{\alpha}_t}},
\end{equation}
$$
</p>
which regared to as the *"input-output reversed"* equation of Eq.[$$\ref{computediffusionforward} $$], i.e. $$ q_{\theta}(x_0 | x_t, x_T) $$. Here, $$ x_T  $$ is the output of our $$ \epsilon $$-predictor, $$ x_T = \epsilon_{\theta}(x_t) $$, where the $$ x_t $$ is an output for the previous sampling process. 


#### Visualizing intermediate outputs step by step

##### Forward diffusion process Eq.[$$\ref{computediffusionforward}$$].
As described above, this forward process can be computed straightforwardly, since we know distribution of our observation, $$ p(x_0) $$, and latent, $$ p(x_T) $$. The right, and left-most images are $$ x_0 $$, and $$ x_T $$, respectively. Remainings are $$ x_t $$.

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/diffusion/qt.png">
</p>

##### Estimating $$ x_0 $$ in Eq.[$$\ref{approxx0}$$].
To estimate the $$ x_0 $$, one needs to sample $$ x_{t} $$ which is an output of the previous reverse process in actual sampling (generation) process. However, we can make use of a result of Eq.[$$\ref{computediffusionforward}$$] computed in training for just visualization.

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/diffusion/x0.png">
</p>

##### Progressive estimatation of Eq.[$$\ref{ddpmsample}$$].
Following examples are results of the Eq.[$$\ref{ddpmsample}$$]. Samples drawn from the normal distribution (left-most images) are progressively goes to corresponding samples as if they are drawn from true distribution (right-most images).

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/diffusion/progressive_actually_qt.png">
</p>

#### Conditional DPMs


#### Keywords:
Diffusion Probabilistic Models (DPMs), (conditional) Latent Diffusion Models (cLDMs), Classifier-Free Guidance (CFG), Dataset Generation
