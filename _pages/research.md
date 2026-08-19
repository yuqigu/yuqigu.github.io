---
layout: page
permalink: /research/
title: Research
description:
nav: true
page_order: 1
---

My research develops statistical foundations and methodology for learning interpretable latent representations from complex data. A recurring goal is to understand when latent structures are identifiable, how they can be learned and quantified reliably in high dimensions, and how statistically grounded representations can support scientific measurement and modern AI.

For a complete chronological list of papers and preprints, see [Publications]({{ '/publications/' | relative_url }}).

In the selected work below, <u>underlined</u> names are students or postdoctoral researchers under my supervision; &#9993; marks corresponding authors, * marks co-first authors, and ⁺ marks alphabetical authorship.

### Recurring questions

+ **Identifiability.** Which features of a latent representation or architecture are determined by the distribution of the observed data, and under what structural assumptions?
+ **Learning and inference.** How can latent structure be recovered efficiently in high dimensions, with finite-sample guarantees and principled uncertainty quantification?
+ **Measurement and interpretation.** How can latent representations support interpretable measurement of heterogeneous populations, scientific constructs, and complex AI systems?

These questions recur across three connected research directions: (a) Identifiable deep and causal representations; (b) High-dimensional statistical inference with latent structure, and (c) Statistical measurement for humans and AI systems.

<figure class="my-4">
  <img class="img-fluid" src="{{ '/assets/img/research-overview.svg' | relative_url }}" alt="Research overview showing observed data, structured latent representations, identifiable causal structure, statistical inference, and interpretable measurement.">
</figure>

## 1. Identifiable deep and causal representations

I study how latent representations in deep generative models can be made structurally meaningful rather than arbitrary. This work develops identifiable models with discrete latent layers, including Bayesian Pyramids and Deep Discrete Encoders, and investigates when latent dimension, graphical structure, and other features of a latent architecture can be recovered from observed data.

A related line of work studies causal structure among latent variables. I develop theory and methods for discrete causal representation learning, identifiability of latent causal graphical models, and tensor-unfolding approaches to learning unknown latent bipartite architectures. The broader aim is to connect expressive representation models with assumptions that make their learned structure statistically interpretable.

### Selected work

<div class="publications">
{% bibliography -f papers -q @*[key=lee2025dde || key=zhang2026dcrl || key=lee2025causal || key=gu2025unfold-q || key=gu2024bless || key=gu2023bp]* %}
</div>

## 2. High-dimensional statistical inference with latent structure

I develop scalable methods for high-dimensional data in which heterogeneity is governed by latent classes, mixed membership, factors, or clusters. The methods draw on spectral, tensor, likelihood-based, and geometric ideas, with an emphasis on finite-sample guarantees, optimal recovery, and uncertainty quantification.

Recent work moves beyond idealized local-independence assumptions by modeling latent graphical dependence, local dependence, and shared block structure. I also study transfer and adaptation across related populations. This program asks not only whether latent structure is identifiable, but also when computational procedures recover it at statistically optimal rates.

### Selected work

<div class="publications">
{% bibliography -f papers -q @*[key=chen2024local || key=gu2024atc || key=lyu2024dhlcm || key=lyu2025sola || key=huang2025copo || key=lee2026local]* %}
</div>

## 3. Statistical measurement for humans and AI systems

Psychometrics provides an intellectual foundation for my work on statistical measurement through latent-variable models. I develop models and theory for measuring latent attributes, response processes, and heterogeneous performance in educational, psychological, biomedical, and other scientific settings.

My recent work extends this measurement perspective to modern AI evaluation. Rather than reducing model behavior to a single aggregate score, I study structured variation in capabilities, reasoning behavior, semantic item structure, response accuracy, and chain-of-thought length. The goal is to build statistically grounded measurement frameworks for increasingly complex AI systems while maintaining a clear connection to the broader theory of latent-variable modeling.

### Selected work

<div class="publications">
{% bibliography -f papers -q @*[key=xu2025lart || key=liu2026cdm-llm || key=liu2025exploratory || key=kang2024mmmpd || key=gu2023grom3 || key=gu2022joint]* %}
</div>

{% comment %}
## Current directions

+ Learning the unknown depth, width, and connectivity of latent architectures.
+ Developing finite-sample theory and uncertainty quantification for high-dimensional latent representations.
+ Studying causal relationships among latent representations across heterogeneous environments.
+ Characterizing when spectral, tensor, and likelihood-based methods achieve optimal recovery.
+ Building statistical measurement frameworks for increasingly complex AI systems.
{% endcomment %}

For the complete chronological record, including all older publications, see [Publications]({{ '/publications/' | relative_url }}).
