# Adding OMV-Extras to OMV

<a href="https://wiki.omv-extras.org/doku.php?id=misc_docs:omv_extras" target="_blank">OMV Extras Website</a>

1. Run the following script in the terminal of the OMV machine:
```bash
wget -O - https://github.com/OpenMediaVault-Plugin-Developers/packages/raw/master/install | bash
```

2. Enable the openmediavault-flashmemory plugin once omv-extras is installed

!!! note
    I had to run the command `su -` and authenticate with my root password before the above command to run it as root.
