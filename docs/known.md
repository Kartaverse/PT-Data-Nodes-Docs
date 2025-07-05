# Known Issues

## Texture2D Node

If you want to connect the output from a "ptImage" or "ptmask" node to Fusion's 3D system, you have to pass the image data through a "Texture2D" node before connecting the image data to an image plane or mesh. If you don't use a Texture2D node as an intermediate step you will get an instant lockup in Fusion when you view the mesh with the texture map applied.

## STMap Creation

You need to have a copy of PTGui Pro v11-13+ if you wish to use the ptSTMap and ptBatchStitcher nodes to create a set of STMap based warping template images.

The regular PTGui (non pro) version is unable to save out HDR (High Dynamic Range) images.
