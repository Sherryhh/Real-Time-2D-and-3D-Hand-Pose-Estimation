## 2D and 3D Hand Pose Estimation from RGB Image


Specifically, we seeked to improve upon their method of 3D hand pose estimation by introducing
a biologically inspired loss function to further enhance the machine learning model generalization. 
Furthermore, we intended to resolve the issue of image occlusion by utilizing [FreiHAND dataset](https://github.com/lmb-freiburg/freihand):


### Installation
1. Install pytorch >= v0.4.0 following [official instruction](https://pytorch.org/).
2. Clone this repo, and we'll call the directory that you cloned as ${HAND_ROOT}.
3. Install dependencies:
    ```
    pip install -r requirements.txt
    ```

### Pre-trained models
Pre-trained models can be found in ${HAND_ROOT}$/model/FreiHAND_BoneLoss_models.

### Running the code
#### Evaluation
1. Evaluate on FreiHAND dataset (first 200 samples are provided in ${HAND_ROOT}/data/FreiHAND_testset):
    ```
    python 6.evaluation_FreiHAND.py --config-file "configs/eval_FreiHAND_dataset.yaml"
    ```
    The visualization results will be saved to ${HAND_ROOT}/output/configs/eval_FreiHAND_dataset.yaml/

    The pose estimation results will be saved to ${HAND_ROOT}/output/configs/eval_FreiHAND_dataset.yaml/pose_estimations.mat
    
#### Training
1. Put the downloaded FreiHAND dataset in ${HAND_ROOT}$/data/

2. Change the background set (0-3, 4 sets in total) and training data size (0-32960) in ${HAND_ROOT}/configs/train_FreiHAND_dataset.yaml

3. Train the hourglass network:
    ```
    python 1.train_hg_FreiHAND_baseline2.py --config-file "configs/train_FreiHAND_dataset.yaml"
    ```

4. Train proposed model:
    ```
    python 5.train_full_model_FreiHAND_bone_loss.py --config-file "configs/train_FreiHAND_dataset.yaml"
    ```

For each step, the trained model weights (mlp.pth and net_hm.pth) will be located at ${HAND_ROOT}$. Simply copy and paste the trained model into 
${HAND_ROOT}/model/FreiHAND_separate_trained_models before the next step.



#### Credit
Thanks to Eng Hock Lee and Chih-Tien Kuo's idea on [github](https://github.com/enghock1/Real-Time-2D-and-3D-Hand-Pose-Estimation)
This project aimed to improve the existing work by [Ge et al.](https://github.com/3d-hand-shape/hand-graph-cnn) 


