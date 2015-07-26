LED Matrix GUI controller and Python library
===========
## LED Controller GUI
This PyQt4 based GUI, allows you to control the individual LEDs on your matrix, as well as generate a text file encoding the 8x8 graphic.

### Requirements
* Python 2
* PyQt4
* max7219 (https://github.com/rm-hull/max7219)

### Usage
Launch either via the terminal, or through the Python 2 IDLE in Raspbian, when controlling the Desktop over a VNC server. PyQt4 programs do not work over the X11 remote desktop service, hence they must be launched through the Python 2 IDLE, and not through the terminal.
```
sudo python led-controller-gui.py
```
To control the LEDs on your matrix, simply click the radio buttons to enable them. Once you've made your design, press the 'Update Matrix' button to light up the LEDs. 

Press the 'Generate Matrix' button to output a `.txt` file containing a 1-dimensional array which you can read into the Python library in your own project. The 'Output style' dropdown box will let you control the output style of the file, although currently there's only one output coded in. 
The 'Matrix orientation' dropdown box let's you control the orientation of the matrix, so as to ensure you see your 8x8 graphic upright as in the program. This sometimes becomes an issue if you plug in the matrix using the pins into the breadboard, meaning it's actually upside down.

![LED GUI controller interface](http://www.scienceexposure.com/wp-content/uploads/2015/07/led-gui-screenshot.png)

## LEDController Python package
This small library provides simple functions for lighting up the LEDs on a MAX7219 LED matrix using an array / matrix.

### Requirements
* Python 2
* Raspberry Pi (any model will do) with Raspbian
* max7219 (https://github.com/rm-hull/max7219)

### Installation
```
wget https://github.com/ismailuddin/raspberrypi/raw/master/led-matrix/dist/LEDController-0.1.1.tar.gz
tar -xzf LEDController-0.1.1.tar.gz
cd LEDController-0.1.1/
sudo python setup.py install
```

### Usage
```
from LEDController.functions import MatrixFunctions
func = MatrixFunctions()
```

### Functions
`func.readMatrix()`

Reads file generated by 'Generate Matrix' button in LED GUI Controller
and outputs a NumPy array or matrix (specified by second argument) that
can be used for the 'updateMatrix' function.

###### Arguments
Argument | Description
--- | ---
filename | String or variable, directing to file.
output  | Specify 'list' to output a 1-D NumPy array; 'matrix' to output a 8*8 2-D NumPy matrix

`func.updateMatrix()`

Function to read in a NumPy 1-D array or 2-D matrix, and update
LEDs on LED matrix.

###### Arguments
Argument | Description
--- | ---
array | 1-D array / 2-D NumPy matrix
update  | Set by default to False. Set to True to update LEDs, one by one, creating a transition effect.
transition  | Integer value in milliseconds. Only active if 'update' argument set to True. Specifies time delay for updating LEDs in matrix.



`func.rotationAnim()`

Function to create an inifinitely looping rotation animation on the matrix.

###### Arguments
Argument | Description
--- | ---
matrix  | NumPy 2-D matrix, shape: 8x8
delay | Float value, default at 0.25. Specifies the time delay between rotations.
transition  | Alias to 'transition' argument in 'updateMatrix' function
redraw  | Alias to 'redraw' argument in 'updateMatrix' function