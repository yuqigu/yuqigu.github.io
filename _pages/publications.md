---
layout: page
permalink: /research/
title: Research
description: 
years: [2023, 2022, 2021, 2020, 2019, 2018]
nav: true
page_order: 1 
---

<div class="publications">

<u>Underlined</u> are student or postdoc authors under my supervision.
&#9993; indicates I am the corresponding author.<br/>

* indicates co-first authors. ⁺ indicates alphabetical authorship.<br/><br/>

<h2> Preprints </h2>

{% bibliography -f papers -q @*[pubtype=preprint]* %}

<h2> Publications </h2>

{% bibliography -f papers -q @*[pubtype=pub]* %}


</div>
