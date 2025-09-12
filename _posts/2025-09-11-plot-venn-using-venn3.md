---
title:  "Plot Venn diagram using venn3" 
excerpt: "Python code to plot a Venn diagram using venn3 package from matplotlib."
date: 2025-09-11
header:
  teaser: 2025-09-11-plot-venn-using-venn3-thumbnail.png
categories:
  - plots
tags:
  - bioinformatics
  - coding
  - plots
---

![Plot of a Venn diagram made using the venn3 package](/assets/images/posts/2025-09-11-plot-venn-using-venn3.png)

```python
import matplotlib_venn
from matplotlib_venn import venn3
print("matplotlib_venn", matplotlib_venn.__version__)

only_group1 = 648626
only_group2 = 18515
only_group3 = 496281
group1_and_group2 = 72131
group2_and_group3 = 74965
group1_and_group3 = 206664
overlap123 =  180651

# Create Venn diagram with custom colors
venn = venn3(
    subsets=(only_group1, only_group2, group1_and_group2,
             only_group3, group1_and_group3, group2_and_group3, overlap123),
    set_labels=('Group 1', 'Group 2', 'Group 3'),       # Labels for each group
    set_colors=('green', 'red', 'lightgrey')            # Fill colors for each group
)

# Adjust font size for the numbers shown inside the diagram
for label in venn.subset_labels:
    if label:  # Skip labels that don't exist (empty subsets)
        label.set_fontsize(12)

# Add a plot title
plt.title("Overlap of Group 1, Group 2, and Group 3", fontsize=12)

# Display the Venn diagram
plt.show()
```