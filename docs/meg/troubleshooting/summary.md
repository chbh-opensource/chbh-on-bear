# IHR Customer Training, Slide Summary

**A comprehensive guide covering system operation, configurations, scheduling, notifications, maintenance, helium management, and safety procedures for TRIUX neo IHR.**

!!! warning "<span style="font-size:medium">Not all suggested usage can now be performed remotely, due to TeamViewer no longer supporting the older version currently in use on the IHR. Only if accessing the IHR Console locally in the Tank Room (G24) will the procedures work as suggested.<br /> - See [Usual Problems, Probable Solutions] for how to now obtain remote access to the IHR.</span>"

#### <span style="color:maroon">System Overview and Operating Modes</span>

- **The system includes basic and advanced operating modes like normal, fail-safe, cool-down, maintenance, and shut down, each with specific functions.**
	- **Normal mode:** Restores normal operation after fail-safe or shutdown. The system re-enters its schedule automatically and adapts operation as well as possible. Use this mode to resume routine operation.
	- **Cool-down mode:** Provides extra liquefaction when needed. It can be interrupted by selecting Normal mode, and Normal mode resumes automatically once storage-tank pressure reaches **1.2 bar**. It may be needed after a prolonged power-off period or to liquefy gas after helium filling.
	- **Maintenance mode:** Used for maintenance activities, including gaseous-helium filling. The training states that it is intended only for MEGIN Customer Care.
	- **Shutdown mode:** Stops the IHR control software and stops control of the cryocooler compressor and pressure-regulator units. Select **Normal mode** to restart the system.
	- **Related states:** In **fail-safe**, MEG use may continue, but helium can be lost through the relief valve until the fault is resolved; switching back to Normal mode must be done manually. After a power cycle, the IHR normally returns to its previous mode, including shutdown; fail-safe instead returns to Maintenance mode.
- **Users can switch modes manually or allow automatic transitions** based on system conditions.
- **Power cycling** involves turning off and on, the control and compressor units to reset or restart the system.
- **Indicators** on the cabinet door show the current system status and operating mode.

#### <span style="color:maroon">Access Control and Control Terminal Use</span>

- **Control software** is accessed via the service GUI login with a password.
- **Remote access** is possible through IP address, telnet, or SSH from DACQ or any PC.
- **Mode settings** can be checked and changed via control terminal commands.
- **Temporary variable changes** are possible without reboot, but permanent changes require editing configuration files and restarting the system.

#### <span style="color:maroon">Configuration Management and Settings Adjustments</span>

- **Configuration files** store settings like default measurement windows and admin contact details.
- **Changes** can be applied by editing files and implementing them with system commands.
- **Default measurement windows** and admin addresses are adjustable for scheduling and notifications.
- **Messaging systems for alerts** include SMS and email interfaces with specific setup instructions.

#### <span style="color:maroon">Main Scheduling Choices</span>

The main scheduling choices are a **single daily MEG window**, a **split window with a pause**, and a **weekly cumulative strategy**; choosing the simplest schedule keeps the calendar attainable without pushing it into orange or red.

**<span style="font-size:large">Strategy comparison</span>**

**<span style="color:blue">Single daily default window</span>**

- **How it works:** One MEG-use period applies every day, including weekends.<br />
- **Strengths:** Simple and predictable; easiest to administer.<br />
- **Tradeoffs / risks:** Less flexibility for long operating days or varying demand.<br />

**<span style="color:blue">Split daily window</span>**

- **How it works:** Two MEG windows separated by a 1–3 hour pause, e.g., 8:00–13:00, 15:00–20:00.<br />
- **Strengths:** Creates a planned interval for liquefaction while supporting two measurement blocks.<br />
- **Tradeoffs / risks:** The gap must be at least 1 hour and may be insufficient if helium recovery demand is high.<br />

**<span style="color:blue">Calendar reservations / tailored windows</span>**

- **How it works:** Measurement windows are set in the calendar rather than relying only on the default.<br />
- **Strengths:** Best fit for known exceptions, changing demand, or unusually long sessions.<br />
- **Tradeoffs / risks:** Requires accurate, current reservations; missed or incorrect calendar information can cause poor compressor scheduling.<br />

**<span style="color:blue">Weekly cumulative cycle</span>**

- **How it works:** Helium capacity is managed across the week rather than being fully balanced each day.<br />
- **Strengths:** Allows heavier usage on some days when total weekly demand is manageable.<br />
- **Tradeoffs / risks:** Extra MEG use early in the week mainly limits Friday capacity. Calendar colors may not show green across the weekly cycle: Tuesday–Thursday may appear yellow and Thursday–Friday orange.<br />

!!! info "CHBH MEG allows usage until 7pm, Monday -> Wednesday. Until 5pm, Thursday -> Saturday. NO USAGE ON SUNDAYS!"

**<span style="color:blue">Weekend dummy windows</span>**

