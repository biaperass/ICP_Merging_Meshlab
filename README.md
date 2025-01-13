# ICP_Merging_Meshlab

## Overview

This project focuses on comparing and aligning two different 3D models in SPLAT PLY format by using MeshLab. One model represented the complete statue, while the other simulated a broken version with missing parts. The primary objectives of this project are: 

- Exploring two different alignment techniques available in MeshLab: Point Pairs Picking and Iterative Closest Point (ICP).
- Understanding the process of applying transformations and alignments to 3D models.
- Performing a merge operation to combine align models into a single output model.

## Requirements

- MeshLab version 2023.12 or later.
- Two 3D models in SPLAT PLY format. Example models can be found in this repository in the section 'models'.

## Usage

### Import the model

1) Open **MeshLab**
2) Go to **File** > **Import Mesh** and load **Model 1** (complete statue).
3) Repeat the same step to load **Model 2** (broken version). You should now see both models in the workspace.

mettere immagine modelli 

### Navigation in MeshLab 

- Left mouse button + drag: rotate around trackball center
- Mouse wheel: move forward or backward
- Center mouse button + drag: pan
- Shift + mouse wheel: change camera field of view
- Double click on specific point: places that point at the trackball center
- Control + mouse wheel: moves near clipping plan
- Control + Shift + mouse wheel: moves far clipping plan
- Alt + Enter: enter full screen mode
- Control + Shift + left mouse button + drag: changes light direction (this only takes effect if there are normals)

### Perform Alignment 

To start the alignment process, click on the respective icon (symbolized with letter A in the tool bar). It will launch the align dialog as it is shown.

mettere immagine finestra di dialogo

1) In the pop-up window you need to choose which point cloud is to be set as reference. Select **Model 1** (complete statue) and click on **Glue Here Mesh**. With this, an asterisk appears next to the point cloud name.
2) Select **Model 2** and click on **Point Based Glueing**. The following window appears. In one side you have the reference point cloud. On the other side you have the moving point cloud. 
This stage is called Points Pair Picking: the idea is to roughly align both point clouds by manually defining homologous points (4 points are recommended).

foto modelli vicini

Points are picked by double clicking with the left mouse button. They can be all selected in one point cloud and then all selected in the other point cloud (by the same order), or we can select one point at each time on both point clouds. 
To remove a point do CTRL + double click with left mouse button. 
After the points are picked, click OK. You can change the view point whilst selecting the points.

At this moment you can see that both point clouds are roughly aligned. And another asterisk can be found next to the aligned point cloud.

After the initial alignment is done we will proceed to the final optimization by running the ICP (Iterative Closest Point). 
Pay attention to the DEFAULT ICP PARAMETERS. They are set in absolute units. So it is important to have an idea of the units you are using. Terrestrial Laser Scanning point clouds are usually in meters.
- The sample number means the number of homologous points that the software will try to find and use for the optimization.
- The minimal starting distance means the radius that will be used to find the homologous points in one point cloud starting with a set of points in the other point cloud.
- The target distance is an average alignment error value that the software will try to obtain from the process. With terrestrial laser scanning point clouds, this value should be small (0.005m at least).
- The Max Iteration Num is the maximum number of iterations that the software will perform.

The Rigid matching option should be selected if we are aligning point clouds that have the same scale. If we don’t select this option, a scale factor will be introduced in the final transformation matrix.

After clicking PROCESS, the ICP algorithm is launched and the results are shown in a log window.

mettere foto finale 

## Color Visualization



## Merge the Aligned Models

1) Once the alignment is complete, go to Filters > Mesh Layer > Flatten Visible Layers.
2) Ensure that both models are visible and selected in the layer panel.
3) Click Apply to merge the two aligned models into a single output model.

## Export the merged model

1) Go to File > Export Mesh As.
2) Choose the desired output format (PLY) and click Save.
3) Make sure to enable the options for saving vertex colors and normals if applicable.

## Acknoledgements
 
This project was developed to explore the potential of Gaussian Splatting techniques for cultural heritage preservation, as part of the project exam for the course [Augmented and Virtual Reality](https://corsi.unige.it/off.f/2023/ins/66562) during Master's degree in Computer Engineering - Artifical Intelligence at the University of Genova.
