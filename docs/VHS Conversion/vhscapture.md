# VHS Capture to Digital Media

## <a href="https://www.youtube.com/watch?v=tk-n7IlrXI4" target="_blank">YouTube video used for reference</a>


## Pre-requisite work
1. Connect your USB capture device and install the appropriate drivers.
2. Install OBS
3. Docks > select to show Stats
4. Create the following so that we can save our default settings
    - Profile > New > Name the scene VHS Capture (un-check the box to show the wizard)
    - Scene Collection > New > Name the collection VHS
5. Open the Settings window and select the Video section.
    - Change the Base (Canvas) Resolution to 1440x1080 which is a 4x3 aspect ratio
    - Change the Output (Scaled) Resolution to 1440x1080 which is a 4x3 aspect ratio
    - Set the "Common FPS Values" dropdown to 59.94
    - Click Apply and then OK to close the Settings window
6. Click the + symbol in the Sources dock to add a video source.
7. Select the Dazzle DVC100 Video device from the dropdown.
    - You can click "Configure Video" to change display settings, but the defaults produce a good image quality.
8. If audio is working by default as part of the video capture device settings, great!
9. If audio is not working, you will need to identify another way to capture the audio.
    - I chose to use an RCA (female) to 3.5mm headphone jack adapter plugged into the 3.5mm jack on my computer.

## Recording Settings
1. Open the Settings window again and select the Output section.
2. Set the output directory to record to.
    - This is typically C:\Users\username\Videos
3. Set the Recording Quality to "High Quality, Medium File Size"
4. Set the Recording Format to MP4 as it is the most compatible option
5. Select the appropriate option for Encoder based on the hardware being utilized for the capture. Prefer hardware if available.
    - Software (x264) - for newer CPUs and no hardware encoding option available
    - Software (x264 low CPU usage preset, increases file size) - for older CPUs that can't handle the capture without this setting
    - Hardware (QSV, H.264) - This is for Intel QuickSync graphics, whether integrated or dedicated GPU
    - Hardware (NVENC) - This is for Nvidia graphics cards
    - Hardware (AMD) - This is for AMD graphics cards
6. Click OK to close the Settings window.
7. Do a test recording to validate settings.
8. After stopping the recording, open the resulting file to play it and verify that everything is working properly.

## Other Configurations
1. Right-click on the Video Capture Device and go to Deinterlacing and select Yadif 2x (or one of the other 2x options if Yadif isn't available or doesn't work properly).
2. Right-click on the Video Capture Device and go to Transform > Stretch to screen to fill the canvas.
3. Right-click on the Video Capture Device and go to Scale Filtering and select Lanczos.
4. Profit.
