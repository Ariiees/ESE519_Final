# ESE519_Finald

For ESE 519 Final project. balanced board controled Drone and Panel kit Camera.

**TEAM - I believe I can fly:**

Yuxuan Li: https://github.com/Yuxuan-Li295

Xingqi Pan: https://github.com/anniepan8215

Yuxin Wang: https://github.com/Ariiees


## What it does?

You coud using a balanced board to control the....

### Demo

add a git here

## How we made it

### Circuit connection 【Hardware】

**PIN MAP**

| RP2040 | Contoler | PICO4ML |
| :--| :--  |:-- |
| 'A2 | X | N/A |
|  |  |   |     |
|  |  |   |     |
|  |  |   |     |


add picture and description here.

### Control theory 【Code for each MCU】

add code description here.

**RP2040_Drone**

We use PIO to write PWM that out put a DC voltage which will mimic the output the joystick, and this is the main part that we used to control the drone.

```
// partten: 001
void move_forward(PIO pio, uint sm_x, uint sm_y){
    pio_pwm_set_level(pio, sm_x, 125);
    pio_pwm_set_level(pio, sm_y, 77);
}

// partten: 010
void move_back(PIO pio, uint sm_x, uint sm_y){
    pio_pwm_set_level(pio, sm_x, 122);
    pio_pwm_set_level(pio, sm_y, 205);
}

//partten: 011
void move_left(PIO pio, uint sm_x, uint sm_y){
    pio_pwm_set_level(pio, sm_x, 85);
    pio_pwm_set_level(pio, sm_y, 120);
}

//partten: 100
void move_right(PIO pio, uint sm_x, uint sm_y){
    pio_pwm_set_level(pio, sm_x, 155);
    pio_pwm_set_level(pio, sm_y, 117);
}
```

**PICO4ML_IMU**

xxxx

**RP2040_Servo**

xxxx

**PICO4ML_Camera**

xxxx

### Communication protocol 【Code between each MCU】

**RP2040_Drone with PICO4ML_IMU**

We use 3 pins to indict the pattern of drone's direction. `000` means stay, '001': forward, `010`: backward, `011`: left, `100`: right.

For RP2040, it will get the digital value of pin, and distinguish the pattern.

```
int get_pattern(uint pin1, uint pin2, uint pin3){
    int a, b, c;
    sleep_us(50);
    if(gpio_get(pin1)==0){
        a = 0;
    }else{
        a = 1;
    }

    if(gpio_get(pin2)==0){
        b = 0;
    }else{
        b = 1;
    }

    if(gpio_get(pin3)==0){
        c = 0;
    }else{
        c = 1;
    }
    int pattern = c << 2 | b << 1 | a;
    return pattern;
}
```


xxxx

## Further...

We plan to ...

## File description

【File_name】: What is it

【README_midpoint】: Our midpoint project report.

【code/IBICF/motor/pwm_new.c】: Main code for RP2040_Drone.

