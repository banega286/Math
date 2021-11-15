
<!-- rnb-text-begin -->

---
title: "Foundation Mathematics & Statistics in R"
author: Vi Tu (617634), Khoa Nguyen (617102), Amir Mohamed (513528)
output: html_notebook
---

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuaW5zdGFsbC5wYWNrYWdlcyhcImdncGxvdDJcIilcbmluc3RhbGwucGFja2FnZXMoXCJ0aWR5clwiKVxuaW5zdGFsbC5wYWNrYWdlcyhcImphbml0b3JcIilcbmluc3RhbGwucGFja2FnZXMoXCJkcGx5clwiKVxuaW5zdGFsbC5wYWNrYWdlcyhcInNoaW55XCIpXG5pbnN0YWxsLnBhY2thZ2VzKFwidGlkeXZlcnNlXCIpXG5pbnN0YWxsLnBhY2thZ2VzKFwibWF0cml4U3RhdHNcIilcbmluc3RhbGwucGFja2FnZXMoXCJlMTA3MVwiKVxuaW5zdGFsbC5wYWNrYWdlcyhcImRlc2NyXCIpXG5gYGAifQ== -->

```r
install.packages("ggplot2")
install.packages("tidyr")
install.packages("janitor")
install.packages("dplyr")
install.packages("shiny")
install.packages("tidyverse")
install.packages("matrixStats")
install.packages("e1071")
install.packages("descr")
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



Load all the necessary packages for later use in the assignment

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubGlicmFyeShnZ3Bsb3QyKVxubGlicmFyeSh0aWR5cilcbmxpYnJhcnkoamFuaXRvcilcbmxpYnJhcnkoZHBseXIpXG5saWJyYXJ5KHNoaW55KVxubGlicmFyeSh0aWR5dmVyc2UpXG5saWJyYXJ5KG1hdHJpeFN0YXRzKVxubGlicmFyeShlMTA3MSlcbmxpYnJhcnkoZGVzY3IpXG5gYGAifQ== -->

```r
library(ggplot2)
library(tidyr)
library(janitor)
library(dplyr)
library(shiny)
library(tidyverse)
library(matrixStats)
library(e1071)
library(descr)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->




<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDcmVhdGUgYSBkYXRhIGZyYW1lIGJhc2VkIG9uIHRoZSBFeGNlbCBmaWxlXG5TdHVkZW50cyA8LSBjKFwiYVwiLCBcImJcIiwgXCJjXCIsIFwiZFwiLCBcImVcIiwgXCJmXCIsIFwiZ1wiLCBcImhcIiwgXCJpXCIsIFwialwiLCBcImtcIilcbkNvdXJzZTEgPC0gYyg2LjE0LCA4LjIwLCA5LjA1LCA1LjU0LCA0LjA2LCAzLjE0LCA2Ljk4LCA4LjU1LCA4LjIxLCA5Ljk0LCAyLjM5KVxuQ291cnNlMiA8LSBjKDcuNzAsIDkuMTcsIDkuNzcsIDcuNDQsIDkuNDEsIDcuNDgsIDYuMTMsIDcuMzgsIDcuNTMsIDguMTEsIDkuNDEpXG5Db3Vyc2UzIDwtIGMoNS44OCwgOC4yOCwgNS4wNCwgOC40OSwgNi4wMCwgOC42MiwgNi4yMCwgOC4xMywgOS4xOSwgOS40MywgNy4wMClcbkNvdXJzZTQgPC0gYygyLjgwLCAxLjIzLCA3Ljk4LCA4LjQzLCAxLjgxLCA2LjQ3LCAzLjQwLCA1LjM3LCAzLjM5LCAxLjYxLCAwLjcyKVxuQ291cnNlNSA8LSBjKDcuNjMsIDUuMTksIDUuNzEsIDYuNjAsIDQuOTUsIDYuOTEsIDUuODAsIDYuODMsIDcuOTMsIDUuMzUsIDYuODYpXG5Db3Vyc2U2IDwtIGMoOC40MywgOS45MSwgOC41OCwgOC4yOSwgMTAuMDAsIDguMTUsIDguOTMsIDguODAsIDguNjEsIDguOTQsIDkuNTkpXG5zdHVkZW50X2RhdGEgPC0gZGF0YS5mcmFtZShTdHVkZW50cywgQ291cnNlMSwgQ291cnNlMiwgQ291cnNlMywgQ291cnNlNCwgQ291cnNlNSwgQ291cnNlNilcbnN0cihzdHVkZW50X2RhdGEpXG52aWV3KHN0dWRlbnRfZGF0YSlcbmBgYCJ9 -->

