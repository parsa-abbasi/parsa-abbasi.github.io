---
title: 'CQD-SHAP: Explainable Complex Query Answering via Shapley Values'

# Authors
# If you created a profile for a user (e.g. the default `admin` user), write the username (folder name) here
# and it will be replaced with their full name and linked to their profile.
authors:
  - admin
  - Stefan Heindorf

# Author notes (optional)
author_notes:

date: '2026-09-05T00:00:00Z'
doi: '10.1007/978-3-032-37673-2_19'

# Schedule page publish date (NOT publication's date).
publishDate: '2026-09-05T00:00:00Z'

# Publication type.
# Accepts a single type but formatted as a YAML list (for Hugo requirements).
# Enter a publication type from the CSL standard.
publication_types: ['paper-conference']

# Publication name and optional abbreviated publication name.
publication: In *Machine Learning and Knowledge Discovery in Databases. Research Track (ECML PKDD 2026)*
publication_short: In *ECML PKDD*

abstract: Complex query answering (CQA) goes beyond the widely studied link prediction task by addressing more sophisticated queries that require multi-hop reasoning over incomplete knowledge graphs (KGs). Research on neural and neurosymbolic CQA methods is still an emerging field. Almost all of these methods can be regarded as black-box models, which may raise concerns about user trust. Although neurosymbolic approaches like CQD are slightly more interpretable, allowing intermediate results to be tracked, the importance of different parts of the query remains unexplained. In this paper, we propose CQD-SHAP, a novel framework that computes the contribution of each query part to the ranking of a specific answer. This contribution explains the value of leveraging a neural predictor that can infer new knowledge from an incomplete KG, rather than a symbolic approach relying solely on existing facts in the KG. CQD-SHAP is formulated based on Shapley values from cooperative game theory and satisfies all fundamental Shapley axioms. Automated evaluation of these explanations in terms of necessary and sufficient explanations, and comparisons with various baselines, show the consistent effectiveness of this approach across all studied datasets and query types.

# Summary. An optional shortened abstract.
summary:

tags:
  - Knowledge Graphs
  - Explainable AI
  - Complex Query Answering
  - Shapley Values
  - Machine Learning

# Display this page in the Featured widget?
featured: true

# Custom links (uncomment lines below)
# links:
# - name: Custom Link
#   url: http://example.org

url_pdf: 'https://arxiv.org/pdf/2510.15623'
url_code: 'https://github.com/ds-jrg/CQD-SHAP'
url_dataset: ''
url_poster: ''
url_project: ''
url_slides: ''
url_source: 'https://arxiv.org/abs/2510.15623'
url_video: ''

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
image:
  caption: ''
  focal_point: ''
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
projects:


# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
slides:
---
