Composting Monitor Lesson Kit Instructions
======


## Table Of Contents  

1. Overview
  1. What We’re Building  
  2. Materials List
2. Compost Lesson
3. The Web Application
  1. Ruby
  2. Github and Cloning the Repository
  3. Running the App Locally
  4. The Code  
  5. Testing Manually  
  6. Deploy to Heroku
  7. Recap
4. The Monitor
  1. Getting Started
  2. Prep the Wifi Shield and Sensor
  3. Wire the Circuit
  4. The Sketch  
  5. Upload
  6. Recap
5. Improvement and Contributing  


Overview
------

### What We’re Building
This is a project aimed towards middle-school and high-school science educators who would like to do a project that combines lessons in ecology, sustainability, computer science, and web development.  

In this project, students will read the temperature and moisture level of a compost pile using a wifi-connected sensor and send the sensor data to a web application that displays a webpage that students can visit from their phone or computer. However, there’s no reason this can’t just be a generic exercise in measuring temperature and water moisture using some computer software.

The lesson leverages the Ruby programming language, Arduino and the Github and Heroku services.Therefore the instructions assume that the educator has at least a little bit of familiarity with the Ruby programming language, Arduino, and using the command line (Terminal) program for the OSX operating system, or at least be willing to read and Google a bit while you learn some basics.  

### Materials List
Each circuit contains parts that add up to a cost of approximately $130 before shipping. Add a little more if you need to acquire a soldering iron (or a computer). The Github and Heroku accounts that are needed can utilize their free service.

The biggest thing outside of these instructions that is needed to complete the experiment is a compost pile that is near a wifi connection.

* Basic Arduino Parts
  * Arduino Uno - http://www.adafruit.com/products/50
  * Arduino/USB Wire - http://www.adafruit.com/products/62
  * Male/Male Wires - http://www.adafruit.com/products/759
  * Prototyping Breadboard -  http://www.adafruit.com/products/64

Or, you can also just purchase an Arduino starter kit that has all the above and more - http://store.arduino.cc/product/K000007  

* Wifi Shield and Sensor
  * CC3000 Wifi Breakout Board - http://www.adafruit.com/product/1469
  * SH-10 Soil Temperature/Moisture Sensor - http://www.adafruit.com/product/1298

* Other Materials  
  * Soldering Iron
  * Soldering Stand  
  * Solder Wire
  * Compost Pile near a wifi signal

* Accounts
  * Github (free) - http://www.github.com  
  * Heroku (free) - http://www.heroku.com  

* Software
  * Arduino IDE - http://arduino.cc/en/Main/Software
  * Text Editor (I use Atom) - https://atom.io/
  * Mac OS X Terminal (installed by default)

Compost Lesson
------

The idea is that this monitor is built and completed in the context of a composting lesson. Temperature and moisture levels are important components to monitor in a compost pile. By using (and improving upon) this monitor, it shows a way that this could be done remotely.

If you have not completed a composting lesson yet, please read my 5 minute composting lesson: https://medium.com/p/5ebdf1ad31c5

The Web Application
------

