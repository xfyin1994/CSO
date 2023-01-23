# CSO: Constraint-guided Space Optimization for Active Scene Mapping

## BUILD

```shell
conda create -p ./venv python=3.6
source activate ./venv
sh ./build.sh && python -m gibson2.utils.assets_utils --download_assets
```

## DATASET

+ Gibson

1. get dataset [here](https://forms.gle/36TW9uVpjrE1Mkf9A)

2. copy URL of `gibson_v2_4+.tar.gz`

3. run command

  ```shell
  python -m gibson2.utils.assets_utils --download_dataset {URL}
  ```


+ Matterport3D

1. get dataset according to [README](https://github.com/StanfordVL/GibsonEnv/blob/master/gibson/data/README.md)

2. run command

  ```shell
  python2 download_mp.py --task_data igibson -o . `
  ```

3. move each folder of scenes to `Gibson Dataset path`

  You can check `Gibson Dataset path` by running

  ```shell
  python -m gibson2.utils.assets_utils --download_assets
  ```


## USAGE

+ Train

```shell
python main.py \
--critic_lr_coef 5e-2 \
--num_robots 1 \
--num_processes 4 \
--train_global 1 \
--dump_location "train" \
--global_lr 5e-5 \
--scenes_file "scenes/my_test/full_big_train.scenes" \
--info_mode 2 \
--info_type 1 \
--action_masked 3 \
--info_gain_map_length 60 \
--exp_name 'exp_1'
```

+ Test

```shell
python main.py \
--num_robots 1 \
--num_processes 1 \
--dump_location "test" \
--num_episodes 20 \
--info_mode 2 \
--scenes_file "scenes/my_test/full_big_test_new.scenes" \
--info_type 1 \
--exp_name 'exp_1' \
--action_masked 3 \
--info_gain_map_length 60 \
--load_global "path_to_your_model/periodic_x.global"
```

+ Visualization

```shell
python main.py \
--num_robots 1 \
--num_processes 1 \
--dump_location "test_vis" \
--info_mode 2 \
--num_episodes 13 \
--scenes_file "scenes/my_test/full_big_test_new.scenes" \
--info_type 1 \
--vis_type 3 \
--exp_name 'exp_1' \
--action_masked 3 \
--info_gain_map_length 60 \
--load_global "path_to_your_model/periodic_x.global"
```

## ACKNOWLEDGMENT
In this repository, we mainly conduct experiments based on the open source code of [NeuralCoMapping](https://github.com/siyandong/NeuralCoMapping). And we also use parts of the implementation from [Active Neural SLAM](https://github.com/devendrachaplot/Neural-SLAM), [SuperGlue](https://github.com/HeatherJiaZG/SuperGlue-pytorch) and [iGibson](https://github.com/StanfordVL/iGibson). We thank the respective authors for open sourcing their code.





