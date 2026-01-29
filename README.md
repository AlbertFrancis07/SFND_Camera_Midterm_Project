# SFND_Midterm_Camera_Project-Report

MP.1) Data Buffer Optimization :-
The 'deque' container class from c++ library  was used to implement the ring buffer. The new images were added at the tail of the databuffer and once the databuffer is full , the old elements were removed first from the head part of the buffer ,  using the 'pop_front' method of the deque data structure, before pushing  a new image to the tail/end part of the  databuffer. 

MP.2)KeyPoint Detection
Implemented the following Detectors ( Harris, FAST, BRISK, ORB, AKAZE and SIFT) in addition to Shi Thomasi with the help of ready to use modules in OpenCv library. A Condition loop ( if-else) was implemented which checked for a string match inorder to choose the type of Detector to be used. The name of the detector that was inteded to be used was defined prior to calling the conditional loop.  All the images where converted to Grayscale before passing into the detectors. The detected Keypoints were passed into an vector array named 'keypoints'.

MP.3) The keypoints returned from the Keypoint detector contains keypoints from all over the image.. Inorder to concentrate only the keypoins located on the preceding vehicle,  a rectangle region was defined on the image plane enclosing only the preceding vehicle of interest. All the Keypoints that were outside the speciifed region was removed using the 'erase' method from Keypoints class of OpenCV. The keypoints present inside the rectangular region was pushed into a new array named 'filteredkeypoints'

MP.4) Similar to implementation of Keypoint detecctors , the Keypoint Descriptors ( BRISK, BRIEF, ORB, AKAZE, SIFT, FREAK ) were all implemented with the help of ready to use modules from OpenCV library. A Condition loop ( if-else) was implemented to check for a string match inorder to choose the type of Descriptor. The name of the Desciptor that was intended to be used was defined prior to calling the conditional loop.


MP.5)In addition to Brute Force Matcher which was already implemented, a descriptor matcher was created using OpenCV’s FLANN-based approach, which enables fast and efficient matching of feature descriptors by performing approximate nearest-neighbor searches. A conditional loop checks for specific string input,  which on becoming true initialises FLANN-based descriptor matcher using OpenCV. Once initialised, another conditional loop checks if 'Nearest neighbour(NN)' or 'K-NN' approach is needed and implements it accordingly. For KNN approach, the best 2 Nearest neighbours were selected.


MP.6) In order to filter out ambigous results and remove false matches from KNN approach, the Lowe's distace ratio was conducted between two best matches. For each pair of the two closest matches, the best match was accepted as valid only if its descriptor distance was less than 80% of the distance of the second-best match. The keypoints that passed this was stored in an array called 'matches'

MP.7) The initial filtered out keypoints (from MP.3), that lived inside the rectangular region defining the preceding vehicle, were counted using 'filteredkeypoints.size()' and noted.

MP.8) For every successive images, the keypoints that were matched(from MP.6) were counted using 'matches.size()'

MP.9)To measure the execution time of Keypoint Detection and Keypoint Descriptor Extraction, the OpenCV timing functions were used. The system tick count was recorded before starting the execution of the Keypoint Detection  and then immediately after Keypoint Descriptor Extraction completion. The elapsed time was then computed by taking the difference between the two tick counts and normalizing it using the tick frequency provided by OpenCV.

The Performance results for all the Keypoint Detector - Keypoint Descriptor combo on all the 10 images were then recorded inside an excel sheet which is attached along with this project. From the results the 3 best Detector-Descriptor pairs are listed below.
1) FAST / ORB
2) FAST / BRIEF
3) FAST / SIFT

These combo provide the best balance between speed and total number of detections making it suitable for real time applications. 