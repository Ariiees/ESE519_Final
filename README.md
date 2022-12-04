# ESE519_Final
For ESE 519 Final project. Drone with learning.

# ESE519_Final
For ESE 519 Final project. Drone with learning.

- **code:**
  - **working:**
    - RP2040
    - balance board Python code
    - PIO PWM code on PIO 0:修改到没有main只有调用的样式
    - I2C communication on PIO 1 from lab 2B
  - **in-progress:**
    - Pico4ML
    - Machine learning
    - gyroscope
  - **libraries:**
    - pwm.pio, uart_rx.pio, uart_tx.pio
    - pico_stdlib, hardware_pio, hardware_pwm
    - pico_multicore
  - **reference:**
    - https://cla.purdue.edu/academic/rueffschool/ad/etb/resources/robotics01_SN754410_Arduino.pdf
- **media:**
  - **materials:**
    - 整理一下元器件的图片 用元器件名称命名图片
  - **design:**
 
  ![circuit](https://user-images.githubusercontent.com/87698138/205519976-f471acd5-c7fc-46cb-b8ed-c9c0dd39164f.jpg)
  
  - **troubleshooting:**
    - 如何从0开始让扇叶转动
    - 使用示波器hack无人机原有电路得知舵机是DC输入
    - pwm转DC
    - 调整pwm让舵机可以以不同速度转动
  - **demos:**
    - video
    
    
    - circuit connection
    
    ![now](https://user-images.githubusercontent.com/87698138/205520253-aa817341-2fac-4a60-998f-c7cdaaf69fd9.jpg)

- **diagram:**
 - 画一张完整的图片 包含全部的设计