```r
# Create a data frame based on the Excel file
Students <- c("a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k")
Course1 <- c(6.14, 8.20, 9.05, 5.54, 4.06, 3.14, 6.98, 8.55, 8.21, 9.94, 2.39)
Course2 <- c(7.70, 9.17, 9.77, 7.44, 9.41, 7.48, 6.13, 7.38, 7.53, 8.11, 9.41)
Course3 <- c(5.88, 8.28, 5.04, 8.49, 6.00, 8.62, 6.20, 8.13, 9.19, 9.43, 7.00)
Course4 <- c(2.80, 1.23, 7.98, 8.43, 1.81, 6.47, 3.40, 5.37, 3.39, 1.61, 0.72)
Course5 <- c(7.63, 5.19, 5.71, 6.60, 4.95, 6.91, 5.80, 6.83, 7.93, 5.35, 6.86)
Course6 <- c(8.43, 9.91, 8.58, 8.29, 10.00, 8.15, 8.93, 8.80, 8.61, 8.94, 9.59)
student_data <- data.frame(Students, Course1, Course2, Course3, Course4, Course5, Course6)
str(student_data)
view(student_data)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


 The data contains 77 scores from 7 courses between 11 students. Each students has 1 score recorded per course. 



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb252ZXJ0IHRoZSBzdHVkZW50IG5hbWVzIGludG8gcm93IG5hbWVzXG5zdHVkZW50X2RhdGEyIDwtIHN0dWRlbnRfZGF0YVssLTFdXG5yb3duYW1lcyhzdHVkZW50X2RhdGEyKSA8LSBzdHVkZW50X2RhdGFbLDFdXG52aWV3KHN0dWRlbnRfZGF0YTIpXG50b3RhbCA8LSBzdHVkZW50X2RhdGFbLC0xXVxudmlldyh0b3RhbClcbmBgYCJ9 -->

```r
# Convert the student names into row names
student_data2 <- student_data[,-1]
rownames(student_data2) <- student_data[,1]
view(student_data2)
total <- student_data[,-1]
view(total)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDcmVhdGluZyBuZXcgY29sdW1ucyB0byBjYWxjdWxhdGUgU3VtLCBNZWFuIGFuZCBTdGFuZGFyZCBkZXZpYXRpb24sIFNrZXduZXNzIGFuZCBLdXJ0b3NpcyBvZiBlYWNoIFNUVURFTlQgb24gc3R1ZGVudF9kYXRhMlxuU3VtcGVyU3R1ZGVudCA9IHJvd1N1bXMoc3R1ZGVudF9kYXRhMilcbk1lYW5wZXJTdHVkZW50ID0gcm93TWVhbnMoc3R1ZGVudF9kYXRhMilcblNEcGVyU3R1ZGVudCA9IGFwcGx5KHN0dWRlbnRfZGF0YTIsIDEsIHNkKVxuU2tld3BlclN0dWRlbnQgPSBhcHBseShzdHVkZW50X2RhdGEyLCAxLCBza2V3bmVzcylcbkt1cnRvc2lzcGVyU3R1ZGVudCA9IGFwcGx5KHN0dWRlbnRfZGF0YTIsIDEsIGt1cnRvc2lzKVxuIyBDcmVhdGluZyByb3dzIHRvIGNhbGN1bGF0ZSBTdW0sIE1lYW4gYW5kIFN0YW5kYXJkIGRldmlhdGlvbiwgU2tld25lc3MgYW5kIEt1cnRvc2lzIG9mIGVhY2ggQ09VUlNFIG9uIHN0dWRlbnRfZGF0YVxuU3VtcGVyQ291cnNlID0gY29sU3VtcyhzdHVkZW50X2RhdGEyKVxuTWVhbnBlckNvdXJzZSA9IGNvbE1lYW5zKHN0dWRlbnRfZGF0YTIpICAgICAgXG5TRHBlckNvdXJzZSA9IGMoc2QoQ291cnNlMSksIHNkKENvdXJzZTIpLCBzZChDb3Vyc2UzKSwgc2QoQ291cnNlNCksIHNkKENvdXJzZTUpLCBzZChDb3Vyc2U2KSlcblNrZXdwZXJDb3Vyc2UgPSBjKHNrZXduZXNzKENvdXJzZTEpLCBza2V3bmVzcyhDb3Vyc2UyKSwgc2tld25lc3MoQ291cnNlMyksIHNrZXduZXNzKENvdXJzZTQpLCBza2V3bmVzcyhDb3Vyc2U1KSwgc2tld25lc3MoQ291cnNlNikpXG5LdXJ0b3Npc3BlckNvdXJzZSA9IGMoa3VydG9zaXMoQ291cnNlMSksIGt1cnRvc2lzKENvdXJzZTIpLCBrdXJ0b3NpcyhDb3Vyc2UzKSwga3VydG9zaXMoQ291cnNlNCksIGt1cnRvc2lzKENvdXJzZTUpLCBrdXJ0b3NpcyhDb3Vyc2U2KSlcbmBgYCJ9 -->

