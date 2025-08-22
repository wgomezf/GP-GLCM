# GLCM-based texture features constructed by genetic programming for breast tumor classification

Two sets of GLCM-based texture features for breast tumor classification in ultrasound are provided. These texture features were automatically constructed using the genetic programming (GP) algorithm, and they outperformed the well-known Haralick features that are widely used in radiomics for tumor classification. The success of these novel features is due to the fact that they were specifically constructed for a particular classification task, while Haralick features are general-purpose texture features and may not effectively describe the tumors' nature to distinguish them into benign and malignant classes.

The first set contains 10 texture features representing the best configuration obtained in 1000 runs of the GP algorithm tested with different configurations, including the number of trees (i.e., number of features) and tree depth (i.e., complexity of the expressions).

| ID       | Expression                                                                                                                                   |
|----------|----------------------------------------------------------------------------------------------------------------------------------------------|
| $z_1$    | $\sum\nolimits_{ij} {\log \sqrt {p(i,j)_1^{90}} }$                                                                                           |
| $z_2$    | $\sum\nolimits_{ij} {\max \left( {{\textstyle{{p(i,j)_4^{90}} \over {p(i,j)_4^0}}},{\textstyle{{HXY1_2^{90}} \over {HXY_8^{90}}}}} \right)}$ |
| $z_3$    | $\sum\nolimits_{ij} {(HXY2_8^0 - p(i,j)_8^{135}) - \max (HXY2_1^{135},HXY1_2^{90})}$                                                         |
| $z_4$    | $\sum\nolimits_{ij} {\min ({\mu _x}_4^{90},{\sigma _y}_2^0) + \log (p(i,j)_1^{90}})$                                                           |
| $z_5$    | $\sum\nolimits_{ij} {(HXY2_1^{135} + p(i,j)_4^0) - (p(i,j)_8^0 + HXY2_1^0)}$                                                                 |
| $z_6$    | $\sum\nolimits_{ij} {\left( {{\textstyle{{{\mu _x}_4^{45}} \over {{\sigma _y}_2^{45}}}}} \right)} - p(i,j)_4^0$                              |
| $z_7$    | $\sum\nolimits_{ij} {\log (p(i,j)_4^{45} \times p(i,j)_1^{135})}$                                                                            |
| $z_8$    | $\sum\nolimits_{ij} {(p(i,j)_1^{90} - HX_1^{135}) + {\textstyle{1 \over {p(i,j)_4^0}}}}$                                                     |
| $z_9$    | $\sum\nolimits_{ij} {\sqrt {p(i,j)_1^{90}} } - HX_1^{135}$                                                                                   |
| $z_{10}$ | $\sum\nolimits_{ij} {{\textstyle{{p(i,j)_4^{90} - p(i,j)_1^0} \over {p(i,j)_4^{90}/p(i,j)_4^0}}}}$                                           |

The second set contains three features that achieved a classification performance statistically similar to the best set according to the McNemar test (p-value > 0.6). This feature set represents the smallest feature space dimensionality that can perform similarly to the best one.

| ID    | Expression                                                                                                             |
|-------|------------------------------------------------------------------------------------------------------------------------|
| $z_1$ | $\sum\nolimits_{ij} {{\textstyle{{p(i,j)_1^{90}} \over {{\mu _y}_4^0}}} - {\textstyle{{HXY2_2^0} \over {HY_4^{45}}}}}$ |
| $z_2$ | $\sum\nolimits_{ij} {{\textstyle{{HX_8^{90}} \over {HX_4^0 - p(i,j)_1^{90}}}}}$                                        |
| $z_3$ | $\sum\nolimits_{ij} {{\textstyle{{HY_4^{45}/HX_8^{90}} \over {p(i,j)_4^{90}}}}}$                                       |

These GLCM-based texture features were implemented in MATLAB 2024b. The GPGLCMfeats.zip file contains the source codes and data organized into the following folders:

* BUS: It contains the breast ultrasound datasets (UDIAT, BUSI, and Thammasat) with benign and malignant cases, where the images were already cropped to obtain the tumor ROI for texture analysis.
* data: It contains the files BUSBRA3feats.mat and BUSBRA10feats.mat with the 3 or 10 texture features computed on the BUS-BRA dataset (http://doi.org/10.1002/mp.16812). These files contain two variables: X, the feature space, and Y, the class labels (0-benign and 1-malignant), which can be used as training data.
* funset: It contains the mathematical operators in the equations of texture features; some of them are protected to avoid indeterminations.
* stats: It contains some basic statistics used in the equations of texture features.
* gpfeats: It contains the functions GP3feats.m and GP10feats.m that compute the texture feature in the tables above.
* misc: Miscellaneous functions.

Run the program demo.m to calculate the texture features on the BUS datasets. Next, a logistic regression model is trained using BUS-BRA texture data. Finally, the BUS texture data is used as a test set to evaluate the classification performance, reproducing the results in the paper. It is necessary to set the variable 'opt' to 3 or 10 to calculate three or ten texture features.

Any use of these codes, please cite:

Wilfrido Gomez-Flores, "Constructing GLCM-based Texture Feature Expressions Using Genetic Programming for Breast Tumor Classification", In revision in *IEEE Transactions on Evolutionary Computation*, 2025.
