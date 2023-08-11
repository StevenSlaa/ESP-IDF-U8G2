# ESP-IDF v5 - u8g2
This is a working example of how you can use u8g2 Library in ESP-IDF.
This contains an updated driver by J0003 of [nkolban](https://github.com/nkolban/esp32-snippets/tree/master/hardware/displays/U8G2)

Special Thanks to:
- [adamwilt](https://www.esp32.com/viewtopic.php?t=18656#:~:text=by-,adamwilt,-%C2%BB%20Wed%20Dec)
- [J00003](https://www.esp32.com/viewtopic.php?t=18656#:~:text=by-,J00003,-%C2%BB%20Tue%20Mar)
- [Original Post](https://www.esp32.com/viewtopic.php?t=18656)

## Background
I wanted to use my SSD1306 Monochrome OLED display inside of the ESP-IDF, but wanted something more versitile than [LVGL](https://lvgl.io/).
I started of with the [example within the ESP-IDF](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/lcd/i2c_oled). This works reasonably well, but overtime I noticed it is not really optimized to work with monochrome and non touch displays. Also I was running into problems with styling and outdated forum posts. I wanted to have more control. From experience with Arduino I remembered [u8g2](https://github.com/olikraus/u8g2). Trying to implement it in ESP-IDF I noticed that a hal-driver was neccesary to use it within ESP-IDF. I came a cross a [driver from nkolban](https://github.com/nkolban/esp32-snippets/tree/master/hardware/displays/U8G2). It was however not compatible with the latest version of ESP-IDF(V5.2 at time of writing)

## How to load U8g2 inside of your ESP-IDF project
### Add u8g2 to your project
When you created your clean ESP-IDF project, you have to add a folder inside of you project folder (folder where your main folder is located in) called `components`. inside of this folder you have to add the u8g2 library. To make it easy, just navigate to your components folder and execute the following command:
```bash
git clone https://github.com/olikraus/u8g2.git
```
> **Tip:**
> Rename your u8g2 repository folder to `u8g2` instead of `u8g2-master` this keeps your project nice and clean. 😉

### Add the hal-driver
In this repository you have to download two files: `u8g2_esp32_hal.c` and `u8g2_esp32_hal.h` these two files have to be placed inside of the `main` folder (where your `main.c` file is located).

### Add the files to the CMakeLists.txt
In the same `main` folder there is a `CMakeLists.txt` file. In this file you should add the c-file we have just added. The content of this file should look like this:
```txt
idf_component_register(SRCS "main.c" "u8g2_esp32_hal.c" INCLUDE_DIRS ".")
```
> **Note:**
> The content of the CMakeLists.txt can differ depending on your specific project. Just remember that `u8g2_esp32_hal.c` should be added. Otherwise the compiler will complain that it cannot find the file.



Thats it! Take a look inside of the example folder on how to use it.


## Other helpfull recources (might be outdated):
- [u8g2 IDF-Component (seems to be up to date)](https://github.com/mkfrey/u8g2-hal-esp-idf)
- [Original post](https://www.esp32.com/viewtopic.php?t=18656)
- [Working alternative to u8g2 which is less versitile but works really well](https://www.youtube.com/watch?v=9v-5XzEFTvw)
- [Reddit post about the subject](https://www.reddit.com/r/esp32/comments/g9jkgv/a_good_esp_idf_component_for_oled_i2c_displays/)
