java c
DAT561: Midterm Project: 
Smart Logistic Warehouse System in AmazonAmazon  Inc.  is  an  American  multinational  retail  corporation  that  operates  a  chain  of  online hypermarkets with huge warehouses in the United States. Amazon warehouses are located throughout the country to ship out products and provide on-time delivery for customers.Example of one Amazon warehouseRecently, Amazon has been planning a 25-day countdown promotion for Christmas, and David King, a manager of Amazon Company, must make sure that the stored products in each warehouse are proper and sufficient. After consideration, David breaks this project into two parts:
1.   Selecting products for each warehouse before the promotion starts
2.   Simulating cross-warehouse-transshipment solution for possible product shortage problem for a random warehouse after the promotion starts
Working as a consulting team, you would provide your analysis to David, and all the data you need is available in the “Products.csv” file.
Here is some information about this dataset:
Each column contains the weight and value of each product, and there is a total of 50 available product options (Product No. 0 - Product No. 49) that can be selected for one warehouse.
Every two rows contain all product information in one warehouse, and there are 300 warehouses (Warehouse No. 0 - Warehouse No. 299) in total.
For each warehouse, there are four variables:
1. n - total number of products chosen to be stored in the warehouse
2. C - total weight capacity of the warehouse
3. Vi - the value of available product i 
4. Wi - the weight of available product i Specifically, for each warehouse, there is a weight capacity (C) of 850, meaning that the total weight of n products selected to be stored in a warehouse should be less than or equal to 850. Each available product i has its own weight (Wi) and value (Vi). Besides, the product information for each warehouse is different.

