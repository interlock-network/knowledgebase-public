# Visual Blockhash

A visual blockhash is a [visual threat indicator](./visual-threat-indicator.md).
It segments an image into blocks (rectangles) and averages out the color values,
effectively blurring the image. It is the primary way in which [our extension](./interlock-extension.md)
identifies threats. If two images are basically the same, but they differ in
some subtle way (i.e. transparent background, vs non-transparent background)
the blockhash blurs them enough so that they look the same. This is less
effective for tiny images (i.e. 16x16 images).

#threat-detection