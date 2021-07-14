# Mango Messenger Diploma Thesis

## Build
- Install MikTeX (https://miktex.org/download)
- Update MikTeX
- Install SumatraPDF viewer (https://www.sumatrapdfreader.org/download-free-pdf-viewer)
- Install Intellij IDEA Ultimate (https://www.jetbrains.com/idea/download/#section=windows)
- Activate Intellij IDEA Ultimate, you should have student license
- Install TeXiFy IDEA plugin (https://plugins.jetbrains.com/plugin/9473-texify-idea)
- Clone this repository locally: git clone https://github.com/kolosovpetro/BachelorsThesis.git
- Open diploma-document.iml in IDEA
- Configure Inverse Search in IDEA for SumatraPDF, Tool -> LaTeX -> Configure Inverse Search
- Compile it, Shift + F10

## Git flow
- Each task is assigned a number (MANGO-ID)
- Tasks are at Trello board https://trello.com/b/5kdQBsYE/bachelor-thesis-trello
- There are two main branches: master, develop
- Develop will be merged with master when diploma will be ready
- In order to contribute:
  - Clone this repo locally, or pull last changes fropm develop
  - Create new branch, based on develop, name it as task ID, e.g MANGO-ID
  - Solve the task
  - Create pull request to develop