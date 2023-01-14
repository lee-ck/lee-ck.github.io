---
layout: single
title:  "Koopman-based MPC"
tags: [TubeMPC, MPC, All]
comments: true
author_profile: false
toc: true
---


# Test header
## Test header
### Test header
#### Test header
##### Test header
###### Test eq


$$
\begin{bmatrix}
x_2\\
y_2\\
z_2  
\end{bmatrix}
= R \begin{bmatrix}
                  x_1\\
                  y_1\\
                  z_1  
                  \end{bmatrix}
$$
This post should not appear in the search index because it has the following YAML Front Matter:

```yaml
search: false
\overline{bel}(x_t) = \int_{x_{t-1}}p(x_t \mid x_{t-1}, u_{t}) bel(x_{t-1}) dx_{t-1}
```

**Note:** `search: false` only works to exclude posts when using **Lunr** as a search provider. \overline{bel}(x_t) = \int_{x_{t-1}}p(x_t \mid x_{t-1}, u_{t}) bel(x_{t-1}) dx_{t-1}

{: .notice--info}

To exclude files when using **Algolia** as a search provider add an array to `algolia.files_to_exclude` in your `_config.yml`. For more configuration options be sure to check their [full documentation](https://community.algolia.com/jekyll-algolia/options.html).
$$
\overline{bel}(x_t) = \int_{x_{t-1}}p(x_t \mid x_{t-1}, u_{t}) bel(x_{t-1}) dx_{t-1}
$$


```yaml
algolia:
  # Exclude more files from indexing
  files_to_exclude:
    - index.html
    - index.md
    - excluded-file.html
    - _posts/2017-11-28-post-exclude-search.md
    - subdirectory/*.html
```