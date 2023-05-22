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

#### Introduction
As far as we know, discriminative models always require a large amount of labeled data in general. The deep learning success in previous decay is also based on labor-intensive curated annotations and crawled images for training. Nowadays, there exist few research works to overcome the need for composing a training dataset manually, but their success is limited. We got started ice-breaking such a limitation. We hypothesize that if we can generate a sample from $$ p_{\theta}(x) $$ without error, then a performance of a trained discriminative model on synthetically generated samples meets that of the counterpart model trained on real data. By referring to the current notable improvement to mimic sampling on true distribution with Diffusion Probabilistic Model (DPM), we adopted the DPM to generate a training dataset for recognition. 

#### Latent Variable Models (LVMs), and Diffusion Probabilistic Models (DPMs)
Inspired by the diffusion (Brownian motion) as a natural phenomenon in thermodynamics, the diffusion process can be modeled as finding a posterior as the time-introducing LVMs, 

\begin{align}
\label{diffusionforward}
q(x_{T}, x_{t-1}, \cdots, x_{1}, x_{0}).
\end{align}

The diffusion process is a special case of the Probabilistic Graphical Model (PGM), where the distribution of the latent variable is known, such that 

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

can be tractable. To solve this reverse process, Denoising Diffusion Probabilistic Model (DDPM) proposes the $$ q_{\theta} $$ as a $$ \epsilon $$-predictor so that the procedure in training is to be dramatically simple (under the Markov property):

$$
\begin{equation}
\label{ddpmobjectives}
\mathcal{L}_{\text{simple}} := 
    \mathbb{E}_{t, x_0, x_T} \Big [ \|
        x_T - \epsilon_{\theta}(
            \underbrace{\sqrt{\bar{\alpha}_t} x_0 + \sqrt{1 - \bar{\alpha}_t}x_T}_{\text{The output of the (forward) diffusion process}}, t
        ) 
    \|^2 \Big ].
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

which means that if we know $$ x_0 $$, computing $$ x_{t-1} $$ of Eq.[$$\ref{ddpmsample}$$] is tractable via reparameterization trick. The authors of DDMP describe approximating $$ x_0 $$ such that:

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
As described above, this forward process can be computed straightforwardly, since we know the distribution of our observation, $$ p(x_0) $$, and latent, $$ p(x_T) $$. The right and left-most images are $$ x_0 $$, and $$ x_T $$, respectively. The remainings are $$ x_t $$.

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/diffusion/qt.png">
</p>

##### Estimating $$ x_0 $$ in Eq.[$$\ref{approxx0}$$].
To estimate the $$ x_0 $$, one needs to sample $$ x_{t} $$ which is an output of the previous reverse process in the actual sampling (generation) process. However, we can make use of a result of Eq.[$$\ref{computediffusionforward}$$] computed in training for just visualization.

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/diffusion/x0.png">
</p>

##### Progressive estimatation of Eq.[$$\ref{ddpmsample}$$].
The following examples are results of Eq.[$$\ref{ddpmsample}$$]. Samples drawn from the normal distribution (left-most images) progressively go to corresponding samples as if they are drawn from the true distribution (right-most images).

<p align="center">
<img src="https://raw.githubusercontent.com/taey16/taey16.github.io/main/assets/diffusion/progressive_actually_qt.png">
</p>

#### Conditional DPM
The conditional DPM is a variant of the diffusion process conditioned on the class label, segmentation mask, CLIP/LAION embeddings, etc. We denote these various conditions as a random variable, $$ c $$ (for simplicity), where the true distribution of the random variable, $$ c $$, is known as a part of the observation. Then, previously mentioned Eq.[$$\ref{diffusionforward}$$] changes the form such that

\begin{align}
\label{cdiffusionforward}
q(x_{T}, x_{t-1}|c, \cdots, x_{1}|c, x_{0}|c).
\end{align}

Note the known latent variable, $$ x_{T} $$, is unchanged under the motivation of diffusion in thermodynamics. Then, final objectives (Eq.[$$\ref{ddpmobjectives}$$]) is changed

