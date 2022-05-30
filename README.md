# Mango Messenger Bachelor's Thesis


<p align="center">
  <img src="https://github.com/MangoInstantMessenger/MangoInstantMessenger.github.io/blob/MANGO-414/src/img/logo.png" width="100" height="100"  alt="Mango Messenger Logo"/>
</p>

[![Build PDF](https://github.com/MangoInstantMessenger/MangoMessengerBachelorThesis/actions/workflows/build.yml/badge.svg)](https://github.com/MangoInstantMessenger/MangoMessengerBachelorThesis/actions/workflows/build.yml/badge.svg)
[![Build and Deploy PDF](https://github.com/MangoInstantMessenger/MangoMessengerBachelorThesis/actions/workflows/build-and-deploy.yml/badge.svg)](https://github.com/MangoInstantMessenger/MangoMessengerBachelorThesis/actions/workflows/build-and-deploy.yml/badge.svg)
![contributors count](https://img.shields.io/github/contributors/MangoInstantMessenger/MangoMessengerBachelorThesis)

## What is all about

Mango Messenger is an opensource instant messaging system such that implemented using ASP NET 5 framework as REST API
backend along with Angular framework as frontend. In general, current project is considered to be a diploma project in
order to get bachelor's degree of computer science. However, now it is considered to be a just example of ASP .NET Core
API implementation using best practices in terms of architecture etc., where it is possible to apply different software
development approaches and to see how it works on different environments such as Azure, Heroku etc. Moreover, a few
cryptographical concepts are implemented such as DH key exchange that can be applied in order to implement secret chats
in feature. Current repository contains a LeTeX documentation for the diploma project entitled Mango Messenger and
available online as
<a href="https://mangoinstantmessenger.github.io/web/viewer.html?file=../main.pdf" target="_blank">PDF</a>.

## Table of contents

- Project Assumptions
    - Project description
    - Project objectives
- Project implementation
    - Project tasks
    - Project implementation
        - Theoretical assumptions
        - Description of facts
        - Empiric research
        - System requirements
        - Web service architecture
        - Authorization mechanism (JWT)
        - End-to-end encryption (DH key exchange + AES256)
    - Project outcomes
    - Usefulness of project
    - Project self-evaluation
- Bibliography

## Build and run

- Install MikTeX: https://miktex.org/download
- Update MikTeX
- Install SumatraPDF viewer: https://www.sumatrapdfreader.org/download-free-pdf-viewer
- Install Intellij IDEA Ultimate: https://www.jetbrains.com/idea/download/#section=windows
- Activate Intellij IDEA Ultimate
- Install TeXiFy IDEA plugin: https://plugins.jetbrains.com/plugin/9473-texify-idea
- Fork this repository
- Clone your fork repository locally: `git clone https://github.com/kolosovpetro/BachelorsThesis.git`
- Fetch your local fork and update it locally:
    - `git checkout develop`
    - `git pull`
- Open diploma-document.iml in IDEA
- Configure Inverse Search in IDEA for SumatraPDF: `Tools -> LaTeX -> Configure Inverse Search`
- Compile document using `Shift + F10`

## Useful links

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
- Figma: https://www.figma.com/file/cGtLvO1JuJgWmnzaSbM8Re/Mango-Thesis-Screens
- Trello: https://trello.com/b/5kdQBsYE/bachelor-thesis-trello

## Tasks management

The opened tasks and issues to be organized and handled as follows:

- Each task has an assigned number in the format `THESIS-ID`
- Active tasks are available on the Trello board: https://trello.com/b/Z7IlfrRb/mango-messenger-trello
- Each task branch is based on the actual `develop` branch and pull requested there on complete
- Branch `develop` then merged to `master` on particular milestone complete and document is being deployed to
  https://mangoinstantmessenger.github.io

## Git flow

Version control to be organized as follows:

- Fork this repository
- Clone this repository using `git clone https://github.com/${{ username }}/MangoMessengerBachelorThesis.git`
- If repository is cloned already then pull last changes from `develop` using
    - `git checkout develop`
    - `git pull`
- Create new branch based on `develop` with name according to `THESIS-ID` of the task
- Solve the task
- Create pull request to `develop`

## Logo Attribution

<div>Icons made by <a href="https://www.freepik.com" title="Freepik">Freepik</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a></div>
