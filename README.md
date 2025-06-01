# flipperzero-geigercounter
☢☢ A geiger counter application for the Flipper Zero ☢☢

![banner](https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/logo.jpg)
(banner has been made with **Midjourney**)


You need a **geiger counter** board to run this application, this board can be used: https://fr.aliexpress.com/item/1005005983829775.html (**NOT** sponsored)

Similar boards on AliExpress may also work

You also need jumper wires to connect the board on the **Flipper Zero**.

**Note 1:** This board uses a **J305** geiger tube. According this [website](https://www.rhelectronics.store/j305-glassy-geiger-muller-tube-nuclear-radiation-sensor) gamma conversion factor is **0.0081** for this tube. This value has been declared in the header of the source file so you can change it easily if needed. Incorrect conversion factor will give false measurements when **Sv** or **Rad** is selected.

**Note 2:** **J305** geiger tube is only sensible to **beta** and **gamma** rays. **Alpha** rays cannot be detected. 

**Usable** radioactive sources: 
- natural uranium (alpha, beta, gamma)
- natural thorium (alpha, beta, gamma)
- radium-226 (alpha, beta, gamma)
- cobalt-60 (beta & gamma)
- iodine-131 (beta & gamma)

**Not really usable** radioactive sources (must be in contact with the geiger tube to be detected): 
- americium-241 (alpha & low gamma, some strong beta/gamma rays are emitted during radioactive cascade or due to the presence of radioisotope impurities)
- high purity metallic uranium/thorium (same as am241)


**Totaly unusable** radioactive sources: 
- polonium-210 (pure alpha)
- tritium (very low beta)


The **+5V** power pin on the Flipper Zero can be used to power the Geiger counter board: This pin will be automatically turned on when the program is initiated.

The output pin for measurement on the Arduino is not suitable for use with the **Flipper Zero** due to low output voltage. Use the jack out port instead. Cut an audio jack cable and connect the audio channel (left, right, or both) to a cut half male jumper wire, then connect it to the **A7** GPIO.

<p align="center"><img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/jack.png" width=40% height=40%></p>

The black wire is typically used for ground (sleeve on the schematic). Verify this with a multimeter or by testing the other wires.

Global schema:

<p align="center"><img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/schema.jpg" width=100% height=100%></p>

**Note:** Polarity of the geiger tube may be different on your board


UI of the application:

<p align="center"><img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/flipper3.png" width=33% height=33%></p>

**CPS**: **c**ounts **p**er **s**econd (instantaneous measure of the radioactivity). CPS is alway displayed on the left corner.

**CPM**: **c**ounts **p**er **m**inute (the sum of CPS over a period of one minute). Other units of measurement can be chosen with **Left/Right**.

New CPS bar measure appears on the left every second.

## Build the program

Assuming the toolchain is already installed, copy **flipper_geiger** directory to **applications_user**

Plug your **Flipper Zero** and build the geiger counter:
```
./fbt launch_app APPSRC=applications_user/flipper_geiger
```

The program will automatically be launched after compilation

<img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/flipper1.png" width=25% height=25%>

**A4** GPIO can be connected on **A7** GPIO to test this application without using a geiger tube. **A4** GPIO generates a signal with a frequency that varies every second.

**Button assignments**: 

button  | function
------------- | -------------
**Ok** *[long press]*  | Clear the graph
**Left/Right** *[short press]* | Choose unit on the right corner (cpm, μSv/h, mSv/y, Rad/h, mRad/h, uRad/h), **cps** on the left is always displayed
**Up** *[long press]*  | Enable/disable recording, led of **Flipper Zero** is colored in red when recording
**Up/Down** *[short press]*  | Zoom/unzoom 
**Down** *[long press]*  | Display version of the application
**Back** *[long press]*  | Exit

If you don't want to build this application, just simply copy **flipper_geiger.fap** on your **Flipper Zero** 

Build has been made with official toolchain (0.102.3), **API Mismatch** error may appear if you are using custom firmware. You can bypass this error but the program may crash.

## Use cases

Ambient radioactivity (descendants of radon gas are detected, not radon itself):

<img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/flipper2.png" width=25% height=25%> <img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/flipper8.png" width=25% height=25%> <img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/flipper9.png" width=25% height=25%>

Measurement of a sample of uranium ore within a lead container:

<img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/flipper3.png" width=25% height=25%> <img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/flipper12.png" width=25% height=25%> <img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/flipper13.png" width=25% height=25%> <img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/flipper14.png" width=25% height=25%>

**Note:** measures in **Sv** or **Rad** are not precise

Measurement of a sample of uranium ore (the most radioactive part):

<img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/flipper4.png" width=25% height=25%>

Measurement of radium dial pointers:

<img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/flipper5.png" width=25% height=25%>

All prior measurements in sequence (the scale of the graph is automatically adjusted):

<img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/flipper6.png" width=25% height=25%>

Measurement of uranium orange pottery:

<img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/flipper10.png" width=25% height=25%>

Measurement of americium-241 button from a smoke detector (descendants of americium or radioisotope impurities are detected, not americium itself):

<img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/flipper11.png" width=25% height=25%>

**A4** GPIO on **A7** GPIO (to test this program without a geiger board):

<img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/flipper7.png" width=25% height=25%>

Zoom levels (the third picture is the default zoom):

<img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/zoom0.png" width=25% height=25%> <img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/zoom1.png" width=25% height=25%> <img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/zoom2.png" width=25% height=25%> <img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/zoom3.png" width=25% height=25%>

Version of the application (press down button during 1 sec to display version):

<img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/version.png" width=25% height=25%>

## Recording function

Output **CSV** files are stored in the root directory of the SD card. Date and time are incorporated into the file name (example: **geiger-2023-07-03--23-48-15.csv**)

Data sample:

epoch  | cps
------------- | -------------
0  | 10
1  | 14
2  | 8
3  | 11
4  | 9

## Atomic Dice Roller

<p align="center"><img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/dice.jpg" width=25% height=25%></p>

I maintain another application that uses the **geiger board** to roll dice by using radioactivity: https://github.com/nmrr/flipperzero-atomicdiceroller

## Gallery/video of the community

[BRD8 [Reddit]](https://www.reddit.com/user/BRD8/) - https://www.reddit.com/r/flipperzero/comments/110062z/am_i_a_hacker_now_mom/: 

<img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/user/abQXuEz.jpg" width=50% height=50%>

[Funbob235 [Reddit]](https://www.reddit.com/user/Funbob235/) - https://www.reddit.com/r/flipperzero/comments/13m1qly/testing_of_the_geiger_counter/: 

<img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/user/testing-of-the-geiger-counter-v0-3zv9gdq4nt0b1.jpg" width=50% height=50%>

[Axewarior [Reddit]](https://www.reddit.com/user/axewarior/) - https://www.reddit.com/r/flipperzero/comments/14krjs2/gieger_counter/

<img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/user/IMG-1552.jpg" width=50% height=50%>

[hackster.io] - https://www.hackster.io/news/erwin-ried-s-flippenheimer-gives-the-flipper-zero-pocket-multi-tool-radiation-monitoring-powers-a6fd3460f858

<img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/user/image_36GFUa60bI.jpg" width=50% height=50%>

[Ratrick_E_Pumbol [Reddit]](https://www.reddit.com/user/Ratrick_E_Pumbol/) - https://www.reddit.com/r/flipperzero/comments/17ok9sj/i_got_the_geiger_counter_to_work/

<img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/user/wy8b1vhu4lyb1.jpg" width=50% height=50%>

[Thick_Swordfish6666 [Reddit]](https://www.reddit.com/user/Thick_Swordfish6666/) - https://www.reddit.com/r/flipperhacks/comments/1jfqhkm/flipper_zero_geiger_counter_why_not/

<img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/user/ckjx6uyvwupe1.jpeg" width=50% height=50%>

[thits666 [Reddit]](https://www.reddit.com/user/thits666/) - https://www.reddit.com/r/flipperhacks/comments/1jfqhkm/flipper_zero_geiger_counter_why_not/

<img src="https://github.com/nmrr/flipperzero-geigercounter/blob/main/img/user/flipper-zero-geiger-counter-why-not-v0-8tiv6hg1kxpe1.jpg" width=50% height=50%>

[Seanclark2409 [YouTube]](https://www.youtube.com/@seanclark2409) (click on the picture to see the video): 

[![Watch the video](https://img.youtube.com/vi/JQB2jvY1oZ0/maxresdefault.jpg)](https://youtu.be/JQB2jvY1oZ0)

[Boboso5676 [YouTube]](https://www.youtube.com/@boboso5676) (click on the picture to see the video):

[![Watch the video](https://img.youtube.com/vi/jYQlC2NJScQ/maxresdefault.jpg)](https://youtu.be/jYQlC2NJScQ)

[Talking Sasquach [YouTube]](https://www.youtube.com/@TalkingSasquach) (click on the picture to see the video):

[![Watch the video](https://img.youtube.com/vi/-I57_S_AXYY/maxresdefault.jpg)](https://youtu.be/-I57_S_AXYY)

[Erwin Ried [YouTube]](https://www.youtube.com/@eried) (click on the picture to see the video):

[![Watch the video](https://img.youtube.com/vi/lVqxNnsxskg/maxresdefault.jpg)](https://www.youtube.com/watch?v=lVqxNnsxskg)

## What's next ?

Here are some nice ideas to improve this app:

* ~~Save output data in XML / JSON file~~ **DONE !** Output data are stored in CSV (lighter than XML / JSON and easier to parse)
* ~~Use the geiger board as random number generator~~ **DONE !** A separate project uses the same geiger board to roll dice: https://github.com/nmrr/flipperzero-atomicdiceroller
* Send data on the air in real time to monitor remotly
* Buzz when it gets dangerous like a dosimeter

## Changelog

* 2024-06-24
  * Bug fix

* 2024-03-11
  * Bug fix

* 2024-02-22
  * Bug fix

* 2024-01-15
  * Global schema has been updated
  * Gallery has beed upadated
  * Rebuild of the app with the last toolchain

* 2023-08-06
  * Code optimization (shift operation on CPS array has been removed)
  * Version section has been added

* 2023-07-03
  * Data recording function has been added

* 2023-06-25
  * Add zoom capability
  * User gallery has been added

* 2023-06-08
  * Bug fix

* 2023-04-11
  * More usable/unusable sources
  * Rad unit has been added
  * Code refactoring by replacing old mutex call by new method

* 2023-03-01
  * Usable/unusable sources have been added

* 2023-02-26
  * More clarity about how to connect audio jack cable on A7 GPIO

* 2023-02-02
  * μSv/h and mSv/y have been added
  * 5V pin is now automatically enabled when the program is launched

* 2023-01-15
  * Code fix & optimizations
  * More events can be handled without any issue

* 2023-01-09
  * Code fix
  * Global schema has been added

* 2023-01-08
  * Initial release