```r
# Creating new columns to calculate Sum, Mean and Standard deviation, Skewness and Kurtosis of each STUDENT on student_data2
SumperStudent = rowSums(student_data2)
MeanperStudent = rowMeans(student_data2)
SDperStudent = apply(student_data2, 1, sd)
SkewperStudent = apply(student_data2, 1, skewness)
KurtosisperStudent = apply(student_data2, 1, kurtosis)
# Creating rows to calculate Sum, Mean and Standard deviation, Skewness and Kurtosis of each COURSE on student_data
SumperCourse = colSums(student_data2)
MeanperCourse = colMeans(student_data2)      
SDperCourse = c(sd(Course1), sd(Course2), sd(Course3), sd(Course4), sd(Course5), sd(Course6))
SkewperCourse = c(skewness(Course1), skewness(Course2), skewness(Course3), skewness(Course4), skewness(Course5), skewness(Course6))
KurtosisperCourse = c(kurtosis(Course1), kurtosis(Course2), kurtosis(Course3), kurtosis(Course4), kurtosis(Course5), kurtosis(Course6))
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->




<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBBZGQgdGhvc2UgbmV3IGNvbHVtbnMgaW50byB0aGUgZGF0YSBmcmFtZVxuc3R1ZGVudF9kYXRhMiA8LSBjYmluZChzdHVkZW50X2RhdGEyLCBTdW1wZXJTdHVkZW50LCBNZWFucGVyU3R1ZGVudCwgU0RwZXJTdHVkZW50LCBTa2V3cGVyU3R1ZGVudCwgS3VydG9zaXNwZXJTdHVkZW50KVxuIyBBZGQgdGhvc2UgbmV3IHJvd3MgaW50byB0aGUgZGF0YSBmcmFtZVxuc3R1ZGVudF9kYXRhMiA8LSByYmluZChzdHVkZW50X2RhdGEyLCBTdW1wZXJDb3Vyc2UsIE1lYW5wZXJDb3Vyc2UsIFNEcGVyQ291cnNlLCBTa2V3cGVyQ291cnNlLCBLdXJ0b3Npc3BlckNvdXJzZSlcbiMgQ2hhbmdlIHJvdyBuYW1lc1xucm93bmFtZXMoc3R1ZGVudF9kYXRhMilbcm93bmFtZXMoc3R1ZGVudF9kYXRhMikgJWluJSBjKDEyOjE2KV0gPC0gYyhcIlN1bXBlckNvdXJzZVwiLFwiTWVhbnBlckNvdXJzZVwiLCBcIlNEcGVyQ291cnNlXCIsIFwiU2tld25lc3NwZXJDb3Vyc2VcIiwgXCJLdXJ0b3Npc3BlckNvdXJzZVwiKVxuc3R1ZGVudF9kYXRhMiA8LSBzdHVkZW50X2RhdGEyICU+JSBtdXRhdGVfaWYoaXMubnVtZXJpYywgcm91bmQsIGRpZ2l0cyA9IDIpXG50YWlsKHN0dWRlbnRfZGF0YTIpXG5gYGAifQ== -->

```r
# Add those new columns into the data frame
student_data2 <- cbind(student_data2, SumperStudent, MeanperStudent, SDperStudent, SkewperStudent, KurtosisperStudent)
# Add those new rows into the data frame
student_data2 <- rbind(student_data2, SumperCourse, MeanperCourse, SDperCourse, SkewperCourse, KurtosisperCourse)
# Change row names
rownames(student_data2)[rownames(student_data2) %in% c(12:16)] <- c("SumperCourse","MeanperCourse", "SDperCourse", "SkewnessperCourse", "KurtosisperCourse")
student_data2 <- student_data2 %>% mutate_if(is.numeric, round, digits = 2)
tail(student_data2)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Based on the given dataset, it appears that student C has the highest scores overall with a mean of 7.69. While student K has the lowest with a mean of 35.97 . 

Student e has the highest standard deviation. Meaning his scores tend to be more spread out of the mean. This entails that his scoring is the most volatile.

In terms of skewness student I has the highest negative skewness whereas student E has the highest positive skewness

Student I has the highest Kurtosis since his scores are fairly similar. Student K has the lowest kurtosis because he's scores are more spread out.



