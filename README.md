# Very-Slow-Arduino-IDE-Compilation-Symptom ?
If It takes too long to compile a small program using Arduino IDE versio 1.8.x or 2.x
you must read this repo!





Over the past several years, I have worked with a diverse range of Arduino components for my projects and sensor applications.
Recently, I have encountered a disturbing issue where the compilation process can occasionally take an unreasonably time and
it might be more than 8 minutes while running the Arduino IDE from a stong i7 computer with 16GB of RAM and a fast SSD drive
which is frustrating and does not make sense!

At first, I thought that the compiling process required a long time due to the complexity of my project - and thus the complexity / length
of the code, which demands long processing time, but it turned out that even for short or simple code, the compiling process is long.

It seems that the phenomenon depends on the board model/libraries installed, which extend the compilation time.
Thus, choosing a board with other libraries can help the compilation process to be shorter, but the whole idea of using Arduino is to choose 
the appropriate board according to the project needs and not according to the time required to perform the compilation.

Therefore, replacing the selected board type because Arduino IDE is slow is not the desired solution.

To solve the problem of long compilation time, I made a number of attempts to first understand the cause.

1st test:
I began by stopping the antivirus software, suspecting it might be the reason behind the slow compilation time. 
However, this did not resolve the issue.

Next, since I was unsure whether stopping the antivirus was effective, I completely uninstalled it. This did lead to 
some improvement, but compilation still took over eight minutes.

2nd test:
Was to completely uninstall the installation of Arduino 2.2.1 and re-install the previous version 1.8.19.
However, it turned out that the phenomenon of the long compilation process exists with both versions of Arduino IDE.

3rd test:
Would a powerful and fast computer solve the problem? 
I tried to check how much the computer hardware affects the compilation speed. 
Since I didn't have a powerful computer available, I set up a dedicated cloud computer with 8 cores and 32GB of memory. 
This virtual computer passed successfully in a few benchmark tests and turned out to be much faster than my personal i7 computer.

I have installed the Arduino IDE on it with the same settings and the same libraries. However, the compilation speed 
improved to four minutes. Since the code has not been changed, and I'm using a faster computer, the compilation speed is still 
not reasonable. 

To try to understand where the problem is, I selected the "Show verbose output during compilation" option in the Arduino IDE Preferences, 
which will show detailed comments while the compilation progress is running.


**Setting the compilation Preferences in the Arduino IDE:**

```
File>Settings>Preferences>Show verbose output during compilation
```

