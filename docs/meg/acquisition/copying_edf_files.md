# Copying EyeLink EDF files

**<span style="color:red">Ideally leave for MEG Support to do , but ...</span>**

If there is a need to copy off EyeLink EDF files from **/elcl/exe** - **<span style="color:blue"> e.g. because the EyeLink partition is almost full (TRACK may/will not start if the partition is full!)</span>**

- Make sure the **Stim PC** is **On** and **Logged in**.
- Turn **On** the EyeLink PC, and **exit to FileManager**.
- On the STIM PC, **open the Bing incognito browser** shortcut from the **Taskbar**.
- Then either...
	- Click on the **"EyeLink Host PC FileManager" shortcut**, in the **Bookmarks toolbar**. Or...
	- In the **Address Bar**, type "**100.1.1.1**" (*without the quotes*). A connection should now be made to the **SR Research EyeLink FileManager**, and the following page **should be displayed in the Stim PC Browser window...**

!!! Info "**<span style="color:maroon"> The link is not a secure link, so make sure the address is headed by "http://" and not "https://"</span>**"

![Browser Linked to EyeLink Host PC](../../images/meg/Browser_linked_to_EyeLink_Host.png)
**Stim PC linked to EyeLink Host PC FileManager.**

- Click on the "**+**" button, by the "**/elcl**" folder icon to **open up the sub-folders**.
- Click on the "**exe**" folder icon to **show the folder contents in the right-hand window**.
- Click on the "**Change view**" icon and select "**Details**" from the dropdown menu.
- Click on "**Type**" to **list all the EDF files together**.
- Select **relevant EDF files** (using *shift-leftclick* or *ctrl-leftclick*) in the right-hand window, and **right-click the selected files to view the options**. 
- Select "**Download (*no. selected*) items**".
- Select "**OK**" to download the files **as a compressed file** to the **Stim PC *Downloads*** folder.
	- Filename: "**exe (*no. of items*).zip**"
- Once **transfer is complete**, check the ***Downloads*** folder to **confirm ZIP file is there and can be opened**.
- **Copy the zip file** to **RDS partition**, or **University OneDrive** (depending on what **share has been mapped** on the Stim PC).
- **Return** to the **open browser window**, right-clicking to now, ***<span style="color:red">carefully</span>***, select "**Delete (*no. selected*) items**", to **make space** on the EyeLink partition **enabling the recording of EDF files again**.

