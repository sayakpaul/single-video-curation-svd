# single-video-curation-svd

**Educational** repository for applying the main video data curation techniques presented in the Stable Video Diffusion [paper](https://arxiv.org/abs/2311.15127). The goal is to provide an interactive resource for the community dig deeper into the curation techniques presented in the paper. As such, it doesn't guarantee precise correctness. 

The curation techniques used in this repository are discussed in _Appendix C_ of the paper, in detail. These include:

* Cascaded Cut Detection
* Keyframe-Aware Clipping
* Optical Flow
* Synthetic Captioning
* Caption similarities and Aesthetics
* Text Detection

The notebooks present these techniques on a single video file sourced from the UCF-101 dataset. 

| **Video** | **CoCa Caption** | **V-BLIP Caption** | **Zephyr-7B Caption** |
|:------------:|:-----:|:------------:|:-----:|
|  ![](https://huggingface.co/datasets/sayakpaul/sample-datasets/resolve/main/Basketball.gif) |  a group of men playing basketball on a court .  | the basketball player dribbles to the basket | A basketball player in a group of men dribbles towards the basket on a court. |

Readers are advised to first go through the Appendix C of the Stable Video Diffusion paper before referring to the notebooks.

## Setup 

Below are the primary dependencies:

* PyTorch (follow the installation instructions from the [official site](https://pytorch.org/))
* `transformers`
* `opencv-python`
* `numpy`
* `ffmpeg`

Other dependencies will be detailed below.

## Notebooks (should be run in order)

<details>
<summary>Clip extraction</summary>

Refer to the `video_preprocessing_clip_extraction.ipynb` notebook for this. You'd need to install the `scenedetect` library from here: https://github.com/Breakthrough/PySceneDetect. This shows both cascaded cut detection and keyframe-aware clipping. At the end of the notebook, you should expect to see different clips extracted from the provided video.

</details>

<details>
<summary>Captioning</summary>

`video_preprocessing_captioning.ipynb` presents synthetic captioning from a single video clip. 

This uses three models:

* CoCa (relies on `open_clip`)
* V-BLIP (relies on [EILEV](https://github.com/yukw777/EILEV))
* Zephyr-7B (relies on `transformers`)

We had to apply some corrections to `eilev` to make it work. The correction patch can be found [here](./correction_patches/corrections_eilev.patch).

</details>

<details>
<summary>Optical Flow</summary>

`video_preprocessing_optical_flow_score.ipynb` notebook shows the optical flow score computation only using the Farneback algorithm. It doesn't, however, show [RAFT](https://arxiv.org/abs/2003.12039).

<details>
<summary>Caption similarities and Aesthetics</summary>

This is straightforward and is implemented in the `video_preprocessing_similarity_aesthetics.ipynb` notebook.

</details>

<details>
<summary>Text Detection</summary>

Refer to the `video_preprocessing_text_detection.ipynb` notebook for this. We use a wrapper library called `craft_text_detector` ([repository](https://github.com/fcakyon/craft-text-detector)) for this as it provides a handy package around the CRAFT text detection model. However, to make it work, we had to do some changes. The patch can be found [here](./correction_patches/corrections_craft.patch).

</details>

## Acknowledgements

Thanks to ChatGPT for all the help.

Thanks to [Dhruv Nair](https://github.com/DN6) for his reviews. 