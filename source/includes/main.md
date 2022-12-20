# Introduction

The Daytrip API is organized around REST. Our API accepts JSON-encoded request bodies, returns JSON-encoded responses, and uses standard HTTP response codes and verbs.

The API can be used to search for trip options, customize a trip with stops, book a trip or cancel a booking.

# Authentication

> To authorize, use this code:

```python

```

```bash
curl "https://api.mydaytrip.com/partners/v3/trip/search"
  -H "x-api-key: your-api-key"
```

```javascript

```

> Make sure to replace `your-api-key` with your API key.

Daytrip API uses API keys to allow access to the API. The API key needs to be included in `x-api-key` header with each API request.

Your API key carries many privileges, so be sure to keep it secure! Do not share your secret API key in publicly accessible areas such as GitHub, client-side code, and so forth.

# Trip API

A trip is a representation of passenger transportation from point A to point B. Each search will usually return multiple trip options that can be booked. Options can differ by vehicle type or by being private or shared with other travelers. Shared trips have predefined pick up and drop off points and departure times. For private trips pick up and drop off points as well as departure time are matching the search request. Private trips can also be customized by adding stops if available.

Trip API can be used to search for trip options, customizing an option with stops and then booking the option. A typical simple flow without stop customization would look like this:

1. call /search endpoint to get possible options
2. call /book endpoint to book the chosen option

A flow with adding stops would look like this:

1. call /search endpoint to get possible options
2. call /customize endpoint to add stops to the chosen option
3. call /book endpoint to book the customized option

## Search

> To search for a trip from Prague to Vienna for three passengers, use this call:

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```bash
curl "https://api.mydaytrip.com/partners/v3/trip/search?originLongitude=14.2559&originLatitude=50.10&destinationLongitude=16.3738&destinationLatitude=48.2082&departureTime=1766227088&passengersCount=3"
  -H "x-api-key: your-api-key"
```

```javascript

```

> The above call returns JSON structured like this:

