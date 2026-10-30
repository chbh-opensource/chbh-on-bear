# IHR Status Codes

**Status Codes on IHR (seen in “Follow data log”, column 6)**

***<span style="color:maroon">“I had a look over TeamViewer, and the cryocooler status code is <span style="color:blue">0x8a0</span>, 
which means that there is a <span style="color:blue">cooling water flow issue which has caused the working gas temperature to rise</span>.<br />
...Oh, now the code changed back to <span style="color:blue">0x800, meaning normal idle status</span>. I'll try setting the system back to Normal mode…<br />Oh, it failed again due to the same reason :( Please call someone to check the water circulation, Jonathan”</span>***

**Antti Teliö - 29/08/2019 - *pumps were "0FF" on the day of the chiller service, when informed they wouldn't be (sigh!).***

<br />
![IHR Status Codes](../../images/meg/IHRStatusCodes.png)
**IHR Status Codes**

***“<span style="color:blue">These codes (<span style="color:red">underlined</span> in the image above) can be seen in the IHR “Follow data log”, column 6.<br />
The codes are from the Manufacturer, Sumitomo, and indicate the status of the compressor/cold head.
By adding the hexadecimals <span style="color:red">0x800 + 0x080+  0x020 = 0x8a0</span> which actually means that the water flow is low 
and causes the work gas lines to heat up => fail safe mode => restart compressor when water cooling is working again</span>”.***

**Henri Hautaniemi - 03/09/2019**

<br />
**From the NM25887A-B_TRIUX_neo_Corrective_Maintenance_Manual ...**

"***<span style="color:maroon">The cryocooler compressor reports errors in hexadecimal format and these values appear both in the cryodata
log file (column 6), and in error notifcations. The reported error condition is a sum of the bits below. This means
multiple bits may be present at a time.</span>***"

!!! info "<span style="font-size:medium"><span style="color:green">Normal - no errors - code is 0x800</span>. In water flow/temperature problem cases the error codes are typically: 0x820, 0x840 or 0x420.<br />Status and error bits are summed up to form the error codes. For example <span style="color:red">0x8a0</span> means <span style="color:red">0x800</span> (*cooler on*) + <span style="color:red">0x020</span> (*water not flowing*) + <span style="color:red">0x080</span> (*working gas overtemperature*).</span>"

|  **<span style="font-size:medium">Cryocooler compressor diagnostic interface codes</span>**  |    |
|  -------------  |  -------  |
|  SUMITOMO_DIAG_LOW_PRESSURE_SHUTDOWN  |  0x001  |
|  UNCONNECTED  |  0x002  |
|  UNCONNECTED  |  0x004  |
|  UNCONNECTED  |  0x008  |
|  SUMITOMO_DIAG_POWER_ERROR  |  0x010  |
|  **<span style="color:red">SUMITOMO_LOW_WATER_FLOW</span>**  |  **<span style="color:red">0x020</span>**  |
|  SUMITOMO_DIAG_HIGH_WATER_TEMP  |  0x040  |
|  **<span style="color:red">SUMITOMO_DIAG_GAS_TEMP_ERROR</span>**  |  **<span style="color:red">0x080</span>**  |
|  SUMITOMO_DIAG_OIL_SHUTDOWN  |  0x100  |
|  SUMITOMO_DIAG_MOTOR_WINDING_TEMP  | 0x200  |
|  **The following two bits are not actual errors but are also summed to the reported value. The SUMITOMO_DIAG_RUN_STATUS bit being set indicates that the cryocooler compressor is running, and SUMITOMO_DIAG_SOLENOID_OPEN is the negation of SUMITOMO_DIAG_RUN_STATUS always. Hence, one of these bits should always be present, unless the cryocooler compressor is powered off, or the cable is disconnected**  |
|  SUMITOMO_DIAG_RUN_STATUS  | 0x400  |
|  **<span style="color:red">SUMITOMO_DIAG_SOLENOID_OPEN</span>**  |  **<span style="color:red">0x800</span>**  |

!!! info "<span style="font-size:medium"><span style="color:maroon">02/05/2023</span> - Status code <span style="color:red">0x420</span> - was seen during a IHR fail-safe error received that evening (7:26pm). <br /> Based on the above codes, it would signify the cryocooler was in "*Run*" mode, but with "*Low Water Flow*", consequently generating the sent "*Error in cryocooler! Recycler is now in fail-safe mode*" SMS text and email.</span>"