Remove intersect values to NA?

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuc3R1ZGVudF9kYXRhMiRTdW1wZXJTdHVkZW50WzEyOjE2XSA9IE5BICMgY2VydGFpbiBwYXJ0IG9mIGEgY29sdW1uIGlzIHJldHVybmVkIHRvIE5BLiBEbyB0aGUgc2FtZSB3YXkgZm9yIG90aGVyIGNvbHVtbnNcbnN0dWRlbnRfZGF0YTIkTWVhbnBlclN0dWRlbnRbMTI6MTZdID0gTkFcbnN0dWRlbnRfZGF0YTIkU0RwZXJTdHVkZW50WzEyOjE2XSA9IE5BXG5zdHVkZW50X2RhdGEyJFNrZXdwZXJTdHVkZW50WzEyOjE2XSA9IE5BXG5zdHVkZW50X2RhdGEyJEt1cnRvc2lzcGVyU3R1ZGVudFsxMjoxNl0gPSBOQVxudmlldyhzdHVkZW50X2RhdGEyKVxuYGBgIn0= -->

```r
student_data2$SumperStudent[12:16] = NA # certain part of a column is returned to NA. Do the same way for other columns
student_data2$MeanperStudent[12:16] = NA
student_data2$SDperStudent[12:16] = NA
student_data2$SkewperStudent[12:16] = NA
student_data2$KurtosisperStudent[12:16] = NA
view(student_data2)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Create mean of means 

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBQZXIgQ291cnNlXG5tZWFuQyA9IGFwcGx5KHN0dWRlbnRfZGF0YTJbMTMsMTo2XSwgMSwgbWVhbikgI0NhbGN1bGF0ZSBtZWFuIHBlciBtZWFucyBieSBDb3Vyc2UgXG5TZEMgPSBhcHBseShzdHVkZW50X2RhdGEyWzE0LDE6Nl0sIDEsIG1lYW4pXG5Ta0MgPSBhcHBseShzdHVkZW50X2RhdGEyWzE1LDE6Nl0sIDEsIG1lYW4pXG5LdUMgPSBhcHBseShzdHVkZW50X2RhdGEyWzE2LDE6Nl0sIDEsIG1lYW4pXG5Nb01fQ291cnNlIDwtIGRhdGEuZnJhbWUobWVhbkMsIFNkQywgU2tDLCBLdUMpICNDcmVhdGUgZGF0YSBmcmFtZSBmb3IgTW9NIHBlciBDb3Vyc2VcblZpZXcoTW9NX0NvdXJzZSlcbiMgUGVyIFN0dWRlbnRcbm1lYW5TID0gbWVhbihzdHVkZW50X2RhdGEyJE1lYW5wZXJTdHVkZW50WzE6MTFdKSAjQ2FsY3VsYXRlIG1lYW4gcGVyIG1lYW5zIGJ5IFN0dWRlbnRcblNkUyA9IG1lYW4oc3R1ZGVudF9kYXRhMiRTRHBlclN0dWRlbnRbMToxMV0pXG5Ta1MgPSBtZWFuKHN0dWRlbnRfZGF0YTIkU2tld3BlclN0dWRlbnRbMToxMV0pXG5LdVMgPSBtZWFuKHN0dWRlbnRfZGF0YTIkS3VydG9zaXNwZXJTdHVkZW50WzE6MTFdKVxuTW9NX1N0dWRlbnQgPC0gZGF0YS5mcmFtZShtZWFuUywgU2RTLCBTa1MsIEt1UykgI0NyZWF0ZSBkYXRhIGZyYW1lIGZvciBNb00gcGVyIFN0dWRlbnRcblZpZXcoTW9NX1N0dWRlbnQpXG4jIFRvdGFsIGRhdGFmcmFtZVxubWVhblQgPSBtZWFuKGFzLm1hdHJpeCh0b3RhbCkpXG5TZFQgPSBzZChhcy5tYXRyaXgodG90YWwpKVxuU2tUID0gc2tld25lc3MoYXMubWF0cml4KHRvdGFsKSkgXG5LdVQgPSBrdXJ0b3Npcyhhcy5tYXRyaXgodG90YWwpKVxuTW9NX1RvdGFsIDwtIGRhdGEuZnJhbWUobWVhblQsIFNkVCwgU2tULCBLdVQpXG5WaWV3KE1vTV9Ub3RhbClcbiAgICAgICAgICAgICAgICAgIFxuICAgICAgICAgICAgICAgICAgXG5gYGAifQ== -->

```r
# Per Course
meanC = apply(student_data2[13,1:6], 1, mean) #Calculate mean per means by Course 
SdC = apply(student_data2[14,1:6], 1, mean)
SkC = apply(student_data2[15,1:6], 1, mean)
KuC = apply(student_data2[16,1:6], 1, mean)
MoM_Course <- data.frame(meanC, SdC, SkC, KuC) #Create data frame for MoM per Course
View(MoM_Course)
# Per Student
meanS = mean(student_data2$MeanperStudent[1:11]) #Calculate mean per means by Student
SdS = mean(student_data2$SDperStudent[1:11])
SkS = mean(student_data2$SkewperStudent[1:11])
KuS = mean(student_data2$KurtosisperStudent[1:11])
MoM_Student <- data.frame(meanS, SdS, SkS, KuS) #Create data frame for MoM per Student
View(MoM_Student)
# Total dataframe
meanT = mean(as.matrix(total))
SdT = sd(as.matrix(total))
SkT = skewness(as.matrix(total)) 
KuT = kurtosis(as.matrix(total))
MoM_Total <- data.frame(meanT, SdT, SkT, KuT)
View(MoM_Total)
                  
                  
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Course 6 has the highest mean and also contains the highest scores. Students however seem to struggle with course 4. It shows a mean of 3.39. Meaning that the average grade is low but it also has the highest standard deviation meaning that there is a lot of spread between the students' scores. 