```json
{	
	"searchId": "f0e34a1b-2b3d-4747-b426-292633b615b4",
	"passengersCount": 3,
    "currency": "EUR",
    "options": [
		{
			"id": "1d32109f-c2e2-44fe-b2cf-461ef3730541",
			"type": "Private",
			"distanceKm": 334,
			"travelTimeMinutes": 208,
			"pickUp": {
				"lat": 50.10,
				"lon": 14.25,
				"time": "2022-12-05T18:00:00Z"				
			},
			"dropOff": {
				"lat": 48.20,
				"lon": 16.37			
			},
			"pricing": {				
				"totalPrice": 254
			},
			"vehicle": {
			    "type": "sedan",
				"maxPassengers": 3,
				"description": "Sedan comparable to a Volkswagen Passat, up to 3 passengers with luggage.",
				"image": "https://daytrip.imgix.net/vehicles/sedan.png"			
			},
			"luggage": {
				"maxTotalCarryons": 3,
				"maxTotalSuitcases": 3
			},
			"availableChildSeatTypes": [
				{
					"childSeatType": "RearFacing",
					"description": "Rear-facing infant seat",
					"ageFrom": 0,
					"ageTo": 1,
					"weightInPoundsFrom": 0,
					"weightInPoundsTo": 26,
               "weightInKilosFrom": 0,
               "weightInKilosTo": 10
				},
				{
					"childSeatType": "ForwardFacing",
					"description": "Forward-facing w/harness",
					"ageFrom": 1,
					"ageTo": 4,
					"weightInPoundsFrom": 18,
					"weightInPoundsTo": 36,
               "weightInKilosFrom": 8,
               "weightInKilosTo": 16
				},
				{
					"childSeatType": "BoosterSeat",
					"description": "Booster seat with high back",
					"ageFrom": 4,
					"ageTo": 6,
					"weightInPoundsFrom": 30,
					"weightInPoundsTo": 50,
               "weightInKilosFrom": 14,
               "weightInKilosTo": 23
				},
				{
					"childSeatType": "Booster",
					"description": "Backless booster",
					"ageFrom": 6,
					"ageTo": 12,
					"weightInPoundsFrom": 44,
					"weightInPoundsTo": 72,
               "weightInKilosFrom": 20,
               "weightInKilosTo": 33
				}
			],
			"possibleStops": [
				{
					"id":"d280ce2a-6224-4d95-af17-a250f81b97dd",
				    "price": 31,
				    "name":"Lednice Chateau and Park",
					"image":"https://daytrip.imgix.net/lednice-chateau-and-park4.jpg",
					"title":"Vacation like a King",
					"perex":"This UNESCO-listed chateau and sprawling park was the Lichtenstein's holiday home - exactly the kind of extravagance you'd expect from a dynasty with their own country. ",
					"description":"The Liechtensteins really came into the money with the fortunes seized from Czech noblemen after their victory at the Battle of White Mountain in 1620, and Lednice was one of the presents they bought themselves. In the mid-19th century the baroque manor was given a complete makeover in the 'Windsor Gothic' style, leaving it as we see it today: a shameless flaunting of fabulous wealth, a slap in the face to anyone foolish enough to think that the French Revolution had ended high-living in Europe. The surrounding English landscape park, the largest in the country, is an incomparable swath of green, sprinkled with Romantic follies. There's also a monumental greenhouse open all year round, overflowing with exotic growths gathered by an army of botanists across the Americas. The greenhouse's exoticism is echoed by the charming minaret, constructed at the turn of the 18th century, bringing a whiff of Morocco to Moravia.\nFor more info: www.zamek-lednice.com",					  
					"durationInMinutes":60,
               "order": 1,
					"timezone":"Europe/Prague",
					"country":{
						"englishName":"Czech Republic"
					}
				},
				{
					"id":"4ee58c0c-4e56-46ef-bd22-406a1bc60e1c",
					"price": 28,
                    "name":"Mikulov",
                    "image":"https://daytrip.imgix.net/510.jpg",
                    "title":"The Heart of Czech Wine Country",
                    "perex":"A town with a history as deep and flavourful as its wine, Mikulov provides a perfect combination of relaxation and exploration.",
                    "description":"Often favoured by visitors with a more active approach to life, Mikulov has much to offer. Surrounded by idyllic countryside, crisscrossed by bicycle paths and marked hiking trails, and the nearby Nové Mlýny lakes, there is something for everyone to enjoy. After all that fresh air, a glass of wine will be more than welcome, and fortunately, Mikulov is the centre for Czech wine making. Due to a high concentration of limestone in the local soil, wine from this region has a unique character and distinct taste. If you like your wine with a side-serving of history, Mikulov Castle dates from the 1730s, and the Dietrichstein Tomb is the final resting place of a Bohemian noble family. Mikulov is also significant for its strong Jewish history. In the early 1800s Mikulov's Jewish Quarter was the largest in Moravia with half the town's inhabitants being of Jewish faith.",
                    "durationInMinutes":60,
                    "order": 2,
                    "timezone":"Europe/Prague",
                    "country":{
                      "englishName":"Czech Republic",
                    }
				}
         ]
		},
		{
			"id": "b071e9f8-54d9-44be-bb5f-feae5aafd771",
			"type": "Private",
			"distanceKm": 334,
			"travelTimeMinutes": 208,
			"pickUp": {
				"lat": 50.10,
				"lon": 14.25,
				"time": "2022-12-05T18:00:00Z"				
			},
			"dropOff": {
				"lat": 48.20,
				"lon": 16.37			
			},
			"pricing": {				
				"totalPrice": 320
			},
			"vehicle": {
			    "type": "mpv",
				"maxPassengers": 4,
				"description": "Compact MPV comparable to a Volkswagen Touran, up to 4 passengers with luggage.",,
				"image": "https://daytrip.imgix.net/vehicles/mpv.png"
			},
			"luggage": {
				"maxTotalCarryons": 4,
				"maxTotalSuitcases": 4
			},
			"availableChildSeatTypes": [
				{
					"childSeatType": "RearFacing",
					"description": "Rear-facing infant seat",
					"ageFrom": 0,
					"ageTo": 1,
					"weightInPoundsFrom": 0,
					"weightInPoundsTo": 26,
               "weightInKilosFrom": 0,
               "weightInKilosTo": 10
				},
				{
					"childSeatType": "ForwardFacing",
					"description": "Forward-facing w/harness",
					"ageFrom": 1,
					"ageTo": 4,
					"weightInPoundsFrom": 18,
					"weightInPoundsTo": 36,
               "weightInKilosFrom": 8,
               "weightInKilosTo": 16
				},
				{
					"childSeatType": "BoosterSeat",
					"description": "Booster seat with high back",
					"ageFrom": 4,
					"ageTo": 6,
					"weightInPoundsFrom": 30,
					"weightInPoundsTo": 50,
               "weightInKilosFrom": 14,
               "weightInKilosTo": 23
				},
				{
					"childSeatType": "Booster",
					"description": "Backless booster",
					"ageFrom": 6,
					"ageTo": 12,
					"weightInPoundsFrom": 44,
					"weightInPoundsTo": 72,
               "weightInKilosFrom": 20,
               "weightInKilosTo": 33
				}
			],
			"possibleStops": [
				{
					"id":"d280ce2a-6224-4d95-af17-a250f81b97dd",
				    "price": 31,
				    "name":"Lednice Chateau and Park",
					"image":"https://daytrip.imgix.net/lednice-chateau-and-park4.jpg",
					"title":"Vacation like a King",
					"perex":"This UNESCO-listed chateau and sprawling park was the Lichtenstein's holiday home - exactly the kind of extravagance you'd expect from a dynasty with their own country. ",
					"description":"The Liechtensteins really came into the money with the fortunes seized from Czech noblemen after their victory at the Battle of White Mountain in 1620, and Lednice was one of the presents they bought themselves. In the mid-19th century the baroque manor was given a complete makeover in the 'Windsor Gothic' style, leaving it as we see it today: a shameless flaunting of fabulous wealth, a slap in the face to anyone foolish enough to think that the French Revolution had ended high-living in Europe. The surrounding English landscape park, the largest in the country, is an incomparable swath of green, sprinkled with Romantic follies. There's also a monumental greenhouse open all year round, overflowing with exotic growths gathered by an army of botanists across the Americas. The greenhouse's exoticism is echoed by the charming minaret, constructed at the turn of the 18th century, bringing a whiff of Morocco to Moravia.\nFor more info: www.zamek-lednice.com",					  
					"durationInMinutes":60,
               "order": 1,
					"timezone":"Europe/Prague",
					"country":{
						"englishName":"Czech Republic"
					}
				},
				{
					"id":"4ee58c0c-4e56-46ef-bd22-406a1bc60e1c",
					"price": 28,
                    "name":"Mikulov",
                    "image":"https://daytrip.imgix.net/510.jpg",
                    "title":"The Heart of Czech Wine Country",
                    "perex":"A town with a history as deep and flavourful as its wine, Mikulov provides a perfect combination of relaxation and exploration.",
                    "description":"Often favoured by visitors with a more active approach to life, Mikulov has much to offer. Surrounded by idyllic countryside, crisscrossed by bicycle paths and marked hiking trails, and the nearby Nové Mlýny lakes, there is something for everyone to enjoy. After all that fresh air, a glass of wine will be more than welcome, and fortunately, Mikulov is the centre for Czech wine making. Due to a high concentration of limestone in the local soil, wine from this region has a unique character and distinct taste. If you like your wine with a side-serving of history, Mikulov Castle dates from the 1730s, and the Dietrichstein Tomb is the final resting place of a Bohemian noble family. Mikulov is also significant for its strong Jewish history. In the early 1800s Mikulov's Jewish Quarter was the largest in Moravia with half the town's inhabitants being of Jewish faith.",
                    "durationInMinutes":60,
                    "order": 2,
                    "timezone":"Europe/Prague",
                    "country":{
                      "englishName":"Czech Republic",
                    }
				}
         ]
		},
		{
			"id": "282a8a94-2a18-42f6-9af6-c53b13d007cb",
            "type": "Shared",
			"distanceKm": 350,
			"travelTimeMinutes": 235,
			"pickUp": {
				"lat": 50.12,
				"lon": 14.27,
				"time": "2022-12-05T19:00:00Z",
				"description": "In front of the hotel Europa"				
			},
			"dropOff": {
				"lat": 48.21,
				"lon": 16.36,
				"description": "Next to the railway station"
			},
			"pricing": {
				"pricePerPassenger": 180,
				"totalPrice": 540
			},
			"vehicle": {
			    "type": "shuttle",
				"maxPassengers": 10,
				"description": "Shuttle comparable to a Mercedes-Benz Vito, up to 10 passengers with luggage.",
				"image": "https://daytrip.imgix.net/vehicles/shuttle.png"
			},
			"luggage": {
				"maxCarryonsPerPerson": 1,
				"maxSuitcasesPerPerson": 1,
				"maxTotalCarryons": 3,
				"maxTotalSuitcases": 3
			},
			"seatsAvailable": 8,
			"availableChildSeatTypes": [],
			"possibleStops": []			
		},
		{
			"id": "4b137906-008a-49cf-b248-e3827b3a3175",
            "type": "Shared",
			"distanceKm": 350,
			"travelTimeMinutes": 235,
			"pickUp": {
				"lat": 50.12,
				"lon": 14.27,
				"time": "2022-12-05T21:00:00Z",
				"description": "In front of the hotel Europa"				
			},
			"dropOff": {
				"lat": 48.21,
				"lon": 16.36,
				"description": "Next to the railway station"
			},
			"pricing": {
				"pricePerPassenger": 190,
				"totalPrice": 570
			},
			"vehicle": {
			    "type": "shuttle",
				"maxPassengers": 10,
				"description": "Shuttle comparable to a Mercedes-Benz Vito, up to 10 passengers with luggage.",
				"image": "https://daytrip.imgix.net/vehicles/shuttle.png"
			},
			"luggage": {
				"maxCarryonsPerPerson": 1,
				"maxSuitcasesPerPerson": 1,
				"maxTotalCarryons": 3,
				"maxTotalSuitcases": 3
			},
			"seatsAvailable": 5,
			"availableChildSeatTypes": [],
			"possibleStops": [],
			"includedStops": [
				{
					"id":"d280ce2a-6224-4d95-af17-a250f81b97dd",
				    "price": 31,
				    "name":"Lednice Chateau and Park",
					"image":"https://daytrip.imgix.net/lednice-chateau-and-park4.jpg",
					"title":"Vacation like a King",
					"perex":"This UNESCO-listed chateau and sprawling park was the Lichtenstein's holiday home - exactly the kind of extravagance you'd expect from a dynasty with their own country. ",
					"description":"The Liechtensteins really came into the money with the fortunes seized from Czech noblemen after their victory at the Battle of White Mountain in 1620, and Lednice was one of the presents they bought themselves. In the mid-19th century the baroque manor was given a complete makeover in the 'Windsor Gothic' style, leaving it as we see it today: a shameless flaunting of fabulous wealth, a slap in the face to anyone foolish enough to think that the French Revolution had ended high-living in Europe. The surrounding English landscape park, the largest in the country, is an incomparable swath of green, sprinkled with Romantic follies. There's also a monumental greenhouse open all year round, overflowing with exotic growths gathered by an army of botanists across the Americas. The greenhouse's exoticism is echoed by the charming minaret, constructed at the turn of the 18th century, bringing a whiff of Morocco to Moravia.\nFor more info: www.zamek-lednice.com",					  
					"durationInMinutes":60,
               "order": 1,
					"timezone":"Europe/Prague",
					"country":{
						"englishName":"Czech Republic"
					}
				}
         ]
		}
	]
}
```

This endpoint returns all trip options for given origin, destination, departure time and passenger count. Origin and destination are passed as latitude and longitude coordinates. The unit used is degree with decimal places, for example `39.753657, -117.610215`. Departure time is passed as a UNIX timestamp in seconds, like `1679463169`.

### HTTP Request

`GET https://api.mydaytrip.com/partners/v3/trip/search`

### Query Parameters

Parameter            | Description
-------------------- | -----------
originLatitude       | Origin latitude in degrees.
originLongitude      | Origin longitued in degrees.
destinationLatitude  | Destination latitude in degrees.
originLongitude      | Destination longitued in degrees.
departureTime        | Departure time as a UNIX timestamp in seconds.
passengersCount      | Count of passengers to transport.
