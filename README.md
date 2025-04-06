# 📘 Ebook Reader cu ESP32-C6

Acest proiect este un **Ebook Reader portabil**, cu consum redus, bazat pe **ESP32-C6** și ecran **E-Paper**, ideal pentru lectură prelungită.  
Dispozitivul citește fișiere `.txt` de pe un card **microSD** și permite navigarea cu **butoane fizice**, având alimentare din **baterie Li-Po** și opțional monitorizare a nivelului acesteia.

---

## 📦 Bill of Materials (BOM)

| Componentă           | Model/Tip                  | Link comandă | Datasheet     |
|----------------------|----------------------------|--------------|----------------|
| Microcontroller      | ESP32-C6                   | Mouser       | [ESP32-C6](#)  |
| Ecran                | E-Paper Display 2.9"       | Comet        | [GDEH029A1](#) |
| Cart Reader          | MicroSD SPI module         | Mouser       | [Modul SD](#)  |
| Senzor de mediu      | BME688                     | Mouser       | [BME688](#)    |
| RTC                  | DS3231SN                   | Mouser       | [DS3231](#)    |
| Battery Monitor      | MAX17048                   | Mouser       | [MAX17048](#)  |
| Flash extern         | W25Q512JV (64MB)           | Mouser       | [W25Q512JV](#) |
| Regulator tensiune   | MCP1826S-3302E/DB          | Mouser       | [MCP1826](#)   |
| BMS                  | TP4056                     | Comet        | [TP4056](#)    |
| Butoane              | Tactile Switches           | Comet        | [SKQG](#)      |

---

## ⚙️ Funcționalitate Hardware

### 1. ESP32-C6
- Interfață principală: SPI, I2C, GPIO  
- Flash extern NOR (64MB) prin QSPI  
- UART pentru debug  
- Alimentare 3.3V prin LDO

### 2. E-Paper Display
- Alimentat prin EPD Power Driver (boost + FET)  
- Conectat prin SPI la ESP32-C6  
- Pini dedicați: DIN, CLK, CS, DC, RST, BUSY

### 3. Modul SD Card
- Interfață SPI  
- Stocare fișiere `.txt`

### 4. RTC DS3231SN
- I2C cu backup battery (CR2032)  
- Oră exactă cu temperatură compensată

### 5. Senzor BME688
- I2C – temperatură, presiune, umiditate, calitate aer  
- Util pentru monitorizare ambientală (opțional)

### 6. MAX17048
- Monitorizare nivel baterie prin I2C  
- Poate afișa procentul pe ecran

### 7. TP4056 Charging
- Încărcare Li-Po prin USB-C  
- Protecție la supradescărcare/supraincărcare

---

## 📌 Pini ESP32-C6 Utilizați

| Pin ESP32-C6 | Funcție hardware         | Componentă              |
|--------------|--------------------------|--------------------------|
| GPIO0        | I2C SCL                  | BME688, MAX17048, DS3231 |
| GPIO1        | I2C SDA                  | BME688, MAX17048, DS3231 |
| GPIO2        | SPI MOSI                | E-paper, SD, Flash       |
| GPIO3        | SPI MISO                | SD, Flash                |
| GPIO4        | SPI CLK                 | E-paper, SD, Flash       |
| GPIO5        | SPI CS (e-paper)        | E-paper                  |
| GPIO6        | SPI CS (SD card)        | SD Card                  |
| GPIO7        | SPI CS (Flash extern)   | W25Q512JV                |
| GPIO8        | GPIO Buton 1            | Pag. înainte             |
| GPIO9        | GPIO Buton 2            | Pag. înapoi              |
| GPIO10       | GPIO Buton 3            | Reset/Menu               |
| GPIO11       | UART TX                 | Debug UART               |
| GPIO12       | UART RX                 | Debug UART               |

---

## 🖼️ Design PCB & Randări

- **PCB**: 2 straturi, dimensiuni: `92.2mm x 67.2mm`  
- **Componente** poziționate compact pentru portabilitate  
- **Acces ușor** la card microSD, USB-C și butoane  
- **Protecție ESD** pe liniile USB și SPI  


## ✅ Alte Detalii Relevante

- **Mod Deep Sleep**: activat după 30s de inactivitate  
- **W25Q512JV Flash extern**: stocare rapidă pentru sute de cărți `.txt`  
- **Qwiic/Stemma QT header**: pentru expansiune cu alte periferice  
- **Test Pads**: depanare & validare semnal
