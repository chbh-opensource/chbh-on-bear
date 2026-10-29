# IHR Status Codes

**Status Codes on IHR (seen in “Follow data log”)**

***<span style="color:maroon">“I had a look over TeamViewer, and the cryocooler status code is <span style="color:blue">0x8a0</span>, 
which means that there is a <span style="color:blue">cooling water flow issue which has caused the working gas temperature to rise</span>.<br />
...Oh, now the code changed back to <span style="color:blue">0x800, meaning normal idle status</span>. I'll try setting the system back to Normal mode…<br />Oh, it failed again due to the same reason :( Please call someone to check the water circulation, Jonathan”</span>***

**Antti Teliö - 29/08/2019 - *pumps were "0FF" on the day of the chiller service, when informed they wouldn't be (sigh!).***

<br />
![IHR Status Codes](../../images/meg/IHRStatusCodes.png)
**IHR Status Codes**

***“<span style="color:blue">These codes (<span style="color:red">underlined</span> in the image above) can be seen in the IHR “Follow data log”.<br />The codes are from the Manufacturer, Sumitomo, and indicate the status of the compressor/cold head</span>”.***


|    |  **Status Code**  |
|  -------------  |  -------  |
|  SUMITOMO_DIAG_LOW_PRESSURE_SHUTDOWN  |  0x001  |
|  UNCONNECTED  |  0x002  |
|  UNCONNECTED  |  0x004  |
|  UNCONNECTED  |  0x008  |
|  SUMITOMO_DIAG_POWER_ERROR  |  0x010  |
|  **<span style="color:blue">SUMITOMO_LOW_WATER_FLOW</span>**  |  **<span style="color:blue">0x020</span>**  |
|  SUMITOMO_DIAG_HIGH_WATER_TEMP  |  0x040  |
|  **<span style="color:blue">SUMITOMO_DIAG_GAS_TEMP_ERROR</span>**  |  **<span style="color:blue">0x080</span>**  |
|  SUMITOMO_DIAG_OIL_SHUTDOWN  |  0x100  |
|  SUMITOMO_DIAG_MOTOR_WINDING_TEMP  | 0x200  |
|  SUMITOMO_DIAG_RUN_STATUS  | 0x400  |
|  **<span style="color:blue">SUMITOMO_DIAG_SOLENOID_OPEN</span>**  |  **<span style="color:blue">0x800</span>**  |


***“By adding the hexadecimals <span style="color:blue">0x800 + 0x080+  0x020 = 0x8a0</span> which actually means that the water flow is low 
and causes the work gas lines to heat up => fail safe mode => restart compressor when water cooling is working again”.***

**Henri Hautaniemi - 03/09/2019**

<br />
!!! info "Another example ...<br /><span style="color:maroon">02/05/2023</span> - Status code <span style="color:blue">0x420</span> - was seen during a IHR fail-safe error received that evening (7:26pm). <br /> Based on the above codes, it would signify the cryocooler was in "*Run*" mode, but with "*Low Water Flow*", consequently generating the sent "*Error in cryocooler! Recycler is now in fail-safe mode*" SMS text and email."