- **How it works:** Schedule 09:00–10:00 measurement windows on weekends when using a cumulative weekly cycle.<br />
- **Strengths:** Helps avoid overfilling the tanks and possible helium loss.<br />
- **Tradeoffs / risks:** Uses calendar time even when no actual measurements are planned.<br />

!!! info "CHBH MEG implements this procedure only on Sundays."

**<span style="font-size:large">Operating implications</span>**

- **Protect liquefaction time:** Keep the gantry in the liquefaction position when possible. This maximizes liquefaction and minimizes boil-off because the cryocooler is vertical.
- **Avoid short compressor cycles:** Mode changes are allowed at any time, but engaging the cryocooler for less than 0.5 hours is not recommended.
- **Use schedule status as the constraint:** If the scheduler shows orange or red, the planned MEG use is not comfortably attainable; shorten or reschedule use rather than relying on recovery later in the week.
- **Use Cool-down only for recovery demand:** For extra liquefaction, Cool-down mode can be used, or the next MEG window can be scheduled very early. Cool-down ends automatically when tank pressure reaches 1.2 bar.

**A stable daily window is best for routine operation; split or calendar-specific windows suit predictable breaks and exceptions; weekly cumulative scheduling offers flexibility but needs close monitoring to prevent late-week capacity limits or tank overfill.**
 

#### <span style="color:maroon">Advanced Scheduling and Data Visualization</span>

- **Weekly measurement schedules** use calendar data; extra HE liquefaction windows can be scheduled.
- **Gantry position** affects liquefaction efficiency, with optimal vertical position (**25**).
- **History plots** display metrics such as pressure, temperatures, and gantry positions, covering last days.
- **Plotting tools** can generate detailed graphical data over various periods and metrics.

#### <span style="color:maroon">Notifications, Alerts, and Troubleshooting</span>

- The **system provides alerts** for normal, fail-safe, power outages, and cryocooler errors.
- **Notifications** often **require manual intervention or system switches** to restore normal operation.
- **Error logs can be checked** via command-line tools to diagnose issues.
- **Effective response** includes checking gantry positions, system status, and DACQ connections.

#### <span style="color:maroon">Recovery and Maintenance Procedures</span>

- **Water circulation failures** are addressed by checking water flow, cycling compressors, and restoring system modes.
- **Helium levels are monitored**, with guidelines for adding gaseous helium safely and maintaining minimum levels.
- **System warm-up, helium loss, and dewar relief valve issues are important maintenance points**.
- **Regular checks** of helium levels and schedule adjustments help prevent system failures during extended use.

#### <span style="color:maroon">Helium Management and Safety Precautions</span>

- **Gaseous helium should be handled in well-ventilated areas with proper procedures to prevent injury and environmental hazards**.
- **Filling tanks involves connecting regulators, verifying pressures, and liquefying gas in tanks**.
- **Safety warnings emphasize proper handling, connection checks, and avoiding improper disassembly**.
- **Additional manuals** provide further safety instructions and technical details.

#### <span style="color:maroon">Holiday and Emergency Procedures</span>

- **Alerts can be redirected to on-duty personnel**, and system schedules should be adjusted for overnight or weekend operation.
- **Regular inspection** of schedules and helium levels ensures continued operation.
- **Error logs and history plots** assist in troubleshooting during emergencies.
- **On-duty personnel** should manually restore system modes and monitor dewar liquid helium levels during outages.

#### <span style="color:maroon">Summary of Core Parameters & Commands</span>

!!! note "Not all commands available remotely, due to TeamViewer unavailability. Those commands need perfoming locally at IHR in Tank Room (G24)"

|  Parameter / Metric  |  Value / Command Syntax  |  Purpose  |
| -------------  |  -------  |  ------  |
| **Default Password**  |  [Information]  |  Authenticates access to the Control Terminal.  |
| **Cool-down Cutoff** |  **1.2 bar**  |  Pressure threshold where Cool-down mode reverts to Normal.  |
| **UPS Battery Buffer**  |  **5-25 minutes**  |  Handles brief brownouts before complete power loss.  |
| **Optimal Gantry State**  |  Vertical, 25 (Liquefaction position) |  Maximises liquefaction and mininises helium boil-off.  |
| **Weekend Helium Minimum**  |  **50% level** in the Dewar |  Minimum level required to survive an IHR failure over a weekend.  |
| **Daily Helium Minimum** |  **13 Litres** of lHe (Liquefaction position)  |  Minimum volume required to survive a 1-day system failure.  |
| **Log Error Command** |  ```cd /neuro/cryo/bin``` followed by ```./errors```  |  Displays a list of application log errors.  |
| **History Plot Command** |  ```./plot <period> --wins```  |  Overlays measurement windows on top of pressure data.  |
| **Leak Detection Plot** |  ```./plot <period> --heliumvolume```  |  Plots total system helium volume over time.  |
