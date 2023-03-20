# Summit Events App Campaign Recipe
 Align Campaign and Campaign Member to the Summit Events App

 ## Goal of the Campaign Recipe
 The goal of this recipe is to allow Events and Event Instances to align with Campaigns while the Event Registrations Lead or Contact have a related Campaign Member. The idea is driven by Campaigns being utilized for communication purposes, not to manage the event as that is what Summit Events App is intended for!

 The way this flow works, it'll capture the Campaign ID from the Event or Event Instance.  It will always depend on if there is an Instance Override.  If there is a Campaign Instance Override, it'll utilize the Instance Campaign ID.  If the Instance Campaign Override field is null, it'll use the Campaign ID from the Event record.  If both blank, it'll do nothing.

 Once it captures the Campaign ID, it'll look to see that a Contact or Lead exists on the record.  If there isn't one, it'll end the flow. At this point in the flow, it knows who the Contact or Lead is and will proceed to look if that Lead or Contact has a Campaign Member record related to teh Campaign ID it captured initially in the flow. If a Campaign Member ID is found, it'll update the Campaign Member Status.  If it doesn't find a Campaign Member, it will create one associated to the Lead or Contact. This ends the flow

 In Context: You may write a report of constituents and add them to a campaign to invite them to an event. That invitation has a registration link associated to it. When the individual registers, it'll create the event registration record, find the Campaign Member with a Status of "Sent" and update it to "Responded".  If you're using something like Journey Builder in Marketing Cloud, you can have the journey check the status and ensure they don't get the reminder email.

 You can use different status', but you'll want to make sure they are available on all campaigns and then update the flow accordingly.

 ## Best Practice
 This flow is a template, so best practice would be to create a new flow from this template should there be future updates.

## Installation Process

### Steps Post Installation
- Update permissions to ensure that the Campaign field on the Event and Campaign Override on Instance are accessible to the appropriate users. This may happen on a profile, but a permission set is preferred
- Update the Event Lightning Layout to add "Campaign" to the Event Details tab
- Update the Event Instance standard page layout to add "Campaign Override" into the Override Section
- Review the Flow and Update according to your process and business outcome

### Creating the Package
- To create this org-dependent package start with the following command `sfdx package:create -t Unlocked -r force-app -n SummitEventsAppCampaigns --org-dependent`
- Create the Beta Version of the package: `sfdx package:version:create --path force-app/ --code-coverage --installation-key-bypass --wait 10`
- Promoete the package: `sfdx force:package:version:promote -p version_id -n`

### Installation Links
- Sandbox: https://test.salesforce.com/packaging/installPackage.apexp?p0=04t5f000000rM7xAAE
- Production: https://login.salesforce.com/packaging/installPackage.apexp?p0=04t5f000000rM7xAAE
