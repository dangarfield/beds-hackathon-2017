# Scenarios


## Technology Assumptions

It is assumed that the following are available to all students:
- A statically-typed language
- A dynamically-typed language
- An IDE and/or editor suitable for - and compatible with - the above.
- A web framework - ideally, one dynamically-typed and one statically-typed.
- A web server or other means of serving static web pages
- A JavaScript enabled web browser
- An internet connection
- A database on which the student has sufficient permissions to create, manage & drop tables, and load data.
- A means to view the above database and all data stored in it.


## Scenario 1

__Title__ A static website from imported data files.

__Description__

TUI is a global holiday brand that offers: beach, city, ski & cruise holidays and much more besides.  Recently, a number of advancements have been made to the content stored about cruises, itineraries & cruise Ships.  Your team has been assigned the task of re-designing the current cruise website from the ground up, to include this enhanced content.

Cruise is a premium product primarily aimed at affluent customers, couples, parents of grown up children & those over 50.  The display of cruise content is expected to reflect the quality of the product & the target market.  

__Level 1__

- Analyse the given data files & create a normalised data structure to store the data.
- Create a database from the above structure in which to store the data from the data files.
- Programatically load the data from the data files into the database.  This program should be capable of being automated.

__Level 2__

- Design & build a suitable HTML template to display a cruise, it's itinerary & ship information.
- Programatically build a number of HTML pages (one per cruise) using the contents of the database & the above template.  This program should also be capable of being automated.

__Level 3__

- Design & build an index.html page for your site.  Include suitable navigation to enable the customer to find & display every cruise within the site.  Like all the other pages - this needs to be programatically built.


## Scenario 2

__Title__ Onboard excursion booking system.

__Description__

One of the main reasons for customers choosing a cruise is the potential to see many different countries, cities & places of interest in a short period of time.

At TUI we are very keen to ensure that our customers have great time, relax & and have the opportunity to see as much of the countries & their culture we visit as possible.  One of the best ways of doing this is to offer excursions (trips away from the ship at a particular port).  

Excursions are tricky to manage as there is a limitation on the number of coaches & seats on them to transport the customers while off-ship.

__Level 1__

- You have access to a file which has the available excursions for a particular cruise & that are available from each of the ports-of-call that the cruise stops at.
- Design & build an on-board excursion booking system using the given data.  At this stage all a customer can do is book a number of seats on an excursion - you should require their name, number of seats required & their cabin number.  The customer/cabin number combination must be unique - a customer cannot book twice.
- Once all seats are sold no more bookings can be taken.
- Assume that no seats are handed back.

__Level 2__

- Your booking system has proven highly effective & very popular.  But, some customers would like to return some seats previously booked.  Implement booking cancellation within the system.
- You have also been asked to add a 'wait list' for seats on each excursion.  So that when the coach is full a customer can register interest in obtaining one or more seats.  
- For this purpose - assume there is only one coach with 32 seats per excursion & that the customer initially always accepts & purchases the seats they have requested.  Even though they might cancel their booking at a later date.
- Implement the following business logic - choose suitable data structure(s) to support your algorithm:
  - If the incoming request is for less than the number of available seats - allocate seats to the requesting customer.  This must be done in the order that the requests come in.  Assume requests arrive one at a time.
  - If fewer seats are available than the number being requested - put the customers request 'on hold' until sufficient seats become available.  Do the same for all subsequent requests irrespective of wether or not the request could have been fulfilled (for example, when the next request is for fewer seats than are currently available).  When seats are handed back (booking cancellation) and sufficient have become available - allocate the seats to the first requesting customer in the order they were originally requested.

__Level 3__

- You have had complaints from some customers who are unable to go on some excursions due to lack of seats, but then going on other excursions where there have been empty seats!
- Optimise your 'wait list' by maximising the use of available seats at all times.  
- Change your data structures & queuing mechanism to support your algorithm.
- You have also been informed more coaches can be made available.  The cruise team have given the logic for this as follows...
  - If the 'wait list' requested seats total is greater than 50% of the number available on the coach (32 in this case, so more than 16) - make another coach available, increment the total number of seats as appropriate & and proceed as normal.
  - In the case of booking cancellations - if the number of required seats goes below the need for the additional coach or coaches.  Remove the appropriate number of coaches - except one.  All excursions have a minimum of one coach.
  - Once you have make available an additional coach - even if only one seat is used it is not removed unless the above rule is true.  Once you have made a commitment to your customers - you must uphold it.
  - There is no limit to the number of coaches that can be added in this way.  But, clearly there is a limit to the total number of customers on the cruise.  As the cruise director John Luke-Pickard says - "If all customers on cruise want to go on a particular excursion - make it so!"


## Scenario 3

__Title__ "What's the weather like?"

__Description__

On-board ship - keeping up-to-date with changes in the weather is vital.  On-board a cruise ship, this is no different - except now there are many more interested parties - our customers!

At TUI we always strive to give our customers the best holiday experience we can.  Of course, we can't change the weather - but we can give our customers the most accurate & up-to-date information possible to help them make the right choice for them.

__Level 1__

