Date: 2024-05-15
Time: 12:16
Tags:
Up: 

---
# StereoMatching

## Introduction


 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 1 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 2 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 3 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 4 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 5 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 6 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 7 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 8 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 9 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 10 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 11 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 12 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 13 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 14 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 15 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 16 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 17 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 18 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 19 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 20 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 21 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 22 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 23 
 scale: 0.8 
 ```

We need to resort on a sistem like this, where we have the image plane, find the epipolar line that are parallel. We have to calculate the displacement of one image to the other, since if we have a situation like this, there is no rotation of the two camera. 

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 24 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 25 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 26 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 27 
 scale: 0.8 
 ```

The difference between the two camera needs to be large enought. And the image needs to be warped.

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 28 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 29 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 30 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 31 
 scale: 0.8 
 ```

We need to rectify both images, like warping

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 32 
 scale: 0.8 
 ```
Not useful for exam

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 33 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 34 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 35 
 scale: 0.8 
 ```
The epipolar lines are now parallel
 
 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 36 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 37 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 38 
 scale: 0.8 
 ```
## Local Stereo Matching Algorithm

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 39 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 40 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 41 
 scale: 0.8 
 ```
THe dimention of the patch is important. The bleck values = is not possible to calcolulate the disparity, meaning that in the other image maybe that pasrt ther isnt. 

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 42 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 43 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 44 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 45 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 46 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 47 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 48 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 49 
 scale: 0.8 
 ```

Left right consistency, apply disparity from a to b, viceversa and then sum up togheter

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 50 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 51 
 scale: 0.8 
 ```

for each pixel we can say what is the match score? using the similarity matrix we choose. 

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 52 
 scale: 0.8 
 ```

using for each patches

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 53 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 54 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 55 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 56 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 57 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 58 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 59 
 scale: 0.8 
 ```
## Beyond local stereo matching

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 60 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 61 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 62 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 63 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 64 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 65 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 66 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 67 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 68 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 69 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 70 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 71 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 72 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 73 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 74 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 75 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 76 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 77 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 78 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 79 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 80 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 81 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 82 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 83 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 84 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 85 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 86 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 87 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 88 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 89 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 90 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 91 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 92 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 93 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 94 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 95 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 96 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 97 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 98 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 99 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 100 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 101 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 102 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 103 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 104 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 105 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 106 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 107 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 108 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 109 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 110 
 scale: 0.8 
 ```


** Process exited - Return Code: 0 **
Press Enter to exit terminal