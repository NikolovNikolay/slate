# Referrals

The referral service is used to provide partner redirects
to Skyscanner pages based to provided request parameters. 
It can redirect to different pages within Skyscanner based on the provided {pagetype} parameter 
(for the full list of page types and examples see below).

*API endpoint*

The API is accessible at **https://skyscanner.net/g/referrals/v1**

There is one main endpoint with the following URL structure:

`https://skyscanner.net/g/referrals/v1/{vertical}/{pagetype}?associateid={associateId}`

The endpoint serves only GET requests and responds with HTTP status 301 redirecting to the desired Skyscanner page.

For the different possible values of the parameters and for additional query parameters
check the tables below.

*TRY IT OUT*

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/84b89b3a51c23e6230d7)

*REQUEST PARAMETERS*

| Parameter | Description |
| --------- | ------- |
| ```vertical``` <br><span class="required">REQUIRED</span> | The vertical you want to redirect to. Allowed values: flights, cars|
| ```pagetype``` <br><span class="required">OPTIONAL</span> | Page type supported by each vertical. E.g. for flights -> day-view, browse-view... take a look at the next table|
| ```associateid``` <br><span class="required">OPTIONAL</span> | Associate partner id to attribute traffic to|
| ```utm_term``` <br><span class="required">OPTIONAL</span> | Used to send through a unique variable that you can track back to your campaigns.|

*PAGE TYPES*

| Vertical | Pagetypes |
| --------- | ------- |
| flights | home, day-view, calendar-month-view, browse-view, multicity, cheap-flights-to, flights-airline |
| cars | home, day-view |

## Examples

An example including some of the parameters looks like:

Please try to avoid using `locale`, `market` and `currency`, as these values will be governed by Skyscanner market detection logic on the Skyscanner site. If you believe you need to use these, please discuss with your account manager.

`GET https://skyscanner.net/g/referrals/v1/flights/day-view/?origin=cdg&destination=edi&outboundDate=2019-10-14&utm_term=summer&associateid=MY_ID_123`

`GET https://skyscanner.net/g/referrals/v1/flights/calendar-month-view/?origin=cdg&destination=edi&iym=1910&utm_term=summer&associateid=MY_ID_123`

`GET https://skyscanner.net/g/referrals/v1/cars/day-view/?pickupPlace=BCN&dropoffPlace=BCN&pickupTime=2019-09-10T10:00&dropoffTime=2019-09-15T10:00&driverAge=42&associateid=MY_ID_123`

Preferred airlines:  
You can find IATA airline codes [here](https://www.iata.org/publications/pages/code-search.aspx)

`GET https://skyscanner.net/g/referrals/v1/flights/day-view?airlines=AA,!FB&market=UK&currency=GBP&locale=en-GB&origin=cdg&destination=edi&outboundDate=2020-10-14&inboundDate=2020-10-21`

Preferred alliances:

`GET https://skyscanner.net/g/referrals/v1/flights/day-view?alliances=oneworld,Star%20Alliance&market=UK&currency=GBP&locale=en-GB&origin=cdg&destination=edi&outboundDate=2020-10-14&inboundDate=2020-10-21`

Departure times - In this example the query paramter configures the filters to have the first leg's departure time as default (-), and the second leg between 0 (00:00) and 990 minutes (16:30).

`GET https://skyscanner.net/g/referrals/v1/flights/day-view?departure-times=-%7C0-990&market=UK&currency=GBP&locale=en-GB&origin=cdg&destination=edi&outboundDate=2020-10-14&inboundDate=2020-10-21`

Duration:

`GET https://skyscanner.net/g/referrals/v1/flights/day-view?duration=1320&market=UK&currency=GBP&locale=en-GB&origin=cdg&destination=edi&outboundDate=2020-10-14&inboundDate=2020-10-21`


Specific request query parameters are provided in tables below.

*RESPONSE PARAMETERS*

A successful response contains no content and returns [HTTP 301](https://en.wikipedia.org/wiki/HTTP_301).
The URL to redirect to is provided in the Location header of the response.

<aside class="warning">
Please refer to our <a href="#response-codes">response codes</a> in case of unsuccessful response.
</aside>

## Flights Parameters

*Flights - Referral*

| Page type | Description  |
| --- | ---|
| [day-view](#flights-day-view-supported-parameters-schema) | Flights Day View [Example Link](https://www.skyscanner.net/transport/flights/sof/ams/200813/200819/?adults=1&children=2&adultsv2=1&childrenv2=3%7c2&infants=0&cabinclass=economy&rtn=1&preferdirects=false&outboundaltsenabled=false&inboundaltsenabled=false&ref=home#/)|
| [calendar-month-view](#flights-calendar-month-view-supported-parameters-schema) | Flights MonthView [Example Link](https://www.skyscanner.net/transport/flights/sof/ams/?adults=1&children=2&adultsv2=1&childrenv2=3%7C2&infants=0&cabinclass=economy&rtn=1&preferdirects=false&outboundaltsenabled=false&inboundaltsenabled=false&oym=2008&iym=2008&ref=home&selectedoday=01&selectediday=01)|
| [browse-view](#flights-browse-view-supported-parameters-schema) | Flights BrowseView [Example Link](https://www.skyscanner.net/transport/flights-from/edi/?adults=1&children=2&adultsv2=1&childrenv2=3%7c2&infants=0&cabinclass=economy&rtn=1&preferdirects=false&outboundaltsenabled=false&inboundaltsenabled=false&oym=2008&iym=2008&ref=home)|
| [multicity](#flights-day-view-for-multicity-search-schema) | Flights Multicity [Example Link](https://www.skyscanner.net/transport/d/sof/2020-08-13/ams/ams/2020-08-19/lond/lond/2020-08-20/sof?adults=1&children=2&adultsv2=1&childrenv2=3%7c2&infants=0&cabinclass=economy&ref=home#/)|
| [home](#flights-home-page-supported-parameters-schema) | Skyscanner's Home [Example Link](https://www.skyscanner.net/)|
| [cheap-flights-to](#cheap-flights-to-supported-parameters-schema) | Cheap Flights To [Example Link](https://www.skyscanner.net/za/en-gb/zar/flights-to/bom/cheap-flights-to-mumbai-airport.html)|
| [flights-airline](#flights-airline-supported-parameters-schema) | Flights Airline [Example Link](https://www.skyscanner.net/airline/airline-emirates-ek.html)|

For more details, please see our [Examples](#examples) 

## Cars Parameters

*Cars - Referral*

| API endpoint | Description  |
| --- | ---|
| [day-view](#carhire-day-view-supported-parameters-schema) | CarHire DayView [Example Link](https://www.skyscanner.net/carhire/results/95565041/95565041/2020-08-20T10:00/2020-08-21T10:00/30)|
| [home](#carhire-home-page-supported-parameters-schema) | CarHire Home [Example Link](https://www.skyscanner.net/carhire) |
