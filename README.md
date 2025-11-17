# On P\&ID Symbol Recognition using Transformers

This repository contains the code for the paper **“On P\&ID Symbol Recognition using Transformers”**. This project investigates the use of transformer-based object detection, specifically the **DEtection TRansformer (DETR)** model, for recognizing symbols in Piping and Instrumentation Diagrams (P\&IDs).

The primary goal is to address the challenge of automatically digitizing P\&IDs, which are often locked in non-machine-readable formats like PDF or DWG. Robust, automated symbol detection is a critical first step toward creating machine-interpretable graphs, enabling digital twins, and advancing automation in industrial facilities.

## Methodology

This work focuses on evaluating how different pretraining strategies for the DETR backbone affect generalization when moving from synthetic training data to real-world diagrams.

  * **Model:** The core model is **DETR** with a **ResNet-50** backbone.
  * **Training Data:** The model was trained exclusively on a **synthetic dataset** generated with two layout patterns (grid-based and automatic layouts). This dataset includes 40 distinct symbol classes.
  * **Backbones Compared:** We compared three different pretraining strategies for the backbone:
    1.  **ImageNet:** Standard pretraining on the ImageNet dataset.
    2.  **COCO:** Fine-tuning a DETR model previously pretrained on the COCO dataset.
    3.  **PIDClassify:** A domain-specific pretraining where the backbone was first trained as a classifier for the 40 P\&ID symbol classes used in the synthetic dataset.

## Key Results

The models were evaluated on three datasets, one synthetic to evaluate overfitting and two real-world datasets, **OPEN100** (PID2Graph subset) and **IPD** (an internal dataset), to measure the synthetic-to-real transfer gap.

The key finding is that **domain-specific pretraining (PIDClassify) consistently improves performance**, even when the pretraining data is synthetic the PIDClassify-pretrained model outperformed both COCO and ImageNet pretraining on all three test sets, demonstrating better generalization. This approach yielded an improvement of approximately **1 mAP point** across all test datasets.

### Performance (mAP%)

| Backbone Pretrain | Synthetic | IPD | OPEN100 |
| :--- | :---: | :---: | :---: |
| COCO | 90.5 | 33.8 | 4.0 |
| ImageNet | 52.4 | 25.1 | 1.9 |
| **PIDClassify** | **91.6** | **35.3** | **4.9** |

## Usage

### Environment Installation
Follow the [pixi installation](https://pixi.sh/latest/installation/) steps and then execute the environment installation:
```bash
git clone https://github.com/LeoKenny/pnid_symbol_recognition.git
cd pnid_symbol_recognition
pixi shell
jupyter lab
```

### Dataset
Place your custom dataset inside the `Eramia_dataset` folder.

### Notebooks
Training DETR Model: `detr_augmented.ipynb`
Training ResNet50 Backbone: `classification_backbone_pretrain.ipynb`
Evaluating DETR Model: `detr_evaluation.ipynb`

## Citation

If you use this work in your research, please cite the original paper:

Leonardo K. T. da Cunha, Eduardo F. Leite, Lucas Eduardo C. Morais, Alessandra Harrison, and João F. Valiati. “On P\&ID Symbol Recognition using Transformers”

## Acknowledgments
This research was carried out in association with the ongoing R\&D project registered as ANP nº 24520-9 “3D APT: 3D Automated Perception and Tagging” (SENAI/Shell Brazil/ANP), sponsored by Shell Brasil Petróleo Ltda under the ANP R\&D levy as “Compromisso de Investimentos com Pesquisa e Desenvolvimento”. We also thank all contributors from SENAI which are not named authors, but helped develop tasks related to the results shown.