- Using the OpenWeatherMap API (https://openweathermap.org/api) & the supplied cruise/itinerary data - obtain & display the current weather (weather.main & weather.description from the API response) for each port-of-call (by latitude & longitude) in the itinerary.

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

__Title__ "What do you mean - some of our customers are missing...?"

__Description__

The nature of a cruise is that every so often - daily sometimes - the ship will dock at a particular port for long periods of time.  This affords the opportunity for the customers to disembark & sample some of the local food, drink, entertainment, customs & popular sites in the vicinity.

This - of course - is a total nightmare for the cruise team!  

It has been known, for example that one or more customers have become lost or have strayed too far from the ship to return in time for the ship to sail on to the next port.  Ship sailing times need to be carefully managed.  Returning lost customers to their ship is both difficult & costly.

__Level 1__

- You have been requested to implement a logging system for all customers.  For now it simply logs when a particular customer is on-board or has disembarked.  
- You'll need to store the customers name & cabin number for this purpose.

__Level 2__

- The captain of the Enterprise - a bright spark by the name of James T Kirk - has asked for a status board.  This should simply show the total number of on-board & disembarked customers in real-time.  This will help him plan departure times better.
- How you display this data is up to you - Capt Kirk doesn't much care for this _"technology stuff"_.  But it does need to be clear, up-to-date & accurate.

__Level 3__

- Everything is going well with the status board and Capt Kirk is very happy.  However, the customers are starting to complain about the amount of time it's taking the crew to get them off of the ship & back on again.
- You've heard about a new technology that you feel might help with your project & are keen to give it a try.
- You've got a number of RFID chips - your plan is to give these to the customers at the start of the cruise - get them to wear them during the entire cruise - then use them to automatically get the logging system to register if they are on-board or not by scanning the chip as they disembark & return.
- Convert your logging system to use these RFID chips.  You'll need to keep the old 'manual' entry system tough, just in case!


## Scenario 5

__Title__ Battleships.

__Description__

Being the captain of a cruise ship can (at times) be very stressful.  There is much to do, plan & manage.  But, there is also time for a little rest & relaxation.

At these times all our captains choose a nice game of... what else - Battleships (https://en.wikipedia.org/wiki/Battleship_(game))!

These games are highly competitive & there is even a captains table showing games won & lost.  The overall winner each year gets to keep the - much sought after - _Admirals Cup_ in their cabin.

However, games are currently played by radio - this is inefficient as it requires both players to be tied to the radio set for the duration of the game.  It's also been alluded to that some games have been so long - & so heated - that some essential operational information could not get through due the radio being used for this 'other' purpose!

__Level 1__

- TUI values it's captains highly - but it values it's customers much higher.  The use of the radio is unacceptable for playing games, but we do need a way for our captains to relax, chill out & kickback with a nice game of Battleships.
- You've have been asked to implement Battleships.  The choice of how the players communicate is up to you, but it must be via your program - NOT the radio!  All ships have direct connections to all other ships & of course - an internet connection.
- For now, assume that each player can set their ships up on specific squares - send a message to the other player & the system indicates a hit or miss in response.  The state of the game is kept up-to-date & displayed to both players at all times. In particular, you should show hits & misses on a per square basis within the grid to both players, whilst hiding each others ships of course!

__Level 2__

- Your Battleship game is going down a storm!  But, two of your captains have recently been involved in heated exchanges regarding a recent game between them.  
- Whilst in this case the difference of opinion is unlikely to resolved - you have been asked to mitigate against more instances like this by introducing three things to the game:
  - A way to store all moves, hits, misses etc for each game.
  - An league table that is automatically created from the actual game results.
  - And a way to display each game move-by-move.
- It is hoped this will stop the captains arguing.

__Level 3__

- The competition is __really__ hotting up now & some of the captains have started some very serious training regimes.
- They've got together (for once!) & have asked you to create a 'training' mode in the game.
- You are keen to strut your stuff & willingly agree.  _Personally, I think you're crazy!_


## Scenario 6

__Title__ "Whoops! I did it again."

__Description__

The cruise team have a new system.  Unfortunately, there is a slight flaw in it.  Under certain circumstances (Thursday's usually) all of the sequencing information for all cruise itineraries is wiped out.  Just the sequences - nothing else.

Even more unfortunately, every night this itinerary data is sent to all the cruise ships.  Some captains have alluded to this loss of 'which port is next' as being responsible for them arriving at the wrong port the following day!

__Level 1__

- Given the cruise itinerary data - write a program to analyse the ports-of-call for each itinerary and find the shortest route.  Once done - add the correct sequence back into the data.
- Fortunately, the distance between each port & all others is still in the data.

__Level 2__

- Oh no!  Guess what?  You know that distance information we used to get?  We'll it's getting wiped out too (Monday's this time).  We've still got the latitude & longitude though.
- Update your first program - to calculate the distance between each port & the next then add that back into the data.  At which point the rest of the program should continue working as normal.
- Problem is - how can you figure out the relevant distance between each latitude/longitude point?  _Hint: the 'haversine' formula might help you here_

__Level 3__

- The cruise team love your program & have had an idea (_this is never good_).  They'd like to add one more port-of-call per itinerary.  
- They'd like you to give them a program that will automatically suggest the best additional port from the given data.  This means finding all available ports across the entire itinerary that they do not currently stop at & finding the shortest path between the actual itinerary (which you cannot alter) with each additional port.  Then use this to suggest the most appropriate additional port to add.





## Pen test a website

__TODO__ Security team...


## Simulator (big data maybe?)

__TODO__ Dan...?



## Basic e-comm site with cart & checkout


## Can we get real-time flight data?  If so, show all TUI flights on map - data etc
