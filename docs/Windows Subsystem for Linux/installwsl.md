# Installing WSL2 on Windows

<a href="https://learn.microsoft.com/en-us/windows/wsl/install" target="_blank">https://learn.microsoft.com/en-us/windows/wsl/install</a>

```powershell
wsl --install
```

!!! note
    The above command only works if WSL is not installed at all. If you run `wsl --install` and see the WSL help text, please try running `wsl --list --online` to see a list of available distros and run `wsl --install -d <DistroName>` to install a distro.
