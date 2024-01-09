Install CLI –
	https://developer.salesforce.com/tools/sfdxcli

Install VSCode –
	https://code.visualstudio.com/

Install Extension –
	Salesforce Extension Pack
	Salesforce CLI Integration
------------------------------
Open Teminal (View > Terminal)
Control + Shift + p to open command pallet instead of typing in terminal
------------------------------
To get the help of specific command –
	sfdx force:project:create -h

Execute the following command to create new project –
	sfdx force:project:create -n "Project Name"
	Note: Replace "Project Name" with the name you want
	Note: Control + Shift + p and select "SFDX: Create Project with Manifest" to see all the sfdx commands in the pallet.

Setting Instance url -
	sfdx force:config:set instanceUrl=https://login.salesforce.com
	Note: for sandbox: instanceUrl=https://test.salesforce.com	
	Note: "sfdx-project.json" file can be modified if you want to execute from pallet (select "SFDX: Authorize an Org")

Execute the following command to authenticate and login –
	sfdx force:auth:web:login -a OrgAliasName	
	Example: sfdx force:auth:web:login -a Batch61 -d
	-d if you want to keep the org as default	
	
To verify that already if the org is already authenticated use -
	sfdx force:org:list
	Note: It will show the list of authorized orgs. 
	(-u means: username or alias for the target org; overrides default target org)

To open a specific org with the alias name - 
	sfdx force:org:open -u Batch62
To rename or assign alias to the org -
	sfdx force:alias:set Batch60=rudra@batch60.com
	Note: Batch60 is the alias name, rudra@batch60.com is the username
If you want to switch from one org to another org use - 
	"SFDX: Set a Default Org" in the Pallet. (Contrl + Shift + P)

Create new apex class –
	sfdx force:apex:class:create -n ApexClassName -d force-app/main/default/classes/
	Note: -n is for the name, -d for the directory to store the apex class.
	Please make sure to give the directory of the classes or else it might store somewhere else.

To retrive only apex classes -
	sfdx force:source:retrieve -m ApexClass
	Note: for the more commands -
	https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_force_source.htm

To retrive all the components or specific components from the server with package.xml -
	sfdx force:source:retrieve --manifest manifest\package.xml
	Note: open the package.xml which can find in manifest and right click > select "SFDX: Retrieve This Source from Org"

Directly retrieve or deploy the components by opening a specific Apex Class/ Apex Trigger so on or execute the command as below -
	sfdx force:source:deploy --json --loglevel fatal --sourcepath force-app\main\default\classes\Calculations.cls

-------------------------------------------------------------------------------------------------------------
********************
Apex Replay Debugger
********************
Commant Pallet (Contrl + Shift + p)
-----------------------------------
To turn on Apex Replay Debugger -
	SFDX: turn on apex debug log for replay debugger

After running the test methods, to see the logs execute -
	SFDX:Get Apex Debug Logs

Open the recent or whatever the log you want and right click on the file and select the following command -
	SFDX: Launch Apex Relay Debugger with Current File

Press F11 to debug line by line
-----------------------------------------
************************************
Scratch Org creation process
************************************
	1. Enable Dev Hub: Setup > Dev Hub > Enable Dev Hub
	2. In Vs Code Create a Project folder for the Deb Hub Org
	3. In Command Pallet execute: SFDX: Authorize a Dev Hub (Command: sfdx force:auth:web:login -a Batch60 --setdefaultdevhubusername)
	Before proceeding with point 4 to have sample data included modify 'config > project-scratch-def.json' file with -
		{
		  "orgName": "Srinu Sfdc",
		  "edition": "Developer",
		  "features": [],
		  "hasSampleData":true,
		  "settings": {
		    "orgPreferenceSettings": {
		      "s1DesktopEnabled": true
		    }
		  }
		}
		--
		"hasSampleData":true should be included.
	4. In Command Pallet execute: SFDX: Create a Default Scratch Org (Command: sfdx force:org:create -f config\project-scratch-def.json --setalias Release1 --durationdays 30 --setdefaultusername)
		Note: It takes time to create. It will generate the username automatically.
	