Course's 1 and 3 have a negative skewness while the rest are all positive. The 2nd course has a normal distribution.

Course 3 has the highest kurtosis.





                


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuQmluIDwtIGMoMDoxMClcbkJpblxudG90YWwgPC0gIHRvdGFsICU+JSBhZGRfY29sdW1uKEJpbiA9IEJpbilcbnZpZXcodG90YWwpXG4gIFxuICBcbkN1bXVsYXRpdmVfTiA8LSBjKDAsIDEgLCA0LCA2LCA5LCAxMSAsIDE5LCAzMCwgMzgsIDU1LCA2NilcbkZyZXF1ZW5jeV9OIDwtIGMoMCwgMSwgMywgMiwgMywgMiwgOCwgMTEsIDgsIDE3LCAxMSlcbnRvdGFsIDwtIHRvdGFsICU+JSBtdXRhdGUoQ3VtdWxhdGl2ZV9OLCBGcmVxdWVuY3lfTilcbnZpZXcodG90YWwpXG5QcmVjZW50QmluIDwtICgwOjEwKVxuUHJlY2VudEN1bXVsYXRpdmU8LSBjKDAuMCwgMS41ICwgNi4xLCA5LjEsIDEzLjYsIDE2LjcgLCAyOC44ICwgNDUuNSwgNTcuNiwgODMuMywgMTAwKVxuUHJlY2VudEZyZXF1ZW5jeSA8LSBjKDAuMCwgMS41LCA0LjUsIDMuMCwgNC41LCAzLjAsIDEyLjEsIDE2LjcsIDEyLjEsIDI1LjgsIDE2LjcpXG50b3RhbCA8LSB0b3RhbCAlPiUgbXV0YXRlKFByZWNlbnRCaW4sIFByZWNlbnRDdW11bGF0aXZlLCBQcmVjZW50RnJlcXVlbmN5KVxudmlldyh0b3RhbClcblRvdGFsX04gPC0gdG90YWwgJT4lIG11dGF0ZShCaW4sIEN1bXVsYXRpdmVfTiwgRnJlcXVlbmN5X04pXG52aWV3KFRvdGFsX04pXG5Ub3RhbF9EYXRhX04gPC0gZGF0YS5mcmFtZShCaW4sIEN1bXVsYXRpdmVfTiwgRnJlcXVlbmN5X04pXG5WaWV3KFRvdGFsX0RhdGFfTilcblRvdGFsX0RhdGFfUHJlY2VudGFnZSA8LSBkYXRhLmZyYW1lKFByZWNlbnRCaW4sIFByZWNlbnRDdW11bGF0aXZlLCBQcmVjZW50RnJlcXVlbmN5KVxuVmlldyhUb3RhbF9EYXRhX1ByZWNlbnRhZ2UpXG5cbmdncGxvdChUb3RhbF9EYXRhX04sIGFlcyhCaW4sIEZyZXF1ZW5jeV9OLCBncm91cCA9IDEpKSArXG5nZW9tX2hpc3RvZ3JhbShjb2xvciA9IFwiZ3JleVwiKSArXG5nZW9tX2xpbmUoVG90YWxfRGF0YV9OJEN1bXVsYXRpdmVfTixjb2xvciA9IFwib3JhbmdlXCIpICtcbmxhYnMoeCA9IFwiTWFya3NcIiwgeSA9IFwiRnJlcXVlbmN5IChpbiBudW1iZXIpXCIsIHRpdGxlID0gXCJPdmVyIERpc3RyaWJ1dGlvbiBvZiBNYXJrc1wiKVxuYGBgIn0= -->