$$
\begin{equation}
\label{cddpmobjectives}
    \mathcal{L}_{\text{simple}} := 
    \mathbb{E}_{t, x_0|c, x_T} \Big [ \|
        x_T - \epsilon_{\theta}(
            \sqrt{\bar{\alpha}_t} x_0 + \sqrt{1 - \bar{\alpha}_t}x_T, c, t
        ) 
    \|^2 \Big ].
\end{equation}
$$

To implement the term, 
$$
    \epsilon_{\theta}(x_t, c) := \epsilon_{\theta}(\sqrt{\bar{\alpha}_t} x_0 + \sqrt{1 - \bar{\alpha}_t}x_T, c, t)
$$, 
the authors of Stable-Diffusion introduce QKV spatial attention mechanism in their $$\epsilon$$-predictor for conditioning. Another approach is that a diffusion score computed by the $$\epsilon$$-predictor is modified as the amount of gradient of a classifier, $$ p_{\phi}(c|x_t) $$, additionally introduced (i.e., Classifier-Guidance Diffusion).

$$
\begin{equation}
\label{classifierguid}
    \hat{\epsilon}_{\theta}(x_t, c) := \underbrace{\epsilon_{\theta}(x_t)}_{\text{unconditional part}} - \sqrt{1 - \bar{\alpha}_t} \underbrace{\nabla_{x_t} \log p_{\phi}(c | x_t)}_{\text{conditional part}}.
\end{equation}
$$

The Eq.[$$\ref{classifierguid}$$] could be interpreted as that a diffusion score from unconditional $$\epsilon$$-predictor is changed considering the condition variable $$c$$ by a mount of gradient w.r.t.  $$ x_t $$ of
$$
    \log p_{\phi}(c|x_t).
$$
The authors of the Classifier-Free Guidance (CFG) design their algorithm to get the *conditional part* in Eq.[$$\ref{classifierguid}$$] without explicit classifier such that:

$$
\begin{equation}
\label{cfg}
    \tilde{\epsilon}_{\theta}(x_t, c) := \epsilon_{\theta}(x_t) + w \big (\underbrace{\epsilon_{\theta}(x_t, c) - \epsilon_{\theta}(x_t)}_{\text{the same effect of using explicit classifier}} \big ),
\end{equation}
$$

where $$w$$ is a guidance-scale constant. In this case, we could plug the QKV attention module of the Stable-Diffusion into the term, $$\epsilon_{\theta}(x_t, c)$$ to implement. **We utilized them to implement our dataset generation for a recognition task**.


#### Latent Diffsion Models (LDMs)
The dimensionality of the random variable, $$ x_0 $$ is the same as the resolution of a generated image in common, .e.g., $$ x_0 \in \mathbb{R}^{3 \times 256 \times 256} $$. Such a high dimensional space yields in difficulties to scaling up. To resolve this, the authors of Stable-Diffusion introduce a pretrained encoder-decoder architecture used for reducing the dimensionality of $$x_0$$. Specifically, a sample of $$ x_0 $$ is first pass through the encoder 

$$
    f_{\text{enc}}: \mathbb{R}^{C \times H \times W} \mapsto \mathbb{R}^{C \times H^{\prime} \times W^{\prime}}, \text{where } H \gg H^{\prime}, W \gg W^{\prime},
$$ 

so that resulting dimensionarity of $$ x_0 $$ is reduced. The forward and reverse diffusion processes are conducted in $$ \mathbb{R}^{C \times H^{\prime} \times W^{\prime}} $$. To put back to the $$ x_t $$ to the original image space, the pretrained decoder, $$ f_{\text{dec}}: \mathbb{R}^{C \times H^\prime \times W^\prime} \mapsto \mathbb{R}^{C \times H \times W} $$, 
is used. **We employed the LDM to implement our dataset generation for a recognition task**.

#### Identity-Preserving Face-Recognition Dataset Generation via Conditional Diffusion Probabilistic Models (Ongoing)


**I'm sorry but I didn't have an enough time to complete this post. Please stay tuned. It will be filled completely in the near future.** 

#### Keywords:
Diffusion Probabilistic Models (DPMs), conditional Diffusion Probabilistic Models (cDPMs), Latent Diffusion Models (LDMs), Classifier-Free Guidance (CFG), Dataset Generation
