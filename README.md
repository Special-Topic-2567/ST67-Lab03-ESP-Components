# ESP-Components

Components ใน ESP32 ใช้สำหรับเก็บ source code และทรัพยากรที่จะใช้กับ component ที่ต้องการ reuse ในโปรเจคอื่นๆ
การเพิ่ม component สามารถทำได้ที่ local เพื่อออกแบบ สร้าง และทดสอบการทำงานในระบบ หรือ นำเข้าจากแหล่งที่ตั้งภายนอก เช่น folder หรือ internet เพื่อนำมาใช้งานในระบบ

ในการทดลองนี้จะเริ่มจากการออกแบบและสร้าง component ขึ้นในระบบ (local)

## 1. สร้าง component ใหม่ โดยใช้ command palette

โดยทั่วไปแล้ว การสร้าง component ใดๆ สามารถทำได้เช่นเดียวกับการสร้าง component main ในใบงานที่ผ่านมา
ซึ่งนักศึกษาสามารถควบคุมองค์ประกอบต่างๆ ได้เองทั้งหมด แต่ในใบงานนี้เราจะทดลองสร้าง component ผ่านทาง command palette ของ VSCODE
แต่เมื่อสร้่างเสร็จแล้ว นักศึกษาสามารถเข้าไปแก้ไขได้เองเช่นเดียวกับใบงานที่ผ่านมา

1.1 สร้าง component ใหม่

![alt-text](./Pictures/Image_01.png)

vscode จะแสดงช่องให้ใส่ชื่อ component  ให้ตั้งชื่อเป็น LED

![alt-text](./Pictures/Image_02.png)

เมื่อกด enter จะได้โฟลเดอร์ของ component ชื่อ LED 

![alt-text](./Pictures/Image_03.png)

โดยมีเนื้อหาแต่ละไฟล์ดังต่อไปนี้

### CMakeLists.txt

``` CMake
idf_component_register(SRCS "LED.c"
                    INCLUDE_DIRS "include")
```

### LED.c

```c
#include <stdio.h>
#include "LED.h"

void func(void)
{

}
```



### LED.h

```c
void func(void);
```


## 2. แก้ไข code 
### 2.1 ไฟล์ LED.h

```c
void SET_LED_OUTPUT();
void LED_ON();
void LED_OFF();

```
### 2.2 ไฟล์ LED.c

```c
#include <stdio.h>
#include "LED.h"
#include "driver/gpio.h"

void SET_LED_OUTPUT()
{
  gpio_set_direction(5, GPIO_MODE_OUTPUT);  
}
void LED_ON()
{
    gpio_set_level(5,1);
}

void LED_OFF()
{
    gpio_set_level(5,0);
}
```
### 2.2 ไฟล์ CMakeLists.txt ใน component LED
```
idf_component_register(SRCS "LED.c"
                    INCLUDE_DIRS "include" 
                    REQUIRES driver)
```

### 2.4 แก้ไขไฟล์ CMakeLists.txt ใน Main

``` CMake
# Edit following two lines to set component requirements (see docs)
set(COMPONENT_REQUIRES driver LED)
set(COMPONENT_PRIV_REQUIRES )


set(COMPONENT_SRCS 
   "main.c"
   )
set(COMPONENT_ADD_INCLUDEDIRS "")

register_component()
```

### 2.5 ทดสอบรันโปรแกรม

#### ลิงค์งาน: https://github.com/AnchisaPhetnoi/ESP32_Blank.git

### LAB_3.1

![image](https://github.com/user-attachments/assets/dda8e6e8-caac-44d3-8199-974e18058ed2)
![image](https://github.com/user-attachments/assets/30f21e01-5638-42ad-a74a-5589d5cbb70d)
![image](https://github.com/user-attachments/assets/df6ca4d5-4bf2-49dc-9199-3bc7ab50a820)

![image](https://github.com/user-attachments/assets/8cd03fbd-3541-489e-a5a9-b687aad99004)

![image](https://github.com/user-attachments/assets/c05a7584-72c6-4b9a-88e0-5526acc22874)

![image](https://github.com/user-attachments/assets/1a0d0b18-c772-499e-8d5c-0aa5e9f9f10e)

![image](https://github.com/user-attachments/assets/dbf5c68c-6888-47ac-897a-80d5d04ab78a)


### LAB_3.2






















