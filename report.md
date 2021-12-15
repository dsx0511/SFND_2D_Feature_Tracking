# Mid-term Report

## MP.1 Data Buffer Optimization
First, the new element is pushed in on the end of the `std::vector` data buffer.
After that, the length of the data buffer is checked.
If the length is greater than the pre-defined data buffer size (2 here), the oldest element is removed using `std::vector::erase`.

## MP.2 Keypoint Detection
All the keypoints are built-in functions in Opencv.
The Harris keypoint detection with NMS is implemented in the function `detKeypointsHarris` similar to the one in the exercise.
An instance of other detectors with the type `cv::Ptr<cv::FeatureDetector> ` can be created using `cv::(name)::create`, where `(name)` corresponds to the name of the keypoint detector.
Thus they are called in the function `detKeypointsModern` by selecting them using their name.

## MP.3 Keypoint Removal
The pre-defined area is represented as `cv::Rect`.
The keypoints are removed if `cv::Rect::contain` returns `false`.

## MP.4 Keypoint Descriptors
All the keypoint descriptors are built-in functions in Opencv.
They are selectable in the function `descKeypoints` by comparing the name string.
Similar to the keypoint detectors, all the keypoint descriptors can be created using `cv::(name)::create` which returns a `cv::Ptr<cv::DescriptorExtractor>` instance based on the name of descriptor.

## MP.5 Descriptor Matching
Both FLANN matching and k-nearest neighbor selection are built-in function in opencv.
They are implemented in the function `matchDescriptors` and can be called by setting `matcherType` to `MAT_FLANN` and setting `selectorType` to `SEL_KNN`.

## MP.6 Descriptor Distance Ratio
The descriptor distance ratio is implemented in the same way in the exercise.
It compares the distance between best and second-best matchings.
If the distance ratio between both matchings is below a threshold (0.8 here), the best matching is kept.

## MP.7 Performance Evaluation 1
### number of keypoints on the preceding vehicle:
| Frame | SHITOMASI | HARRIS | FAST | BRISK | ORB | AKAZE | SIFT |
| :---: | :-------: | ------ | ---- | ----- | --- | ----- | ---- |
| 1     | 125       | 17     | 419  | 264   | 92  | 166   | 138  |
| 2     | 118       | 14     | 427  | 282   | 102 | 157   | 132  |
| 3     | 123       | 18     | 404  | 282   | 106 | 161   | 124  |
| 4     | 120       | 21     | 423  | 277   | 113 | 155   | 138  |
| 5     | 120       | 26     | 386  | 297   | 109 | 163   | 134  |
| 6     | 113       | 43     | 414  | 279   | 125 | 164   | 140  |
| 7     | 114       | 18     | 418  | 289   | 130 | 173   | 137  |
| 8     | 123       | 31     | 406  | 272   | 129 | 175   | 148  |
| 9     | 111       | 26     | 396  | 266   | 127 | 177   | 159  |
| 20    | 112       | 34     | 401  | 254   | 128 | 179   | 137  |