```r
Bin <- c(0:10)
Bin
total <-  total %>% add_column(Bin = Bin)
view(total)
  
  
Cumulative_N <- c(0, 1 , 4, 6, 9, 11 , 19, 30, 38, 55, 66)
Frequency_N <- c(0, 1, 3, 2, 3, 2, 8, 11, 8, 17, 11)
total <- total %>% mutate(Cumulative_N, Frequency_N)
view(total)
PrecentBin <- (0:10)
PrecentCumulative<- c(0.0, 1.5 , 6.1, 9.1, 13.6, 16.7 , 28.8 , 45.5, 57.6, 83.3, 100)
PrecentFrequency <- c(0.0, 1.5, 4.5, 3.0, 4.5, 3.0, 12.1, 16.7, 12.1, 25.8, 16.7)
total <- total %>% mutate(PrecentBin, PrecentCumulative, PrecentFrequency)
view(total)
Total_N <- total %>% mutate(Bin, Cumulative_N, Frequency_N)
view(Total_N)
Total_Data_N <- data.frame(Bin, Cumulative_N, Frequency_N)
View(Total_Data_N)
Total_Data_Precentage <- data.frame(PrecentBin, PrecentCumulative, PrecentFrequency)
View(Total_Data_Precentage)

ggplot(Total_Data_N, aes(Bin, Frequency_N, group = 1)) +
geom_histogram(color = "grey") +
geom_line(Total_Data_N$Cumulative_N,color = "orange") +
labs(x = "Marks", y = "Frequency (in number)", title = "Over Distribution of Marks")
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


The students tend to score 7's, 9's and 10's the most. While score's below 5 are far less frequent. This gives the impression that the students tend to do fairly well on tests. 






Plotting

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZGZncmFwaFMgPC0gZGF0YS5mcmFtZShTdHVkZW50cyxNZWFucGVyU3R1ZGVudCxTRHBlclN0dWRlbnQsU2tld3BlclN0dWRlbnQsS3VydG9zaXNwZXJTdHVkZW50KVxuVmlldyhkZmdyYXBoUylcbkNvdXJzZSA8LSBhcy5jaGFyYWN0ZXIoYygxOjYpKVxuZGZncmFwaEMgPC0gZGF0YS5mcmFtZShDb3Vyc2UsTWVhbnBlckNvdXJzZSxTRHBlckNvdXJzZSxTa2V3cGVyQ291cnNlLEt1cnRvc2lzcGVyQ291cnNlKVxuVmlldyhkZmdyYXBoQylcbmBgYCJ9 -->

```r
dfgraphS <- data.frame(Students,MeanperStudent,SDperStudent,SkewperStudent,KurtosisperStudent)
View(dfgraphS)
Course <- as.character(c(1:6))
dfgraphC <- data.frame(Course,MeanperCourse,SDperCourse,SkewperCourse,KurtosisperCourse)
View(dfgraphC)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->




<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyMgQ3JlYXRlIGEgZ3JhcGggd2l0aCB0aGUgbWVhbiBncmFkZSBieSBzdHVkZW50XG5nZ3Bsb3QoZGZncmFwaFMsIGFlcyhTdHVkZW50cywgTWVhbnBlclN0dWRlbnQsIGdyb3VwID0gMSkpICtcbiAgICAgICBnZW9tX3BvaW50KGNvbG9yID0gXCJibHVlXCIpICsgZ2VvbV9saW5lKGNvbG9yID0gXCJibHVlXCIpICtcbiAgICAgICBnZW9tX3Ntb290aChtZXRob2Q9bG0sIHNlPUZBTFNFLCBjb2w9J3JlZCcpICsgIHlsaW0oMCwxMCkgK1xuICAgICAgIGxhYnMoeCA9IFwiU3R1ZGVudHNcIiwgeSA9IFwiTWVhbiBncmFkZVwiLCB0aXRsZSA9IFwiTWVhbiBncmFkZSBieSBTdHVkZW50XCIpXG5gYGAifQ== -->

