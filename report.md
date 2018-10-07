# Introduction

Bangkok is a crowded city. Most inner areas are already developed, so real estate developer can only purchase land to develop new condominium on farther areas, and it is harder to sell.

When it comes to advertising, there are condominium advertisement campaign in Bangkok describing how many stations away from their condomunium buildings to CBD. While the S2 station is well known as true CBD (central business district), the E6 station is on different side as popular residential area among expats.

There should be more ways to describe characteristic of other stations by comparing their overlooked building to the dominant stations that they share similar characteristics.

It will be beneficial for real estate developer to persuade customers to buy a condominium in inferior areas. There should be at least 2-3 ways to communicate that the condominium in the new area is worth buying.

# Data

There are train stations data gathered manually as a json file, each record contains latitude, longitude, and station name.

for example:
```
{
 "lat": 13.72906,
 "lng": 100.53566,
 "desc": "S2"
}
```

Each station record will be further used to find surrounding venues within 650 meters on Foursquare. Those venues will include category data, and the assumption is that top 500 popular venues of each location has different mixture across categories. The expected features are number of venues of each main category on the location.

The venues can be overlapped among stations, which is not a problem as adjacent stations are likely to share similar characteristics.

# Methodology

Because food is available everywhere in Thailand, the majority of venues tends to be food related, so the venues those are food related are too much overwhelming and should be excluded from the analysis.

There are so many sub-categories while the FourSquare API limit number of venue to 50, the data tend to be sparse, i.e. very few venues are in each sub-category, and importance of each sub-category will be diluted. The sub-category data of each venue must be mapped to its main category.

Location's character analysis will focus only on the main categories excluding food, those are:
- Arts & Entertainment
- College & Education
- Event
- Nightlife
- Outdoors & Recreation
- Professional
- Residence
- Shops
- Travel

Several location characteristics features will be used to classified using k-mean clustering. When all stations are classified in clusters, each cluster numeric label will be analyzed to describe which category contributes the most to location's characteristic using one way ANOVA F-test score with p-value < 0.05 to indicate unique characteristic among other clusters.

# Results

## cluster 0
stations: PET,S12,SAM

There are Chulalongkorn University near SAM station, Srinakharinwirot University near PET station, and Siam University near S12 station.
​

| category | F |
| --- | --- |
| **College & Education** | **171.092051** |
| Shops | 5.647899 |
​

## cluster 1

stations: CEN,CUL,E1,E5,N1,PHA,W1

These are commercial areas located at the most prime area. Siam paragon at CEN station, Emquartier at E5 station, Esplanade Ratchada at CUL station, and Central Plaza Ladprao at PHA station are large shopping complexes with leisure centre.
​

| category | F |
| --- | --- |
| **Arts & Entertainment** | **37.466271** |
| **Shops** | **28.120129** |
| Professional | 12.419282 |
| Residence | 8.249203 |
​

## cluster 2

stations: E10,E11,E12,E13,E14,E6,E7,E8,E9,HUI,KAM,LAT,N5,N7,RAM,RAT,S10,S11,S7,S8,S9,SUT

These are residential areas with no surprise, as most of them are in outer city areas.
​

| category | F |
| --- | --- |
| **Residence** | **91.370287** |
| Travel | 11.554251 |
| Nightlife | 6.767196 |
| Arts & Entertainment | 4.138550 |
​

## cluster 3

stations: BAN,E2,E3,E4,HUA,KHO,LUM,N2,N3,N4,N8,S1,S2,S3,S5,S6,SIR

The stations in this cluster are mostly located around the center of the Bangkok, comprise of office buildings.
​

| category | F |
| --- | --- |
| **Professional** | **26.424944** |
| Residence | 18.271038 |
| Shops | 17.559918 |
| Travel | 16.312009 |
| Nightlife | 6.215488 |
​

# Discussion
​
The cluster number 0 is dominated by university campuses. While PET and SAM are in inner city, S12 is at the end of train line, the most farther station in sub-urban area. The advertisement message for condominium around S12 station may emphasize on education opportunity of customer's childs.
​
The cluster number 1 is dominated by shopping and lifestyle venues. Condominiums at PHA station are at prime intersection, but still considered as outer city. The advertising campaign might set inside all those malls as they it should match customer's lifestyle.
​
The cluster number 2 are residential areas. As indicated in the introduction that there is E6 station which popular among expats, E6 is fallen in this cluster. Advertising direction would be selling these condominums to foreigners as a second home.
​
The cluster number 3 are office zones. As indicated in the introduction that S2 station is at the true CBD, a lot of white-collar jobs are available in these areas, not limited just to the S2 station. RAM station is also an example of an emerging location with new office buildings. Advertisement for condominiums in these areas should emphasize on work-life balance, as the condominium is already located in an office zone, so there is little commute time between the condominium and the office.
​
​
# Conclusion
​
This cluster prediction is based on real data, and it complies with physical potential of each location. The advertisement campaign for condominiums on outer city areas and sub-urban areas might be inspired by the condominiums inside inner city, which is sharing similar location characteristics, and belongs to the same prediction cluster.