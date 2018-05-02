## Running a Local Server

First you need to make sure you have Python installed. Check if you have Python installed and which version it is. We will be using Python to run a local server.

### (Mac) Check which Python version you have (if any)

1. Open a Terminal Window 
2. Type `$ python -V` hit 'Return'
4. Make a note of which Python version you have, you will need it later.

### (Windows) Check which Python version you have (if any)
1. open Command Prompt
2. type python --version hit 'Return'
	* if python is installed something like this will appear
	![img](https://github.com/CenterForSpatialResearch/NYCDHWeek/blob/master/Images/pythontest.png)
	* if it isn't then a message stating that will appear
	* if Python is installed make note of which version you have installed, you will need it later
3. if python is not installed then go to [python.org](python.org) to download python. We recommend installing version 2.7. 
4. After downloading the installer, double-click to open it and follow the installation prompts, selecting the default settings until you get to the page that reads "Customize Python 2.7.XX" 
	* Scroll to the bottom of options, and click the drop-down selection that reads "Add python.exe to Path" (it should have a red "X" by default)
	* Select the option that reads "Entire feature will be installed on local hard drive"
5. Follow the prompts on the rest of the setup, allow the installation to finish. When it's done, it will tell you, and python is now installed on your computer and available to use.
6. To test that python was installed, open the Command Prompt application, and enter `python --version`. It should read `Python 2.12.XX`.

### (Mac) Set up a local server

We will run a local server from our computers. The details of this are far beyond this tutorial, for more on  the technical details, visit the [Mozilla Developer site](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Set_up_a_basic_working_environment). For more on how the web works the difference between a local and remote server, [read this](https://devdojo.com/blog/technology/local-vs-remote-servers).

1. In a Terminal window, navigate to the folder where you have saved your html file (directions below on how to "navigate"). In my case it is in Documents > MappingForTheUrbanHumanities_2017 > Class_Data >3_Webmaps. To navigate there, I type the following commands (don't type the $, that just indicates that you are in the Terminal):

	* `$ cd Documents`
	* `$ cd MappingForTheUrbanHumanities_2017` 
	* `$ cd Class_Data`
	* `$ cd 3_Webmaps`
	
2. If you have Python 3, type:

	* `$  python -m http.server`  
	
2. If you have Python 2, type:

	* `$ python -m SimpleHTTPServer`
	
3. Return to your browser window (Chrome, Firefox, or Safari) and type `localhost` in the navigation bar. You should see an empty webpage. 

### (Windows) Set up a local server
1. Open Command Prompt. Then navigate to the folder where you have saved your html file (directions below on how to "navigate"). In my case it is in Documents > MappingForTheUrbanHumanities_2017 > Class_Data >3_Webmaps. To navigate there, I type the following commands:

	* cd Documents
	* cd MappingForTheUrbanHumanities_2017
	* cd Class_Data
	* cd 3_Webmaps

2. If you have python 2 type:

	* python -m SimpleHTTPServer

3. If you have python 3 type: 

	* python -m http.server

	It will look something like this:
	![img](https://github.com/CenterForSpatialResearch/NYCDHWeek/blob/master/Images/localhost.png)

3. Return to your browser window (Chrome, Firefox, or Safari) and type `http:\\localhost` in the navigation bar. You should see an empty webpage.