```r
## Create a graph with the mean grade by student
ggplot(dfgraphS, aes(Students, MeanperStudent, group = 1)) +
       geom_point(color = "blue") + geom_line(color = "blue") +
       geom_smooth(method=lm, se=FALSE, col='red') +  ylim(0,10) +
       labs(x = "Students", y = "Mean grade", title = "Mean grade by Student")
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


## Create a graph with the mean grade by course

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KGRmZ3JhcGhDLCBhZXMoQ291cnNlLCBNZWFucGVyQ291cnNlLCBncm91cCA9IDEpKSArXG4gICAgICAgIGdlb21fcG9pbnQoY29sb3IgPSBcImJsdWVcIikgKyBnZW9tX2xpbmUoY29sb3IgPSBcImJsdWVcIikgK1xuICAgICAgICBnZW9tX3Ntb290aChtZXRob2Q9bG0sIHNlPUZBTFNFLCBjb2w9J3JlZCcpICsgeWxpbSgwLDEwKSArXG4gICAgICAgIGxhYnMoeCA9IFwiQ291cnNlXCIsIHkgPSBcIk1lYW4gZ3JhZGVcIiwgXG4gICAgICAgICAgICAgdGl0bGUgPSBcIk1lYW4gZ3JhZGUgYnkgQ291cnNlXCIpXG5gYGAifQ== -->

```r
ggplot(dfgraphC, aes(Course, MeanperCourse, group = 1)) +
        geom_point(color = "blue") + geom_line(color = "blue") +
        geom_smooth(method=lm, se=FALSE, col='red') + ylim(0,10) +
        labs(x = "Course", y = "Mean grade", 
             title = "Mean grade by Course")
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


## Create a graph with the std of grades by student

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KGRmZ3JhcGhTLCBhZXMoU3R1ZGVudHMsIFNEcGVyU3R1ZGVudCwgZ3JvdXAgPSAxKSkgK1xuICAgICAgIGdlb21fcG9pbnQoY29sb3IgPSBcImJsdWVcIikgKyBnZW9tX2xpbmUoY29sb3IgPSBcImJsdWVcIikgK1xuICAgICAgIGdlb21fc21vb3RoKG1ldGhvZD1sbSwgc2U9RkFMU0UsIGNvbD0ncmVkJykgKyB5bGltKDAsNCkgK1xuICAgICAgIGxhYnMoeCA9IFwiU3R1ZGVudHNcIiwgeSA9IFwiIFN0YW5kYXJkIGRldmlhdGlvbiBvZiBncmFkZXNcIiwgdGl0bGUgPSBcIlN0YW5kYXJkIGRldmlhdGlvbiBvZiBncmFkZXMgYnkgU3R1ZGVudFwiKVxuYGBgIn0= -->

```r
ggplot(dfgraphS, aes(Students, SDperStudent, group = 1)) +
       geom_point(color = "blue") + geom_line(color = "blue") +
       geom_smooth(method=lm, se=FALSE, col='red') + ylim(0,4) +
       labs(x = "Students", y = " Standard deviation of grades", title = "Standard deviation of grades by Student")
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


## Create a graph with the std of grades by course

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KGRmZ3JhcGhDLCBhZXMoQ291cnNlLCBTRHBlckNvdXJzZSwgZ3JvdXAgPSAxKSkgK1xuICAgICAgIGdlb21fcG9pbnQoY29sb3IgPSBcImJsdWVcIikgKyBnZW9tX2xpbmUoY29sb3IgPSBcImJsdWVcIikgK1xuICAgICAgIGdlb21fc21vb3RoKG1ldGhvZD1sbSwgc2U9RkFMU0UsIGNvbD0ncmVkJykgKyB5bGltKDAsNCkgK1xuICAgICAgIGxhYnMoeCA9IFwiQ291cnNlXCIsIHkgPSBcIiBTdGFuZGFyZCBkZXZpYXRpb24gb2YgZ3JhZGVzXCIsIHRpdGxlID0gXCJTdGFuZGFyZCBkZXZpYXRpb24gb2YgZ3JhZGVzIGJ5IENvdXJzZVwiKVxuYGBgIn0= -->

```r
ggplot(dfgraphC, aes(Course, SDperCourse, group = 1)) +
       geom_point(color = "blue") + geom_line(color = "blue") +
       geom_smooth(method=lm, se=FALSE, col='red') + ylim(0,4) +
       labs(x = "Course", y = " Standard deviation of grades", title = "Standard deviation of grades by Course")
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


## Create a graph with the skewness of grades by student

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KGRmZ3JhcGhTLCBhZXMoU3R1ZGVudHMsIFNrZXdwZXJTdHVkZW50LCBncm91cCA9IDEpKSArXG4gICAgICAgZ2VvbV9wb2ludChjb2xvciA9IFwiYmx1ZVwiKSArIGdlb21fbGluZShjb2xvciA9IFwiYmx1ZVwiKSArXG4gICAgICAgZ2VvbV9zbW9vdGgobWV0aG9kPWxtLCBzZT1GQUxTRSwgY29sPSdyZWQnKSArIHlsaW0oLTIsMSkgK1xuICAgICAgIGxhYnMoeCA9IFwiU3R1ZGVudHNcIiwgeSA9IFwiIFNrZXduZXNzIG9mIGdyYWRlc1wiLCB0aXRsZSA9IFwiU2tld25lc3Mgb2YgZ3JhZGVzIGJ5IFN0dWRlbnRcIilcbmBgYCJ9 -->

