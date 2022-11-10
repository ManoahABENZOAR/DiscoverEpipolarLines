# DiscoverEpipolarLines

Exercice :
•Take two-view images and estimate Essential Matrix or Fundamental Matrix.
• Draw epipolar lines on the images.
• Evaluate the accuracy of the E‐Matrix or F‐Matrix by computing the distance of the corresponding points and the corresponding epipolar lines.

1/ Here my 2 images :

![image](https://user-images.githubusercontent.com/79518374/201151669-de1df68f-1f51-4db9-82f6-9bd514690451.png)
![image](https://user-images.githubusercontent.com/79518374/201151680-22be977e-6600-4ca3-b659-8851330ea4e9.png)

And the resulting foundamental matrix : 

F = ![image](https://user-images.githubusercontent.com/79518374/201151917-b1c15f14-f8bd-487a-a07e-ef69b99b9a4f.png)

2/
Use SIFT algo to find keypoint
![image](https://user-images.githubusercontent.com/79518374/201152081-31b1f706-ec0e-4563-bb8b-75db11194fbe.png)
And obtain 2 images containing our epipolar lines 
![image](https://user-images.githubusercontent.com/79518374/201152187-dbf65378-269a-4ec6-b91c-703359077d8f.png)
![image](https://user-images.githubusercontent.com/79518374/201152200-219807cb-257b-4951-ac72-b0af6a858b2e.png)

3/ Evaluate the accuracy of our foundamental matrix :
  To do so we use the link between foundamental matrix, coordonates and line, which is :  
  ![image](https://user-images.githubusercontent.com/79518374/201152422-a243588c-0193-464b-b3c1-4c3335b3acb5.png)
  So to estimate its accuracy we will compute (a b c) thanks to F and the coordonates of the points on the right image (x’ y’). 
  After we will use the formula : ax+by+c = 0 to estimate the mean error and have a view on the accuracy of our matrix. 
  If the matrix is perfect the mean should be equal to 0.
  We will obtain two mean error as in the program we call two time the function where I implemented these calculs : 
    -the first time to find epilines corresponding to points in right image (second image) and drawing its lines on left image 
    -the second time to find epilines corresponding to points in left image (first image) and drawing its lines on right image

    When we use the coordonate of the right image (= x’y’ coordonates) to compute (a b c) and test (a b c) on the left image ( the x y coordonate) we obtain this two error :
    ![image](https://user-images.githubusercontent.com/79518374/201152851-4e5ade55-208c-4bac-b22f-ae7929494ebf.png)
    So the global error = (-4.57 + -0.67) / 2 = -2.62
    
    Even if we use the left image (= x y coordonates) to compute (a b c) and test (a b c) on the left image ( x y coordonates) we obtain two errors which are not equal to 0:
    ![image](https://user-images.githubusercontent.com/79518374/201152980-d24dc6ba-c817-43f1-8ed0-3bc9c5049127.png)
    So the global error = (1.60 1.23) / 2 = 1.415. 
    It logically lower than when we took (x’ y’) coordonates to create (x y). 
    But it still not equal to 0 and shows that our matrix could be improve as she isn’t perfect.
    
Futher look on the code :
Here starts the part to estimate the accuracy of our matrix, by computing the mean error.
![Screenshot from 2022-11-10 17-34-01](https://user-images.githubusercontent.com/79518374/201153299-17e3d006-8641-471b-b1fb-9c691a3b65e5.png)

As you can see to obtain the mean I divided by 26. Why?
Because at the line before the right arrow I checked the number of points found to create our epipolar lines and we used the 26 best points.
More, thanks to the program I haven’t to manage the two lists with (x’ y’) and (x y) coordonates, because the computing is done in a for loop and for each of the 26 points pt1 and pt2 will be its coordanates on the left image and on the right image.