### Distribution of their neighborhood size (represented as "mean &#177; variance" in each cell):
|  <i></i>  | SHITOMASI  | HARRIS     | FAST       | BRISK              | ORB                | AKAZE            | SIFT             |
|  :-----:  | :-------:  | ------     | ----       | -----              | ---                | -----            | ----             |
| 1         | 4 &#177; 0 | 6 &#177; 0 | 7 &#177; 0 | 21.11 &#177; 14.64 | 56.78 &#177; 25.69 | 7.20 &#177; 4.09 | 4.54 &#177; 5.87 | 
| 2         | 4 &#177; 0 | 6 &#177; 0 | 7 &#177; 0 | 21.35 &#177; 14.62 | 56.94 &#177; 26.08 | 6.96 &#177; 3.69 | 4.62 &#177; 6.16 | 
| 3         | 4 &#177; 0 | 6 &#177; 0 | 7 &#177; 0 | 21.20 &#177; 13.87 | 56.22 &#177; 25.89 | 6.91 &#177; 3.72 | 4.46 &#177; 6.01 | 
| 4         | 4 &#177; 0 | 6 &#177; 0 | 7 &#177; 0 | 19.93 &#177; 12.66 | 54.85 &#177; 25.06 | 7.05 &#177; 3.64 | 4.22 &#177; 5.29 | 
| 5         | 4 &#177; 0 | 6 &#177; 0 | 7 &#177; 0 | 22.18 &#177; 14.93 | 56.45 &#177; 24.99 | 7.23 &#177; 3.62 | 4.21 &#177; 5.56 | 
| 6         | 4 &#177; 0 | 6 &#177; 0 | 7 &#177; 0 | 22.52 &#177; 15.90 | 56.32 &#177; 24.41 | 7.18 &#177; 3.56 | 4.15 &#177; 5.60 | 
| 7         | 4 &#177; 0 | 6 &#177; 0 | 7 &#177; 0 | 21.38 &#177; 14.76 | 56.48 &#177; 25.40 | 7.24 &#177; 3.62 | 4.86 &#177; 6.51 | 
| 8         | 4 &#177; 0 | 6 &#177; 0 | 7 &#177; 0 | 21.71 &#177; 15.12 | 55.15 &#177; 25.71 | 7.33 &#177; 3.70 | 4.02 &#177; 5.17 | 
| 9         | 4 &#177; 0 | 6 &#177; 0 | 7 &#177; 0 | 22.11 &#177; 15.25 | 54.40 &#177; 25.23 | 7.32 &#177; 3.68 | 4.96 &#177; 6.76 | 
| 10        | 4 &#177; 0 | 6 &#177; 0 | 7 &#177; 0 | 21.59 &#177; 14.72 | 54.09 &#177; 23.64 | 7.40 &#177; 3.77 | 5.09 &#177; 6.67 | 


## MP.8 Performance Evaluation 2

### Number of matched keypoints 
For each keypoint descriptor, the numbers of matched keypoints of every keypoint detector for all 10 frames are shown in a table.

* BRISK descriptor
    | Keypoints | 1-2 | 2-3 | 3-4 | 4-5 | 5-6 | 6-7 | 7-8 | 8-9 | 9-10 |
    | :---:     | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-:  |
    | SHITOMASI |  95 |  88 |  80 |  90 |  82 |  79 |  85 |  86 |  82  |
    | HARRIS    |  12 |  10 |  14 |  15 |  16 |  16 |  15 |  23 |  21  |
    | FAST      | 256 | 243 | 241 | 239 | 215 | 251 | 248 | 243 |  247 |
    | BRISK     | 171 | 176 | 157 | 176 | 174 | 188 | 173 | 171 |  184 |
    | ORB       |  73 |  74 |  79 |  85 |  79 |  92 |  90 |  88 |  91  |
    | AKAZE     | 137 | 125 | 129 | 129 | 131 | 132 | 142 | 146 |  144 |
    | SIFT      |  64 |  66 |  63 |  67 |  59 |  64 |  64 |  67 |  80  |

* BRIEF descriptor
    | Keypoints | 1-2 | 2-3 | 3-4 | 4-5 | 5-6 | 6-7 | 7-8 | 8-9 | 9-10 |
    | :---:     | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-:  |
    | SHITOMASI | 115 | 111 | 104 | 101 | 102 | 102 | 100 | 109 |  100 |
    | HARRIS    |  14 |  11 |  15 |  20 |  24 |  26 |  16 |  24 |  23  |
    | FAST      | 320 | 332 | 299 | 331 | 276 | 327 | 324 | 315 |  307 |
    | BRISK     | 178 | 205 | 185 | 179 | 183 | 195 | 207 | 189 |  183 |
    | ORB       |  49 |  43 |  45 |  59 |  53 |  78 |  68 |  84 |  66  |
    | AKAZE     | 141 | 134 | 131 | 130 | 134 | 146 | 150 | 148 |  152 |
    | SIFT      |  86 |  78 |  77 |  86 |  69 |  74 |  76 |  70 |  88  |