Problem 1: The Estimated Value for Each Warehouse 
In this part, David wants to select products for each warehouse. He will choose as many products as possible with the top “Value Weight Ratios” before reaching the capacity of each warehouse (850).
That  is,  he  will  first  choose  the  product  with  the  highest  “Value_Weight  Ratio”  to  store  in  the warehouse, then select the product with the second-highest “Value_Weight Ratio” to store, and so on until the warehouse reaches its capacity.
Here is a simplified example for one warehouse, assuming its capacity is 265, and 10 products could be selected. The weights and values of these products are listed below:
Product No 
0 
1 
2 
3 
4 
5 
6 
7 
8 
9 
Weight 
112 
67 
94 
58 
47 
9 
98 
31 
81 
12 
Value 
195.71 
62.59 
105.44 
57.15 
64.21 
8.79 
71.14 
11.19 
62.89 
1.64 
First of all, calculate the Value Weight Ratio for each product.
Product No 
0 
1 
2 
3 
4 
5 
6 
7 
8 
9 
Value/Weight 
1.7474 
0.9342 
1.1217 
0.9853 
1.3662 
0.9767 
0.7259 
0.3610 
0.7764 
0.1367 
Secondly, the products should be sorted based on the Value-Weight ratio in ascending order.Thirdly, start selecting products, and at the same time, look at the accumulated weight of products to ensure the accumulated weight does not exceed the warehouse weight capacity. With the capacity of this warehouse (265), after we select products 0, 4, and 2, the accumulated weight approaches 253, and only 12 are left for the next product. When we choose the fourth product, we select product 5 rather than product 3 because the weight of product 3 (58) is larger than the remaining capacity (12). Moreover, this warehouse has no space to contain extra products. As a result, we finally have products 0, 2, 4, and 5 stored in this warehouse.
Lastly, calculate the corresponding estimated value of the warehouse, which, in this case, is 374.15.
Now, you would try to help David with his product selection problem for those 300 warehouses (each capacity  is  850)  with  the  dataset  “Products.csv” .  Calculating  the  estimated  total  value  and  the accumulated  weight  of  each  300  warehouses  will  be  helpful  for  the  later  decision  of  the  cross- warehouse-transshipment solution.
Notes:
1.   Please do not use other packages to read the CSV file.
2.   You should perform. all the steps above with python codes rather than a spreadsheet
3.   Sometimes, when the warehouse  is  nearly full, the next product with the next highest ratio cannot  be  put  in  the  warehouse,  but  there  are  still  chances  that  one  or  more  remaining products can be placed in the warehouse. Make sure you take every product into consideration; otherwise, you may have the risk of missing products.
4.   You canNOT use the dynamic programming method in this problem; otherwise, you may get 0.
Problem 2: Top Alternative Selections Thank you for your great job helping David with the warehouse storage arrangement! In this part, he would like to simulate the situation when some products in the warehouses may run out during the promotion period. Please treat this part as an independent part, which means the settings in Problem 1 don’t apply here.David manages the following types of products: Product A, Product B, and Product C. Each warehouse stores these three types of products. A warehouse is expected to run out of these three products during promotion. Cross-region shipment from other warehouses (let’s call them “Helpers”) is necessary to keep the promotion activities and ensure on-time delivery in one region.Before seeking help from those Helpers, David must figure out which Helpers he could choose. For the Helpers selection, David would choose 3 Helpers for each product. For each product,  the three helpers have the top 3 highest “Value_per_Weight” ratios. It’s acceptable to recommend more than 3 Helpers for each product because two or more Helpers may have the same “Value_per_Weight” ratio.
1.   Total_Value: total value of the product i stored in one warehouse 
2.   Total_Weight: total weight of the product i stored in one warehouse 
3.   Distance: the distance, generated by you, between the out-of-stock warehouse and the Helpers 
4.   Transportation_Cost: 0.012 per distanceCross-warehouse-transshipment begins with the warehouse that has three products out-of-stock (total number of the stored  products  i  is 0), and this warehouse would contact  Helper to  see  if  help  is available.  Once  the  Helper  agrees  to  do  the  Cross-warehouse-transshipment,  it  will  transport  all product i in its warehouse. In this case, David assumes that Helpers have not sold any products i. In other words, the total number of sto代 写DAT561: Midterm Project: Smart Logistic Warehouse System in AmazonPython
代做程序编程语言red product i in each Helper remains the same as before the promotion started. Since the distances between this product-shortage warehouse and the Helpers are different,    the    transportation    fee     will    be     correspondingly    different.     By    calculating    the “Value_per_Weight,”  David  could  find Helpers  with  the  top  3  highest  “Value_per_Weight”  after considering transportation costs (The cost of a one-way trip from the Helper to the product-shortage warehouse).Step 1: First, generate a distance matrix among the 150 warehouses. Each distance can be generated using a normal distribution with a mean of 500 and a standard deviation of 150. (Please make sure that each generated distance is positive). Below is an example of a 10*10 distance matrix.You  must  create  your  own  distance  matrix  with  a  size  of  150*150.  Be  careful,  all  the  distances generated should be positive numbers and rounded to an integer using round (). After successfully developing the  distance  matrix,  please  write  it  to  a  new  CSV  file  called  “Distances.csv”,  without including row or column indices.
Notes:
1.   Please do not use any packages to write the CSV file.
2.   For better understanding, we included the warehouse index in the screenshot, but the distance matrix you generated does not need to include the index.
Step 2: Let's generate product data.
First of all, David would randomly choose a warehouse (from Warehouse No.0 to Warehouse No.149) and assume it would face out-of-stock problems in this simulation.
Secondly, for each warehouse (including the out-of-stock warehouse), generate random values for the following attributes for three types of products (A, B, and C):
1.   Total_Value:  Random  integer  between  3000  and  15000  for  Product  A,  4000  to  20000  for Product B, and 2000 to 12000 for Product C.
2.   Total_Weight: Random integer between 500 and 3000 for Product A, 1000 to 5000 for Product B, and 700 to 3500 for Product C.
In  the  next  step,  you  will  use  these  values  to  calculate  the  Value_per_Weight  for  each  Helper warehouse. Below is a sample of 10 warehouses:

