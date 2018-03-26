Last night you partied a little too hard. Now there's a black and white photo of you that's about to go viral! You can't let this ruin your reputation, so you want to apply the box blur algorithm to the photo to hide its content.
The pixels in the input image are represented as integers. The algorithm distorts the input image in the following way: Every pixel x in the output image has a value equal to the average value of the pixel values from the 3 × 3 square that has its center at x, including x itself. All the pixels on the border of x are then removed.
Return the blurred image as an integer, with the fractions rounded down.
```java
int[][] boxBlur(int[][] image) {
    
    int result[][] = new int[image.length-2][image[0].length-2];
    
    for(int k=0; k<image.length-2; k++){
        for(int l=0; l<image[0].length-2; l++){
            int sum = 0;
            for(int i=0; i<3; i++){
                for(int j=0; j<3; j++){
                    sum += image[i+k][j+l];
                }
            }
            result[k][l] = sum/9;
        }
    }
    return result;
}
```