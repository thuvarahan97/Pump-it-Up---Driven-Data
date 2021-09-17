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

* It is identified that 'latititude', 'longitude' and 'gps_height' columns have outliers where the 'longitude' and 'gps_height' have negative values. The 'latitude' column values that correspond to 'longitude' negative values too are unreal values which are nearly 0.
* 'latitude' values that correspond to the 'longitude' values which are less than 1, are set as null at first and then, grouped by 'region_code' and the null values in the 'latitude' are filled with the mean values of each group.
* 'longitude' values which are less than 1, are set as null and then, grouped by 'region_code' and the null values in the 'longitude' are filled with the mean values of each group.
* 'gps_height' values which are less than 1, are set as null and then, grouped by 'region_code' and the null values in the 'gps_height' are filled with the mean values of each group.
* The missing data count is again checked, and the null values which are still in the 'gps_height' column are filled with the mean value of the column.
* Then, 'construction_year' are identified to have 0 values. They are replaced with a value (1950) lower than the actual year minimum value (1960) in the column, assuming that the records were not made for the 'construction_year' before 1960.

### Analyzing column relationships based on dates

* "date_recorded" is obtained in datetime format.
* "construction_year" too is converted from year value to datetime format.
* A new "period" column is defined which means how long the pumps are kept planted, that is the time period between the constructed year and the last date the record was made.
* At first, the "period" is calculated by finding the difference between "construction_year" and "date_recorded".
* The obtained "period" values are converted to numeric values (timedelta64[D]).
* The "period" negative values replaced with the mean of non-negative values.
* Since the "period" values are distributed in wide range of numeric values, they are obtained into 5 bins, and label encoded.
* The "construction_year" and "date_recorded" columns are dropped from train and test datasets.

### Analyzing correlation between features

* Using Pearson Correlation, heatmap is plotted.
* 4 features such as 'extraction_type_group', 'quantity_group', 'source_type' and 'waterpoint_type_group' are identified to be the highly correlated features for the threshhold 0.85, and they are dropped from train and test dataset.

