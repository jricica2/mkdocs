# Synology

## First things to do:

1.  Schedule a task for recycle bin emptying
    - Run nightly and keep last 2 days’ worth of files (BTRFS snapshots are better for this functionality)
2.  Enable auto block in Security > Protection
3.  Disable password expiration under Users > Advanced
4.  Set up S.M.A.R.T. tests for the drives in Storage Manager > Task Scheduler
    - S.M.A.R.T.
    - Quick test
    - Test all supported drives
    - Schedule monthly on specific day and time
    - Also schedule a S.M.A.R.T. Extended test:
    - S.M.A.R.T.
    - Extended Test
    - Test all supported drives
    - Run every 6 months on specific day and time
5.  Schedule Data Scrubbing
    - Enable data scrubbing
    - Repeat every 3 months
    - Run during hours of non-use
6.  In Control Panel > File Services > SMB > Advanced Settings
    - Make sure SMB1 is **NOT** enabled
    - Make sure “Enable NTLMv1 authentication” is **NOT** enabled (may be used by Sonos)
7.  Disable AFP and use SMB instead
8.  Disable the admin account and create a different user account with admin access
9.  Control Panel > Hardware & Power > General
    - Under Power Recovery, enable “Restart automatically when power supply issue is fixed
    - Also enable WOL on LAN1 and LAN2 (never know which one will be connected)
10. Sign into a Synology Account and use Active Insight for email notifications
11. Identify the most important/irreplaceable data and set up a remote backup
12. Set up snapshot replication for BTRFS snapshots
    - Immutable snapshots are best for ransomware