# Virtual Pi Jam Photobooth
The Virtual Pi Jam Photobooth - updated for each theme. Last update was: 27/01/18

Its features include:

Interactivity provided by text annotations and the push button for control
By default takes 4 photographs, each controlled by the button
Tweets the 4 photographs (unless the button is pressed to cancel) with the Virtual Pi Jam theme logo overlaid in the corner, and a specified message with the tweet
Works offline or without Twitter feature if not configured, and saves to Pi.

Requirements
Hardware:

Raspberry Pi (any model with a camera port)
Raspberry Pi camera module
Any kind of standard GPIO push button (arcade button with quick-connect wire reccomended)
Software:

Picamera
GPIO Zero
Twython
Automated installation
Open a terminal window and type:

curl -sSL http://rpf.io/jampb | bash
Note this reboots the Pi at the end of the script, and launches the program automatically.

Manual installation
Start with a Raspbian Stretch desktop image.

Connect the camera module and wire your button to GPIO14.

Enable the camera module using the Raspberry Pi Configuration Tool in the main menu, or using raspi-config on the command line.

Reboot.

Open a Terminal window.

Git clone this repository:

git clone https://github.com/yorkpijam/Virtual-Pi-Jam-Photobooth
Install Twython:

sudo pip3 install twython
Enter the project directory and run the photobooth script:

python3 photobooth.py
You should see an image preview appear, and the message:

Ready!
Press the button to start...
Now use the button to progress to the next step, and continue.

Without a Twitter API key, the application will not attempt to tweet the photos. It will simply save the photos in the Pictures folder at /home/pi/Pictures.

Press and hold the GPIO button for 5 seconds to close the application.

To make the program run on boot, add the following entry using crontab -e:

@reboot python3 /home/pi/Virtual-Pi-Jam-Photobooth/photobooth.py &
Twitter API keys
In order to enable the Twitter feature, you'll need to provide Twitter API keys for the account you wish the photobooth to tweet from, i.e. your Club/School/Indivisual Twitter account.

Log in to Twitter and ensure a mobile number is added to your account.

Go to apps.twitter.com and create a new app.

Fill out your application details. If you use https://github.com/yorkpijam/Virtual-Pi-Jam-Photobooth as the website, other people will be able to see what generated the tweet.

Go to Keys and tokens and click the Create my access tokens button.

Open auth.py from the project folder and enter your consumer key, consumer secret, access token and access token secret in the variables provided, e.g:

CON_KEY = '0GrZb5jUk9O9KK9W6xhALmNhD'
CON_SEC = 'CDXCGvmGuMvOBQvvrDZO7lzbj83rDMVpcEnqWYXxkfLGfGrFpL'
ACC_TOK = '27241881-XPa2YtoA4PwHkIelgYYgMbf24kaEYXj4bp6Ualmk8'
ACC_SEC = 'ruydKmwQ1ft5fPNkL3AVsOS6EltMdutkek3N80Dlhsjkl'
Now when you run photobooth.py, it will be able to tweet the photos. There is an option to cancel a tweet before it is sent.

Photos tweeted are still stored in the Pictures folder.

To disable the Twitter feature, simply restore the CON_KEY variable to an empty string

IMPORTANT: Do not share the API keys. Do not accidentally push them to GitHub.

Languages
Simply edit text.py, which contains dictionaries of the strings used as camera text annotations, and add a copy of the English language dictionary text_en below, renaming it as appropriate. Then replace the dictionary values (right hand side) with the translated equivalents, leaving the keys (left hand side) the same.

Please note that the camera firmware does not support non-ASCII characters.

To select a language, edit the following line in photobooth.py:

text = get_text(language='en')
Current language support:

English - en
German (Deutsche) - de
French (Français) - fr
Spanish (Español) - es
Welsh (Cymraeg) - cy
Pull requests with more language support welcome, as are any improvements to existing translations (they were all done using Google Translate).

Credits
Thanks to Ben Nuttall for allowing us to borrow and edit the code for Virtual Pi Jam use.
