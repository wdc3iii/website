---
layout:     post
title:      Random Coding Stuff
author:     Will Compton
tags: 		Miscellaneous
subtitle:  	International Conference on Robotics and Automation 2025
category:   misc
---
<!-- Start Writing Below in Markdown -->

# Mamba (python virtual environments)

- Creating virtual environment with specific python version: ```mamba create -n env_name python==3.v```
- Removing virtual environment: ````mamba env remove -n env_name```
- Creating virtual environment from yaml file: ```mamba env create -f environment.yaml```
- Exporting virtual environment to yaml file: ```mamba export > environment.yaml```

# Matlab Plotting

- General setup for "nice" plots: ```set(groot, 'DefaultAxesFontSize', 17);  % Set default font size for axes labels and ticks
set(groot, 'DefaultTextFontSize', 17);  % Set default font size for text objects
set(groot, 'DefaultAxesTickLabelInterpreter', 'latex');  % Set interpreter for axis tick labels
set(groot, 'DefaultTextInterpreter', 'latex');  % Set interpreter for text objects (e.g., titles, labels)
set(groot, 'DefaultLegendInterpreter', 'latex')
set(groot, 'DefaultFigureRenderer', 'painters');
set(groot, 'DefaultLineLineWidth', 2)
set(groot, 'DefaultLineMarkerSize', 15)```
- Reset the color order to default: `set(gca,'ColorOrderIndex',1)`

# Latex Style file
```\\usepackage\{amsmath\}
\\usepackage\{amsfonts\}
\\usepackage\{amssymb\}
\\usepackage\{balance\}
\\usepackage\{graphicx\}
\\usepackage\{xcolor\}
\\usepackage[capitalize]\{cleveref\}
\\usepackage\{optidef\}    % optimization problems

\\newcommand\{\\R\}\{\\mathbb\{R\}\}
\\newcommand\{\\red\}[1]\{\\textcolor\{red\}{#1\}\}
\\newcommand\{\\blue\}[1]\{\\textcolor\{blue\}\{#1\}\}

\\newcommand\{\\Z\}\{\\mathbb\{Z\}\}
\\renewcommand\{\\cal\}[1]\{\\mathcal\{#1\}\}

\\renewcommand\b[1]\{\%
  \\ifcat\\noexpand#1\\relax % check if the argument is a control sequence
    \boldsymbol\{#1\}\% probably Greek
  \\else
    \\mathbf\{#1\}\% single character
  \\fi
\}
```
