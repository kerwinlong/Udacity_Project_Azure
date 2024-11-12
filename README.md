Resource Group
Resource Group Name: tms
2. SQL Database
DB name: tmsdb
Server: tmsserver1.database.windows.net
DB region: us-east
Admin login: cmsadmin
Admin password: CMS4dmin
Resource group: tms
DB workload env: Development
DB compute + storage: DTU - Basic
Press the "Next: Networking" button, then select "Public Endpoint", and set both of the Firewall rules that appear to "Yes".
Set everything else to default
Run SQL queries in sql_scripts/ directory after completion, starting from the users table. Don't forget to take screenshots.
3. Storage Account
Resource group: tms
Storage account name: tmsimages1 (needs to be unique)
Advanced - Allow enabling anonymous access on individual containers: Enable
Advanced - Access tier: Cool
Network access: Enable public access from all networks (the default)
Create container named "images". Set its access level to Container.
From Security + networking > Access keys:
Blob Storage key: S6bzS0PF/s1Dhwlf3hkVMJtAO7+suJjslA1BF/QUbe6scAkAkoh3YEDdgcud7f+Rdr3Z5pNC2LY8+ASt8lbp1Q==

4. Microsoft Entra ID
4.1. App Registration
Name: cmsEntraID
Who can use? "Accounts in any organizational directory (Any Microsoft Entra ID tenant - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)"
4.2. Secret Creation
Secret description: cmsSecret
Secret Key: f6709e2a-6d15-400d-a8f5-2a868c9ebf5e
Client Secret: 1WP8Q~TIsPp~WpsNEb5pTq1Tph8DfRbdMNMqga0J
Application (client) ID: 4b2ba46b-1415-41e3-8322-95bd4d31310b

Application

Name: udacitycms.azurewebsites.net
Runtime stack: Python 3.10
Pricing Plan: Free F1
If you are getting a "Validation failed for a resource" error, pick a different region.
After creation:

Settings -> Environment variables - Add the following variables (sample values are included, replace them with your values):
BLOB_ACCOUNT: tmsimages1
BLOB_CONTAINER: images
BLOB_STORAGE_KEY: S6bzS0PF/s1Dhwlf3hkVMJtAO7+suJjslA1BF/QUbe6scAkAkoh3YEDdgcud7f+Rdr3Z5pNC2LY8+ASt8lbp1Q==

SQL_SERVER: tmsserver1.database.windows.net
SQL_DATABASE: cms
SQL_USER_NAME: cmsadmin
SQL_PASSWORD: CMS4dmin
CLIENT_SECRET: 1WP8Q~TIsPp~WpsNEb5pTq1Tph8DfRbdMNMqga0J
SECRET_KEY: f6709e2a-6d15-400d-a8f5-2a868c9ebf5e
CLIENT_ID: 4b2ba46b-1415-41e3-8322-95bd4d31310b
Deployment Center
Source: GitHub
Pick the repo that contains the starter files.
6. Setting up OAuth2
At this point, your application should already be running. You should already be able to log in with username admin and password pass and you can create new posts or update existing ones.

The next part is getting the OAuth2 login to work.

Go to Microsoft Entra ID > App Registrations, click on the App Registration created earlier, and then pick Authentication from the left sidebar.

6.1. Microsoft Entra ID - Authentication - Add a Platform - Web
Redirect URIs: https://[IP ADDRESS FROM VM or WEB APP ADDRESS]/getAToken
logout URL: https://[IP ADDRESS FROM VM or WEB APP ADDRESS]/login