Step 3: Now, you could calculate the “Value_per_Weight” and help David decide the 3 Helpers for each product with the top 3 highest “Value_per_Weight” .Firstly, based on the out-of-stock warehouse he picks in Step 2, you need to find the corresponding distance  between  this  warehouse  and  each  of  the  other  Helpers  from  the  distance  matrix  you generated in Step 1. In addition, you also need to find the corresponding total value and the total weight of each of the three products stored in each Helper.Thirdly, calculate the “Value_per_Weight”  ratio for each  product  in  each  Helper,  sort the  ratio  in descending order, and choose the top helpers with the three highest “Value_per_Weight” ratios for each product. Recall this formula:
5.   Total_Value: total value of the product i stored in one warehouse 
6.   Total_Weight: total weight of the product i stored in one warehouse 
7.   Distance: the distance, generated by you, between the out-of-stock warehouse and the Helpers 
8.   Transportation_Cost: 0.012 per distanceHere is a simplified example. Suppose now there are ten warehouses in total, and David needs Helpers with the top 3 “Value_per_Weight” ratios. He assumes Product A, B, and C in warehouse No. 5 are out- of-stock, and as a result, the total number of all three products in it becomes 0, while the rest of the warehouses  (Helpers)  remain  with the  same  amount of  product  as you generated  in  Step  2. The corresponding distance data is located in the 6th row of the distance matrix you have generated in Step 1 (the row starts with index 5, highlighted by the red rectangle below).Finding the corresponding distance Take product A as an example (the same for products B and C); after calculating the “Value_per_Weight” ratio for each helper, you would sort those Helpers and return the top 3 “Value_per_Weight” and the  corresponding index of the Helpers. (It is important you show the corresponding relationship between  the “Value-per-Weight” and the index of the Helpers!)The logic of how you calculate the “Value_per_Weight” Sorted result
(You should use the code to show this logic instead of Excel; you do not need to generate a file here.) 
Notes:
1.   You are  NOT allowed to use dynamic programming in this problem. Otherwise, your project may receive 0 points.
2.   In  this  problem,  there  is  a  chance  that  the  “Value_per_Weight”  of  product  i  in  the  two warehouses is the same. Return the top 3 Value_per_Weight, the distance to the out-of-stock warehouse, and if multiple warehouses have the same Value_per_Weight, determine those warehouses in the output.
Submission of the Project 
Your final submission will contain two files:1. The first would be the "FL24_Midterm.ipynb" notebook. You need to provide the Python code as well as your answers. We strongly recommend that you explain critical steps in the code so that we can understand what you were trying to do when something goes wrong.
2. The second is the “Distances.csv” file.
Note: Please submit all files (Distances.csv, and FL24_Midterm.ipynb files) as one zip file on Canvas. Please add all teammates' IDs to the zip file's name. For example, 14325_34672_12345.zip.
Grading 
Total - 100 points 
10 points: towards how good your solution is.
We will  check  how you  write  the  code  and  solve  the  problem  and  how  efficient  and optimized your  code is. Specifically, your code will be graded based on the following factors:
1. Correctness: The code should produce the expected outputs and solve the problem correctly.
2. Readability: The code should be easy to read and understand with added comments.
3. Structure and organization: The code should be well-structured and organized. It
should contain functions to modularize the code. Functions must have clear responsibilities and be appropriately organized.
4. Documentation and comments: The code should have clear and concise documentation to explain its purpose, inputs, outputs, and any important details.
5. Efficiency: The code should be efficient in terms of time and space complexity.
90 points: 
The Estimated Value for Each Warehouse – 30 points The 150*150 distance matrix generated – 30 points
Top 3 Helper Warehouses Chosen for each product - 30 points
•     Your code needs to pass the auto-grader for us to see whether it works.
●    We will look at your logic and whether your code is working.
●    We will look at whether you submitted all files correctly.
●    We will examine how effectively you solved the problems (functions, global scobe, etc.).





         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
