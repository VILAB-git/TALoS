# TALoS: Enhancing Semantic Scene Completion via Test-time Adaptation on the Line of Sight

This repository contains the official PyTorch implementation of the paper "TALoS: Enhancing Semantic Scene Completion via Test-time Adaptation on the Line of Sight" paper (NeurIPS 2024) by [Hyun-Kurl Jang*](https://blue-531.github.io/
) , [Jihun Kim*](https://jihun1998.github.io/
) and [Hyeokjun Kweon*](https://sangrockeg.github.io/
).

## News
(* denotes equal contribution.)
<ul>
  <li> TALoS is accepted at NeurIPS 2024 🎉.</li>
  <li> Official code and Paper will be released soon! </li>
</ul>


## Installation

- PyTorch >= 1.10 
- pyyaml
- Cython
- tqdm
- numba
- Numpy-indexed
- [torch-scatter](https://github.com/rusty1s/pytorch_scatter)
- [spconv](https://github.com/tyjiang1997/spconv1.0) (tested with spconv==1.0 and cuda==11.3)



## Data Preparation

### SemanticKITTI
```
./
├── 
├── ...
├── model_load_dir
    ├──pretrained.pth
└── dataset/
    ├──sequences
        ├── 00/           
        │   ├── velodyne/	
        |   |	├── 000000.bin
        |   |	├── 000001.bin
        |   |	└── ...
        │   └── labels/ 
        |       ├── 000000.label
        |       ├── 000001.label
        |       └── ...
        │   └── voxels/ 
        |       ├── 000000.bin
        |       ├── 000000.label
        |       ├── 000000.invalid
        |       ├── 000000.occluded
        |       ├── 000001.bin
        |       ├── 000001.label
        |       ├── 000001.invalid
        |       ├── 000001.occluded
        |       └── ...
        ├── 08/ # for validation
        ├── 11/ # 11-21 for testing
        └── 21/
	    └── ...
```

## Test-Time Adaptation
1. Download the pre-trained models and put them in ```./model_load_dir```.
2. (Optional) Download pre-trained model results and put them in ```./experiments/baseline``` for comparison.
3. Generate predictions on the Dataset.

### Validation set
```
python run_tta_val.py --do_adapt --do_cont --use_los --use_pgt 
```
### Test set
```
python run_tta_test.py --do_adapt --do_cont --use_los --use_pgt --sq_num={sequence number} 
```
## Evaluation
To evaluate test sequences in SemanticKITTI, you should submit the generated predictions to [link](https://codalab.lisn.upsaclay.fr/competitions/7170).
After generate predictions, prepare your submission in the designated format, as described in the competition page.
Use the validation script from the [semantic-kitti-api](https://github.com/PRBonn/semantic-kitti-api) to ensure that the folder structure and number of label files in the zip file is correct.


## Acknowledgements
We thanks for the open source project [SCPNet](https://github.com/SCPNet/Codes-for-SCPNet).
