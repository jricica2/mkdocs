# Mkdocs Initial Setup

- Official site: <a href="https://squidfunk.github.io/mkdocs-material/" target="_blank">https://squidfunk.github.io/mkdocs-material/</a>
- Developer's GitHub: <a href="https://github.com/squidfunk/mkdocs-material" target="_blank">https://github.com/squidfunk/mkdocs-material</a>

## Setup Instructions

### Pre-Requisites
1. Download and install GitHub Desktop
2. Download and install Python for Windows
3. Download and install VS Code (if you don't already have it)
4. Set up a virtual environment for Python
```powershell
python -m venv venv
```
### Install Mkdocs

5. Install mkdocs-material
```powershell
pip install mkdocs-material
```

6. Run the script to activate the virtual environment. This script will need to be run every time you edit/make changes to the website.
```powershell
venv\Scripts\Activate.ps1
```

7. If you encounter an error about running scripts being disabled, you can run the following command and then run the Activate.ps1 script again
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
```

8. Open the website in VS Code by typing the following command:
```powershell
code .
```

### Scaffold New Site
9. Open a new terminal if one is not already open and run the following commands:
```powershell
mkdocs new .
```
```powershell
mkdocs serve
```

10. Add the material theme to the mkdocs.yml file
```yml
theme:
	name: material
```

11. Add the following to the mkdocs.yml file to add the light mode/dark mode toggle:
```yml
  palette: 
    # Palette toggle for light mode
    - scheme: default
      primary: green
      accent: purple
      toggle:
        icon: material/brightness-7 
        name: Switch to dark mode
     
    # Palette toggle for dark mode
    - scheme: slate
      primary: indigo
      accent: yellow
      toggle:
        icon: material/brightness-4
        name: Switch to light mode
```

12. Add the following to the mkdocs.yml file to add necessary features and plugins:
```yaml
theme:
  name: material
  font:
    text: Roboto

  features:
    - content.code.annotate
    - content.code.copy
    - content.tabs.link
    - header.autohide
    - announce.dismiss
    - navigation.footer
  #  - navigation.expand
    - navigation.indexes
    - navigation.instant
    - navigation.instant.progress
    - navigation.path
    - navigation.sections
  #  - navigation.tabs
    - navigation.top
    - navigation.tracking
    - search.highlight
    - search.share
    - search.suggest
  #  - toc.integrate

  plugins:
    - typeset
    - search
    - blog

  palette:

    # Palette toggle for light mode
    - scheme: default
      primary: red
      accent: red
      toggle:
        icon: material/brightness-7 
        name: Switch to dark mode

    # Palette toggle for dark mode
    - scheme: slate
      primary: red
      accent: red
      toggle:
        icon: material/brightness-4
        name: Switch to light mode

markdown_extensions:
  - admonition
  - pymdownx.details
  - pymdownx.superfences
```
