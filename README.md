# TDC Data Analysis and Modelling

Definition: A small-molecule drug is a chemical and it needs to travel from the site of administration (e.g., oral) to the site of action (e.g., a tissue) and then decomposes, exits the body. To do that safely and efficaciously, the chemical is required to have numerous ideal absorption, distribution, metabolism, and excretion (ADME) properties. This task aims to predict various kinds of ADME properties accurately given a drug candidate's structural information.

Impact: Poor ADME profile is the most prominent reason of failure in clinical trials. Thus, an early and accurate ADME profiling during the discovery stage is a necessary condition for successful development of small-molecule candidate.

Generalization: In real-world discovery, the drug structures of interest evolve over time. Thus, ADME prediction requires a model to generalize to a set of unseen drugs that are structurally distant to the known drug set. While time information is usually unavailable for many datasets, one way to approximate the similar effect is via scaffold split, where it forces training and test set have distant molecular structures.

Product: Small-molecule.

Pipeline: Efficacy and safety - lead development and optimization.

The source of this information and more useful resources are available at https://tdcommons.ai/single_pred_tasks/adme/#caco-2-cell-effective-permeability-wang-et-al



For measuring the ADME properties, the following datasets have been chosen:
+	**HIA (Human Intestinal Absorption)**, Hou et al.- For **Adsorption** (A)
+	**BBB (Blood-Brain Barrier)**, Martins et al. – For **Distribution** (D)
+	**CYP P450 2C19 Inhibition**, Veith et al. -  For **Metabolism** (M)
+	**Half Life**, Obach et al. – For **Excretion** (E)

The above-mentioned datasets are chosen to benchmark the models. The first three are datasets allow binary classification. While the Half-life is a dataset for regression. These datasets are specifically chosen as they would help to tell which model could generalize better.

Algorithms/Models used:

MPNN (supervised graph neural network),
Transformer, 
 XGBoost (Tree model, ensemble)


**Metrics**

While benchmarking models for classification, it’s best to use ROC Curve and AUC score over accuracy. As the AUC is well-suited to measure the model’s performance on an imbalanced set and to compare the performance.  Overall accuracy is based on one specific Threshold, while ROC tries all of the Threshold and plots the sensitivity and specificity. So when we compare the overall accuracy, we are comparing the accuracy based on some Threshold. The overall accuracy varies from different thresholds.
For a better understanding of how to interpret the ROC graph please see the figure below:
 
![img](https://github.com/KA0335/DeepMirror/blob/main/chugh_metric_accuracy_auc_2.png)
Figure 1: Reference ROC curve, the larger the better



![img2](https://github.com/KA0335/DeepMirror/blob/main/Transformer_BBB_Martins.png)

Figure 2: ROC and AUC for XGBoost for A,D,M




![img3](https://github.com/KA0335/DeepMirror/blob/main/roc-auc.jpg)

Figure 3: ROC and AUC curve for ADM using MPNN and Transformer


The models’ performance could be seen from the fig 2 and fig 3. 
Since the first three categories consist of Classification and the last (Excretion) consists of regression. the model benchmarking is done on the first three categories. 
XGBoost is chosen over MPNN as XGBoost is able to generalize and produce decent results both for classification and regression.
 Here is a graph showing the AUC score for classification: 
 
 
![](https://github.com/KA0335/DeepMirror/blob/main/Comparison.png)
Figure 4: Comparison of all three models

In real-world discovery, the drug structures of interest evolve over time. Thus, ADME prediction requires a model to generalize to a set of unseen drugs that are structurally distant from the known drug set. Therefore, XGBoost is a model which could do this task well both for regression as well as classification. 