![image](https://github.com/RamiLup/Very-Slow-Arduino-IDE-Compilation-Symptom/assets/42478562/7b759cbf-0c10-4780-9aa4-4cb3605197d0)



What I saw after setting that option, that the Arduino is not stuck. It is working really hard to go over all the files in 
some of the libraries.

Here is a short example from the huge log:

```

"C:\\Users\\RAM\\AppData\\Local\\Arduino15\\packages\\esp32\\tools\\xtensa-esp32s3-elf-gcc\\gcc8_4_0-esp-2021r2-patch3/bin/xtensa-esp32s3-elf-g++" -DHAVE_CONFIG_H "-DMBEDTLS_CONFIG_FILE=\"mbedtls/esp_config.h\"" -DUNITY_INCLUDE_CONFIG_H -DWITH_POSIX -D_GNU_SOURCE "-DIDF_VER=\"v4.4.1-1-gb8050b365e\"" -DESP_PLATFORM -D_POSIX_READER_WRITER_LOCKS "-IC:\\Users\\RAM\\AppData\\Local\\Arduino15\\packages\\esp32\\hardware\\esp32\\2.0.3/tools/sdk/esp32s3/include/config" "-IC:\\Users\\RAM\\AppData\\Local\\Arduino15\\packages\\esp32\\hardware\\esp32\\2.0.3/tools/sdk/esp32s3/include/esp_hw_support/include/soc/esp32s3" "-IC:\\Users\\RAM\\AppData\\Local\\Arduino15\\packages\\esp32\\hardware\\esp32\\2.0.3/tools/sdk/esp32s3/include/spi_flash/include" "-IC:\\Users\\RAM\\AppData\\Local\\Arduino15\\packages\\esp32\\hardware\\esp32\\2.0.3/tools/sdk/esp32s3/include/bootloader_support/include" "-IC:\\Users\\RAM\\AppData\\Local\\Arduino15\\packages\\esp32\\hardware\\esp32\\2.0.3/tools/sdk/esp32s3/include/nvs_flash/include" "-IC:\\Users\\RAM\\AppData\\Local\\Arduino15\\packages\\esp32\\hardware\\esp32\\2.0.3/tools/sdk/esp32s3/include/pthread/include" "-IC:\\Users\\RAM\\AppData\\Local\\Arduino15\\packages\\esp32\\hardware\\esp32\\2.0.3/tools/sdk/esp32s3/include/esp-dsp/modules/windows/blackman_nuttall/include" "-IC:\\Users\\RAM\\AppData\\Local\\Arduino15\\packages\\esp32\\hardware\\esp32\\2.0.3/tools/sdk/esp32s3/include/esp-sr/esp-tts/esp_tts_chinese/include" "-IC:\\Users\\RAM\\AppData\\Local\\Arduino15\\packages\\esp32\\hardware\\esp32\\2.0.3/tools/sdk/esp32s3/include/esp-sr/include/esp32s3" "-IC:\\Users\\RAM\\AppData\\Local\\Arduino15\\packages\\esp32\\hardware\\esp32\\2.0.3/tools/sdk/esp32s3/include/esp32-camera/driver/include" "-IC:\\Users\\RAM\\AppData\\Local\\Arduino15\\packages\\esp32\\hardware\\esp32\\2.0.3/tools/sdk/esp32s3/include/esp32-camera/conversions/include" "-IC:\\Users\\RAM\\AppData\\Local\\Arduino15\\packages\\esp32\\hardware\\esp32\\2.0.3/tools/sdk/esp32s3/include/fb_gfx/include" "-IC:\\Users\\RAM\\AppData\\Local\\Arduino15\\packages\\esp32\\hardware\\esp32\\2.0.3/tools/sdk/esp32s3/qspi_opi/include" -mlongcalls -ffunction-sections -fdata-sections -Wno-error=unused-function -Wno-error=unused-variable -Wno-error=deprecated-declarations -Wno-unused-parameter -Wno-sign-compare -ggdb -Os -freorder-blocks -Wwrite-strings -fstack-protector -fstrict-volatile-bitfields -Wno-error=unused-but-set-variable -fno-jump-tables -fno-tree-switch-conversion -std=gnu++11 -fexceptions -fno-rtti -c -w -x c++ -E -CC -DF_CPU=240000000L -DARDUINO=10819 -DARDUINO_ESP32S3_DEV -DARDUINO_ARCH_ESP32 "-DARDUINO_BOARD=\"ESP32S3_DEV\"" "-DARDUINO_VARIANT=\"esp32s3\"" -DARDUINO_PARTITION_default -DESP32 -DCORE_DEBUG_LEVEL=0 -DARDUINO_RUNNING_CORE=1 -DARDUINO_EVENT_RUNNING_CORE=1 -DBOARD_HAS_PSRAM -DARDUINO_USB_MODE=1 -DARDUINO_USB_CDC_ON_BOOT=0 -DARDUINO_USB_MSC_ON_BOOT=0 -DARDUINO_USB_DFU_ON_BOOT=0 "@C:\\Users\\RAM\\AppData\\Local\\Temp\\arduino_build_113463/build_opt.h" "-IC:\\Users\\RAM\\AppData\\Local\\Arduino15\\packages\\esp32\\hardware\\esp32\\2.0.3\\cores\\esp32" "-IC:\\Users\\RAM\\AppData\\Local\\Arduino15\\packages\\esp32\\hardware\\esp32\\2.0.3\\variants\\esp32s3" "-IC:\\Users\\RAM\\Documents\\Arduino\\libraries\\Wire\\src" "-IC:\\Users\\RAM\\Documents\\Arduino\\libraries\\SPI\\src" "-IC:\\Users\\RAM\\Documents\\Arduino\\libraries\\lvgl\\src" "-IC:\\Users\\RAM\\Documents\\Arduino\\libraries\\GFX_Library_for_Arduino\\src" "-IC:\\Users\\RAM\\Documents\\Arduino\\libraries\\gt911-arduino-main" "C:\\Users\\RAM\\Documents\\Arduino\\libraries\\lvgl\\src\\draw\\stm32_dma2d\\lv_gpu_stm32_dma2d.c" -o nul

```

![image](https://github.com/RamiLup/Very-Slow-Arduino-IDE-Compilation-Symptom/assets/42478562/08a564e8-dfcd-4de0-9a8b-94a8fbcf74c2)


This is very strange. The compiler is not supposed to verify all files.
But it might do so in the first compilation process of the project, After that it should only go over files that have been modified.

In other words, even if the first compilation process might take ~8 minutes, the second it should be much shorter.

At this testing state, there were not many directions and options left, so I started to think that there is a problem in the Arduino IDE software...


**The fourth and last experiment:**
My last test was very short. I have added the Visual Micro plugin to the Visual Studio development environment. 
So far, I haven't used Visual Studio for Arduino projects.

Performing a compilation process for the same code endwed very fast! it took less than 30 seconds using my computer, 
and not on the fast virtual machine.

The paradox here is that the installation of Visual Micro pluging for Arduino relies on the installation of Arduino IDE
and its libraries, which are already installed on the computer.

Conclusion:
Most likely the problem is in the Arduino IDE settings or there is a bug in the two versions I have checked.
The compilation process using the Arduino IDE is not performed optimally for some Arduino boards / libraries. 
Maybe there are some configuration files which I have missed in the Arduino IDE settings which can configure the 
compliation prosses to be much more efficient ?

Therefore, my solution for anyone who encounters the same phenomenon of a long compilation process in Arduino IDE is to work:
Visual studio from [microsoft.com](https://visualstudio.microsoft.com/) , and add the Arduino plugin form visual micro from [https://www.visualmicro.com and Visual Studio ](https://www.visualmicro.com/)https://www.visualmicro.com/

![image](https://github.com/RamiLup/Very-Slow-Arduino-IDE-Compilation-Symptom/assets/42478562/fc378d67-f6cd-43cf-8262-48bfe1d60dd7)



