## Process

### PowerFlow Setup

![search-setup](./img/image-2.png)
![alt text](./img/image-70.png)
![alt text](./img/image-71.png)

Each Type can be configured with a default PowerAutomate flow that will copy to the Power Workflow Definitions.
Click Edit to modify the Authentication for the Flow Setup.

> Note: The authentication must match the PowerAutomate authentication method. If "Any user in my tenant" option is selected, you need to create a app registration in Azure, with the PowerAutomate User permission.
>
> ![alt text](./img/image-4.png)


### Open Power Workflow Definitions
 
![alt text](./img/image-5.png)

- Create a new Record Change Power Workflow Definition

![alt text](./img/image-6.png)

- Enter **Workflow Description**

![alt text](./img/image-7.png)

- Set **Type** to *Record Change*

![alt text](./img/image-8.png)

- Select Customer table and lookup Page

![alt text](./img/image-9.png)

- Select Customer Card

![alt text](./img/image-10.png)

- Select the **Power Automate Flow Id** from lookup or click the **Use default Flow URL and ID **action

![alt text](./img/image-11.png)

- Set **Event Selection** to *New*
- Add **Event Description** and click in the Field Name cell under Record Change Conditions
 
![alt text](./img/image-12.png)

- Select fields

![alt text](./img/image-13.png)
![alt text](./img/image-14.png)

- Selected fields are populated in the Record Change Conditions

![alt text](./img/image-15.png)

- Add approvers

![alt text](./img/image-16.png)

- You can make use of Security Groups, Mail Groups and individual Users. 
It will sequentially send to everyone in the group. Everyone in the group must approve. If someone in the group rejects it, it will not go to the next person in that group and or to any subsequent approvers setup in this sequence.

- Enable the **Allow requestors to approve their own requests** option if requestors are in the list of approvers, and they are allowed to approve their own changes.

![alt text](./img/image-17.png)

- Click the Approval conditions assist edit button

![alt text](./img/image-72.png)

- Add approver conditions

![alt text](./img/image-19.png)

- Add conditions for when this approver will be used.
The approvers on this line will only be used, if the Customer Posting Group on the Customer card is FOREIGN

- Add second approver conditions, for when this approver will be used

![alt text](./img/image-20.png)
![alt text](./img/image-21.png)

- Click the Create Workflow action

![alt text](./img/image-22.png)

- Duplicate Approver Warning

![alt text](./img/image-23.png)

- This is just a warning that potential duplicates have been detected, and you have to ensure that the conditions are setup correctly so that the same approver isn't used twice in an approval run.

- Click the Yes to create new Run and Cancel Event Codes

![alt text](./img/image-24.png)

- Review and enable workflow

![alt text](./img/image-25.png)

- Open a DOMESTIC customer card

![alt text](./img/image-26.png)

- Change Name 2, Address and VAT Registration No.

![alt text](./img/image-27.png)
![alt text](./img/image-28.png)

- Change to View mode

![alt text](./img/image-29.png)

- Changes have been reverted. Click the OK button

![alt text](./img/image-30.png)

- Open the Your Approval Required for changes made to email

![alt text](./img/image-31.png)
![alt text](./img/image-32.png)
![alt text](./img/image-33.png)

- Verify changes have been applied

![alt text](./img/image-34.png)
![alt text](./img/image-35.png)


### Create a new Approval workflow for custom tables

> You can apply this logic to standard tables too and then only add additional fields and actions to pages as required

![alt text](./img/image-36.png)

Extend `Workflow Trigger BTR` by adding 2 new options

![alt text](./img/image-37.png)

Build table and verify OnDelete trigger is required

![alt text](./img/image-38.png)

Create page

![alt text](./img/image-39.png)

Update Workflow trigger Enum options

![alt text](./img/image-40.png)

Update Workflow trigger Enum options

![alt text](./img/image-41.png)

Get Approval Status

![alt text](./img/image-42.png)

Check if approval request is possible

![alt text](./img/image-43.png)

Required Variables

![alt text](./img/image-44.png)

Test 1 - new record approval, create a new record

![alt text](./img/image-45.png)

Click the Send Approval Request action, we are expecting an error

![alt text](./img/image-46.png)
![alt text](./img/image-47.png)

Create new Power Workflow Definition

![alt text](./img/image-48.png)

Enter **Workflow Description** and select **Type** = *Approval*

![alt text](./img/image-49.png)

Enable the **Enable Custom Trigger** and **PowerFlow Manages Status** toggle buttons
PowerFlow stores a separate record linked to this record and maintains the status there.

![alt text](./img/image-50.png)
![alt text](./img/image-51.png)

Select new custom table and lookup the page

![alt text](./img/image-52.png)

Click the **Use default Flow URL and ID **action

![alt text](./img/image-53.png)

Set Event Selection = New

![alt text](./img/image-54.png)

Set workflow event details

![alt text](./img/image-55.png)

Add approvers

![alt text](./img/image-56.png)

Create workflow

![alt text](./img/image-57.png)

Review and enable the workflow

![alt text](./img/image-58.png)

Click the **Send Approval Request** action

![alt text](./img/image-59.png)

Create new record and Send Approval Request

![alt text](./img/image-61.png)

Review status

![alt text](./img/image-60.png)

Open mail 1

![alt text](./img/image-62.png)

Approve with comment

![alt text](./img/image-63.png)

Open mail 2, reject with a reason

![alt text](./img/image-64.png)

Approval outcome email confirmations

![alt text](./img/image-65.png)
![alt text](./img/image-66.png)
![alt text](./img/image-67.png)

Result
The workflow response was set to "Reopen Document". One could just as well have used the "Reject Document" status to set the status to *Rejected*.

![alt text](./img/image-68.png)

[**⬆️ Back to Top**](#process) &nbsp;&nbsp;&nbsp;&nbsp; [**🏠 Home**](/PowerFlow)