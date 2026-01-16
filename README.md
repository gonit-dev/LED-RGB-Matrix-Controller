# LED-RGB-Matrix-Controller

Web-based controller untuk LED RGB Matrix menggunakan ESP8266 dan FastLED library.

## Features

- 🎨 Drag & drop color palette
- 📱 Responsive web interface
- 🔧 Configurable matrix layout (rows, cols, LEDs per strip)
- 🔄 Zigzag/serpentine wiring support
- 💾 Save/load configurations to ESP8266
- 💡 Brightness control
- 📍 Multiple starting corner positions

<img width="500px" height="auto" alt="FireShot Capture 129 - LED RGB Matrix Controller - 192 168 4 1" src="https://github.com/user-attachments/assets/9691a73d-477b-42be-863f-155aebe69ff7" />

## Hardware Requirements

- ESP8266 (NodeMCU/Wemos D1 Mini)
- WS2812B LED strips
- 5V Power supply (sesuai jumlah LED)
- Relay module (optional, untuk delay startup)

## Wiring

```
ESP8266 D4  → LED Data In
ESP8266 D1  → Relay (optional)
LED 5V      → External 5V Power Supply
LED GND     → ESP8266 GND + Power Supply GND
```

## Software Dependencies

### Arduino Libraries
- **FastLED** (3.x) - LED control
- **ArduinoJson** (6.x) - JSON parsing
- **ESP8266WiFi** - WiFi AP mode
- **ESP8266WebServer** - Web server
- **LittleFS** - File system

Install via Arduino Library Manager.

## Installation

### 1. Upload File System (LittleFS)
- Install [ESP8266LittleFS Plugin](https://github.com/earlephilhower/arduino-esp8266littlefs-plugin)
- Create `data` folder in project directory
- Put `index.html` and `css/foundation.min.css` in `data` folder
- Tools → ESP8266 LittleFS Data Upload

### 2. Upload Sketch
- Open `led.ino` in Arduino IDE
- Set board to "NodeMCU 1.0 (ESP-12E Module)" or your ESP8266 board
- Upload sketch

### 3. Configure LEDs
Edit in `led.ino`:
```cpp
#define LED_PIN     D4      // Data pin
#define NUM_LEDS    300     // Total LEDs (max)
#define MAX_GROUPS  20      // Max color groups
```

## Usage

1. **Connect to WiFi**
   - SSID: `LED_Matrix_Config`
   - Password: `12345678`

2. **Open Web Interface**
   - Browse to: `http://192.168.4.1`

3. **Configure Matrix**
   - Set rows, columns, LEDs per strip
   - Choose starting corner
   - Enable/disable zigzag mode

4. **Select LEDs**
   - Click LED then choose color
   - OR drag & drop color to LED
   - Use "Pilih Semua" for all LEDs

5. **Save Configuration**
   - Click "💾 Simpan ke Arduino"
   - Configuration saved to LittleFS
   - Auto-loads on restart

## Configuration Limits

```cpp
#define NUM_LEDS 300              // Max total LEDs
#define MAX_GROUPS 20             // Max color groups
#define MAX_LEDS_PER_COLOR 50     // Max LEDs per color
```

Adjust these values based on your ESP8266 memory.

## Troubleshooting

**LEDs not lighting:**
- Check data pin connection (D4)
- Verify power supply voltage (5V)
- Ensure common ground

**Web interface not accessible:**
- Check WiFi connection
- Verify IP address (192.168.4.1)
- Check Serial Monitor for errors

**Configuration not saving:**
- Ensure LittleFS uploaded correctly
- Check Serial Monitor for errors
- Verify JSON size < 8KB

## File Structure

```
project/
├── led.ino                  # Main Arduino sketch
├── data/
│   ├── index.html          # Web interface
│   └── css/
│       └── foundation.min.css

- FastLED by Daniel Garcia
- ArduinoJson by Benoit Blanchon
- Foundation CSS by ZURB
