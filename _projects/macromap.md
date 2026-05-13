---
layout: page
title: MacroMap
description: Interactive global trade network explorer — community detection across 150+ countries
img: assets/img/macromap_preview.png
importance: 2
category: data science
---

Pick any country and see who it actually trades with, which economic bloc it belongs 
to, and how dependent it is on its top partners. That's what MacroMap does.

It's built on OEC bilateral trade data for 2023 — 27,000+ country-pair relationships, 
modeled as a directed weighted graph. Two steps reduce that to something meaningful: 
a disparity filter extracts the statistically significant backbone, then Louvain community 
detection finds the clusters. The blocs you see on the map come from trade volume and 
directionality alone, no manual grouping. The dashboard also computes HHI 
concentration indices, trade-to-GDP ratios, eigenvector centrality, and export/import 
rankings per country.

Built with Plotly Dash, Dockerized, and deployed on Render.

**Stack:** Python, NetworkX, Plotly Dash, pandas, Docker

[GitHub](https://github.com/farrellsid/macromap_alpha) · [Live demo](https://wtrademap.onrender.com/)