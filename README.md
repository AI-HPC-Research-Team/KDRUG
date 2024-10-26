# KDRUG
[![bioRxiv](https://img.shields.io/badge/bioRxiv-<10.1101>-36C?logo=BioRxiv&logoColor=white)](https://www.biorxiv.org/content/10.1101/2024.10.17.618828v1)
[![DOI](https://img.shields.io/badge/DOI-<2024.10.17.618828>-blue)](https://doi.org/10.1101/2024.10.17.618828)

Here we introduce **A Multi-Modal Genomic Knowledge Distillation Framework for Drug Response Prediction**. Specifically, we train a teacher network by feature re-weighting based on inter-modality dependencies and align the inter-sample correlations through our proposed relation-aware differentiation distillation.

![Paper overview](figures/Figure1.png)

**Note:** The sections on Datasets, Model, and Training below describe the contents of the respective directories. Due to size constraints and permissions, some data and ckpts may not be uploaded. The download url can be found in our paper.

## Datasets
Download GDSC origion dataset from https://pan.baidu.com/share/init?surl=Z7xiX4TQyaXKydSceNhp0g (code:KDRU)

    `global_data/`                  - path of origional GDSC/TCGA files  
    `data/processed/xxxxGDSCxx.pt`  - path of processed bulk data, train, val and test

## Model
### training model:
	`1` - models/gat_gcn_transformer_meth_ge_mut.py   
	`2` - models/gat_gcn_transformer_meth_ge_mut.py -> models/gat_gcn_transformer_ge_only.py  
	`3` - models/gat_gcn_transformer_meth_ge_mut_multiple.py  
	`4` - models/gat_gcn_transformer_meth_ge_mut_multiheadattn.py  
	`5` - models/gat_gcn_transformer_meth_ge_mut_multiple.py -> models/gat_gcn_transformer_ge_only.py  
	`6` - models/gat_gcn_transformer_meth_ge_mut_multiheadattn.py -> models/gat_gcn_transformer_ge_only.py  
	`7` - models/gat_gcn_transformer_meth_ge_mut_multiheadattn.py -> models/gat_gcn_transformer_ge_only.py  
	`8` - models/gat_gcn_transformer_meth_ge_mut_multiheadattn.py -> models/gat_gcn_transformer_ge_only.py  

## Training
### training code:
    `1 training.py` - origion multi-modal/single-modal module  
    `2 training_continue_KD1.py` - distill from origion multi-modal  
    `3 training_continue_combine.py` - our proposed privileged information knowledge distillation framework  
    `4 training_continue_combine.py` - feature re-weighting strategy using in 3   
    `5 training_continue_KD.py` - distill from module 3  
    `6 training_continue_KD.py` - distill from module 4  
    `7 training_continue_KD.py`  - distill from module 4; KD LOSS + RAD loss  
    `8 training_continue_KD.py`  - distill from module 4; only RAD loss  

### loss:
1| MSE  
2| MSE + KD  
3| MSE  
4| MSE  
5| MSE + KD  
6| MSE + KD  
7| MSE + KD + RAD  
8| MSE + RAD  

`origion ge-modal weights used in code`  
- result/2024-05-14 18:37:42/model_GAT_GCN_Transformer_ge_only_GDSC.model  

`origion multi-modal weights used in code`  
- model_GAT_GCN_Transformer_meth_ge_mut_GDSC.model  

`origion combined model`  
- model_continue_combine_pretrain_relu_GDSC.model  

`our multi-modal & re-weighted strategy`  
- model_continue_combine_pretrain_multiheadattn(ge_others)_relu_GDSC.model  

### TCGA test
result/plot_TCGA/compute_GDSC_TCGA_distribution.py

* Thanks to [Thang Chu, et al.] for providing excellent code and documentation. This project was inspired by and includes some code from [GraTransDRP] T. Chu, T. T. Nguyen, B. D. Hai, Q. H. Nguyen and T. Nguyen, "Graph Transformer for Drug Response Prediction," in IEEE/ACM Transactions on Computational Biology and Bioinformatics, vol. 20, no. 2, pp. 1065-1072, 1 March-April 2023

## References
```
[1]: Yang, W., Soares, J., et al.: Genomics of drug sensitivity in cancer (gdsc): a resource for therapeutic biomarker discovery in cancer cells. Nucleic acids research 41(D1), 955–961 (2012)
[2]: Barretina, J., Caponigro, G., et al.: The cancer cell line encyclopedia enables predictive modelling of anticancer drug sensitivity. Nature 483(7391), 603–607 (2012)
[3]: Ma, J., Fong, S.H., et al.: Few-shot learning creates predictive models of drug response that translate from high-throughput screens to individual patients. Nature Cancer 2(2), 233–244 (2021)
[4]: Shen, B., Feng, F., Li, K., Lin, P., Ma, L., Li, H.: A systematic assessment of deep learning methods for drug response prediction: from in vitro to clinical applications. Briefings in Bioinformatics 24(1), 605 (2023)
[5]: Ding, M.Q., Chen, L., et al: Precision oncology beyond targeted therapy: combining omics data with machine learning matches the majority of cancer cells to effective therapeutics. Molecular cancer research 16(2), 269–278 (2018)
```
## Citation
```
@article {Ge2024.10.17.618828,
	author = {Ge, Shuang and Sun, Shuqing and Xu, Huan and Cheng, Qiang and Ren, Zhixiang},
	title = {A Multi-Modal Genomic Knowledge Distillation Framework for Drug Response Prediction},
	elocation-id = {2024.10.17.618828},
	year = {2024},
	doi = {10.1101/2024.10.17.618828},
	publisher = {Cold Spring Harbor Laboratory},
	URL = {https://www.biorxiv.org/content/early/2024/10/17/2024.10.17.618828},
	eprint = {https://www.biorxiv.org/content/early/2024/10/17/2024.10.17.618828.full.pdf},
	journal = {bioRxiv}
}
```
