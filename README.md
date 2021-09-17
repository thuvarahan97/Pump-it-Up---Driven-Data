# Pump-it-Up---Driven-Data

## Preprocessing

### Initiate the preprocessing

* At first, "id" is set as the index of train data and test data.
* Count of train labels are plotted in a bar graph, and it shows that the train data is unbalanced.

### Check distribution of features with train labels

* Count of status_group values for some of the columns of the train data are plotted to check the distribution of data.

### Remove duplicate values from "installer" and "funder" columns

* In both train data and test data, the "installer" column values have duplicates with captial and small letters, extra spaces, and forward and backward slashes. Thus, the values of "installer" column are trimmed, splitted by spaces, first element of the splitted output array is obtained, and "/" and "\" are replaced.
* Furthermore, the "installer" column values have only very small count for many values compared to the maximum count in the column. Therefore, the values with count less than 100 are replaced with "other".
* Similarly, the "funder" column values have only very small count for many values compared to the maximum count in the column. Therefore, the values with count less than 100 are replaced with "other".
