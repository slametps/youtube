# youtube
This is my first module contribution to the community of MagicMirror2!

# Acknowledgement 
I would like to thank Michael Teeuw ,Jopyth and Strawberry 3.141 for their guidance in this module. As of course, my buddy Huang Kai for teaching me the basics.
This code was initially based on Michael's compliment module.

#Prerequisites 

You have to install Jopyth's Remote Control module before you can start controlling the embedded youtube video. Here's the link to Jopyth's Remote module:
https://github.com/Jopyth/MMM-Remote-Control

# Installation

Navigate to MagicMirror's modules folder through your terminal window, execute `git clone https://github.com/zichao92/youtube.git`


# Configuration 

For config.js , use the following code:
 ```
		{
			module: 'youtube',
			position: 'lower_third' //used to be lower_third, keep it as module 5
		},
```
For my youtube module, it's listed as the 5th module. If you dont know sequence of the module, start counting from the top.

Example :
```
	modules: [
		{
    			module: 'MMM-Remote-Control' //module 1
    // uncomment the following line to show the URL of the remote control on the mirror
    // , position: 'bottom_left'
    // you can hide this module afterwards from the remote control itself
		},

		{
      module: 'MMM-PIR-Sensor', //module 2
    config: {
			sensorPIN: 22,
			relayPIN: false,
			powerSaving: true,
			relayOnState: 1
          }
         }, 

		{
			module: 'alert', 
		},
		{
			module: 'clock', //module 3
			position: 'top_left'
		},
		{
			module: 'calendar', //module 4
			header: 'SG Holidays',
			position: 'top_left',
			config: {
				calendars: [
					{
						symbol: 'calendar-check-o ',
						url: 
					}
				]
			}
		},
		{
			module: 'youtube', //module 5
			position: 'lower_third' //used to be lower_third, keep it as module 5
		},
```

# Configurating Jopyth's Remote Control module
I was still using Jopyth's older version of Remote Control module as it appears to be more smoother as compared to his new version.
Nevertheless here's what you have to change if you are using Jopyth's modules:

This code can be found from line 178 onwards, im not too sure what's the exact line but what you can do is hit crt+f and search for " 'show-all-button' ".

```
    // edit menu buttons, This is showall
    'show-all-button': function() {
        var buttons = document.getElementsByClassName("edit-button");
        var notification = "PAUSE_VIDEO";

        for (var i = 0; i < buttons.length; i++) {
                        if (buttons[i].id!="module_5_youtube"){                             // notice that it has some expectional task for module5?
            buttons[i].className = buttons[i].className.replace("toggled-off", "toggled-on");
            Remote.showModule(buttons[i].id);
            Remote.getWithStatus("action=NOTIFICATION&n"+"otification=" + notification );
                        }
                        else{
            buttons[i].className = buttons[i].className.replace("toggled-on", "toggled-off");
            Remote.getWithStatus("action=NOTIFICATION&n"+"otification=" + notification );
            Remote.hideModule(buttons[i].id);
                        }
        }
    },


    // this is hide all
    'hide-all-button': function() {
        var buttons = document.getElementsByClassName("edit-button");
        var notification = "PLAY_VIDEO";
        for (var i = 0; i < buttons.length; i++) {

            if (buttons[i].id=="module_5_youtube"){
            buttons[i].className = buttons[i].className.replace("toggled-off", "toggled-on");
            Remote.showModule(buttons[i].id);
            Remote.getWithStatus("action=NOTIFICATION&n"+"otification=" + notification );
            }
            else{
            buttons[i].className = buttons[i].className.replace("toggled-on", "toggled-off");
            Remote.getWithStatus("action=NOTIFICATION&n"+"otification=" + notification );
            Remote.hideModule(buttons[i].id);
            }
        }
    },
```


    If you are using Jopyth's older version of Remote Control , you have to add these few lines into your code:

https://github.com/Jopyth/MMM-Remote-Control/blob/master/node_helper.js#L658-L676 , This is for node_helper.js
https://github.com/Jopyth/MMM-Remote-Control/blob/master/MMM-Remote-Control.js#L122-L124 , this is for MMM-REmote-Control.js


# Choosing your youtube video

Im using this video as an example : https://www.youtube.com/embed/H1Ej5qMqxxw?enablejsapi=1&autoplay=1

notice `H1Ej5qMqxxw` ? , that's the thing that you will need to change. 

# Fire it up

Go to localhost:8080/remote.html#main-menu and press hide-all ( To play the video) & Show-all ( To pause the video)

#ScreenShots

Here are some ScreenShots
![demo] https://cloud.githubusercontent.com/assets/26163624/24041795/fa8aae7a-0b49-11e7-9815-97bb998d62a3.png
![demo] https://cloud.githubusercontent.com/assets/26163624/24041811/067154dc-0b4a-11e7-84c1-e9d40c558f46.png