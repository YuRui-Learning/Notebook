

## floodFill

**floorFill**（**image**, **mask** , **seedPoint**, **newVal**, **loDiff**, **upDiff**, **flags**）

![image-20230705170029197](C:\Users\18423\AppData\Roaming\Typora\typora-user-images\image-20230705170029197.png)

其中mask表示要填充部分，mask也为矩阵，为0表示要填充，为1表示不用填充

flags=FLOODFILL_FIXED_RANGE表示无论背景如何都会填充

flags=FLOODFILL_MASK_ONLY会根据背景中是否存在像素决定是否填充