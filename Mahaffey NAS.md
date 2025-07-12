# Mahaffey NAS

## PrintTracker VM is running on the Synology NAS

- IP address is 192.168.1.115 (at least at the time of installation)
- Username is itadmin
- Password is one of my main defaults
- Need to check/verify by remoting into Dez’s computer and navigating to http://192.168.1.115:1301 in the browser
- 

## Business Use

1.  ~~MahaffeyNAS~~
2.  ~~Jeff as admin user w/ secure password~~
3.  ~~For updates:~~
    - ~~Leave at default “Automatically install important DSM and package updates only (Recommended)”~~
4.  ~~Sign into a~~ [~~Synology.com~~](http://Synology.com) ~~account - who at Mahaffey would like to receive alerts? Ty?~~
5.  ~~Skip/do not enter QuickConnect for now~~
6.  ~~Enable Active Insight and DSM configuration backup~~
7.  ~~Decline automatic installation of default apps~~
8.  ~~Dismiss extended warranty~~
9.  ~~No Thanks to 2FA for now~~
10. ~~Set static IP for NAS - used 192.168.1.11~~
11. ~~Create storage pool~~
    - ~~SHR (1 drive can fail) or SHR2 (2 drives can fail) allow for disparate drive sizes without sacrificing space until all drives are upgraded~~
    - ~~RAID 5 allows for 1 drive to fail, RAID 6 allows for 2 drives to fail~~
12. ~~Select Btrfs and not ext4~~
13. ~~Encrypt or no? Do not because who knows if the key will be accessible in 10 years~~
14. ~~Set up Data Scrubbing schedule via Storage Manager > Storage Pool > Schedule Data Scrubbing~~
    - ~~Enable data scrubbing schedule~~
    - ~~Repeat every 3 months~~
    - ~~Set time grid to scrub outside of normal working hours~~
    - ~~Set it to run later since there is no/minimal data on the storage pool~~
15. ~~Volume 1 > Settings > Never for frequency of record file access time~~
16. ~~Schedule a quick SMART test 1x a month~~
17. ~~Schedule an extended SMART test 1x every 6 months~~
18. ~~In Control Panel > Notifications > select to enable for Synology Account~~
19. ~~Set up email for Outlook using some Mahaffey account - which one?~~
20. ~~In Control Panel > Security~~
    - ~~Enable 2-Factor Auth for administrator users, maybe all users depending on what they want~~
    - ~~If don’t set up Email server in previous step, make sure Adaptive MFA is enabled~~
    - ~~Under the Protection tab, make sure Auto Block is enabled~~
        - ~~Defaults are fine for login attempts within minutes~~
        - ~~Set unblock after to 2 days~~
21. ~~In Hardware & Power, enable “Restart automatically when power supply issue is fixed”~~
    - ~~Also enable WOL for LAN1 and LAN2 so either work depending on which one is plugged into~~
22. ~~Go to Control Panel > Task Scheduler~~
    - ~~Create a task to empty the recycle bin~~
    - ~~Run every night~~
    - ~~All files, Retention policy of 7 days~~
23. ~~Go to Control Panel > User & Group~~
    - ~~Be sure admin and guest accounts are disabled~~
    - ~~Create appropriate group(s)~~
        - ~~Management and Employees?~~
24. ~~Create a Shared Folder - “Shared”~~
    - ~~Enable recycle bin for everyone (uncheck restrict to administrators only)~~
    - ~~Do not encrypt~~
    - ~~Enable checksum for advanced data integrity~~
    - ~~Grant permissions based on groups and add employees to groups later~~
25. ~~Create Management shared folder~~
    - ~~Same settings as above, but Employees will not have access and Management will~~
26. ~~Create user account for every person in the office and add them to the appropriate group(s)~~
    - ~~Make their password the same password as the login for their workstation so they aren’t prompted as often for credentials?~~
27. ~~Jennifer and Ty will be in management group - anyone else?~~
28. ~~In Package Center, search for Snapshot Replication app and install~~
29. ~~Open Snapshot Replication and go to Snapshots~~
30. ~~Add all shared folders (make sure to add any new root shares to this if any are created down the line)~~
31. ~~For the schedule settings:~~
    - ~~Enable snapshot schedule~~
    - ~~Daily~~
    - ~~8 AM to 8 PM (8:00 to 20:00)~~
    - ~~Every 1 hours~~
    - ~~Enable immutable snapshots for 14 days~~
32. ~~Retention settings:~~
    - ~~Uncheck/deselect “Keep the original retention policy of the selected targets”~~
    - ~~Enable retention policy~~
    - ~~Advanced retention policy > Set Rules~~
        - ~~Keep all snapshots for 14 days~~
        - ~~Deselect "Keep the latest snapshot of the hour for”~~
        - ~~Keep the latest snapshot of the day for 60 days~~
        - ~~Keep the latest snapshot of the week for 52 weeks~~
33. ~~Advanced tab:~~
    - ~~Make snapshot visible~~
34. Go to File Services > SMB settings
    - ~~Change log settings to enable every event except read to track access and actions~~
    - ~~Under the Advanced tab, enable File Fast Clone~~
        
        :::info
        To set up a shared folder that is not visible to everyone, select the checkbox to “Hide this shared folder in “My Network Places”
        :::
        

## Other things to do

1.  Type up instructions for mapping share on MacOS and Windows
    - MacOS:
        - Go
        - Connect to server
        - Enter smb://192.168.1.11 or whatever IP address it is
        - Click the + to add as favorite
        - Can also add/view from the Network view in Finder
    - Windows:
        - Map as drive letter Z or S
        - Map Network Drive
        - Select drive letter
        - Folder in \\\\MahaffeyNAS\\SharedFolder format
        - Re-connect at sign-in
2.  Do they want Google Drive-like functionality?
    - Super handy, but issues with file formats when opening on web
3.  Do they want to back their computers up (Documents folder) to the NAS automatically or do they primarily work directly off of the NAS?

## Back up the NAS to anything else?

Hyper backup

## Remote Access

Is this something they need/want? Can leave remote access disabled to have better security.

Check to see what ports, if any, have been opened on the router.

1.  QuickConnect
    - Proxy through Synology’s servers
    - Does expose NAS to internet
    - Have strong passwords, disable Admin account (done by default), have 2FA enabled
2.  Synology Drive
    - Good for accessing files from mobile apps and syncing computer/files
    - Limitations from editing .docx, xlsx, pptx, etc. files in Synology Drive web - they need to be converted to Synology Drive files which allows you to edit but then they are locked in that format unless you export as .docx, etc. again.
3.  Tailscale
    - Great, maybe even best option for remote access, but costs for business use
    - Does not require any port forwarding, could potentially be used as VPN solution for others
4.  WebDAV
    - not going to use this
5.  OpenVPN Server
    - May need to do this for remote admin situations, but will require opening port 1194 on Mahaffey router

Recommend Bitwarden

Need access to GoDaddy DNS to set up custom domain if interested

Can figure out phone stuff, but need “master” credentials that Tim probably uses to make most changes

Set up Active Backup for Business if they want it for PC backup

Do they want/would they use Synology Drive functionality?

## Business Setup

1.