### Ruby
The example code uses the [Ruby](http://en.wikipedia.org/wiki/Ruby_(programming_language)) programming language, and a simple web application framework known as [Sinatra](http://en.wikipedia.org/wiki/Sinatra_(software).

Ruby should be installed on your Mac by default, but it may be an old version.  

Open terminal and type `ruby -v` then hit enter:

We’re going to want a version of Ruby 2.0.0. If you don’t have that, then there’s some work to do.  

RVM is a good way to get new versions of ruby. To install RVM and the proper ruby, give Terminal this command: \curl -sSL https://get.rvm.io | bash -s stable --ruby=2.0.0

As the program downloads terminal will print out the progress. If any errors happen, the best way to fix them is to just google the error message. Someone has likely had the same issue and posted a way to fix it.

Once the correct ruby version is installed, ‘cd’ to the folder that will encase all of the projects (This is a good article for a quick lesson on ‘cd’ and ‘ls’, two handy commands). For example you might have one folder called “projects” that encases each individual’s project, like so:

Now it is time to clone the project from Github.

### Github and Cloning the Repository
It is a good idea to use the version control software git to keep track of changes to the project. If you have not yet, sign up for a free Github account, and go through all their getting started steps. Once you have a good feel for the basics “git add”, “git commit”, “git push”, “git clone”, ect.

Go to this project: https://github.com/jsimms/weathervane

Copy the SSH Clone URL:

Double check that you are still in your projects folder on the command line, and enter:
git clone git@github.com:jsimms/weathervane.git

This clones the project into the directory:

Change the name of the folder to whatever you want, but do change it. You could copy and paste that for each kid, but I think it is better to have the kids do a little typing on the command line so they can understand there’s more than one way to operate the computer.

### Running the App Locally
Let’s run the app on localhost - aka, our computer.

The app uses Sinatra, which is a framework that takes care of a lot of things so you don’t have to worry about them. Between Sintra, and the code, there should be very little you need to do in order to make the app work. It just should, once you get the server running.

So, ‘cd’ into the cloned project folder and type this command into Terminal:

ruby weathervane.rb

This should print out a response that let’s you know Sintra is up and running on localhost on port 4567.

So, go there in your browser, and you should see something like this:

If you don’t, check a few things:  
1. Make sure that you started Sintra
2. Make sure that you are in the right project directory
3. Make sure that you didn’t accidentally delete the weathervane.rb file after cloning.

### The Code  
Even though ‘it just works,’ this is a lesson, so let’s do a quick breakdown of how the app works so kids can have a basic understanding of how what they see is just the tip of the iceberg.

If Atom is your text editor, type ‘atom .’ into terminal while in the project directory, and it should open up atom with the project directory tree.

###### Files and direcories that aren’t super important now
*config.ru* - A configuration file that sets up the app.
*.DS_Store* - Nothing. A system file that Apple often generates.
*Gemfile* - The Gemfile is where we edit and keep track of the Ruby gems (‘libraries’ or ‘packages’) the application uses.
*Gemfile.lock* - An auto generated file that the web server uses to determine what gems to use.
*.gitignore* - This tells git what to ignore. You use this to make sure large image files or things that are unimportant to the app running (like .DS_Store) don’t get tracked and saved.
*Procfile* - Some configuration settings used by Heroku
*README.md* - The readme file.
*.git/ directory* - Things that are used by git to keep track of revisions.

###### Where the magic happens
The guts of this small app lie in weathervane.rb, let’s break down each piece of code in here.

This tells the application what other libraries are needed to run this part of the program.

This tells the application to render the index view when a user visits the root directory URL (http://weathervane.herokuapp.com/). This is where everything is actually displayed to the end user (more on this later).

This block of code stores the time at the server to be used in the index view.

This is where we will send the HTTP GET request using the Arduino. This code takes the parameters sent to the /sensor url (aka the stuff after the ? mark: http://localhost:4567/sensor?temp=100&hum=50) and writes .txt files with those values. The last line is the OK response that gets sent back to the client that sent the request.

These blocks of code read the txt files that are created and makes them a string to be used in the index view.

This block of code creates a status page at (http://localhost:4567/status). When the user visits, it checks to see what txt data files are present. Helpful for troubleshooting issues.

###### What you actually see
The code that controls what you actually see when you go to (http://localhost:4567/) is determined by a handful of files in the /public and /views directories.

*/public/jquery-2.1.1.min.js* -  We don’t actually change anything here. This is the javascript library that we will call from the index.erb page to dynamically refresh the page with new times, temperatures, and humidity values.
*/public/style.css* - The CSS file that controls how the elements on the page look. This is how text is blue, fonts are chosen, ect.
*/views/index.erb* - Finally...this is the file that tells the server what content is displayed when the user visits. erb is embedded ruby. Embedded ruby files allow a combination of basic HTML and Ruby. Useful for when you want some dynamic information to be displayed. Let’s break it down a bit more.

This tells the web browser that it is looking at HTML and starts the document.

The head section is where you tell the browser about important things like the location of the CSS files, javascript files (some people like to put those at the bottom of the page), and other metadata like page title.

This is the start of the body. We have a header (Hi there!), and then we break each reading we take into their own distinct divs with classes, ids, and placeholder content.  

We use those divs, classes and ids for both styling reasons, and for replacing the values dynamically using javascript.

This is the bottom of the body, where we declare a short javascript function that checks the values at an interval of 5000 milliseconds and loads them into the page at the declared ids.

Note that the ids line up with the ids used earlier in the erb file, and the urls they check line up with what was written in weathervane.rb

And there you have it. The entire iceberg.  

### Testing Manually  
You don’t have to wait for the arduino to send data to test if the app works. You can send your own GET requests to the /sensor/ endpoint through a browser. Try it:
http://localhost:4567/sensor?temp=10000&hum=1

Then go to:
http://localhost:4567/

### Deploy to Heroku
It’s more fun to have this app hosted somewhere besides localhost so kids can check it from anywhere, at anytime. For this, we will use Heroku.

Sign up for their free service, and then go through all the setup steps. Their documentation should get you through the process. Once you get to the “deploy an app” step, pull up the Ruby documentation.  Because you cloned our app, you have everything you need to deploy. You just need to type a few commands.

cd into the project directory and enter: heroku create  

This creates an empty app on heroku. Then enter: git push heroku master

This pushes the master git branch to the heroku app you created. All that code is now up on a remote heroku server! Now just enter: heroku open  

And boom goes the dynamite. You have a live web application.

Test it out by manually inputting a few values like you did earlier. It should work just like it did on localhost - it’s just a different url.

### Recap
1. We cloned an open sourced web application written in Ruby using the git version control system. We then deployed it to a remote web server we created on heroku.

2. The app works by receiving an HTTP GET request from a client. In this case, the browser. Soon it will be the arduino. The app then parses the parameters (?temp=1&hum=2) of that GET request and creates a couple txt files to store that data.

3. When the user visits the root directory of the application, the server returns the .erb file that contains the HTML code used that tells the browser how to display the data to the user. That HTML file also uses some CSS to style the page, and some javascript to dynamically load the new data on the page.

The Monitor
------

### Getting Started
Now it is time to build the circuit that will read the temperature and humidity, connect to a wifi network, and send the GET request to our web application.

If you haven’t yet, install the Arduino IDE software, and get familiar with it and sketches using their getting started documentation, their libraries explanation, and a few of their examples.

It might be good to have students do a few of those examples so they understand some circuit and EE basics before jumping into this part of the project.  

### Prep the Wifi Shield and Sensor
You will need to do a little bit of assembly using a soldering iron on two pieces of the circuit so they can work on the breadboard. The CC3000 Wifi Shield and the SHT-10 Temp/Humidity sensor. There are a lot of videos out there on YouTube that cover soldering, including this one from Adafruit, so go ahead and give it a bit of practice.  

You will also need to download their respective Arduino libraries and install them on your computer so we can use them in the sketch.

SHT-10: https://github.com/practicalarduino/SHT1x
CC3000: https://learn.adafruit.com/adafruit-cc3000-wifi/cc3000-library-software

### Wire the Circuit
Time to wire things up. Let’s bust out the breadboard and get started. The pins I used below are the default setup in the sketch I provide, but you can change it up, as long as you change it in the sketch.

First, wire over 5V power and GND from the Arduino over to the breadboard:

Plug in the CC3000 and the SHT-10 Sensor:  

Wire up the SHT-10:
* Ground (Black or Green) =  GND Source
* Data (Blue) = 6
* Clock (Yellow) = 7
* Power (Red) =  Power Source

Wire up the CC3000 to complete the circuit, and the rats nest of wires:
* GND = GND Source
* IRQ = 3
* VBAT = 5
* CS =  10
* MOSI = 11
* MISO = 12
* SCK = 13
* Power (3v3) = Power Source

### The Sketch
Now it is time to get back into software. Download (or clone) the sketch and put it into your sketchbook: https://github.com/jsimms/compost_monitor

Unlike the Ruby app, there will be a few variables you need to change in this sketch in order to make it work. Crack open the sketch, and replace the WIFI_SSID, WIFI_PASS, and HOST constants with your wifi network name, password, and your heroku app URL.  

With those three changes, everything should work. Before we compile and upload let’s run through each section of the sketch so you know what the software is doing. The Arduino language is based on C, which is an object oriented language. Ruby is also an object oriented language. Although they are very different in syntax - you’ll see some similar concepts. Namely, libraries, variables, functions (methods in Ruby).

###### Importing Libraries and Setting up Global Variables

Make sure you import all the libraries needed to run the sketch.

This tells the Arduino what pins the CC3000 is connected to, and then it initializes the CC3000 object in the sketch.

Then, do the same with the SHT-10. Tell the Arduino what pins it is connected to and then initialize the SHT-10 object.

Here we provide our Wifi information. The name, the password, and what type of security.

Next, we create an Idle timeout variable to use to determine if our server is not responding. We also create a HOST variable since we reference our heroku app several times in the code. An empty ip variable is created so we can store that information later on in the sketch.

###### The Setup Function
Here we start the setup function, and set the baud rate we will use to communicate with our serial. We also print to the serial to let us know things are starting up.

Here we startup the actual CC3000 we have connected to the arduino.

We delete the old connection data that may be stored, otherwise things might error on us. Notice the deleteProfiles function. That’s a function we get to use because we imported the cc3000 library earlier. It saves us from writing it ourselves. We will do that a lot in this sketch. That’s why libraries are important and useful.

Here we connect to the wifi using the variables we declared at the top of the sketch.

Candidly, I don’t fully grasp DHCP. Essentially I believe this is an important step in establishing continued communication with the Wifi router. :)

Once we’re connected, we call a function called displayConnectionDetails() that prints out information to the serial, and close the setup function.

###### The loop function.
We’ve successfully setup our connection with the wifi router. Now it’s time to start measuring with the sensor and sending that data to the our web application.

Once we start the loop function, we immediately read the temperature and humidity with the SHT-10 and assign that data to variables. We then transform that data into string data-type so we can use it in our request later. Finally, we just print it to the serial so we can see that it happened.

This takes the temperature and humidity variables, and uses them to create a string object called “request”. We then print out what the full HTTP GET request will look like to the serial, and finally we call the send_request() function with our request string as a parameter.

A lot happens in that function, so we will examine it a bit more below. But for now, assume it all worked well.

Having sent the request, we wait four seconds before we do it all over again.

###### Other Functions
You noticed that we called a lot of functions through that sketch. Some were provided by the libraries that were imported. A couple were not. Here is a quick breakdown of the two functions we have in our sketch besides the setup and loop functions.

*displayConnectionDetails()*
This function prints out the connection details to the Wifi network. It’s not vital to the sketch working, but it is nice information to know if you wanted to know it.

*send_request()*
This is the function that ties the sensor to the web app. This is where we send the GET request to our web server.

Here we establish that a parameter to the function is a string. We happen to call it request.

Before doing anything with the request string, the CC3000 looks up the IP address of our website. Once it has connected and retrieved the ip, it stores it in a variable called ip, and then prints out that information to the serial port by calling the printIPdotsRev() function.

Here it is, here’s where we actually connect to our application server and send the request. We use the CC3000 library to create a web client that connects to our application server using the IP address we just looked up and port 80. Once we are connected we print out the full request. This matches the sample request we printed to the serial earlier.

Finally, we read the response, and close the connection until we come back around in the loop function and do it all over again.

### Upload  
Got all that? Cool. :)

Compile the sketch, upload it to the Arduino, open up the serial port, open up your browser, stick the sensor into the compost pile, and watch it get the temperature. Wahoo!

### Recap
1. We soldered our wifi shield and sensor so they could be used in our circuit. We also downloaded their needed libraries and installed them so we can use them in our sketch. We learned by doing a few of the intro exercises that all Arduino sketches have at minimum two parts - the setup method, and the loop method.

2. We wired up the circuit, making sure that the circuit is closed and that we placed the wires into the same pins that we will declare in the sketch.

3. We downloaded an open-source sketch, made a few changes, and did a run through of how the code works. The first part of the sketch imports all the libraries and declares all the global variables that will be used through the sketch. The setup method connects us to the wifi network. The loop function reads the temperature and calls the send_request function, which takes care of sending the HTTP request to our web application.  

Areas for improvement
------

There are lots of areas for improvement. This is why everything is up online in accessible, open-source formats. A great exercise with the class would be to have them improve the project and contribute back. Each part of the lesson has their own readme on github with a few ideas to get your started.

* Documentation and Instructions
  * Fixing typos and bad images (I haven’t proofread anything yet…)
  * Other improvements for clarity
  * Troubleshooting tips
* Lesson Plan
  * Fixing typos and bad images (I haven’t proofread anything yet…)
  * Other improvements for clarity
  * Vermicomposting Section

* Weathervane
  * Be able to identify unique devices
  * Store data into a database instead of creating txt files
  * Create visual charts to show temperature and humidity over time
  * Send email or SMS alerts when a pile is cold

* Compost Monitor
  * A power source that is not your computer
  * A sensor the can be submerged longer than an hour
  * Alternative ways besides Wifi network to send data  
  * Design a case for the circuit
  * Find and use cheaper materials  
