# Segregation and integration between visuo-spatial attention and semantic memory across large-scale brain networks

Data and results accompanying Tani, M., Kaur, S., Ciociola, M., Muneghina, M. B., Cecconi, A., Sulpizio, V., Baldassarre, A.,
Capotosto, P., & Galati, G., *Segregation and integration between visuo-spatial attention and semantic memory across
large-scale brain networks* (Journal of Cognitive Neuroscience, in revision).

Sapienza Brain Imaging Lab, Department of Psychology, Sapienza University of Rome.

All surface data are in fsLR 32k grayordinate space (CIFTI-2 `.dscalar.nii`, readable with Connectome Workbench or
nibabel). Twenty-five participants; coded sub-01 to sub-25.

## Contents

### `maps/` — unthresholded group-level maps

- `glm-conditions/`: main general linear model (block regressors for the attention, semantic, combined [`combo`] and
  control conditions). For each condition (vs. the implicit baseline) and each contrast — main effect of Visuo-spatial
  Attention (`mainAttention`), main effect of Semantic Memory (`mainSemantic`), interaction (`interaction`) and its
  reverse (`antiInteraction`), negative main effects, average of the four conditions — the `stat-t` map (one-sample
  t test across participants, 24 degrees of freedom) and the `stat-effect` map (group mean of the contrast).
- `glm-conditionsrt/`: the same model with an additional regressor common to all conditions modeling the reaction time
  of each trial (`reactionTime`), used as a control for task difficulty.

### `regions/` — regions of interest

- `group/`: group-level regions extracted from the clusters of the two main effects (Supplementary Tables 1–3 of the
  paper, Figure 3); each mask holds the t values of its vertices. `regions.tsv` gives the label used in the paper, the
  main effect and, for the six nodes of the connectivity model, the node name.
- `probabilistic/`: for the six nodes of the connectivity model (LaP, PEF, FEF, IFG, aINS, ITL; left hemisphere), the
  proportion of participants whose individual region (defined on participant-level main-effect maps smoothed at 4 mm)
  includes each vertex. `probabilistic.json` gives the number of participants with an individual region for each node.

### `timeseries/` — regional time series of the connectivity model

For each participant, the first eigenvariate of each node (columns aINS, FEF, IFG, LaP, PEF, ITL; repetition time
0.8 s), extracted from unsmoothed data after regressing out the effects of no interest (control blocks, reaction time
regressor, nuisance regressors), and the onsets and durations (s) of the blocks of the three conditions of interest.

### `dcm/` — dynamic causal models (SPM25, DCM12.5)

- `conditionsrtLHsharedAINScomboALL/`: the model reported in the paper (time series adjusted for reaction time; each
  condition can drive the parietal node of its circuit and the anterior insula, the combined condition PEF, LaP and
  aINS). `first-level/`: the DCM of each participant (`.mat`, with the parameter table `.tsv`). `group/`: Parametric
  Empirical Bayes models of the A, B and C matrices with Bayesian model reduction and averaging (`*_peb.mat`, which
  contain the variables `GCM`, `PEB`, `BMR` and `BMA`) and the corresponding tables of the group parameters
  (`*_bmc.tsv`: Bayesian model average; `*_peb.tsv`: parameters of the PEB model).
- `conditionsrtLH/`: first-level DCMs of the model with a single driving input per condition (attention to PEF,
  semantic to LaP, combined to aINS), estimated on the same time series and used for the model comparison.

## Software

fMRIPrep and XCP-D for preprocessing; GLM and DCM estimation with SPM25 (r25.01.02).

## Raw data

Raw and preprocessed image data are available upon request to the corresponding author (michelangelo.tani@uniroma1.it),
subject to a formal data-sharing agreement and to the approval of the requesting researcher's local ethics committee.

## License

The content of this repository is licensed under the Creative Commons Attribution-NonCommercial-NoDerivatives 4.0
International License (CC BY-NC-ND 4.0; see `LICENSE`). Please cite the paper when using these data.
