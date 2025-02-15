# glucose
A Open Source Smart Watch Ecosystem.

## 1. Background

My father has diabetes, which essentially means his pancreas is operating on manual (hard) mode 24/7. A healthy pancreas not only produces insulin, which helps convert glucose in the bloodstream into energy, but it also regulates glucose production, instructing the liver to release glucose into the bloodstream when blood sugar levels are too low. A person with diabetes has to manage without these natural regulatory mechanisms, and low blood sugar can become a medical emergency if left untreated.
\
\
We are fortunate to have access to life-changing technologies like MEMS sensors, ultra-low power microcontrollers, and more. These advancements empower us to create solutions that address this problem.
Another critical point is the frequency with which someone with diabetes checks their blood glucose levels throughout the day. It’s like having an unfinished task lingering in the back of your mind all day, every day, which can lead to fatigue and burnout. If I could reduce the effort or time required to check blood glucose levels—or even better, provide a haptic alert at the right moments so that manual checks aren’t necessary—it could significantly improve quality of life.
\
\
During my M.Tech (Master of Technology) course, I conducted a literature survey and found that many smartwatches offer a plethora of features. They come with numerous shiny features and application notifications, are beautifully designed, but are often too distracting for elderly individuals, especially while they're at work. Additionally, they don’t provide a reliable or clear view of continuous glucose monitoring (CGM) data. What we need is something simple. 

## 2. Project Requirements

    • Simple – doesn't require a ton of effort to configure.
    • Cost-efficient – adds only the necessary functionality to keep costs low. 
    • Modular design – Each component and section of the hardware is designed in a way that makes it easy to replace.
    • Open source – All hardware, software, and firmware are open source under the GNU GPL v3 license. 
    • Ecosystem – Build an ecosystem and libraries for displays, haptic feedback, sensors, and other hardware to support the maximum number of hardware resources.  

## 3. Project Roadmap
 | PHASES  |                              DESCRIPTION                               |        STATUS          |
 | :------:|:-----------------------------------------------------------------------| :----------------------|
 | PHASE 1 | Selection of component based on requirements.                          |          ✅            |
 | PHASE 2 | Develop a prototype and test all functionalities.                      |          ✅            |
 | PHASE 3 | Build the PCB and firmware after completing the prototype.             |   In progress          |
 | PHASE 4 | Final assembly of hardware.                                            |                        |
 | PHASE 5 | Develop Android and iOS application.                                   |                        |


## 4. Hardware 

Initially, my aim was to select hardware components based on the availability of individual components, as well as their firmware/API, so that I wouldn't have to implement all the functionality from scratch.

Moreover, not all components were available at the time of implementation, such as the battery management system IC (**BQ2407x**). Therefore, I chose a different BMS IC during prototyping and kept the design modular, with all sensor ICs connected via the I2C (Inter-Integrated Circuit) communication protocol.

I used the *MPU6050* Inertial Measurement Unit to capture the rate of change and angular velocity. By using a sensor fusion algorithm, I implemented the functionality of step counting (pedometer) in the prototype design to test the sensor and compare the module's performance with the *Apple Watch SE 2nd Gen*. Initially, I planned to use all BGA packages and 0402 SMD components, but for prototyping purposes, I opted for 0603 SMD components (since 0603 is easier to hand-solder). I also chose the castellated *ESP32-C3-WROOM-02* module instead of the *ESP32-C3-MINI-1*. For this, I came up with two revisions of the PCB and their schematic designs.

Choosing the 1.69" rectangular display was an obvious choice for me because its API is easy to implement, and designing graphics and watch faces is simpler compared to a round LCD display. For this reason, I chose the 1.69" Waveshare LCD display module with a 240x280 resolution, which is more than enough to start with. My focus is to keep it simple and avoid adding unnecessary features that might irritate elderly people. Later, I plan to add more watch faces (and since this is open source, anyone can contribute and make their own customizations).


### 4.1 Components selections 

| S. No.  |         NAME        |                      DESCRIPTION                 |                     USE CASE                             |              REMARKS             |
| :------:|:-------------------:|:------------------------------------------------:| :-------------------------------------------------------:|:--------------------------------:|
|    1    |    MPU6050          | Inertial measurement unit                        | 3-axis accelerometer and 3-axis gyroscope                |                                  |   
|    2    |    ESP32-C3-MINI-1  | Wifi & Bluetooth 5 Module                        | Low power, high performance RISC-V SOC                   | ESP32-C3-WROOM-02 for prototyping| 
|    3    |    MAX30102         | Oximeter and heart rate sensor                   | Used to measure blood oxygen saturation and heart rate   |                                  |
|    4    |    TPS63030         | Buck-boost converter                             | Buck-boost converter for 3.3v power supply               | LDO for prototyping              |
|    5    |    BQ2407x          | BMS and charging IC                              | Battery managemnet system                                | TP4056 for prototyping           |
|    6    |    1.69" LCD        | 240x280 Resolution LCD screen                    | Rectangular 1.69" LCD disaply                            |                                  |


### 4.2 Schematic 

![schematic](https://github.com/syeedameen/glucose/hardware/schematic.png)







