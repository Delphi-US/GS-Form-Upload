GoogleScript
============

This repository is dedicated to the Open Source community for Google Scripts

This Google Script web app is designed as a web portal for new hires

The program takes general inputs such as name, email, etc along with multiple file uploads

It then validates that all fields are filled before activating the submit button and enabling the doPost method.

doPost appends all information to a spreadsheet, checks a drive folder to make sure the user's folder does not exisit, if it does it will create a new folder with their name on it and create all the files submitted in it.
