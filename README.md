Composting Monitor Lesson Kit Instructions
======

1. Overview
  1. What We're Doing  
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

### What We’re Doing

This project is aimed towards middle-school and high-school STEM educators who would like to do a project that combines lessons in ecology and sustainability with computer science and web development.  

In this project, I have provided an overview on composting, and instructions for how to build a monitoring device and a web applicaiton.  

[Photo of an example monitor device](http://jdsimms.com.s3.amazonaws.com/compost/header01.JPG)
[Photo of an example web application](http://jdsimms.com.s3.amazonaws.com/compost/header02.PNG)

Students will read the temperature and moisture level of a compost pile using a wifi-connected sensor and send the sensor data to the web application that displays a webpage  students can visit from their phone or computer.

There’s no reason this device can’t just be a generic exercise in measuring temperature and water moisture using some computer software if you can't find a compost pile.

The lesson leverages the Ruby programming language, Arduino and the Github and Heroku services. Therefore the instructions assume that the educator has at least a little bit of familiarity with the Ruby programming language, Arduino, and using the command line (Terminal) program for the OSX operating system, or at least be willing to read and Google a bit while you learn some basics.  

Everything, including these instructions are purposely on Github. Please, feel free to clone, contribute, and otherwise make this lesson better for everyone.

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
The example code uses the [Ruby](http://en.wikipedia.org/wiki/Ruby_(programming_language)) programming language, and a simple web application framework known as [Sinatra](http://en.wikipedia.org/wiki/Sinatra_(software)).

Ruby should be installed on your Mac by default, but it may be an old version.  

Open terminal and type `ruby -v` then hit enter. Terminal will print out your ruby version. We’re going to want a version of Ruby 2.0.0. If you don’t have that, then there’s some work to do.  

[RVM](http://rvm.io/) is a good way to get new versions of ruby. To install RVM and the proper ruby, give Terminal this command:
`\curl -sSL https://get.rvm.io | bash -s stable --ruby=2.0.0`

Terminal will start to download everything you need and print the progress. If any errors happen, the best way to fix them is to just google the error message. Someone has likely had the same issue and posted a way to fix it.

Once the correct ruby version is installed, `cd` to the folder that will encase all of the projects. [This is a good article](http://mac.appstorm.net/how-to/utilities-how-to/how-to-use-terminal-the-basics/) for a quick lesson on `cd` and `ls`, two handy terminal commands.

For example you might have one folder called “projects” that encases each individual’s project, [like so](http://jdsimms.com.s3.amazonaws.com/compost/webapp03.png).

Now it is time to clone the project from Github.

### Github and Cloning the Repository
It is a good idea to use the [version control](http://en.wikipedia.org/wiki/Version_control) software git to keep track of changes to the project. If you have not yet, sign up for a free Github account, and go through all their getting started steps.
Once you have a good feel for the basics `git add`, `git commit`, `git push`, `git clone`, ect.

Go to this project: https://github.com/jsimms/weathervane

Copy the SSH Clone path: `git@github.com:jsimms/weathervane.git`

Double check that you are still in your projects folder on the command line, and enter:
`git clone git@github.com:jsimms/weathervane.git`

[This clones the project into the directory](http://jdsimms.com.s3.amazonaws.com/compost/webapp06.png)

Change the name of the folder to whatever you want, but do change it to save some confustion. You could copy and paste that for each kid, but I think it is better to have the kids do a little typing on the command line so they can understand there’s more than one way to operate the computer.

### Running the App Locally
Let’s run the app on localhost - aka, our computer.

The app uses [Sinatra](http://www.sinatrarb.com/), which is a framework that takes care of a lot of things so you don’t have to worry about them. Between Sintra, and the code, there should be very little you need to do in order to make the app work. It just should, once you get the server running.

So, `cd` into the cloned project folder and type this command into Terminal:

`ruby weathervane.rb`

This should print out a response that let’s you know Sintra is up and running on localhost on port 4567.
````
[2014-07-05 12:21:52] INFO  WEBrick 1.3.1
[2014-07-05 12:21:52] INFO  ruby 2.0.0 (2014-05-08) [x86_64-darwin13.1.0]
== Sinatra/1.4.5 has taken the stage on 4567 for development with backup from WEBrick
[2014-07-05 12:21:52] INFO  WEBrick::HTTPServer#start: pid=10979 port=4567
````

So, go there in your browser, and [you should see something like this](http://jdsimms.com.s3.amazonaws.com/compost/webapp08.png)

If you don’t, check a few things:

1. Make sure that you started Sintra
2. Make sure that you are in the right project directory
3. Make sure that you didn’t accidentally delete the weathervane.rb file after cloning.

### The Code  
Even though ‘it just works,’ this is a lesson, so let’s do a quick breakdown of how the app works so kids can have a basic understanding of how what they see is just the tip of the iceberg.

If Atom is your text editor, type `atom .` into terminal while in the project directory, and it [should open up atom with the whole project directory tree](http://jdsimms.com.s3.amazonaws.com/compost/webapp09.png).

###### Files and direcories that aren’t super important now
* `config.ru` - A [configuration file](http://en.wikipedia.org/wiki/Configuration_file) that sets up the app.
* `.DS_Store` - Nothing. A system file that Apple often generates.
* `Gemfile` - The Gemfile is where we edit and keep track of the [Ruby gems](http://rubylearning.com/blog/2010/12/14/ruby-gems-%E2%80%94-what-why-and-how/) (‘libraries’ or ‘packages’) the application uses.
* `Gemfile.lock` - An auto generated file that the web server uses to determine what gems to use.
* `.gitignore` - This tells git what to ignore. You use this to make sure large image files or things that are unimportant to the app running (like .DS_Store) don’t get tracked and saved.
* `Procfile` - Some configuration settings used by Heroku
* `README.md` - The [readme](http://en.wikipedia.org/wiki/README) file.
* `.git/` directory - Things that are used by git to keep track of revisions.

###### Where the magic happens
The guts of this small app lie in `weathervane.rb`, let’s break down each piece of code in here.

````
require 'rubygems'
require 'sinatra'
````
This tells the application what other libraries are needed to run this part of the program.

````
get '/' do
  erb :index
end
````
This tells the application to render the index view when a user visits the root directory URL (http://weathervane.herokuapp.com/). This is where everything is actually displayed to the end user (more on this later).

````
get '/time' do
  Time.now.asctime
end
````
This block of code stores the time at the server to be used in the index view.

````
get '/sensor' do
  File.open 'temp_data.txt', 'w' do |f|
    f.write params[:temp]
  end
  File.open 'hum_data.txt', 'w' do |f|
    f.write params[:hum]
  end
  "OK, Temp: #{params[:temp]} & Hum: #{params[:hum]}"
end
````
This is where we will send the [HTTP GET](http://www.w3schools.com/tags/ref_httpmethods.asp) request using the Arduino. This code takes the parameters sent to the `/sensor` url (aka the stuff after the ? mark: http://localhost:4567/sensor?temp=100&hum=50) and writes .txt files with those values. The last line is the OK response that gets sent back to the client that sent the request.

````
get '/sensor/temp' do
  temp = File.read 'temp_data.txt'
  temp.to_s
end

get '/sensor/hum' do
  hum = File.read 'hum_data.txt'
  hum.to_s
end
````
These blocks of code read the txt files that are created and makes them a [string](http://en.wikipedia.org/wiki/String_(computer_science)) to be used in the index view.

````
get '/status' do
  if (File.exist?('temp_data.txt') && File.exist?('hum_data.txt'))
    'Both files are here'
  elsif (File.exist?('temp_data.txt') && !File.exist?('hum_data.txt'))
    "hum file is missing."
  elsif (!File.exist?('temp_data.txt') && File.exist?('hum_data.txt'))
    "temp file is missing"
  else
    "Both of the data files are missing"
  end
end
````
This block of code creates a status page at (http://localhost:4567/status). When the user visits, it checks to see what txt data files are present. Helpful for troubleshooting issues.

###### What you actually see
The code that controls what you actually see when you go to (http://localhost:4567/) is determined by a handful of files in the `/public` and `/views` directories.

`/public/jquery-2.1.1.min.js` -  We don’t actually change anything here. This is the javascript library that we will call from the index.erb page to dynamically refresh the page with new times, temperatures, and humidity values.
`/public/style.css` - The [CSS](http://en.wikipedia.org/wiki/Cascading_Style_Sheets) file that controls how the elements on the page look. This is how text is blue, fonts are chosen, ect.
````
.data {
	font-size: 36px;
	margin: 30px;
	margin-left: 30px;
	clear: both;
}

.dataTitle {
	float: left;
	margin-right: 20px;
}

body {
	font-family: Helvetica;
}

h1 {
  color: blue;
}
````

`/views/index.erb` - Finally...this is the file that tells the server what content is displayed when the user visits. erb is embedded ruby. Embedded ruby files allow a combination of basic HTML and Ruby. Useful for when you want some dynamic information to be displayed. Let’s break it down a bit more.

````
<!DOCTYPE html>
<html>
````
This tells the web browser that it is looking at HTML and starts the document.

````
  <head>
    <script src="jquery-2.1.1.min.js"></script>
    <link rel="stylesheet" type="text/css" href="style.css">
    <title>Compost Monitor - aka "weathervane"</title>
  </head>  
```
The [head section](http://www.w3schools.com/html/html_head.asp) is where you tell the browser about important things like the location of the CSS files, javascript files (some people like to put those at the bottom of the page), and other metadata like page title.

````
<body>

    <h1>Hi there!</h1>

    <div class="data">
      <div class="dataTitle">Time (at server):</div>
      <div id="timeDisplay">Getting time....</div>
    </div>

    <div class="data">
      <div class="dataTitle">Pile Tempurature:</div>
      <div id="tempDisplay">Getting temperature...</div>
    </div>

    <div class="data">
      <div class="dataTitle">Pile Humidity:</div>
      <div id="humDisplay">Getting humidity...</div>
    </div>
````
This is the bulk of the body. We have a header (Hi there!), and then we break each reading we take into their own distinct divs with classes, ids, and placeholder content.  

We use those divs, classes and ids for both styling reasons, and for replacing the values dynamically using javascript.

````
  <script type="text/javascript">
    setInterval(function(){
      $("#timeDisplay").load("/time");
      $("#tempDisplay").load("/sensor/temp");
      $("#humDisplay").load("/sensor/hum");
    }, 5000);
  </script>

  </body>

</html>
````
This is the bottom of the body, where we declare a short javascript function that checks the values at an interval of 5000 milliseconds and loads them into the page at the declared ids.

Note that the ids line up with the ids used earlier in the `.erb` file, and the urls they check line up with what was written in `weathervane.rb`

And there you have it. The entire iceberg.  

### Testing Manually  
You don’t have to wait for the arduino to send data to test if the app works. You can send your own GET requests to the `/sensor/` endpoint through a browser. Try it.

Enter this into your browser:
http://localhost:4567/sensor?temp=10000&hum=1

And you should see a [confirmation message](http://jdsimms.com.s3.amazonaws.com/compost/webapp21.png) that the request was received.

Then go to:
http://localhost:4567/

Wait a bit and you should [see the page load the parameters](http://jdsimms.com.s3.amazonaws.com/compost/webapp22.png) that you sent over.

### Deploy to Heroku
It’s more fun to have this app hosted somewhere besides `localhost` so kids can check it from anywhere, at anytime. For this, we will use [Heroku](https://www.heroku.com/).

Sign up for their free service, and then go through all the setup steps. Their [quick start documentation](https://devcenter.heroku.com/articles/quickstart) should get you through the process. Once you get to the “deploy an app” step, pull up their [Ruby documentation](https://devcenter.heroku.com/articles/getting-started-with-ruby).  
Because you cloned our app, you have everything you need to deploy. You just need to type a few commands.

`cd` into the project directory and enter: `heroku create`  

This creates an empty app on heroku. Then enter: `git push heroku master`

This pushes the [master git branch](http://git-scm.com/book/en/Git-Branching-Basic-Branching-and-Merging) to the heroku app you created. All that code is now up on a remote heroku server! Now just enter: `heroku open`  

And boom goes the dynamite. [You should have a live web application](http://jdsimms.com.s3.amazonaws.com/compost/webapp25.png).

Test it out by manually inputting a few values like you did earlier. It should work just like it did on localhost - it’s just a different url.

### Recap
1. We cloned an open sourced web application written in Ruby using the git version control system. We then deployed it to a remote web server we created on heroku.

2. The app works by receiving an HTTP GET request from a client. In this case, the browser. Soon it will be the arduino. The app then parses the parameters (`?temp=1&hum=2`) of that GET request and creates a couple txt files to store that data.

3. When the user visits the root directory of the application, the server returns the `.erb` file that contains the HTML code used that tells the browser how to display the data to the user. That HTML file also uses some CSS to style the page, and some javascript to dynamically load the new data on the page.

The Monitor
------

### Getting Started
Now it is time to build the circuit that will read the temperature and humidity, connect to a wifi network, and send the GET request to our web application.

If you haven’t yet, install the [Arduino IDE software](http://arduino.cc/en/Main/Software), and get familiar with it and sketches using their [getting started documentation](http://arduino.cc/en/Guide/HomePage), their [libraries explanation](http://arduino.cc/en/Guide/Libraries), and a few of their [examples](http://arduino.cc/en/Tutorial/HomePage).

It might be good to have students do a few of those examples so they understand some circuit and EE basics before jumping into this part of the project.  

### Prep the Wifi Shield and Sensor
You will need to do a little bit of assembly using a soldering iron on two pieces of the circuit so they can work on the breadboard. The [CC3000 Wifi Shield](http://www.adafruit.com/product/1469) and the [SHT-10 Temp/Humidity sensor](http://www.adafruit.com/product/1298).
There are a lot of videos out there on YouTube that cover soldering, including [this one from Adafruit](https://www.youtube.com/watch?v=QKbJxytERvg), so go ahead and give it a bit of practice.  

Ultimately, you just want those pins soldered on their so [they are ready to go](http://jdsimms.com.s3.amazonaws.com/compost/arduino01.JPG) into the breadboard.

You will also need to download their respective Arduino libraries and install them on your computer so we can use them in the sketch.

SHT-10: https://github.com/practicalarduino/SHT1x
CC3000: https://learn.adafruit.com/adafruit-cc3000-wifi/cc3000-library-software

### Wire the Circuit
Time to wire things up. Let’s bust out the breadboard and get started. The pins I used below are the default setup in the sketch I provide, but you can change it up, as long as you change it in the sketch.

First, [wire over 5V power and GND from the Arduino over to the breadboard](http://jdsimms.com.s3.amazonaws.com/compost/arduino02.JPG).

Then, [plug in the CC3000 and the SHT-10 Sensor](http://jdsimms.com.s3.amazonaws.com/compost/arduino03.JPG).  

[Wire up the SHT-10](http://jdsimms.com.s3.amazonaws.com/compost/arduino04.JPG).
* Ground (Black or Green) =  GND Source
* Data (Blue) = 6
* Clock (Yellow) = 7
* Power (Red) =  Power Source

[Wire up the CC3000 to complete the circuit, and the rats nest of wires](http://jdsimms.com.s3.amazonaws.com/compost/arduino05.JPG).
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
````
// Provide Your Wifi Network Information
const char* WIFI_SSID = "yourWifi"; // must be less than 32 characters
const char* WIFI_PASS = "yourWifiPass";
````

````
// Server settings and info (where you want to send requests)
#define HOST      "weathervane.herokuapp.com"
````

With those three changes, everything should work. Before we compile and upload let’s run through each section of the sketch so you know what the software is doing. The Arduino language is based on C, which is an object oriented language. Ruby is also an object oriented language. Although they are very different in syntax - you’ll see some similar concepts. Namely, libraries, variables, functions (methods in Ruby).

###### Importing Libraries and Setting up Global Variables
````
// Include required libraries
#include <Adafruit_CC3000.h>
#include <Adafruit_CC3000_Server.h>
#include <ccspi.h>
#include <string.h>
#include <SPI.h>
#include <SHT1x.h>
#include "utility/debug.h"
````
This imports all the libraries needed to run the sketch.

````
// define CC3000 pins
const int ADAFRUIT_CC3000_IRQ  =  3;   // IRQ Must be on an interrupt pin!
const int ADAFRUIT_CC3000_VBAT =  5;   // Can be any pin
const int ADAFRUIT_CC3000_CS   =  10;  // Can be any pin
//Create the CC3000 instance (The SPI library sets remaining pins, for the uno: SCK = 13, MISO = 12, MOSI = 11)
Adafruit_CC3000 cc3000 = Adafruit_CC3000(ADAFRUIT_CC3000_CS, ADAFRUIT_CC3000_IRQ, ADAFRUIT_CC3000_VBAT,
                                       SPI_CLOCK_DIVIDER);
````
This tells the Arduino what pins the CC3000 is connected to, and then it initializes the CC3000 object in the sketch.

````
// define sht10 pins
const int DATA_PIN  = 6;  // Blue wire!
const int CLOCK_PIN = 7;  // Yellow wire!

//Creates the sht10 instnace
SHT1x sht10 (DATA_PIN, CLOCK_PIN);
````
Then, do the same with the SHT-10. Tell the Arduino what pins it is connected to and then initialize the SHT-10 object.

````
// Provide Your Wifi Network Information
const char* WIFI_SSID = "yourWifi"; // must be less than 32 characters
const char* WIFI_PASS = "yourWifiPass";
// Security can be WLAN_SEC_UNSEC, WLAN_SEC_WEP, WLAN_SEC_WPA or WLAN_SEC_WPA2, and I guess it is an int
const int WIFI_SECURITY =  WLAN_SEC_WPA2;
````
Here we provide our Wifi information. The name, the password, and what type of security.

````
#define IDLE_TIMEOUT_MS  3000      // Amount of time to wait (in milliseconds) with no data
                                   // received before closing the connection.  If you know the server
                                   // you're accessing is quick to respond, you can reduce this value.

// Server settings and info (where you want to send requests)
#define HOST      "weathervane.herokuapp.com"
uint32_t ip;
````
Next, we create an Idle timeout variable to use to determine if our server is not responding. We also create a HOST variable since we reference our heroku app several times in the code. An empty ip variable is created so we can store that information later on in the sketch.

###### The Setup Function
````
void setup(void)
{
  Serial.begin(115200);
  Serial.println("If you start me up...");
````
Here we start the setup function, and set the baud rate we will use to communicate with our serial. We also print to the serial to let us know things are starting up.

````
  // Initialise the CC3000
  Serial.println(F("\nInitialising the CC3000..."));
  if (!cc3000.begin())
  {
    Serial.println(F("Unable to initialise the CC3000! Check your wiring?"));
    while(1);
  }
````
Here we startup the actual CC3000 we have connected to the arduino.

````
  // Delete old connection data
  Serial.println(F("Deleting old connection profiles..."));
  if (!cc3000.deleteProfiles()) {
    Serial.println(F("Failed!"));
    while(1);
  }
````
We delete the old connection data that may be stored, otherwise things might error on us. Notice the deleteProfiles function. That’s a function we get to use because we imported the cc3000 library earlier. It saves us from writing it ourselves. We will do that a lot in this sketch. That’s why libraries are important and useful.

````
  // Connect to Wifi
  Serial.print(F("Attempting to connect to ")); Serial.print(WIFI_SSID); Serial.println(F("..."));

  if (!cc3000.connectToAP(WIFI_SSID, WIFI_PASS, WIFI_SECURITY)) {
    Serial.println(F("Failed!"));
    while(1);
  }

  Serial.print(F("Connected to ")); Serial.print(WIFI_SSID); Serial.println(F("..."));
````
Here we connect to the wifi using the variables we declared at the top of the sketch.

````
  // Wait for DHCP to finish
  Serial.println(F("Request DHCP..."));
  while (!cc3000.checkDHCP())
  {
    delay(100); // ToDo: Insert a DHCP timeout!
  }
````
Candidly, I don’t fully grasp DHCP. Essentially I believe this is an important step in establishing continued communication with the Wifi router. :)

````
  // Show the connection details
  while (! displayConnectionDetails()) {
    delay(1000);
  }

 }
````
Once we’re connected, we call a function called displayConnectionDetails() that prints out information to the serial, and close the setup function.

###### The loop function.
We’ve successfully setup our connection with the wifi router. Now it’s time to start measuring with the sensor and sending that data to the our web application.

````
void loop(void)
{
  // create variables, get data from the sensor
  float t_f = sht10.readTemperatureF();
  float h = sht10.readHumidity();

  // transform data to a string
  String temperature = String((int) t_f);
  String humidity = String((int) h);

  // print data to serial port
  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.print(" F /");
  Serial.print("Humidity: ");
  Serial.print(humidity);
  Serial.print("%");
  Serial.println("");
````
Once we start the loop function, we immediately read the temperature and humidity with the SHT-10 and assign that data to variables. We then transform that data into string data-type so we can use it in our request later. Finally, we just print it to the serial so we can see that it happened.

````
  // Create the request.
  String request = "GET /sensor?temp=" + temperature + "&hum=" + humidity + " HTTP/1.1\r\n";
  // Print and Send the request
  Serial.println("About to send: ");
  Serial.print(request);
  Serial.print(F("Host: "));
  Serial.print(HOST);
  Serial.print(F("\r\n"));
  Serial.print(F("User-Agent: Compost Monitor/1.0\r\n"));
  Serial.println();  
  send_request(request);
````
This takes the temperature and humidity variables, and uses them to create a string object called “request”. We then print out what the full HTTP GET request will look like to the serial, and finally we call the send_request() function with our request string as a parameter.

A lot happens in that function, so we will examine it a bit more below. But for now, assume it all worked well.

````
  // include at least a 3.6 second delay between pairs of temperature & humidity measurements.
  delay(4000);

}
````
Having sent the request, we wait four seconds before we do it all over again.

###### Other Functions
You noticed that we called a lot of functions through that sketch. Some were provided by the libraries that were imported. A couple were not. Here is a quick breakdown of the two functions we have in our sketch besides the setup and loop functions.

*displayConnectionDetails()*
````
bool displayConnectionDetails(void)
{
  uint32_t ipAddress, netmask, gateway, dhcpserv, dnsserv;

  if(!cc3000.getIPAddress(&ipAddress, &netmask, &gateway, &dhcpserv, &dnsserv))
  {
    Serial.println(F("Unable to retrieve the IP Address!"));
    return false;
  }
  else
  {
    Serial.println("Connection info...");
    Serial.print(F("\nIP Addr: ")); cc3000.printIPdotsRev(ipAddress);
    Serial.print(F("\nNetmask: ")); cc3000.printIPdotsRev(netmask);
    Serial.print(F("\nGateway: ")); cc3000.printIPdotsRev(gateway);
    Serial.print(F("\nDHCPsrv: ")); cc3000.printIPdotsRev(dhcpserv);
    Serial.print(F("\nDNSserv: ")); cc3000.printIPdotsRev(dnsserv);
    Serial.println("\n");
    return true;
  }
}
````
This function prints out the connection details to the Wifi network. It’s not vital to the sketch working, but it is nice information to know if you wanted to know it.

*send_request()*
This is the function that ties the sensor to the web app. This is where we send the GET request to our web server.
````
void send_request (String request)
{

  ip = 0;
  // Try looking up the website's IP address
  Serial.print(HOST); Serial.print(F(" -> "));
  while (ip == 0) {
    if (! cc3000.getHostByName(HOST, &ip)) {
      Serial.println(F("Couldn't resolve!"));
    }
    delay(500);
  }

  cc3000.printIPdotsRev(ip);
````  
Here we establish that a parameter to the function is a string. We happen to call it request.

Before doing anything with the request string, the CC3000 looks up the IP address of our website. Once it has connected and retrieved the ip, it stores it in a variable called ip, and then prints out that information to the serial port by calling the `printIPdotsRev()` function.

````
  Adafruit_CC3000_Client www = cc3000.connectTCP(ip, 80);
  if (www.connected()) {
    www.print(request);
    www.print(F("Host: "));
    www.print(HOST);
    www.print(F("\r\n"));
    www.print(F("User-Agent: Compost Monitor/1.0\r\n"));
    www.print(F("\r\n"));
    www.println();
  } else {
    Serial.println(F("Connection failed"));
    return;
  }

  Serial.println(F("-------------------------------------"));
````
Here it is, here’s where we actually connect to our application server and send the request. We use the CC3000 library to create a web client that connects to our application server using the IP address we just looked up and port 80. Once we are connected we print out the full request. This matches the sample request we printed to the serial earlier.

````
  /* Read data until either the connection is closed, or the idle timeout is reached. */
  unsigned long lastRead = millis();
  while (www.connected() && (millis() - lastRead < IDLE_TIMEOUT_MS)) {
    while (www.available()) {
      char c = www.read();
      Serial.print(c);
      lastRead = millis();
    }
  }
  www.close();
  Serial.println(F("-------------------------------------"));  
}
````
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
  * Lesson Questions
  * Calling out similarities in Ruby and C
  * Better connecting the composting problem to future improvement ideas

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
