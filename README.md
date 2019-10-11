# Script Runner
This package contains utilities within xMatters. All items below require an xMatters Agent. All items below are to be used in conjunction with the Schedule Message feature in xMatters as they are all batch processes.

# Overview
Below are the following functions of the package.

## Role Sync
This process will synchronize user roles based on Group Membership affiliation. This process will add roles when a user is present in a group and remove an associated role if they have been removed from a group. Group and Role relationship is defined via a JSON structure in a shared library, like so:
```
{
  "data": [{
    "group": "xMatters Developers",
    "roles": ["Developer", "Full Access User"]
  }, {
    "group": "xMatters Company Supervisor",
    "roles": ["Company Supervisor"]
  }]
}
```
### Adding of Roles
Adding of roles is executed leveraging the `GET /groups/{groupID}/members`, based on the roster return the process will add the associated Role in the aforementioned JSON structure to the member of the Group. The add role process will also set a Custom Field to true, to identify that the user has Elevated Privileges. This is required for the removal which is discussed next.

### Removal of Roles
The removal of roles is executed by query the instance for all users with Elevated Privileges on the aforementioned custom field using `GET /people?propertyName={name}&propertyValue={value}`. Once the list of users and associated roles are returned, the process will then inspect each role and will then execute a `GET /people/{personID}/group-memberships` to determine if the user is a member of one of the associated role groups.

## Locations Impacted
This process will query the Sites and populate a select set of List properties in xMatters with the address details for message sending purposes.

## Site - Longitude & Latitude
This process is used in conjunction with the EPIC sync process. EPIC does not currently update the latitude and longitude, this process will read from the Site_Input.csv and then update the associated Site. This should be scheduled to run after each EPIC sync.

## Site - Longitude & Latitude
This process is used in conjunction with the EPIC sync process. EPIC does not currently update the latitude and longitude, this process will read from the Site_Input.csv and then update the associated Site. This should be scheduled to run after each EPIC sync.

## Standard Sync Scheduler
This process is used to execute the Standard Sync from the cloud versus requiring a Windows Task Scheduler to initiate the process. This Scheduler must require the `Execute_Sync.bat` file.
