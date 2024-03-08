# PT Data Node Fuses

The Kartaverse "PT Data Nodes" allow you to access PTGui Pro v11-12 based .pts (JSON) 360VR stitching project files in Fusion using parametric node-based operators.

## Flow

### ptSwitch

The "ptSwitch" node allows you to toggle between several different ScriptVal based input connections to select which data stream you want to access.

![ptSwitch](images/fuse-ptSwitch.png)

The "Which" control on the ptSwitch node is used to select the current input connection you would like to access ScriptVal data from.


#### Comparing Multiple PTGui Files

A common use case for the ptSwitch node would be to allow you to have multiple ptLoder nodes in your comp at the same time. Each ptLoader node would be pointed at a specific .pts file that has slightly different settings. 

You can then change the ptSwitch node's "Which" control to cycle through the different PTGui .pts files quickly to compare the results in a consistent and organized fashion.

![ptSwitch Tip 1](images/tip-ptSwitch-1.png)

### ptWireless

The ptWireless node allows you to create links between nodes without displaying a wireline connection in the node graph. This can help make a complex comp tidy if there are wires crossing all over the place.

![ptWireless](images/fuse-ptWireless.png)

The Wireless link connection is created by holding down the middle mouse button, while dragging the node from the node graph into the Inspector window where the ptWireless node "Input" attribute is. The name of the connected node will be written into the text field.

Typical Node Connections:

        ptLoader > ptWireless > ptRotation > Camera3D

or 

        ptLoader > ptWireless > ptMask

or

        ptLoader > ptWireless > ptImage

![ptWireless Tip 1](images/tip-ptWireless-1.png)

## Image

### ptImage

A "ptImage" node accesses the source images referenced in the .pts file.  The output is an image datatype.

![ptImage](images/fuse-ptImage.png)

The "Index" control allows you to cycle through each of the source images. If you move the Index control past the number of source images found in the .pts file it will hold on to the last image.

Typical Node Connections:

        ptLoader > ptImage > ColorCorrector


![ptImage Tip 1](images/tip-ptImage-1.png)

#### Image Sequence Handling

If the source image defined in the PTGui file is one frame from a longer image sequence, the "Time" control allows you to increment through subsequent images in the image sequence.

Image Sequence Filename Example:

        CameraA.[0001-0144].jpg

### ptOutputImage

The "ptOutputImage" node loads the final rendered panorama image that is referenced in the PTGui document. The output is an image datatype.


![ptOutputImage](images/fuse-ptOutputImage.png)

Note: This node requires that the PTGui .pts was saved with the "Create Panorama > Output File > [x] Use Default" checkbox disabled. This means you defined the image filename manually in the "Output File" textfield that will be used when a newly stitched panorama is saved to disk.


![ptOutputImage Tip 1](images/tip-ptOutputImage-1.png)

In the PTGui "Create Panorama" tab it is possible to define sub-folders you would like a rendered image to be placed within by adding a folder name and a slash before the filename entered in the "Output File" text field:

        Render/Output.jpg


## IO

### ptLoader

A "ptLoader" node imports an existing PTGui .pts file from disk. The output from the ptLoader node is a Fusion ScriptVal data type that stores the PTGui information inside a Lua table structure that can be read by other nodes.

![ptLoader](images/fuse-ptLoader.png)

This node supports the use of Fusion "PathMaps". This allows short form values like "Comp:/" to be used when you want to define a .pts file as being located in the same based folder as the Fusion Studio .comp file.

### ptSaver

A "ptSaver" node exports the Fusion ScriptVal content back to a JSON file. 

![ptSaver](images/fuse-ptSaver.png)

This node supports the use of Fusion "PathMaps". This allows short form values like "Comp:/" to be used when you want to define a .pts file as being located in the same based folder as the Fusion Studio .comp file.

Note: PTGui is very picky about the .pts based JSON files it is willing to load. The ordering of elements and the structure of the file is very important. The ptSaver node at this time does not meet PTGui's file opening JSON standards for formatting.


## Mask

### ptMask

A "ptMask" node accesses the hand painted masking data stored in the .pts file. The output is an image datatype.

![ptMask](images/fuse-ptMask.png)

The "Asset Mode" control can be set to "Image ID" or "Mask ID".

When the "Image ID" mode is used you are accessing the masks based on the index number of the source images defined in the .pts file.

When the "Mask ID" mode is used you are accessing the masks based on the index number of the individual mask assets stored in the .pts file.

Typical Node Connections:

        ptLoader > ptMask1

#### Applying a PTGui Red Exclude Mask to an Image

The masking information from the ptMask node can be fed into a MatteControl node.

