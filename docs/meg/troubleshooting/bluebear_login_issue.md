# BlueBEAR Login Server Issue

### **<span style="color:maroon">Problem</span>**

A **RDS Project was set up** in May 2022, **BlueBEAR access/HPC was added** (to allow scp copying over of data from the MEG Acquisition Console), and the **MEG Operators** using the RDS space **have active BlueBEAR Linux accounts** and **are associated with the Project**. <br /><br />
Unfortunately, when one MEG Operator **attempted** a **```ssh```** BlueBEAR login from the Console to check their data had been copied correctly, the **following error was received** when **attempting to cd to the Project directory** in question...

**```-bash: cd: jenseno-lexical-previewing/: Not a directory```**

### **<span style="color:maroon">Solution</span>**

After Aslam from Advanced Research Computing kindly attended the MEG Lab, it was **found to be an issue** with one of the three **BlueBEAR login servers**, namely server **bblogin01**

If **MEG Operators were defaulted by BlueBEAR to bblogin01** after logging in, e.g. ...

**```[winterj@bb-pg-login01 ~]$```**

... then **cd'ing to a RDS directory might throw up the above error**.<br /> <br />BlueBEAR is now **looking into the issue, and hopefully will resolve it soon**.<br />
**For now**, to check that it's **not an issue with the Project** itself, **change to one of the other two BlueBEAR login servers** that are available...

**```[winterj@bb-pg-login01 ~]$ ssh bb-pg-login02```** or **...```-login03```**

... and **try accessing the RDS Project directory again**.

**<span style="color:red">Note:</span> <span style="color:blue"> Double-check that the MEG Operator has been added to the RDS Project correctly, as the above error will also occur if they haven't been added properly.</span>**
