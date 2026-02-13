# SLEEP Mode

The "**sleep**" issue is stil not resolved completely.<br />
**When the Acquision session is over, logout** of the ***meguser*** account, and, when the **login GUI appears** (*as per the image below*), then **power off the Console/DACQ monitor**.<br /> 
This **appears to help in avoiding** a **sleep mode state** and is the **most-consistent** "***fix***" so far.

<br />
![DACQ login GUI](../../images/meg/Console_login_prompt.jpg){width=40% align=left}

<br />

- **<span style="color:blue">Don't turn the monitor off while *meguser* logged on.</span>**
- **<span style="color:blue">Don't leave the monitor on, once *meguser* logged out.</span>**


<br /><br /><br/><br />
### **<span style="color:maroon">Problem</span>**

Whilst **logged into the console**, but **not running any applications e.g. *Acquisition***, the screen went into "**sleep mode**" (*blank screen, with movable (or stationary) cursor*).<br />
**Moving the mouse/pressing a key (*space, ESC, Enter*) did nothing**, the **screen remained blank**.

(**<span style="color:maroon">Soulution 1)</span>** ***was suggesed as fix by MEGIN initially. Try that first!***)


### **<span style="color:maroon">Solutions</span>**

1) Press **```Ctrl-Alt-Backspace```**

- This restarts the whole Desktop GUI session and will kill all open applications/logout the ***meguser*** account. The login GUI screen should then reappear.
	- Any collected data ***may*** be recoverable. Try the **procedure on page 44** of the **[Data Acquisition User Manual](../../meg/pdfs/NM23732A-B1-Dacq-6.0-UM_FINAL.pdf)** (***Section 6.4: "Rescuing data after a crash"***).

***<span style="color:green">NOT recommended ideally, but if necessary ...</span>***

2) Press the **DACQ Power button** *lightly!!!* **<span style="color:red">Pressing *too* hard will cause a reboot of the Console!!!</span>**

- A window shows 3 prompts...
	- ***Logout***
	- ***Turn Off Computer***
	- ***Restart Computer***
- Click "***Logout***
	- Returns to Login GUI screen.


!!! Note "```Ctrl-Alt-Backspace``` doesn't always work - DACQ screen remains blank.<br /> If so, then the DACQ/Console will need to be rebooted (may have also occured unintentionally if the Power button was pressed too hard.<br />```Ctrl-Alt-Delete``` should also cause a reboot, or perform Point 2) "Restart Computer" shown above."

**<span style="color:maroon">Procedure</span>**

- **Reboot the DACQ/Console**.
- **Wait** while the Centos OS loads, **allowing any disk checking** to take place.
- **Wait** until the system has **rebooted back to the login GUI screen/prompt**. 
- **Login**, and perform a **[RAP](../../meg/acquisition/rap.md)**
- To check the Sensor noise levels, and to make sure the correct tuning file is loaded after a Console reboot ...**[load the latest tuning file](../../meg/acquisition/restart_acquisition.md/#loading-a-tuning-file)**.

- If, on then **starting *Acquisition***, the **gantry position is not detected** ...

```
CHANGE: Gantry position: Detected: illegal value(0), Manual:Supine(0)
```

- Check the **gantry traffic light** in the **MSR** is showing **<span style="color:green">solid green</span>**, in the **desired position e.g. 60**. 
It might be showing **yellow** or **red**.<br /> If it isn't showing **green**, adjust the **up/down gantry buttons** until it does, 
then check to see if the **gantry position is now detected correctly** in **Acquisition** by **left-clicking** on the **Gantry position "Change" button**.<br /> If still not detected correctly, then ...

	- Perform a **[soft boot of the electronics](../../meg/acquisition/restart_acquisition.md/#resetting-the-electronics)**.
	- Then perform another **[RAP](../../meg/acquisition/rap.md)**


