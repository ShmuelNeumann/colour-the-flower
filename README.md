# Colour the Flower GAN model
## Overview
**Starting Date:** 21th September, 2022
**Project Completion:** 14th October, 2022
**Motivation:** Completed as part of MDN training
**Status:** Complete

This is a GAN machine learning model that attempts to colour greyscale images of flowers, developed over three weeks as part of the MDN training program.

It was created in collaboration with the trainees Racharit Ramnarong, Mark Zheng and Satya Jhaveri in addition to the experienced MDN member Nhut Nguyen offering guidance as required.

## Context

This project was completed with [Monash DeepNeuron](https://www.deepneuron.org/) (MDN), a student run engineering team of around 80 members that works with researchers and competes in competitions in the fields of AI and HPC. 

Following my team winning the [LSS X MDN Legal Hackathon](https://github.com/ShmuelNeumann/legal-hackathon), I was invited to join the MDN training program intended for new recruits, in order to gain the knowledge to develop our winning pitch into a MDN project. This program included five practical workshops revolving around foundational Machine Learning (ML) knowledge, followed by a three week min-project.

I chose to work on a project  involving using a GAN model to colour black and white pictures of flowers, and as a team we developed a fully working model.

## Technical Description

This project was coded entirely in Python with the [pytorch](https://pytorch.org/) library, and was based on the [Pix2Pix model architecture](https://phillipi.github.io/pix2pix/). Additionally, when we got stuck we referred to [Aladdin Persson](https://www.youtube.com/@AladdinPersson)'s implementation in this [video series](https://www.youtube.com/playlist?list=PLhhyoLH6IjfwIp8bZnzX8QR30TRcHO8Va). We chose to use [Google Collab](https://colab.research.google.com/?utm_source=scs-index#scrollTo=GJBs_flRovLc) as the platform for development, in order to reach the hardware requirements for testing and running the ML model with reasonable efficiency.
The dataset we trained with is the Kaggle [Color_The_Flower_Dateset](https://www.kaggle.com/datasets/vaibhavrmankar/colour-the-flower-gan-data), which includes both greyscale and colour image pairs.

![enter image description here](https://onedrive.live.com/embed?resid=BE406011F5E2A3C1!488499&authkey=!ABXK-VQ8PqJsvbw&width=500&height=250)

The model we were using is a Generative Adversarial Network (GAN), which works by training two separate models.
The first is the Generator which is given input data, in this case a greyscale image, and attempts to generate a new image from this, in this instance a fake coloured version. 
The second is the Discriminator which is given the intended goal image, in this case the real coloured image, and the fake output image from the Generator. It then attempts to identify which image is the real one.
These two models are repeatedly trained with each other, with the Discriminators choices being used to create the feedback loop for the Generator.

During this project, I primarily focused on creating the Generator, which follows a [U-Net](https://arxiv.org/abs/1505.04597) design involving a series of convolutions first encoding the image data, followed by a series of reverse convolutions decoding it into a new image, with skip connections. More details on this can be found in the Pix2Pix paper above.

## Results and Potential Improvements


The images produced were not perfect, yet showed that the model was working to a reasonable extent. The images below show a sample of the real images below, and the corresponding GAN generated ones above.

![enter image description here](https://onedrive.live.com/embed?resid=BE406011F5E2A3C1!488501&authkey=!AAx-UNUNizQ-JLw&width=3072&height=512)

One of the trends observed is that the model understood shape very well, however it struggled with colour. After a few epochs, it would choose a different colour and apply it to all flowers. It was unable to connect specific petal shapes to the appropriate colours, although this may be a result of the relatively small dataset of 11,000 training images. Furthermore, a major obstacle we found was the lack of cleaning in the dataset. Several image pairs were only tangentially related to flowers, which negatively impacted the results.

## Running the Program

The program is available on a Google Collab page [here](https://colab.research.google.com/drive/1SA9bmUkyp2BywakrIn3Zezqlxk9qVGVd?usp=sharing).

In order for the Collab page to access the dataset, the following steps are required:
- Go to the [Kaggle website](https://www.kaggle.com/#)
- Create a free account
- Go to [account\Settings\API](https://www.kaggle.com/settings#:~:text=Phone%20verify-,API,-Using%20Kaggle%27s%20beta) and select "Create new token"
- Take the _kaggle.json_ file and put it in the ~/content/ path

It's also highly recommended to change the runtime to GPU instead of CPU, to improve the training speed.
Select "Runtime\Run all" to start the model. Every epoch, the sample results will be saved to a folder named _example_results_
