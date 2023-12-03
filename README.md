# Agricultural Productivity Along the NSW Coastline:
This research project evaluated the Agricultural viability of NSW's Coastal Local Government Areas. Originally undertaken as a work project and re-completed here, it showcases the utilisation of excel, R (Programming language) and concludes in a short report on the findings.

## Data Sourcing
The first component of this research project was sourcing appropriate data that could be referenced to quantify the level of agricultural production for different regions along the NSW coastline. While there are many sources that claim to have accurate numbers in their reports, it was important that the data source have a level of public authority and trust behind their reporting.

After some preliminary research I discovered the Australian Government's [*Australian Agricultural Census 2020-2021*](https://www.agriculture.gov.au/abares/aclump/land-use/agriculture-census-dashboards) that is run and managed by the Department of Agriculture, Fisheries and Forestry. Importantly, this has two dashboards that utilise data from the census, extracting  key metrics by [Local Government Area (LGA)](https://www.agriculture.gov.au/abares/aclump/land-use/agriculture-census-dashboards-lga) and [Australian Statistics Geography Standard Edition 3 regions](https://www.agriculture.gov.au/abares/aclump/land-use/agriculture-census-dashboards-sa2), commonly known as "Statistical Areas". The image below is a screenshot of one of these dashboards.

<img width="1173" alt="SA2_Ag_Census_Dashboard" src="https://github.com/HarryLloyd231196/Gross_Agricultural_Value/assets/142588638/b6aacb0d-7e5e-4853-8f3c-1b6bddd62200">

*Reference: Department of Agriculture, Fisheries and Forestry: Agricultural Commodities 2020-2021 by SA2 Region*

