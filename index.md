---
layout: default
---

![](assets/images/teaser.png)

## Abstract

Recovering the geometry of a human head from a single image, while factorizing the materials and illumination, is a severely ill-posed problem that requires prior information to be solved. Methods based on 3D Morphable Models (3DMM), and their combination with differentiable renderers, have shown promising results. However, the expressiveness of 3DMMs is limited, and they typically yield oversmoothed and identity-agnostic 3D shapes limited to the face region. Highly accurate full head reconstructions have recently been obtained with neural fields that parameterize the geometry using multilayer perceptrons. The versatility of these representations has also proved effective for disentangling geometry, materials and lighting. However, these methods require several tens of input images. In this paper, we introduce SIRA, a method which, from a single image, reconstructs human head avatars with high fidelity geometry and factorized lights and surface materials. Our key ingredients are two data-driven statistical models based on neural fields that resolve the ambiguities of single-view 3D surface reconstruction and appearance factorization. Experiments show that SIRA obtains state of the art results in 3D head reconstruction while at the same time it successfully disentangles the global illumination, and the diffuse and specular albedos. Furthermore, our reconstructions are amenable to physically-based appearance editing and head model relighting.

## Method

We follow an analysis-by-synthesis approach to retrieve all the components of a relightable avatar from a single posed image with associated foreground mask, and camera parameters. The 3D geometry is represented as a signed distance function. To capture the complex appearance of human faces, we factor the surface radiance into a global illumination and spatially-varying diffuse and specular albedos, which we also implement as neural fields. Instead of using a single architecture to simultaneously optimize the geometry and appearance from scratch, we split the problem into a 3D reconstruction and an appearance factorization part. This two-step approach, similar to [NeRFactor](https://dl.acm.org/doi/abs/10.1145/3478513.3480496), allows us to adapt the training scheme to each of the two problems independently, and to introduce appropriate inductive biases. These are key to resolve the ambiguities that exist in single-view 3D reconstruction and appearance factorization.

![](assets/images/method.png)

## Results

The proposed method performs well in both few-shot and many-shot scenarios, outperforming model-based methods like [MVFNet](https://openaccess.thecvf.com/content_CVPR_2019/papers/Wu_MVF-Net_Multi-View_3D_Face_Morphable_Model_Regression_CVPR_2019_paper.pdf) and [DFNRMVS](https://openaccess.thecvf.com/content_CVPR_2020/papers/Bai_Deep_Facial_Non-Rigid_Multi-View_Stereo_CVPR_2020_paper.pdf) in 3D face reconstruction from only 3 views, and model-free approaches like [IDR](https://arxiv.org/abs/2003.09852) in full head reconstruction.

Next, we show full head 3D reconstructions from only 3 input images. In these examples, the camera poses have been regressed using a pre-trained [MRL model](https://openaccess.thecvf.com/content_ICCVW_2019/papers/GMDL/Ramon_Hyperparameter-Free_Losses_for_Model-Based_Monocular_Reconstruction_ICCVW_2019_paper.pdf), which minimizes the reprojection error. The masks have been estimated using [U2Net](https://arxiv.org/pdf/2005.09007.pdf) and then have been manually refined.

<p align="center">
  <img src="assets/images/3-views-1.gif" width="350" />
  <img src="assets/images/3-views-2.gif" width="350" />
</p>

We also provide a qualitative and quantitative comparison with respect to [IDR](https://arxiv.org/abs/2003.09852) varying the number of available views. Note how H3D-Net effectively finds realistic and detailed solutions in both few-shot and many-shot scenarios.

<p align="center">
  <img src="assets/images/h3dnet-idr.gif" />
</p>

## Related work

1. [DeepSDF: Learning Continuous Signed Distance Functions for Shape Representation (2019)](https://arxiv.org/abs/1901.05103)
2. [Implicit Geometric Regularization for Learning Shapes (2020)](https://arxiv.org/abs/2002.10099)
3. [Multiview Neural Surface Reconstruction with Implicit Lighting and Material (2020)](https://arxiv.org/abs/2003.09852)

## BibTeX

```
@inproceedings{ramon2021h3d,
  title={H3D-Net: Few-Shot High-Fidelity 3D Head Reconstruction},
  author={Ramon, Eduard and Triginer, Gil and Escur, Janna and Pumarola, Albert and Garcia, Jaime and Giro-i-Nieto, Xavier and Moreno-Noguer, Francesc},
  journal={arXiv preprint arXiv:2107.12512},
  booktitle={Proceedings of the IEEE/CVF International Conference on Computer Vision},
  pages={5620--5629},
  year={2021}
}
```
