# rgbdrecon
This code adds an RGB-D data reader interface into the [Voxel-hashing](https://github.com/niessner/VoxelHashing) code, one of the famous Real-time RGBD Reconstruction platform. The code can take local RGB-D data as input such as [TUM RGB-D dataset](https://vision.in.tum.de/data/datasets/rgbd-dataset).

## Use depth sensor
In **zParametersDefault.txt**:
- `s_sensorIdx` : the corresponding sensor type index.

In **zParametersCameraPoseOpt.txt**:
- `s_bReadRGBData = false`.

## Use RGBD data from local file
In **zParametersDefault.txt**:
- `s_sensorIdx = 0`.
- `s_adapterWidth, s_adapterHeight`: the adapter resolution. The Voxel-hashing code uses adapter resolution for both depth and color image data. If the input color or depth image has different resolution, the code will uniformly sample pixels from input images to fit the adapter resolution. So, if the the input color or depth image has same resolution, just use it to set adapter resolution. Otherwise, use the smaller resolution between the two images, or simply use `640x480`.

In **zParametersCameraPoseOpt.txt**:
- `s_bReadRGBData = true`;
- `s_uDepthScaleFactor = 5000`. This is the depth scale factor and 5000 by default for TUM RGB-D data.
- `s_uRGBDataType`: the RGBD data type. Even though the RGBD data use the same format of RGB and depth images, we have a correction for the ICL-NUIM original trajectories since it is originally generated by a negative fy = -480.0, which will result in a inverse-y-coordinate upside-down model after reconstruction. So in order to generate a valid result mesh, we make some correction on each trajectory in the code to enable the consistency.
- `s_fx, s_fy, s_cx, s_cy`: camera calibration matrix parameters.
- `s_strDataPath, s_strTrajFile, s_strAssociationFile`: the relevant RGB-D data path. Note that the code needs an association file containing corrrespondence between color and depth images. See [TUM RGB-D dataset](https://vision.in.tum.de/data/datasets/rgbd-dataset) for details. 
- `s_depthWidth, s_depthHeight, s_colorWidth, s_colorHeight`: color and depth image resolution.
