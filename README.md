# Arduino Joystick Library
This library can be used with Arduino IDE 1.6.6 (or above) to add one or more joysticks (or gamepads) to the list of HID devices an Arduino Leonardo or Arduino Micro (or any Arduino clone that is based on the ATmega32u4) can support. This will not work with Arduino IDE 1.6.5 (or below).

##Installation Instructions
Copy the Joystick folder to the Arduino libraries folder (typically %userprofile%\Documents\Arduino\libraries). The library (or libraries) should now appear in the Arduino IDE list of libraries.

##Examples
The following example Arduino sketch files are included in this library:

- JoystickTest - Simple test of the Joystick library. Exercises all of the Joystick library functions when pin A0 is grounded.
- MultipleJoystickTest - Creates 4 Joysticks using the library and exercises the first 16 buttons and X and Y axis when pin A0 is grounded.
- JoystickButton - Creates a Joystick and maps pin 9 to button 0, pin 10 to button 1, pin 11 to button 2, and pin 12 to button 3. 

###Simple example

	#include <Joystick.h>
	
	Joystick_ Joystick;
	
	void setup() {
	  // Initialize Button Pins
	  pinMode(9, INPUT_PULLUP);
	
	  // Initialize Joystick Library
	  Joystick.begin();
	}
	
	// Constant that maps the phyical pin to the joystick button.
	const int pinToButtonMap = 9;
	
	// Last state of the button
	int lastButtonState = 0;
	
	void loop() {
	
	  // Read pin values
      int currentButtonState = !digitalRead(pinToButtonMap);
	  if (currentButtonState != lastButtonState)
	  {
	    Joystick.setButton(0, currentButtonState);
	    lastButtonState = currentButtonState;
	  }
	
	  delay(50);
	}

##Joystick Library API
The following API is available if the Joystick library in included in a sketch file.

###Joystick.begin(bool initAutoSendState)
Starts emulating a game controller connected to a computer. By default all methods update the game controller state immediately. If initAutoSendState is set to false, the Joystick.sendState method must be called to update the game controller state.

###Joystick.end()
Stops the game controller emulation to a connected computer.

###Joystick.setXAxis(byte value)
Sets the X axis value. Range -127 to 127 (0 is center).

###Joystick.setYAxis(byte value)
Sets the Y axis value. Range -127 to 127 (0 is center).

###Joystick.setZAxis(byte value)
Sets the Z axis value. Range -127 to 127 (0 is center).

###Joystick.setXAxisRotation(int value)
Sets the X axis rotation value. Range 0° to 360°.

###Joystick.setyAxisRotation(int value)
Sets the Y axis rotation value. Range 0° to 360°.

###Joystick.setZAxisRotation(int value)
Sets the Z axis rotation value. Range 0° to 360°.

###Joystick.setButton(byte button, byte value)
Sets the state (0 or 1) of the specified button (0 - 31). The button is the 0-based button number (i.e. button #1 is 0, button #2 is 1, etc.). The value is 1 if the button is pressed and 0 if the button is released.

###Joystick.pressButton(byte button)
Press the indicated button (0 - 31). The button is the 0-based button number (i.e. button #1 is 0, button #2 is 1, etc.).

###Joystick.releaseButton(byte button)
Release the indicated button (0 - 31). The button is the 0-based button number (i.e. button #1 is 0, button #2 is 1, etc.).

###Joystick.setThrottle(byte value)
Sets the throttle value. Range 0 to 255.

###Joystick.setRudder(byte value)
Sets the rudder value. Range 0 to 255.

###Joystick.setHatSwitch(byte hatSwitch, int value)
Sets the value of the specified hat switch. The hatSwitch is 0-based (i.e. hat switch #1 is 0 and hat switch #2 is 1). The value is from 0° to 360°, but in 45° increments. Any value less than 45° will be rounded down (i.e. 44° is rounded down to 0°, 89° is rounded down to 45°, etc.). Set the value to -1 to release the hat switch.

###Joystick.sendState()
Sends the updated joystick state to the host computer. Only needs to be called if AutoSendState is false (see Joystick.begin for more details).

##Testing Details
I used this library to make an Arduino appear as 1, 2, 3, and 4 joysticks / gamepads.  

I have tested this library using the following Arduino IDE Versions:

- 1.6.6
- 1.6.7
- 1.6.8

I have tested this library with the following boards:

- Arduino Leonardo
- Arduino Micro

(as of 2016-05-13)