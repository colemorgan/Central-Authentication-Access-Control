Central-Authentication-Access-Control
=====================================

A central authentication system that communicates with various nodes to control access to areas/equipment

#Iterations:  

1. Communication between Raspberry Pi & Arduino (transfer a 'users/attributes' file)
2. Pass Fail communication displayed with two lights
3. Authentication with RFID

# Authentication Server
 
## Hardware
Raspberry Pi is being used because it has the ability to run Debian natively.
This gives a great deal of control over control logic.
It has significantly more system resources than an Arduino as well.

## Software/Services
The auth server will run openLDAP.

# Authentication Client

## Hardware
Getting Started documentation: <http://arduino.cc/en/Guide/HomePage>

The base Arduino being used is an Uno r3 - <http://store.arduino.cc/index.php?main_page=product_info&products_code=A000066>
At this point, we would like to use a POE ethernet shield with a microSD reader (Arduino networking is expensive though).

## Software/Services
The client has two primary operations

### Update Userlist
This should pull down the latest userlist from the authentication server into a local file.
If it can't update, the authentication client should attempt to email the board.
An indication LED should be used to identify the status of the last update attempt.

Blink Codes:
* Solid on - Successfully Updated
* Slow constant blinks - File is out-of-date

### Authenticate
Basic logic that compares required permissions for tool authentication against a local file.

Blink Codes:
* Two fast blinks - Permission granted (success)
* Three fast blinks - Permission denied (failure)
* Four fast blinks - User not found
* Five fast blinks - File not found

