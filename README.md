# ESE519_Final

For ESE 519 Final project. balanced board controled Drone and Panel kit Camera.

**TEAM - I believe I can fly:**

Yuxuan Li: https://github.com/Yuxuan-Li295

Xingqi Pan: https://github.com/anniepan8215

Yuxin Wang: https://github.com/Ariiees


## What it does?

You coud using a balanced board to control the fly of the drone in real time(mimic the behavior of the joystick). 

### Demo

add a git here

## How we made it

### Circuit connection 【Hardware】

**PIN MAP**

| RP2040 | Controller | PICO4ML |
| :--| :--  |:-- |
| A2 | X | N/A |
|  A3  |   |     |
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
Initialize three ports for output and communication between RP2040 and Pico4ML:
```c
  ICM42622::Icm42622Init();
  gpio_init(26);
  gpio_set_dir(26, GPIO_OUT);
  gpio_init(27);
  gpio_set_dir(27, GPIO_OUT);
  gpio_init(28);
  gpio_set_dir(28, GPIO_OUT);
``` 
Get the accelerometer value for the IMU
```c
ICM42622::Icm42622ReadGyro(&x,&y,&z);
ICM42622::Icm42622ReadAccel(&accex,&accey,&accez);
//printf("Gyro: X:%.2f, Y: %.2f\n",x,y);
printf("Acce: X:%.2f, Y: %.2f,Z:%.2f\n",accex,accey,accez);
``` 
Then we judge the degree of tilt of the drone and assign different signal indicator that and pass it to RP2040 to control the fly direction of it.

```c
if(accex >= -1.1 && accex <= -0.7)
    {
      gpio_put(26,0);
      gpio_put(27,0);
      gpio_put(28,1);
      printf("Acce: X:%.2f, Y: %.2f\n",accex,accey);
      // move_forward(pio_pwm,smx,smy);
      printf("forward\n");
    }
    else if(accex >= 0.7 && accex <= 1.1)
    {
      gpio_put(26,0);
      gpio_put(27,1);
      gpio_put(28,0);
      printf("Acce: X:%.2f, Y: %.2f\n",accex,accey);
      // move_back(pio_pwm, smx, smy);
      printf("back\n");
    }
    else if(accey >= 0.6 && accey <= 1.1)
    {
      gpio_put(26,0);
      gpio_put(27,1);
      gpio_put(28,1);
      printf("Acce: X:%.2f, Y: %.2f\n",accex,accey);
      //move_left (pio_pwm, smx, smy);
      printf("left\n");
    }
    else if(accey >= -1.1 && accey <= -0.6)
    {
      gpio_put(26,1);
      gpio_put(27,0);
      gpio_put(28,0);
      printf("Acce: X:%.2f, Y: %.2f\n",accex,accey);
      // move_right(pio_pwm, smx, smy);
      printf("right\n");
    }
    else{
      gpio_put(26,0);
      gpio_put(27,0);
      gpio_put(28,0);
      printf("Acce: X:%.2f, Y: %.2f\n",accex,accey);
      // stay(pio_pwm, smx, smy);
      printf("stay\n");
    }
```

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
After got the integer value of the pattern by applying the 'left shift' operation combined with the 'OR' operation we can directly return the pattern value.
## Further...

We plan to ...

## File description

【File_name】: What is it

【README_midpoint】: Our midpoint project report.

【code/IBICF/motor/pwm_new.c】: Main code for RP2040_Drone.

【code/IMU_Part】: The main code for enable the IMU and using the accelerometer value to control the direction of the drone's flying.



