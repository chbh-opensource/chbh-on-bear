# IHR Status Codes

'''Status Codes on IHR (seen in “Follow data log”)'''

'''<span style="color:red">“I had a look over TeamViewer, and the cryocooler status code is <span style="color:blue">* 0x8a0</span>, which means that there is a cooling water flow issue which has caused the working gas temperature to rise.<br />...Oh, now the code changed back to 0x800, meaning normal idle status. I'll try setting the system back to normal mode…<br />Oh, it failed again due to the same reason :( Please call someone to check the water circulation, Jonathan”</span>'''

'''(From Antti - 29th August 2019) - pumps ‘off’ on day of chiller service, when told they wouldn't be).'''

<gallery widths=640x heights=110px>
Image:IHRStatusCodes.png|IHR Status Codes
</gallery>

''“These codes can be seen in the '''IHR “Follow data log” (underlined above)'''. The codes are from Sumitomo and indicate the status of the compressor/cold head”.''

{| class="wikitable"
|+Status Codes:
|-
| SUMITOMO_DIAG_LOW_PRESSURE_SHUTDOWN
| 0x001
|-
| UNCONNECTED
| 0x002
|-
| UNCONNECTED 
| 0x004
|-
| UNCONNECTED
| 0x008
|-
| SUMITOMO_DIAG_POWER_ERROR
| 0x010
|-
|'''<span style="color:blue">SUMITOMO_LOW_WATER_FLOW</span>'''
|'''<span style="color:blue">0x020</span>'''
|-
| SUMITOMO_DIAG_HIGH_WATER_TEMP
| 0x040
|-
|'''<span style="color:blue">SUMITOMO_DIAG_GAS_TEMP_ERROR</span>'''
|'''<span style="color:blue">0x080</span>'''
|-
| SUMITOMO_DIAG_OIL_SHUTDOWN
| 0x100
|-
| SUMITOMO_DIAG_MOTOR_WINDING_TEMP
| 0x200
|-
| SUMITOMO_DIAG_RUN_STATUS
| 0x400
|-
|'''<span style="color:blue">SUMITOMO_DIAG_SOLENOID_OPEN</span>'''
|'''<span style="color:blue">0x800</span>'''
|}

'''''<span style="color:blue">*</span>''' “By adding the hexadecimals '''<span style="color:blue">0x800 + 0x080+  0x020 = 0x8a0</span>''' which actually means that the water flow is low and causes the work gas lines to heat up > fail safe mode > restart compressor when water cooling is working again”.''

'''(Reply from Henri - 3rd September 2019 to my query over IHR code descriptions).'''


'''<span style="color:red">02/05/2023</span>''' - Status code '''0x420''' - was seen during a IHR fail-safe error that evening (7:26pm). <br /> Based on the above codes, it would signify the cryocooler was in '''"Run"''' mode, but with '''"Low Water Flow"''', generating the sent '''"Error in cryocooler!"''' message.


