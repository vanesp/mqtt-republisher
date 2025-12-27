SUMMARY
=======

A quick python script to accept incoming MQTT payloads under the topic of /domoticz/out, and look them up in a table for republishing under a logical topic name

It stems from a suggestion to try and organize disparate sources into one logical hierarchy. 

Anything that is published under /domoticz/out but does not match anything in the map gets republished with /unknown/ prepended to the topic.


INSTALL
=======

Make sure it is installed in:

/home/pi/mqtt-republisher

And that this path is correctly inserted in mqtt-republisher.py and mqtt-republish.service


Set up a virtual environment

    cd /home/pi/mqtt-republisher
    python3 -m venv .
    source bin/activate

Install dependencies:

    pip3 install paho-mqtt
    pip3 install setproctitle

Then modify the path to /home/pi/mqtt-republisher/bin/python3
 
    sudo cp mqtt-republish.service /etc/systemd/system
    sudo touch /var/log/mqtt-republisher.log
    sudo chown pi:pi /var/log/mqtt-republisher.log

    sudo systemctl enable mqtt-republish.service
    sudo systemctl start mqtt-republish.service

Check the status:

    sudo systemctl status mqtt-republish.service
