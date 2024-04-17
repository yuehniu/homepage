---
layout: post
title: "Overview of AI Security and Defense"
categories: research
github_comments_issueid: "4"
use_math: true
author:
- Yue (Julien) Niu
---

## Overview

As machine learning techniques have been widely used in real-world applications,
there are growing concerns regarding the security of AI security and how to defend 
against potential attacks. In this post, I will give an overview of security concerns 
in AI and machine learning domain. Potential defense strategies will also be covered.

As the figure below shows, security concerns can arise in different stages in the
whole AI pipeline, from model training to model deployment. 
These threats can lead to different consequences, such as training data leak, 
undesired output during inference, or even model theft during runtime. 

I will mainly discuss the following security threats in the post: 
training data leak, data and model poisoning, backdoor attacks, and prompt injection.

<p style="text-align: center;">
<img src="https://yuehniu.github.io/homepage//assets/fig/aisecurity/AISecurityOverview.png" alt="Overview of AI Security" width="700"/>
</p>

### Training Data Leak

Training data leak can happen in many scenarios. In this blog, I will mainly
discuss data leak through models. As we know, ML models including CNNs, Transformers
or LLMs are trained to learn patterns in the training datasets. If we put it in 
another way, training data information is encoded in model weights during training.
As a result, by interacting with the model, there are many ways to steal or reveal
the training samples. Researchers have shown that data leak can happen in the 
following cases:

#### Model Inversion

Coming soon

#### Extraction Attacks

Extraction attacks happens due to the fact that a pre-trained model memorizes 
training data, in particular for large language models (LLMs). 
As the figure below shows, some prompts can trigger a model to output the extract
data in the training set. The extracted data may contain private information, like
personal identification information (PII), which can cause critical concerns.

<p style="text-align: center;">
<img src="https://yuehniu.github.io/homepage//assets/fig/aisecurity/ExtractionAttack.png" alt="Overview of AI Security" width="400"/>
</p>

Again the reason is that the pre-trained model overfits to some training datasets.
As a result, as the example above shows, a prefix prompt can immediately induce
the model generating a response that is exactly the same as the training samples. 

One question is: how serious this issue can be? Or specifically, how many samples 
will be revealed? Researchers have shown that for even production models like ChatGPT,
there are still quite a few samples that can be extracted by trying multiple 
queries, as shown in the figure below. 
For model such as ChatGPT, even 3% samples can be exactly extracted. Considering 
the size of the pre-trained dataset of ChatGPT, the ratio is significant. 

<p style="text-align: center;">
<img src="https://yuehniu.github.io/homepage//assets/fig/aisecurity/ExtractionRate.png" alt="Overview of AI Security" width="400"/>
</p>

**How should we prevent that?** Unfortunately, there is no effective way for addressing
the issue. General idea is to train the model but avoid overfitting on the training dataset.
For instance, by adding small perturbation in input or hidden states, the trained 
models will not learn the exact inputs, thereby to some extent alleviating the problem.
However, adding perturbation inevitably affect the model utility. 

---

[1] https://arxiv.org/abs/2311.17035