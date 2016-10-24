# H2o_Data_Science
DataScience_Challenge
From the training set removed the columns that have missing values in the server_room_skull
All the 3 solution files server_skull_predict1 , server_skull_predict_withpca, server_skull_predict_withpca_fullrows have R code

server_skull_predict1: builds ctree on the original data frame and predicts the skull

server_skull_predict_withpca : builds ctree on the trasformed data frame ( transformed with principal components) and predicts the skull for the transformed server_skull vector. As the cov call requires data without missing values, rows with missing values are removed. Thus 36 rows are removed. Fortunately the proportions of rows removed approximately stay the same for the 3 skull types. So removing the rows with missing values probably has no impact. If it were not so one could incorporate back the rows that were removed with appropriate transformation.

results:
server_skull_predict1:predict(octr,newdata=server_room_skull,type="prob") gives: 

A         B         C

0.4444444 0.2222222 0.3333333

server_skull_predict_withpca:
predict(pca_octr,newdata=server_room_skull,type="prob") gives:  

A          B          C

0.9166667 0.02777778 0.05555556

As seen the one with pca gives better prediction( also one could compare the respective plots). As this is achieved with just one first level pca analysis probably there is a (some what) linear relationship between the independent variables and the dependent skull.
Otherwise one needs to do more complex analysis with pcas.

server_skull_predict_withpca_fullrows:
The difference between this and the previous solution is all the rows are "kept". In the previous the rows which have missing values are removed. Here they are also included after transformation with pca's. The 'weightage' corresponding to NA's are distributed to other entries in the row. The hadamard.prod and other matrix related code takes care of this business.
This seems to give better tree. see the attached plot pdfs.

predict(pca_octr,newdata=server_room_skull,type="prob") gives:

          A          B         C
 0.8717949 0.02564103 0.1025641