If you want to extract the "red" exclude masking information, use a Garbage Matte input connection with a "Garbage Matte > Channel: Red" setting to apply the PTGui "exclude" red matte information to your footage.

![ptMask Tip 1](images/tip-ptMask-MatteControl-1.png)

![ptMask Tip 2](images/tip-ptMask-MatteControl-2.png)

Typical Masking Connections:

        ptLoader.ScriptVal > ptMask1.ScriptVal
        ptMask1.Output > MatteControl.Garbage.Matte
        ptLoader.ScriptVal > ptImage.ScriptVal
        ptImage.Output > MatteControl.Background

## Matrix

### ptMatrix

The "ptMatrix" node allows you to send the XYZ rotation values for each PTGui source image to a Vonk Ultra 4x4 transform matrix.

![ptMatrix](images/fuse-ptMatrix.png)

The Vonk Ultra vMatrix nodes allow you to perform matrix math like addition, subtraction, and multiplication. This allows you to offset the position of the images on the fly.

Typical Node Connections:

        ptLoader > ptMatrix > vMatrixToRotation > Camera3D

### ptRotation

The "ptRotation" node allows you to directly access the XYZ rotation values for each PTGui source image. This rotation data can be used to rotate a Camera3D node.

![ptRotation](images/fuse-ptRotation.png)

Typical Node Connections:

        ptLoader > ptRotation > Camera3D

## Number

### ptFocalLength

The "ptFocalLength" node allows you to read the focal length value (in millimetres) for each of the lenses in the PTGui file. This can be used to drive the focal length on a Camera3D node.

The output is a number datatype.

![ptFocalLength](images/fuse-ptFocalLength.png)

The focal length value output by this node can also be used with the "ptOptimumOutputSize" node.

Typical Node Connections:

        ptLoader > ptFocalLength

### ptImageCount

The "ptImageCount" node returns the total number of source images in a PTGui .pts document.  The output is a number datatype.

![ptImageCount](images/fuse-ptImageCount.png)

Typical Node Connections:

        ptLoader > ptImageCount

### ptImageSize

The "ptImageSize" node returns the image width and image height parameters for a PTGui .pts source image. The output is a pair of number datatypes.

![ptImageSize](images/fuse-ptImageSize.png)

Typical Node Connections:

        ptLoader > ptImageSize

### ptLensCount

The "ptLensCount" node calculates the total number of PTGui Global Lens entries. The output is a number datatype.

![ptLensCount](images/fuse-ptLensCount.png)

Typical Node Connections:

        ptLoader > ptLensCount


## Point




## Text

### ptImageFilename


The "ptImageFilename" node returns the source image filename that PTGui uses when loading an image from the .pts file. The output is a string datatype.

![ptImageFilename](images/fuse-ptImageFilename.png)

If you enable the checkbox "Use .pts Parent Directory" then the relative filepath for the image filename will be expanded to an absolute filepath.

Typical Node Connections:

        ptLoader > ptImageFilename > vTextViewer

### ptOutputFilename

The "ptOutputFilename" node returns the filename that PTGui will use when saving a stitched panorama to disk. The output is a string datatype.

![ptOutputFilename](images/fuse-ptOutputFilename.png)

This information is based upon the value saved in the .pts file using the content defined in the PTGui "Create Panorama > Output file:" user interface control. This field can sometimes be empty.

If you enable the checkbox "Use .pts Parent Directory" then the relative filepath for the image filename will be expanded to an absolute filepath.

Typical Node Connections:

        ptLoader > ptOutputFilename > vTextViewer

## Utility

### ptInfo

The "ptInfo" node peeks into the contents of the live PTGui data stream. This is a handy diagnostic tool. The ptInfo input and output connections are ScriptVal datatypes.

![ptInfo](images/fuse-ptInfo.png)

Typical Node Connections:

        ptLoader > ptInfo

### ptOptimumOutputSize

This node allows you to calculate the best output size to use when stitching a 360VR panorama. This calculation is based upon the focal length (in mm), image sensor size (in mm), and the source image size (in pixels).

The output is a number datatype that represents the idea LatLong image width in pixels.

The formula used for the optimum panoramic output size comes from the following PTGui documentation topics:  
[How does PTGui calculate the optimum output size of a panorama?](https://ptgui.com/support.html#3_26)

![ptOptimumOutputSize](images/fuse-ptOptimumOutputSize.png)

![ptOptimumOutputSize Tip 1](images/tip-ptOptimumOutputSize-1.png)

Typical Node Connections:

        ptLoader > ptFocalLength.Output > ptOptimumOutputSize.FocalLength
        ptLoader > ptImageSize.Width > ptOptimumOutputSize.ImageWidth
        vNumberCompReqTime > ptImageSize.Index