These dashboards provided an easy way to understand the available data, but they were restricted in their capacity for the analysis that I was undertaking. They provided very high level details for "Top SA2 Regions" and "Top LGAs" but no scope for detailed comparison between regions. What they did provide however, was a reference for their original data source from the Australian Bureau of Statistics on [Agricultural Commodities Produced 2020-2021.](https://www.abs.gov.au/statistics/industry/agriculture/value-agricultural-commodities-produced-australia/2020-21) The website itself only gave summary statistics on the data collated through the census but at the bottom of the page were links to the raw data in .xlsx format for SA2 Regions as well as Local Government Areas.

With an appropriate first data source downloaded it was now time to select appropriate LGA's for the analysis. For this, the original dashboard provided by the Department of Agriculture, Fisheries and Forestry was extreamly useful due to its in-built map of Australia. For this analysis it was important to select Coastal LGA's that were akin to that of the MidCoast Council. The MidCoast Council is a recently amalgamated Council that is made up of 3 historic areas; The Greater Taree City Council, The Great Lakes Council, and The GLoucester Council. The MidCoast Council covers just over 10,000km2 from Harrington in the north, to Hawks Nest & Tea Gardens in the south, and west to the Barrington Tops.

<img width="1173" alt="MidCoast_Regional_Map" src="https://github.com/HarryLloyd231196/Gross_Agricultural_Value/assets/142588638/37eb0c87-90be-49aa-adb3-7782e230b635">

Reference: [MidCoast Council. Our Region](https://www.midcoast.nsw.gov.au/Your-Council/About-MidCoast-Council/About-us/Our-region)

With this in mind I returned to the dashboard and began to select LGA's that were of comparable geography for my analysis. In total, 39 LGA's were selected (including the MidCoast) and their Council names were downloaded from the dashboard as an xlsx. file. The following is screenshot of the selected LGA's on the SA2 Region Dashboard.

<img width="1173" alt="LGAs_Selected" src="https://github.com/HarryLloyd231196/Gross_Agricultural_Value/assets/142588638/76c45f8c-fb7f-445b-93e5-ea0305095261">

Following this I had all of the required information to begin preparing my data for analysis. I had appropriate sources form which to extract insights into Agricultural production along the NSW east coast as well as a list of 39 LGA's from which to compare against the MidCoast. The only issue that I has with the data was that it included all 485 LGA in Australia. In order to extract the data from this extensive dataframe I was given a few options. I was able to take the two dataframes and perform a LEFTJOIN, matching the larger dataframe to my smaller table of 39 LGA names, or I could perform a VLOOKUP() in excel and pull the data into a new table. Given that I was already working in excel (and the fact my workplace does not have any licensing for Intergrated Development Environments (IDE's), I would go down the VLOOKUP() route.

The first step in this process was to create a new excel workbook that contained both of the relevant dataframes. While this could have been done across workbooks, for the sake of simplifying the cell referenceing and keeping the original data unedited, I opted to create a new book. This new book now contained a copy of the original 485 LGA's and all of their related data in a single sheet, and the 39 selected LGA's and some other data (Lat & Long, Geometry) that was automatically pulled from the dashboard.

<img width="1173" alt="ABS_LGA_Data" src="https://github.com/HarryLloyd231196/Gross_Agricultural_Value/assets/142588638/a4fc1994-d2d6-48d7-9c47-1792389ddcf2">

<img width="1173" alt="LGA_Dashboard_Data" src="https://github.com/HarryLloyd231196/Gross_Agricultural_Value/assets/142588638/fb82caa0-b313-4ad6-86ce-6978dad97a50">

Because the additional columns extracted from the dashboard weren't required they were removed from the dataframe to make way for the import of the agricultural data from the ABS. The first column was also renamed to LGA to simplify its title. In order to extract the unique values from the "Commodity description" column from LGA 1 (Working) excels unique() function was called as . . .

" =UNIQUE(RawData[Commodity description]) "

These values were then transposed as column names for later reference.

<img width="1173" alt="Commodities_Transposed" src="https://github.com/HarryLloyd231196/Gross_Agricultural_Value/assets/142588638/32124575-ac75-438c-b043-8867441b6d46">

The dataframe in LGA-map_data was ready to be filled with the data extracted from LGA 1 (Working). Initially I ran into an issue witth VLOOKUP(). The function is built in such a way that it always returns the first instance of the "lookup_value" that it locates within the "lookup_array". If the LGA column was used as a "lookup_value" all of the data would be pulled from the first commodity class, in this instance "Broadacre crops - Cereal crops - Wheat for grain". If I used the commodity description as the "lookup_value", all of the data for each commodity, irrespective of the LGA, would be pulled from the Australia wide statistics at the top of the table. In order to resolve this, I created a "Reference_column" to the left of the original ABS data. This column would be filled with a reference string that was the LGA and the commodity description, sepperated by a dash ( - ) as the following example demonstrates . . .

Australia - Broadacre crops - Cereal crops - Wheat for grain

This was achieved with the following code. . .

=[@[Region label]]&" - "&[@[Commodity description]]

<img width="1173" alt="Reference_column " src="https://github.com/HarryLloyd231196/Gross_Agricultural_Value/assets/142588638/ee098a50-520e-44fc-9f89-1ca175ffc79c">

The purpose of creating this helper column was to give each row in the LGA data a unique value that could be called upon to fill the LGA_map_data dataframe. By creating a VLOOKUP() with a "lookup_value" that paired with these unique values, I could be sure that the data being pulled across from the ABS was correct. The following code was used to achieve this. . .

=VLOOKUP($A2&" - "&B$1,RawData[#All],6,FALSE)

In the code above the "$" signs were used to ensure that when the code was dragged across the rest of the cells for the dataframe, the VLOOKUP() continued to reference the correct cells (LGA & Commodity description) in the table.

<img width="1173" alt="VLOOKUO_Showcase" src="https://github.com/HarryLloyd231196/Gross_Agricultural_Value/assets/142588638/83305c3f-d92e-4abe-b146-3f222f1f0475">

The issue with the above code is that for some LGA's certain commodities were not produced, and as such are absent from the ABS reference table. To resolve this issue, the VLOOKUP() was wrapped in an simple IFERROR() function and made to return a "0" value. This was used to fill the dataframe. following which the data was converted into a table with appropriate formatting.

<img width="1173" alt="Working_Dataframe_Showcase" src="https://github.com/HarryLloyd231196/Gross_Agricultural_Value/assets/142588638/52226d27-d236-4d9e-94f9-1dcaf60e50e9">

With the table correctly filled and data  formatted, the following stages of this analysis were undertaken in R Studio to allow for a highly tailored approach to the investigation.

