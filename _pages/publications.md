---
layout: page
permalink: /research/
title: Research
description: 
publication_years: [2026, 2025, 2024, 2023]
nav: true
page_order: 1 
---

<div class="publications">

<u>Underlined</u> are student or postdoc authors under my supervision.
&#9993; indicates I am the corresponding author.<br/>

* indicates co-first authors. ⁺ indicates alphabetical authorship.<br/><br/>

<h2> Preprints </h2>

{% bibliography -f papers -q @*[pubtype=preprint]* %}

<h2> 2026 </h2>

{% bibliography -f papers -q @*[pubtype=pub && year=2026]* %}

<h2> 2025 </h2>

{% bibliography -f papers -q @*[pubtype=pub && year=2025]* %}

<h2> 2024 </h2>

{% bibliography -f papers -q @*[pubtype=pub && year=2024]* %}

<h2> 2023 </h2>

{% bibliography -f papers -q @*[pubtype=pub && year=2023]* %}

<h2> Before 2022 </h2>

{% bibliography -f papers -q @*[pubtype=pub && year<2022]* %}

</div>
