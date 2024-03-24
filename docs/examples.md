# PT Data Node Example Comps

The Kartaverse "PT Data Nodes" allow you to access PTGui Pro v11-12 based .pts (JSON) 360VR stitching project files in Fusion using parametric node-based operators.

Listed on this page are the bundled example Fusion .comps that show basic PTGui .pts project file driven nodal workflow concepts.

These files are located on disk in the Reactor PathMap based folder:

        Reactor:/Deploy/Comps/Kartaverse/PT/Demo PT/

## Demo PT Output Image v001.comp

Read a PTGui .pts JSON file and load the final rendered panorama image that is referenced in the PTGui document.

![ptOutputImage Example 1](images/comp-Demo-PT-Output-Image.png)

## Demo PT Batch Stitcher v001

Send the currently open .pts document to the PTGui Pro batch stitcher for processing.

![ptBatchStitcher Example 1](images/comp-Demo-PT-Batch-Stitcher-1.png)

![ptBatchStitcher Example 1](images/comp-Demo-PT-Batch-Stitcher-2.png)

## Demo PT CSV Output v001.comp

Read a PTGui .pts JSON file and export a CSV spreadsheet

![ptCSV Example 1](images/comp-Demo-PT-CSV-Output-1.png)

![ptCSV Example 2](images/comp-Demo-PT-CSV-Output-2.png)

## Demo PT FBX Camera v001.comp

Read a PTGui .pts JSON file and create a 3D camera by extracting the camera rotation values, focal length, and source image names. The animated camera is then exported to an FBX file that can be loaded into other 3D packages.

![ptRotation Example 1](images/comp-Demo-PT-FBX-Camera.png)

## Demo PT Generate IFL v001.comp

Read a PTGui .pts JSON file and create a new IFL (Image File List) text file by extracting all of the source image filenames.

![ptImageFilename1 Example 1](images/comp-Demo-PT-Generate-IFL-1.png)

![ptImageFilename1 Example 2](images/comp-Demo-PT-Generate-IFL-2.png)

## Demo PT Load Images v001.comp

Read a PTGui .pts JSON file and load all of the source images.

![ptImage Example 1](images/comp-Demo-PT-Load-Images-1.png)

![ptImage Example 2](images/comp-Demo-PT-Load-Images-2.png)

## Demo PT Mask v001.comp

Read a PTGui .pts JSON file and apply the exclude region masking data to a source image. The masking data is applied to the source image using a MatteControl node.

![ptMask Example 1](images/comp-Demo-PT-Mask-1.png)

![ptMask Example 2](images/comp-Demo-PT-Mask-2.png)

![ptMask Example 2](images/comp-Demo-PT-Mask-3.jpg)

## Demo PT Optimal Output Image Size v001.comp

Read a PTGui .pts JSON file and calculate the optimal 360° panoramic output size based on the source image dimensions and the lens focal length.

![ptOptimumOutputSize Example 1](images/comp-Demo-PT-Optimal-Output-Image-Size-1.png)

![ptOptimumOutputSize Example 2](images/comp-Demo-PT-Optimal-Output-Image-Size-2.png)

