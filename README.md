# CSO
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
python main.py --global_lr 5e-4 --exp_name 'ma3_history' --critic_lr_coef 5e-2 --train_global 1 --dump_location train --scenes_file scenes/train.scenes
```

+ Test (Example)

```shell
python main.py --exp_name 'eval_coscan_mp3dhq0f' --scenes_file scenes/mp3dhq0-f.scenes --dump_location std --num_episodes 10 --load_global best.global
```

+ Test via scripts

```shell
python eval.py --load best.global --dataset mp3d --method rl -n 5
python eval.py --dataset mp3d --method coscan -n 5
```


+ Visualization

```shell
python main.py --exp_name 'eval_coscan_mp3dhq0f' --scenes_file scenes/mp3dhq0-f.scenes --dump_location /mnt/disk1/vis --num_episodes 5 --load_global best.global --vis_type 2
# dump at ./video/
python scripts/map2d.py --dir /mnt/disk1/vis vis_hrl -ne 5 -ns 4
```

## ACKNOWLEDGMENT
In this repository, we mainly conduct experiments based on the open source code of [NeuralCoMapping](https://github.com/siyandong/NeuralCoMapping). And we also use parts of the implementation from [Active Neural SLAM](https://github.com/devendrachaplot/Neural-SLAM), [SuperGlue](https://github.com/HeatherJiaZG/SuperGlue-pytorch) and [iGibson](https://github.com/StanfordVL/iGibson). We thank the respective authors for open sourcing their code.





