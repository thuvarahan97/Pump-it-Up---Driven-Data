# Pump-it-Up---Driven-Data

## Preprocessing

### Initiating the preprocessing task

* At first, "id" is set as the index of train data and test data.
* Count of train labels are plotted in a bar graph, and it shows that the train data is unbalanced.

### Checking distribution of features with train labels

* Count of status_group values for some of the columns of the train data are plotted to check the distribution of data.

### Removing duplicate values from "installer" and "funder" columns

* In both train data and test data, the "installer" column values have duplicates with captial and small letters, extra spaces, and forward and backward slashes. Thus, the values of "installer" column are trimmed, splitted by spaces, first element of the splitted output array is obtained, and "/" and "\" are replaced.
* Furthermore, the "installer" column values have only very small count for many values compared to the maximum count in the column. Therefore, the values with count less than 100 are replaced with "other".
* Similarly, the "funder" column values have only very small count for many values compared to the maximum count in the column. Therefore, the values with count less than 100 are replaced with "other".

### Handling missing data

* Count of null values in each column in train and test data are checked
* All the columns with named string values are encoded as numbers using Label Encoding, before filling some of the columns with missing data.
  * The columns are 'funder', 'installer', 'wpt_name', 'basin', 'subvillage', 
                  'region', 'lga', 'ward', 'public_meeting', 'recorded_by', 
                  'scheme_management', 'permit', 'extraction_type', 
                  'extraction_type_group', 'extraction_type_class', 'management',
                  'management_group', 'payment', 'payment_type', 'water_quality',
                  'quality_group', 'quantity', 'quantity_group', 'source', 'source_type',
                  'source_class', 'waterpoint_type', and 'waterpoint_type_group'.
* According to the plotted graph, the columns such as 'scheme_name', 'scheme_management', 'installer', 'funder', 'public_meeting', 'permit' and 'subvillage' have null values. Among them, "scheme_name" column has null values of about 50% of all the missing column values, which is much higher percentage compared to other missing columns. Therefore, "scheme_name" is dropped from the train and test data.
* Then, 'scheme_management', 'installer', 'funder', 'public_meeting', 'permit' and 'subvillage' are filled with their respective median values in both train and test data.

### Removing outliers

* It is identified that 'latititude', 'longitude' and 'gps_height' columns have outliers where the 'longitude' and 'gps_height' have negative values. The 'latitude' column values with respect to 'longitude' negative values too seems unreal values. Therefore, 
