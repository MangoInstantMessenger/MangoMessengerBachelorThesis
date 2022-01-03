# Mango Messenger Bachelor's Thesis

[![Build PDF](https://github.com/kolosovpetro/MangoMessengerBachelorThesis/actions/workflows/build.yml/badge.svg)](https://github.com/MangoInstantMessenger/MangoMessengerBachelorThesis/actions/workflows/build.yml/badge.svg)
[![Build and Deploy PDF](https://github.com/kolosovpetro/MangoMessengerBachelorThesis/actions/workflows/build-and-deploy.yml/badge.svg)](https://github.com/kolosovpetro/MangoMessengerBachelorThesis/actions/workflows/build-and-deploy.yml/badge.svg)
![contributors count](https://img.shields.io/github/contributors/kolosovpetro/MangoMessengerBachelorThesis)

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

## Sources

- RSA algorithm video: https://youtu.be/vooHjWxmcIE
- RSA algorithm theory: https://www.di-mgt.com.au/rsa_alg.html
- Diffie-Hellman key exchange video: https://youtu.be/M-0qt6tdHzk
- Diffie-Hellman requirements: https://security.stackexchange.com/a/112318
- Elliptic Curves: https://youtu.be/NF1pwjL9-DE
- SHA256 Hash function video: https://youtu.be/f9EbD6iY9zI
- JWT: https://jwt.io
- JWT claims: https://datatracker.ietf.org/doc/html/rfc7519#section-4.1.3
- About JWT Auth: https://gist.github.com/zmts/802dc9c3510d79fd40f9dc38a12bccfc
- Base64 Encoding: https://youtu.be/aUdKd0IFl34

## Links

- Figma: https://www.figma.com/file/cGtLvO1JuJgWmnzaSbM8Re/Mango-Thesis-Screens
- Trello: https://trello.com/b/5kdQBsYE/bachelor-thesis-trello

## Git flow

- Each task is assigned a number (THESIS-ID)
- Tasks are at Trello board https://trello.com/b/5kdQBsYE/bachelor-thesis-trello
- There are two main branches: master, develop
- Develop will be merged with master when diploma will be ready
- In order to contribute:
    - Clone this repo locally, or pull last changes fropm develop
    - Create new branch, based on develop, name it as task ID, e.g MANGO-ID
    - Solve the task
    - Create pull request to develop