```r
ggplot(dfgraphS, aes(Students, SkewperStudent, group = 1)) +
       geom_point(color = "blue") + geom_line(color = "blue") +
       geom_smooth(method=lm, se=FALSE, col='red') + ylim(-2,1) +
       labs(x = "Students", y = " Skewness of grades", title = "Skewness of grades by Student")
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


## Create a graph with the skewness of grades by course

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KGRmZ3JhcGhDLCBhZXMoQ291cnNlLCBTa2V3cGVyQ291cnNlLCBncm91cCA9IDEpKSArXG4gICAgICAgZ2VvbV9wb2ludChjb2xvciA9IFwiYmx1ZVwiKSArIGdlb21fbGluZShjb2xvciA9IFwiYmx1ZVwiKSArXG4gICAgICAgZ2VvbV9zbW9vdGgobWV0aG9kPWxtLCBzZT1GQUxTRSwgY29sPSdyZWQnKSArIHlsaW0oLTIsMSkgK1xuICAgICAgIGxhYnMoeCA9IFwiQ291cnNlXCIsIHkgPSBcIiBTa2V3bmVzcyBvZiBncmFkZXNcIiwgdGl0bGUgPSBcIlNrZXduZXNzIG9mIGdyYWRlcyBieSBDb3Vyc2VcIilcbmBgYCJ9 -->

```r
ggplot(dfgraphC, aes(Course, SkewperCourse, group = 1)) +
       geom_point(color = "blue") + geom_line(color = "blue") +
       geom_smooth(method=lm, se=FALSE, col='red') + ylim(-2,1) +
       labs(x = "Course", y = " Skewness of grades", title = "Skewness of grades by Course")
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


## Create a graph with the kurtosis of grades by student

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KGRmZ3JhcGhTLCBhZXMoU3R1ZGVudHMsIEt1cnRvc2lzcGVyU3R1ZGVudCwgZ3JvdXAgPSAxKSkgK1xuICAgICAgIGdlb21fcG9pbnQoY29sb3IgPSBcImJsdWVcIikgKyBnZW9tX2xpbmUoY29sb3IgPSBcImJsdWVcIikgK1xuICAgICAgIGdlb21fc21vb3RoKG1ldGhvZD1sbSwgc2U9RkFMU0UsIGNvbD0ncmVkJykgKyB5bGltKC0zLDEpICtcbiAgICAgICBsYWJzKHggPSBcIlN0dWRlbnRzXCIsIHkgPSBcIiBLdXJ0b3NpcyBvZiBncmFkZXNcIiwgdGl0bGUgPSBcIkt1cnRvc2lzIG9mIGdyYWRlcyBieSBTdHVkZW50XCIpXG5gYGAifQ== -->

```r
ggplot(dfgraphS, aes(Students, KurtosisperStudent, group = 1)) +
       geom_point(color = "blue") + geom_line(color = "blue") +
       geom_smooth(method=lm, se=FALSE, col='red') + ylim(-3,1) +
       labs(x = "Students", y = " Kurtosis of grades", title = "Kurtosis of grades by Student")
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


## Create a graph with the kurtosis of grades by course

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2dwbG90KGRmZ3JhcGhDLCBhZXMoQ291cnNlLCBLdXJ0b3Npc3BlckNvdXJzZSwgZ3JvdXAgPSAxKSkgK1xuICAgICAgIGdlb21fcG9pbnQoY29sb3IgPSBcImJsdWVcIikgKyBnZW9tX2xpbmUoY29sb3IgPSBcImJsdWVcIikgK1xuICAgICAgIGdlb21fc21vb3RoKG1ldGhvZD1sbSwgc2U9RkFMU0UsIGNvbD0ncmVkJykgKyB5bGltKC0zLDApICtcbiAgICAgICBsYWJzKHggPSBcIkNvdXJzZVwiLCB5ID0gXCIgS3VydG9zaXMgb2YgZ3JhZGVzXCIsIHRpdGxlID0gXCJLdXJ0b3NpcyBvZiBncmFkZXMgYnkgQ291cnNlXCIpXG5gYGAifQ== -->

```r
ggplot(dfgraphC, aes(Course, KurtosisperCourse, group = 1)) +
       geom_point(color = "blue") + geom_line(color = "blue") +
       geom_smooth(method=lm, se=FALSE, col='red') + ylim(-3,0) +
       labs(x = "Course", y = " Kurtosis of grades", title = "Kurtosis of grades by Course")
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->

