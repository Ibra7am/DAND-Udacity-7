# Flights Data Exploration
## by Ibrahim Alraigi


## Dataset

> Have you ever been stuck in an airport because your flight was delayed or cancelled and wondered if you could have predicted it if you'd had more data? This is our chance to find out!

That was the challenge by RITA when they provided this dataset, it consists of flight arrival and departure details for all commercial flights within the USA for the year 2008. It is a huge "Airline on-time performance" dataset that contains 7,009,728 flights with 29 features.

[Data can be found here](http://stat-computing.org/dataexpo/2009/the-data.html)

#### The following issues were found and resolved:
- `DepDelay` has some missing values, we will fix that by discovering a pattern that is related to those missing data or if we couldn't find one, we will just drop them since they represent only a very small portion
- `DepTime, CRSDepTime, ArrTime, CRSArrTime` are of type float rather than timedelta object
- `CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay, CancellationCode` have both NaN's and 0's, covert all to 0's
- Add column `Delayed` if the flight is delayed based on `DepDelay` as 1 (Yes) or 0 (No)


## Summary of Findings

My main interest was in figuring out the following:

- what features are best for predicting whether there will be a delay for the flight or not.
- what features are best for predicting whether the flight will be canceled or not.

### At the univariate exploration level I found the following:
- For the `Delayed` variable, at first, when I considered any flight with `Departure delay > 0` is a delayed flight, almost 40% of flights were delayed, which is unusual. After invistigation with data visualaization, we found that many flights are delayed with around 5 minutes only, so I changed the threshhold to be 5 minutes which reduced the delayed flights percentage to 28%, which is more reasonable. 
- For the `Cancelled` variable, only 1% of flights are cancelled, and that actually makes sense so we didn't need to perform any transformations.


### At the bivariate exploration level I found the following:
Many categorical features have relationships with the features of interest (i.e. `Delayed` and `Cancelled`), such as `UniqueCarrier, Origin, Dest, DayOfWeek, CRSDepTime and Diverted`. 

Those features (i.e. Carriers, Origins, Destinations, Day of the week, Scheduled departure time and Diverted) affect delaying flights greatly, for example, on Friday's (from DayOfWeek feature) or after 6 PM (from CRSDepTime feature) flights tend to have higher delay rates than on other days or before 6 PM. In a similar manner, some carriers, origins or destinations tend to have more delay rates than others. For instance, carriers such as CD, AA, UA and WN have delay rates above 30% of their flights, while carriers like AQ and HA have delaying rates less than 12%.


### At the multivariate exploration level I found the following:
Flights delay rates vary based on the carriers and the day of the week greatly for some carriers while not as much for others. An example for that is if we consider the carrier HA on Friday's is averaging 10% delay rate while on Mondays the same carrier has a delay rate of 35%. 

Other than that the way that departure times were affecting flights delay rate didn't change when categorized them by the day of the week. Which supports what we observed before about the strong relationship between departure times and flights delay rates.


## Key Insights for Presentation

In the presentation, my main focus was "what" my features of interest (i.e delaying and canceling flights) are related to or may be affected by other features rather than "how" I come up with those visuals or conclusions.
