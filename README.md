# Script Runner
This package contains utilities within xMatters. All items below require an xMatters Agent. All items below are to be used in conjunction with the Schedule Message feature in xMatters as they are all batch processes.

# Overview
Below are the following functions of the package.

## Role - Scheduler
This initiates the process documented here: https://github.com/matthewhenry1/role-sync-py

## Locations Field - Scheduler
This process will query the Sites and populate List properties in xMatters with the address details for the Sites. This is helpful for manual message sending purposes where Site information is needed in the message body.

## Site - Longitude & Latitude - Scheduler
This process is used in conjunction with the EPIC sync process. EPIC does not currently update the latitude and longitude, this process will read from the Site_Input.csv and then update the associated Site. This should be scheduled to run after each EPIC sync.

## Standard Sync Scheduler
This process is used to execute the Standard Sync from the cloud versus requiring a Windows Task Scheduler to initiate the process. This Scheduler must require the `Execute_Sync.bat` file.
