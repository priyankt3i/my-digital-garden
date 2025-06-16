# Can't Access Eclipse Marketplace?

## Eclipse Network Connection Settings

### Step 1: Check / Update Active Provider
Window->Preferences->General->Network Connections
Choose "Active Provider" To "Manual"
Click 'apply' and then 'Ok'

- Restart Eclipse and Check if you can access Eclipse Marketplace

### Step 2: Check / Update Proxy
Window->Preferences->General->Network Connections
Try to add the following host in Proxy bypass.
```sh
marketplace.eclipse.org/catalogs/api*
```
Click 'apply' and then 'Ok'

- Restart Eclipse and Check if you can access Eclipse Marketplace

### Step 3: Open command prompt
```sh
setx _JAVA_OPTIONS -Djava.net.preferIPv4Stack=true
```
Hit enter.

Check if value set. Use this command:
```sh
echo %_JAVA_OPTIONS%
```
Hit Enter, this should return :
```sh
-Djava.net.preferIPv4Stack=true
```
- Restart Eclipse and Check if you can access Eclipse Marketplace

### Step 4: ByPass Firewall
If previous steps didnt work, You could try adding these two lines at the end of your eclipse.ini:
```sh
-Djavax.net.ssl.trustStoreType=Windows-ROOT 
-Djavax.net.ssl.trustStore=NONE
```
Save and Close the file and restart Eclipse.

- Restart Eclipse and Check if you can access Eclipse Marketplace

***Note***: To access Eclipse ini go to installation directory and the eclipse.ini should be in the root folder.

