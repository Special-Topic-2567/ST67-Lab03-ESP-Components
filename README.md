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

## LAB_3.1

![image](https://github.com/user-attachments/assets/dda8e6e8-caac-44d3-8199-974e18058ed2)
![image](https://github.com/user-attachments/assets/30f21e01-5638-42ad-a74a-5589d5cbb70d)
![image](https://github.com/user-attachments/assets/df6ca4d5-4bf2-49dc-9199-3bc7ab50a820)

![image](https://github.com/user-attachments/assets/8cd03fbd-3541-489e-a5a9-b687aad99004)

![image](https://github.com/user-attachments/assets/c05a7584-72c6-4b9a-88e0-5526acc22874)

![image](https://github.com/user-attachments/assets/1a0d0b18-c772-499e-8d5c-0aa5e9f9f10e)

![image](https://github.com/user-attachments/assets/dbf5c68c-6888-47ac-897a-80d5d04ab78a)



## LAB_3.2

Leb จะเปิดไฟขึ้นแสดงครึ่งวิ และจะปิดไฟดับแสดงครึ่งวิ

![image](https://github.com/user-attachments/assets/59cd758f-4206-47c9-b526-aa32516fc12c)

![image](https://github.com/user-attachments/assets/fffc02a3-4cc4-4e80-95d0-09d0258e05f5)

![image](https://github.com/user-attachments/assets/fdf43eca-d3a3-494e-9013-a524610fb0f5)

#### ผลลัพน์
![image](https://github.com/user-attachments/assets/48af654a-10dc-4022-97ea-f663d075d664)

![image](https://github.com/user-attachments/assets/41ce5a16-b4c9-41e9-83d7-e97e243e08c3)

![image](https://github.com/user-attachments/assets/61bfa16b-77d6-4cf3-9874-c751bb6c7b63)

## LAB_3.3


Leb จะเปิดไฟขึ้นแสดงครึ่งวิ และจะปิดไฟดับแสดงครึ่งวิ

#### ผลลัพน์
![image](https://github.com/user-attachments/assets/cc4e5e6e-66d2-4717-865c-9d3c3e83f4b1)
![image](https://github.com/user-attachments/assets/b9ecb53e-7883-467d-b1e8-8b5446fac002)
![image](https://github.com/user-attachments/assets/9e0781e5-9837-46ce-a48c-24ea6d22ddaf)

![image](https://github.com/user-attachments/assets/14e23f95-8778-4500-92c6-dfbdfe632f84)
![image](https://github.com/user-attachments/assets/b83391ec-7095-468e-8ebf-312f0927b33b)


![image](https://github.com/user-attachments/assets/b83785ff-8785-4432-8560-3bc5d1bc5c27)

![image](https://github.com/user-attachments/assets/9c767ff8-c6f7-48bb-b5ce-a38cbae2b2db)
![image](https://github.com/user-attachments/assets/5611881c-d880-446c-a326-998f92d7380c)
![image](https://github.com/user-attachments/assets/ac760b1f-e199-495a-aca2-692b631b5a56)
![image](https://github.com/user-attachments/assets/ba9efcae-05a4-4cbb-b504-b0df83386559)

![image](https://github.com/user-attachments/assets/3420d1ae-0c4e-436b-b1d5-43ec3ea466e1)
















