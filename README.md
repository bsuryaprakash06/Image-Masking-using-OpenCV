# Image Masking using OpenCV

## Objective
The objective of this project is to demonstrate fundamental region-of-interest (ROI) extraction and image masking techniques using OpenCV and Python. By converting RGB images into single-channel grayscale representations, applying global binary thresholding, and utilizing bitwise logical operations, the workflow isolates specific geometric patterns and applies them as spatial masks onto target images.

## Algorithm / Approach
The masking pipeline consists of the following sequential processing stages:

1. **Image Preprocessing and Color Conversion**:
   - Load source images (`green_circle.PNG` and `yellow_square.PNG`) and convert them from BGR to RGB format for consistent color representation.
   - Convert the reference pattern image (`green_circle.PNG`) to a single-channel grayscale image using `cv2.cvtColor` with `cv2.COLOR_RGB2GRAY`.

2. **Binary Mask Generation**:
   - Segment the geometric ring structure from the background using global binary thresholding via `cv2.threshold` with `cv2.THRESH_BINARY` at a threshold value of 10.
   - Produce a binary mask where the ring region corresponds to white pixels (intensity 255) and the background corresponds to black pixels (intensity 0).

3. **Spatial Resizing and Inversion**:
   - Resize the generated binary mask using `cv2.resize` to match the target dimensions of `yellow_square.PNG` (345x351).
   - Invert the binary mask using `cv2.bitwise_not`, flipping values so that the ring region becomes 0 (black) and surrounding pixels become 255 (white).

4. **Mask Application via Bitwise Operations**:
   - Perform a bitwise AND operation (`cv2.bitwise_and`) on the destination image (`yellow_square.PNG`) using the inverted mask.
   - Preserve pixel intensities where the mask is non-zero while zeroing out (blacking out) pixels corresponding to the masked ring region.

## Results
The experiment evaluates each stage of the masking pipeline through visual outputs:

- **Source Images**: `yellow_square.PNG` (345x351 RGB solid yellow image) and `green_circle.PNG` (640x640 RGB image containing a bright green circular ring).
- **Intermediate Outputs**:
  - Grayscale conversion showing intensity variations of the circular feature.
  - Binary mask isolating the circular ring geometry as white pixels against a black background.
  - Inverted binary mask presenting the ring as black pixels against a white background.
- **Final Combined Result**: A composite image showing the yellow square background with the circular ring region cleanly masked out in solid black.

## References
- OpenCV Documentation: [Image Processing (imgproc module)](https://docs.opencv.org/4.x/d7/da8/tutorial_table_of_content_imgproc.html)
- OpenCV Documentation: [Arithmetic Operations on Images and Bitwise Operations](https://docs.opencv.org/4.x/d0/d86/tutorial_py_image_arithmetics.html)
- Bradski, G., & Kaehler, A. (2008). *Learning OpenCV: Computer Vision with the OpenCV Library*. O'Reilly Media.
