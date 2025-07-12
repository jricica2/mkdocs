# GPU Passthrough for Plex/Jellyfin

Install Jellyfin or Plex as you normally would, but add the following variables to the containers:

### **Variable #1**

- Name: `NVIDIA_VISIBLE_DEVICES`
- Key: `NVIDIA_VISIBLE_DEVICES`
- Description: `NVIDIA_VISIBLE_DEVICES`
- Value: `GPU-68bf845a-9c10-54e8-b016-c5d9cabb77bf` (copied from the Nvidia Driver package/add-on)

### **Variable #2**

- Name: `NVIDIA_DRIVER_CAPABILITIES`
- Key: `NVIDIA_DRIVER_CAPABILITIES`
- Description: `NVIDIA_DRIVER_CAPABILITIES`
- Value: `all`
