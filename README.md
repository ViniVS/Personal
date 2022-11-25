# Material Needed
ESP32<br>

## To Web Switch Project
<ul>
  <li>One Relay Module (~5V or ~3V)</li>
  <li>Three Jumpers Wires</li>
  <li>One Micro SD cable to USB</li>
</ul>

## Preparing our Work Space
#### With the ESP32, Relay and Jumpers in hands, let's connect them
 <ul>
  <li>Connect the first jumper to <b>'3v3'</b> pin in <i>ESP32</i> and <b>'VIN'</b> pin in <i>Relay Module</i>
  <li>Connect the second jumper to <b>'GND'</b> pin in <i>ESP32</i> and <b>'GND'</b> pin in <i>Relay Module</i>
  <li>Connect the third jumper to <b>'D22'</b> pin in <i>ESP32</i> and <b>'IN'</b> pin in <i>Relay Module</i>
 </ul>
 
#### To upload our code to ESP32 device, we need to install IDE to configurate our ESP
 <ul>
  <li>Install Arduino IDE <a href="https://www.arduino.cc/en/Guide/Windows#download-the-arduino-software-ide"><img height="45em" src= "https://upload.wikimedia.org/wikipedia/commons/thumb/8/87/Arduino_Logo.svg/720px-Arduino_Logo.svg.png"</img></a></li>
  <li>With our Arduino IDE open: <b><i>File>Preferences</i></b>, in "Additional URLs for Board Managers", paste the url as follow: "https://dl.espressif.com/dl/package_esp32_index.json", then press "OK" button. The packet will starting the download</li>
  <li>If you're getting the error: <i>"Error downloading https://dl.espressif.com/dl/package_esp32_index.json" </i>when you open the Board Manager, execute the below three commands in the Terminal to install the ESP32 Device Settings</li>  
_____________________________________________<br>
<div align="left">
<b> mkdir -p ~/Documents/Arduino/hardware/espressif <br>
  cd ~/Documents/Arduino/hardware/espressif <br>
  git clone https://github.com/espressif/arduino-esp32.git esp32 <br>
  cd esp32 <br>
  git submodule update --init --recursive <br>
  cd tools<br>
  export PYTHONHTTPSVERIFY=0<br>
  python get.py<br></b>
_____________________________________________<br>
</div>
<br>

  <li>Now, we need to: <b><i>Tools>Board>Board Managers</i></b>, search for <b>esp32</b> and press the install button to install the board by <i>Espressif System</i></li>
  <li>Let's select our Board: <b><i>Tools>Board>ESP32 Arduino> ESP32 Dev Module</i></b></li>  
  
</ul>

#### Well Done! Now let's install the libraries needed
<ul>
  <li>Still with Arduino IDE open: <i>Sketch>Include Librerie>Add libreries .ZIP</i>, now, select all the .ZIP in librerie Files <b>(Don't need to extract)</b></li>
</ul>
