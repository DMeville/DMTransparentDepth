- Add a "DMCustomDepthFeature" to your forward renderer asset
- Choose or create a new layer, I'm using the built in "Water" layer.
- Make sure on the Filtering>Opaque Layer Mask, and Filtering>Transparent Layer Mask, this layer is DESELECTED.  We do not want to render anything in this layer by default, as it's handled by our custom rener feature
- Take a look at the "SampleScene.unity" secene.  We have a "water" object, that has two children.  One called "Depth" that is set to the "Water" layer.  This object does not get rendered at all, execpt to our custom depth buffer so it will not be visible in the scene.  We also have our second object "Surface", this is on any other layer, and is rendered like normal.  This object has a TRANSPARENT, ZWRITE OFF shader, so depth blend is done like normal on this material.

In our custom render feature we render out the extra water depth, so we have to combine this together with the no-water depth.  We do this in shader.  See the "CustomDepthVisualization" shader.

Anywhere you want to sample depth that INCLUDES the water depths, you must rewrite any depth method to use max(customdepth, cameradepth). As this is dependant on your usecase, nothing is included to do this and you'll have to write the modified depth functions yourself (or DM me @DMeville on twitter/discord)

GOOD LUCK