* ORB descriptor (ORB doesn't work with SIFT keypoint detctor.)
    | Keypoints | 1-2 | 2-3 | 3-4 | 4-5 | 5-6 | 6-7 | 7-8 | 8-9 | 9-10 |
    | :---:     | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-:  |
    | SHITOMASI | 106 | 102 |  99 | 102 | 103 |  97 |  98 | 104 |  97  |
    | HARRIS    |  12 |  12 |  15 |  18 |  24 |  20 |  15 |  24 |  22  |
    | FAST      | 307 | 308 | 298 | 321 | 283 | 315 | 323 | 302 |  311 |
    | BRISK     | 162 | 175 | 158 | 167 | 160 | 182 | 167 | 171 |  172 |
    | ORB       |  67 |  70 |  72 |  84 |  91 | 101 |  92 |  93 |  93  |
    | AKAZE     | 131 | 129 | 127 | 117 | 130 | 131 | 137 | 135 |  145 |
    | SIFT      |

* FREAK descriptor
    | Keypoints | 1-2 | 2-3 | 3-4 | 4-5 | 5-6 | 6-7 | 7-8 | 8-9 | 9-10 |
    | :---:     | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-:  |
    | SHITOMASI |  86 |  90 |  86 |  88 |  86 |  80 |  81 |  86 |  85  |
    | HARRIS    |  13 |  13 |  15 |  15 |  17 |  20 |  12 |  21 |  18  |
    | FAST      | 251 | 247 | 233 | 255 | 231 | 265 | 251 | 253 |  247 |
    | BRISK     | 160 | 177 | 155 | 173 | 161 | 183 | 169 | 178 |  168 |
    | ORB       |  42 |  36 |  44 |  47 |  44 |  51 |  52 |  48 |  56  |
    | AKAZE     | 126 | 129 | 127 | 121 | 122 | 133 | 144 | 147 |  138 |
    | SIFT      |  65 |  72 |  65 |  67 |  59 |  59 |  64 |  65 |  79  |

* AKAZE descriptor (AKAZE only works with AKAZE keypoint detector.)
    | Keypoints | 1-2 | 2-3 | 3-4 | 4-5 | 5-6 | 6-7 | 7-8 | 8-9 | 9-10 |
    | :---:     | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-:  |
    | AKAZE     | 138 | 138 | 133 | 127 | 129 | 146 | 147 | 151 |  150 |

* SIFT descriptor
    | Keypoints | 1-2 | 2-3 | 3-4 | 4-5 | 5-6 | 6-7 | 7-8 | 8-9 | 9-10 |
    | :---:     | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-:  |
    | SHITOMASI | 112 | 109 | 104 | 103 |  99 | 101 |  96 | 106 |  97  |
    | HARRIS    |  14 |  11 |  16 |  19 |  22 |  22 |  13 |  24 |  22  |
    | FAST      | 316 | 325 | 297 | 311 | 291 | 326 | 315 | 300 |  301 |
    | BRISK     | 182 | 193 | 169 | 183 | 171 | 195 | 194 | 176 |  183 |
    | ORB       |  67 |  79 |  78 |  79 |  82 |  95 |  95 |  94 |  94  |
    | AKAZE     | 134 | 134 | 130 | 136 | 137 | 147 | 147 | 154 |  151 |
    | SIFT      |  82 |  81 |  86 |  94 |  90 |  81 |  82 | 102 |  104 |


## MP.9 Performance Evaluation 3

### Runtime of keypoint detectors
| Types     | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| :---:     | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-:  | :-:  |
| SHITOMASI | 12.49 | 8.51 | 9.46 | 29.98 | 13.35 | 13.55 | 14.62 | 17.57 | 17.80 | 17.50 | 
| HARRIS    | 10.69 | 9.92 | 10.95 | 27.92 | 25.07 | 15.21 | 8.07 | 9.87 | 8.85 | 10.11 | 
| FAST      | 2.06 | 1.63 | 1.45 | 1.52 | 1.71 | 1.57 | 1.45 | 1.31 | 1.61 | 1.40 |  
| BRISK     | 26.72 | 26.19 | 25.87 | 26.61 | 29.02 | 25.57 | 26.78 | 25.08 | 25.47 | 26.48 |
| ORB       | 85.14 | 4.78 | 4.73 | 4.91 | 9.18 | 9.54 | 10.35 | 8.86 | 9.11 | 9.67 |
| AKAZE     | 40.82 | 34.47 | 38.73 | 38.56 | 37.27 | 35.69 | 34.07 | 54.34 | 32.35 | 33.35 |
| SIFT      | 54.07 | 47.43 | 42.96 | 40.61 | 42.54 | 37.79 | 40.67 | 63.91 | 40.76 | 37.09 | 

### Runtime of keypoint descriptors in combination of every keypoint detector 
* BRISK descriptor
    | Keypoints | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
    | :---:     | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-:  | :-:  |
    | SHITOMASI |  1.34 |  1.24 |  1.24 |  1.2 |  0.966 |  0.918 |  0.928 |  1.04 |  0.892 |  0.917 |
    | HARRIS    |  0.306 |  0.255 |  0.28 |  0.297 |  0.338 |  0.45 |  0.282 |  0.375 |  0.334 |  0.402 |
    | FAST      |  3.2 |  3.22 |  3.07 |  2.99 |  2.65 |  3.96 |  2.96 |  2.75 |  2.72 |  2.73 |
    | BRISK     |  2.3 |  2.19 |  2 |  2.05 |  2.15 |  2 |  2.1 |  1.98 |  2 |  2.09 |
    | ORB       |  1.08 |  0.855 |  0.845 |  0.953 |  0.955 |  1.07 |  1.03 |  1.05 |  1.02 |  1.05 |
    | AKAZE     |  1.41 |  1.2 |  1.19 |  1.21 |  1.29 |  1.2 |  1.68 |  1.32 |  1.33 |  1.34 |
    | SIFT      |  1.08 |  1.02 |  0.982 |  1.04 |  1.14 |  1.05 |  1.07 |  1.13 |  1.27 |  1.18 |

* BRIEF descriptor
    | Keypoints | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
    | :---:     | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-:  | :-:  |
    | SHITOMASI |  0.74 |  0.732 |  0.474 |  0.475 |  0.617 |  0.656 |  0.486 |  0.617 |  0.678 |  0.429 |
    | HARRIS    |  0.171 |  0.311 |  0.243 |  0.632 |  0.769 |  0.381 |  0.208 |  0.42 |  0.317 |  0.78 |
    | FAST      |  1.5 |  1.31 |  1.22 |  1.07 |  1.47 |  1.64 |  1.25 |  1.12 |  1.05 |  1.04 |
    | BRISK     |  1.15 |  0.767 |  0.833 |  0.846 |  0.978 |  0.806 |  0.936 |  0.787 |  0.84 |  0.902 |
    | ORB       |  0.618 |  0.434 |  0.367 |  0.559 |  0.85 |  0.784 |  0.901 |  0.871 |  0.864 |  0.897 |
    | AKAZE     |  0.604 |  0.622 |  0.681 |  0.575 |  0.839 |  0.745 |  0.658 |  0.753 |  0.597 |  0.545 |
    | SIFT      |  0.634 |  0.478 |  0.606 |  0.537 |  0.55 |  0.558 |  0.553 |  0.466 |  0.602 |  0.85 |

* ORB descriptor
    | Keypoints | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
    | :---:     | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-:  | :-:  |
    | SHITOMASI |  0.752 |  0.792 |  0.815 |  0.764 |  0.769 |  0.888 |  0.9 |  0.821 |  1 |  0.805 |
    | HARRIS    |  1.05 |  1.11 |  0.657 |  0.954 |  1.05 |  0.786 |  1.18 |  1.08 |  0.894 |  0.92 |
    | FAST      |  1.4 |  1.21 |  1.09 |  1.25 |  1.28 |  1.01 |  1.22 |  1.05 |  1.13 |  1.07 |
    | BRISK     |  3.92 |  2.96 |  3.57 |  3.82 |  3.44 |  3.11 |  4 |  3.45 |  3.08 |  3.04 |
    | ORB       |  5.13 |  3.04 |  3.3 |  3.45 |  6.25 |  3.18 |  3.18 |  4.47 |  3.88 |  7.83 |
    | AKAZE     |  3.73 |  2.16 |  2.03 |  2.63 |  2.12 |  1.97 |  2.06 |  2.2 |  2.15 |  2.09 |
    | SIFT      |

* FREAK descriptor
    | Keypoints | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
    | :---:     | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-:  | :-:  |
    | SHITOMASI |  28.6 |  27.1 |  26.5 |  27.5 |  26.2 |  26.6 |  26.3 |  26.1 |  26.3 |  26.6 |
    | HARRIS    |  31.1 |  27.2 |  24.9 |  33.5 |  30.9 |  26.9 |  32.3 |  31.2 |  31.7 |  27.3 |
    | FAST      |  27.7 |  28 |  31.6 |  26.8 |  27.9 |  27 |  26.9 |  26.3 |  26.2 |  26 |
    | BRISK     |  29.9 |  27.1 |  27 |  26.4 |  28.1 |  26.8 |  26.7 |  26.3 |  26 |  26.7 |
    | ORB       |  26.7 |  26.5 |  26.1 |  24.9 |  33.7 |  37.1 |  39.7 |  33.2 |  33.2 |  34.1 |
    | AKAZE     |  27.7 |  29.3 |  25.4 |  27.5 |  27.5 |  26.1 |  27.9 |  26.2 |  26.4 |  27.3 |
    | SIFT      |  27.5 |  25.3 |  26.2 |  24.9 |  25.1 |  25.3 |  25 |  28.6 |  25.3 |  24.8 |

* AKAZE descriptor
    | Keypoints | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
    | :---:     | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-:  | :-:  |
    | AKAZE     |  28.4 |  28.7 |  29.8 |  27 |  28.5 |  27.5 |  30.1 |  25.7 |  27 |  27 |

* SIFT descriptor
    | Keypoints | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
    | :---:     | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-:  | :-:  |
    | SHITOMASI |  10.7 |  8.66 |  7.34 |  7.72 |  8.55 |  8.71 |  7.99 |  8.96 |  8.34 |  7.94 |
    | HARRIS    |  9.14 |  7.15 |  11.5 |  11.6 |  12.5 |  6.97 |  11.6 |  10.6 |  10.2 |  8.9 |
    | FAST      |  14.4 |  12.2 |  10.9 |  11.4 |  10.6 |  11.6 |  11.2 |  24.1 |  11 |  11.6 |
    | BRISK     |  18.4 |  14.3 |  17.4 |  14.5 |  15.8 |  14.4 |  14.9 |  14.1 |  14.4 |  16.2 |
    | ORB       |  18.8 |  14.7 |  16.6 |  22.8 |  23.9 |  21.6 |  22.9 |  23.8 |  18.8 |  24.4 |
    | AKAZE     |  10.9 |  9.58 |  10 |  9.98 |  12.1 |  11.1 |  10.3 |  10.5 |  10.8 |  10 |
    | SIFT      |  48.2 |  35.3 |  35.3 |  33.2 |  34.1 |  33.8 |  36 |  36.3 |  35.6 |  34.9 |

### Conclusion & Recommendations


1. SIFT detector + SIFT descriptor:

    The SIFT detector is able to detecting most discriminative points as keypoints by qualitative evaluation.
    As shown in the table for neighborhood distribution, SIFT detector is able to find keypoints with a high variety of neighborhood size that consider features in different scales.
    SIFT descriptor provides a good performance as discussed in the lesson.
    Also, the number of matched keypoints is high compared to the number of all keypoints detected.
    The only weakness of this combination is its runtime.

2. BRISK detector + SIFT descriptor

    This combination has a good performance and efficiency balance, where the runtime is reduced surprisingly compared to using SIFT detector.
    BRISK detector is also able to cover features in different scales while detecting more keypoints than SIFT.
    In addition, using SIFT descriptor, more BRISK keypoints are matched than all other descriptors.
    However, BRISK keypoint detector produces keypoints with general larger size, which could be a concern that the performance is not as good as SIFT detector because the object size is not very large.

3. FAST detector + ORB descriptor
    
    This combination provides the best efficiency.
    FAST detector runs significantly faster than all other keypoint detectors.
    ORB descriptor also runs fast in combination of FAST detector despite the large number of keypoints provided by FAST.
    In addition, ORB descriptor is able to provide relative more matched FAST keypoints, which could boost the performance. 
