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
