# Scenarios

## Technology Assumptions

It is assumed that the following are available to all students:
- A statically-typed language (Java, C#, C++ etc)
- A dynamically-typed language (Python, Ruby, Node etc)
- An IDE and/or editor suitable for - and compatible with - the above.
- A web framework - ideally, one dynamically-typed and one statically-typed.
- A web server or other means of serving static web pages
- A JavaScript enabled web browser
- An internet connection
- A database on which they the student has sufficient permissions to create, manage & drop multiple tables, and load data.
- A means to visualise the above database and all data stored in it.

## Scenario 1

__Title__ Design & build a static cruise website from imported data files.

__Description__

TUI is a global holiday brand that offers: Beach, City, Ski & Cruise holidays and much more.  Recently, a number of advancements have been made to the content stored about cruises, itineraries & cruise Ships.  Your team has been assigned the task of re-designing the current cruise website to include this enhanced content.

Cruise is a premium product aimed at affluent customers, parents of grown up children & those over 50.  The display of cruise content is expected to reflect the quality of the product & the target market.  

__Level 1__

- Analyse a number of data files & create a normalised data structure to store the data.
- Create a database in which to store the data from the data files using the above structure.
- Programatically load the data from the data files into the database.  This program should be capable of being automated.

__Level 2__

- Design & build a suitable HTML template to display a cruise, it's itinerary & ship information.
- Programatically build a number of HTML pages (one per cruise) using the contents of the database & the above template.  This program should be capable of being automated.

__Level 3__

- Design & build an index.html template.  Include suitable navigation to enable the customer to find every & display every cruise within the site.  Like all the other web pages - this needs to be programatically built.


## Scenario 2

__Title__ Onboard excursion booking system.

__Description__

One of the main reasons for customers choosing a cruise (over other types of holiday) is the potential to see many different countries, cities & places of interest in a short period of time.

At TUI we are very keen to ensure that our customers have great time, relax & and have the opportunity to see as much (or as little) of the countries we visit as possible.  One of the best ways of doing this is to offer excursions (trips away from the ship at a particular port).  

Excursions are tricky to manage as there is a limitation on coaches & seats on them to transport the customers off-ship.

__Level 1__

- You have access to a file which has available excursions for a particular cruise & that are available from each of the ports-of-call that the cruise stops at.
- Design & build an on-board excursion booking system using the given database.  At this stage all a customer can do is book a number of seats on an excursion - you should require their name, number of seats required & their cabin number.  The customer/cabin number combination must be unique - a customer cannot book twice.
- Once all seats are sold no more bookings can be taken.
- Assume that no seats are handed back.

__Level 2__

- Your booking system has proven highly effective & very popular.  But, some customers would like to return some seats previously booked.  Implement booking cancellation within the system.
- You have also been asked to add a 'wait list' for seats on each excursion.  So that when the coach is full a customer can register interest in obtaining a seat.  
- For this purpose - assume there is only one coach with 32 seats per excursion & that the customer always accepts & purchases the seats they have requested.  Even though they might cancel their booking at a later date.
- Implement the following business logic - choose suitable data structure(s) to support your algorithm:
  - If the incoming request is for less than the number of available seats - allocate seats to the requesting customer.  This must be done in the order that the requests come in.  Assume requests can only arrive one at a time.
  - If fewer seats are available than the number being requested - put the customers request 'on hold' until sufficient seats become available.  Do the same for all subsequent requests irrespective of wether or not the request could have been fulfilled (i.e. the next request is for fewer seats than are available).  When seats are handed back and sufficient become available - allocate the seats to the first requesting customer in the order they were originally requested.

__Level 3__

- You have had complaints from some customers who are unable to go on some excursions due to lack of seats, then going on others excursions where there have been empty seats!
- Optimise your 'wait list' by maximising the use of available seats at all times.  
- Change your data structures & queuing mechanism to support your algorithm.
- You have also been informed more coaches can be made available.  The cruise team have given the logic as follows...
  - If the 'wait list' requested seats total is greater than 50% of the number available on the coach (32 in this case) - make another coach available & and proceed as normal.
  - There is no limit to the number of coaches that can be added in this way.  But, clearly there is a limit to the total number of customers on the cruise.  As the cruise director John Luke-Pickard says - "If all customers on cruise want to go on a particular excursion - make it so!"


## Scenario 3

__Title__ "What's the weather like where we're going today?"

__Description__

On-board ship - keeping up-to-date with changes in the weather is vital.  On-board a cruise ship is no different - except now there are many more interested parties - our customers!

At TUI we always strive to give our customers the absolute best holiday experience we can.  Of course, we can't change the weather - but we can give our customers the most accurate & up-to-date information possible.

__Level 1__

- Using the OpenWeatherMap API (https://openweathermap.org/api) & the supplied cruise/itinerary database - obtain & display the current weather (weather.main & weather.description from the API response) for each port-of-call (by latitude & longitude) in the itinerary.

Example API call...

```
http://samples.openweathermap.org/data/2.5/weather?lat=35&lon=139&appid=b1b15e88fa797225412429c1c50c122a1
```

Example API response...
```javascript
{
  "coord": { "lon": 139.01, "lat": 35.02 },
  "weather": [ { "id": 800, "main": "Clear", "description": "clear sky", "icon": "01n" } ],
  "base": "stations",
  "main": { "temp": 285.514, "pressure": 1013.75, "humidity": 100, "temp_min": 285.514, "temp_max": 285.514, "sea_level": 1023.22, "grnd_level": 1013.75 },
  "wind": { "speed": 5.52, "deg": 311 },
  "clouds": { "all": 0 },
  "dt": 1485792967,
  "sys": { "message": 0.0025, "country": "JP", "sunrise": 1485726240, "sunset": 1485763863 },
  "id": 1907296,
  "name": "Tawarano",
  "cod": 200
}
```

__Level 2__

- Create a rolling display of the above information showing each port-of-call in sequence.  For our purposes we'll assume the ship can make it from one port to the next in 20 seconds.  And - as many cruises are cyclic - you can keep looping these weather updates until the customer stops the display or chooses a different cruise.

- Add the following to your weather display:
  - Current temperature (main.temp) in Celsius & Fahrenheit
  - Current humidity (main.humidity)
  - Min & max temperature for the day (main.temp_min & main.temp_max)

__Level 3__

- Using the supplied JavaScript SVG map library (https://www.amcharts.com/javascript-maps) - display all ports-of-call for a particular cruise & the current weather (as above) at each port.  You might find this  (https://codepen.io/team/amcharts/pen/bee2e2e100518d8368dba1165364ccfc) & some of the samples in the supplied zip file helpful.

## Scenario 4

__Title__ Track cruise customers that are not on-board.

__Description__

The nature of a cruise is that every so often - daily sometimes - the ship will dock at a particular port for long periods of time.  This affords the opportunity for the customers to disembark & sample some of the local food, drink, entertainment, customs & popular sites in the vicinity.

This - of course - is a total nightmare for the cruise team!  It has been known, for example that one or more customers have become lost or have strayed too far from the ship to return in time for the ship to sail on to the next port.  Returning customers to their ship is difficult & costly.

__Level 1__

- You have been requested to implement a logging system for all customers.  For now it simply logs when a particular customer is on-board or has disembarked.  
- You'll need to store the customers name & cabin number for this purpose.

__Level 2__

- The captain of the Enterprise - a bright spark by the name of James T Kirk - has asked for a status board.  This should simply show the total numbers of on-board & disembarked customers in real-time.  This will help him plan departure times better (so he says).
- How you display this data is up to you - Capt Kirk doesn't much care for this _"technology stuff"_.

__Level 3__

- Everything is going well with the status board and Capt Kirk is very happy.  However, the customers are starting to complain about the amount of time it's taking the crew to get them off the ship & back on again.
- You've heard about a new technology that you feel might help with your project & are keen to give it a try.
- You've got a number of RFID chips - your plan is to give these to the customers at the start of the cruise then use them to automatically get the logging system to register if they are on-board or not by scanning the chip as they disembark & return.
- Convert your logging system to use these RFID chips.  You'll need to keep the old 'manual' entry system tough, just in case!


## Scenario 5

__Title__ Battleships in a browser.

__Description__

Being the captain of a cruise ship can (at times) be very stressful.  There is much to do, plan & manage.  But, there is also time for a little rest & relaxation.

At these times all our captains choose a nice game of... what else - Battleships (https://en.wikipedia.org/wiki/Battleship_(game))!

These games are highly competitive & there is even a captains table showing games won & lost.  The overall winner each year gets to keep the _Admirals Cup_ in their cabin.

However, games are currently played by radio - this is inefficient as it requires both players to be tied to the radio set for the duration of the game.  It's also been alluded to that some games have been so long - & so heated - that some essential information could not get through due the radio being used for this 'other' purpose!

__Level 1__

- TUI values it's captains highly - but it values it's customers much higher.  The use of the radio is unacceptable for playing games, but we do need a way for our captains to relax, chill out & kickback with a nice game of Battleships.
- All ships have internet connections so you've have been asked to implement Battleships, over the internet - in a browser.
- For now, assume that each player can set their ships up & by clicking on a specific square - send a message to the other player (of course they'll need to re-fresh each move) & indicate a hit or miss.  Showing hits & misses on a per square basis within the grid to both players.  But hiding each others ships of course!

__Level 2__

- Your Battleships game is going down a storm (cruise joke!).  But, two of your captains have recently been involved in heated exchanges regarding a recent game between the two.  
- Whilst in this case the difference of opinion is unlikely to resolved - you have been asked to mitigate against more instances like this by introducing three things to the game:
  - A way to store all moves, hits, misses etc for each game.
  - An on-line league table - automatically created from the actual game results.
  - And a way to display each game move-by-move.
- It is hoped this will stop the captains arguing about _"who is the best"_.

__Level 3__

- The competition is __really__ hotting up now & some of the captains have started some very serious training regimes.
- They've got together (for once!) & have asked you to create a 'training' mode to the game.
- As you are familiar with Machine Learning & and little Artificial Intelligence you're keen to strut your stuff & willingly agree.  _Personally, I think you're crazy!_


## Pen test a website

__TODO__ Security team...

---

---

## Basic e-comm site with cart & checkout

---


---

## Can we get real-time flight data?  If so, show all TUI flights on map - data etc

---

## Route finder - given flight, cruise, bus, tube routes - give quickest, shortest, fastest cheapest routes

---

## Simulator (big data maybe?)

__TODO__ Dan...?
