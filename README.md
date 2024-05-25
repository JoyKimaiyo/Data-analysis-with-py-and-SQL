Data Description
The dataset encompasses detailed insights into diverse renewable energy systems, encompassing metrics such as installed capacity, energy production, consumption, storage, investment, and environmental impact. Our objective is to furnish a holistic perspective on renewable energy, conducive to research and analysis in the field of sustainable energy.

Data Preprocessing
Our initial task entails canin the dataset's numerical codes representing ‘Type_of_Renewable_Energy’ and ‘Funding_Sources’. To accomplish this, we’ll execute SQL commands:

Funding_Sources

ALTER TABLE dbo.energy_dataset_
ALTER COLUMN Funding_Sources VARCHAR(50);
UPDATE dbo.energy_dataset_
SET Funding_Sources =
 CASE Funding_Sources
 WHEN '1' THEN 'Government'
 WHEN '2' THEN 'Private'
 WHEN '3' THEN 'Public-Private Partnership'
 ELSE 'Unknown'
 END;
Type_of_Renewable_Energy

ALTER TABLE dbo.energy_dataset_
ALTER COLUMN Type_of_Renewable_Energy VARCHAR(50);
UPDATE dbo.energy_dataset_
SET Type_of_Renewable_Energy =
 CASE Type_of_Renewable_Energy
 WHEN '1' THEN 'Solar'
 WHEN '2' THEN 'Wind'
 WHEN '3' THEN 'Hydroelectric'
 WHEN '4' THEN 'Geothermal'
 WHEN '5' THEN 'Biomass'
 WHEN '6' THEN 'Tidal'
 WHEN '7' THEN 'Wave'
 ELSE 'Unknown'
 END;
We use ALTER TABLE to modify the column types of 'Funding_Sources' and 'Type_of_Renewable_Energy' to VARCHAR(50) to accommodate string values. Then, we utilize UPDATE along with CASE statements to replace numerical codes with descriptive strings for these columns.

Subsequently, we’ll verify the efficacy of these transformations by checking for ‘Unknown’ entries using the ‘DISTINCT’ keyword: distinct check for unique values in the column.

SELECT DISTINCT Type_of_Renewable_Energy FROM dbo.energy_dataset_;
SELECT DISTINCT Funding_Sources FROM dbo.energy_dataset_;
These queries utilize the SELECT DISTINCT statement to fetch unique values of 'Type_of_Renewable_Energy' and 'Funding_Sources'. By examining the distinct values, we can verify if the transformation successfully replaced numerical codes with meaningful strings.
Exploratory Analysis
Proceeding with exploratory analysis, let’s examine the relationship between ‘Type_of_Renewable_Energy’ and ‘Jobs_Created’:

SELECT
 Type_of_Renewable_Energy,
 SUM(Jobs_Created) AS Total_Jobs_Created
FROM
 dbo.energy_dataset_
GROUP BY
 Type_of_Renewable_Energy
ORDER BY
 Total_Jobs_Created DESC;
Results;

Type_of_Renewable_Energy Total_Jobs_Created
Wind 5530174
Hydroelectric 5414246
Biomass 5402836
Solar 5401364
Tidal 5352948
Geothermal 5238952
Wave 5199509

This query aggregates the ‘Jobs_Created’ column based on different types of renewable energy sources. It calculates the total jobs created for each type by using SUM along with GROUP BY to group the data based on 'Type_of_Renewable_Energy'. The results are ordered in descending order of total jobs created.
let’s delve into the count of renewable energy per category:

SELECT
 Type_of_Renewable_Energy,
 COUNT(Type_of_Renewable_Energy) AS Count
FROM
 dbo.energy_dataset_
GROUP BY
 Type_of_Renewable_Energy;
Type_of_Renewable_Energy Count
Hydroelectric 2157
Wind 2202
Biomass 2150
Tidal 2124
Wave 2093
Geothermal 2105
Solar 2169

Here, we use SELECT along with COUNT to determine the number of occurrences of each distinct 'Type_of_Renewable_Energy'. The GROUP BY clause ensures that the count is performed for each unique category. This query helps in understanding the distribution of renewable energy sources across categories.
In the next part, we will import the data from SQL to Jupyter Notebook then continue with the analysis
Link to the python part https://medium.com/@joy.kimaiyo25/data-analysis-with-sql-and-python-portfolio-project-part-2-88685e4857de
