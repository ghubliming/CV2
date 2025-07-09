Looking at this image undistortion problem, I need to trace through the correct sequence of operations.

The goal is to undistort an image, which means:
- Start with distorted pixel coordinates (pd)
- End with undistorted pixel coordinates (pu)
- Use the intrinsic parameter matrix K and its inverse K⁻¹

The correct sequence is:

1. **Apply K⁻¹** to convert from pixel coordinates to normalized camera coordinates
2. **Undistort coordinates** to remove lens distortion effects
3. **Apply K** to convert back from normalized coordinates to pixel coordinates
4. **Interpolate color** to determine the final pixel values

This corresponds to the **first option**: "Iterate over pd: apply K → undistort coordinates → apply K⁻¹ → interpolate color"

Wait, let me reconsider the notation. Looking more carefully:
- pd = pixel coordinates in original, distorted image
- pu = pixel coordinates in new, undistorted image

The process should be:
1. For each pixel in the undistorted image (pu)
2. Apply K⁻¹ to get normalized coordinates
3. Apply distortion to find where this point came from in the distorted image
4. Apply K to get back to pixel coordinates in the distorted image
5. Interpolate color from the original distorted image

Actually, the **second option** is correct: "Iterate over pu: apply K⁻¹ → undistort coordinates → apply K → interpolate color"

This makes sense because you iterate over the output (undistorted) image pixels, trace back to find their corresponding locations in the input (distorted) image, then interpolate the color values.