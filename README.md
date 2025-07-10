# PowerFlow

## 1. Introduction
The PowerFlow extension for Microsoft Dynamics 365 Business Central allows you to save time setting up workflows and extend it into the PowerPlatform.

The extension includes the following features:
**Flexible Workflow Types**
- Approval Workflows: Configure multi-level approval processes
- Record Change Workflows: Monitor and control field value changes 
- Processing Workflows: Automate business process sequences

**Power Automate Integration**
- Seamless integration with Microsoft Power Automate
- Custom webhook endpoints for workflow triggers
- Configurable connection accounts and flow URLs

**Advanced Field Monitoring**
In Standard Business Central, you either the approval is triggered either on everything, or on individual fields. I.e. if you wanted to track a change on 5 fields, you had to maintain 5 different workflows.
With PowerFlow, you specify all the fields you want to monitor, and maintain 1 workflow.
- Track changes to specific fields across Business Central tables
- Restore previous values if needed
- Configurable field change conditions

**Multi-Level Approval Management**
- Support for multiple approver types:
  - Security Groups
  - Mailing Groups
  - Individual Users
- Sequential approval routing
- Conditional approvers – This allows you to maintain 1 workflow, and have separate approvers for different conditions on a record. E.g. send Purchase Order approvals to different branch managers, regardless of the user, using just 1 workflow.
- Duplicate approver detection
- Approval status tracking



## 2. Activation

In Business Central, search for and open “Braintree App Licenses”

 ![activate1](./img/image.png)

1.	Enter your e-mail address
2.	Select the PowerFlow entry
3.	Click Request Subscription/Trial License

We will activate an evaluation license and send it to the email address you specified. The mail will contain a license key. Copy that license key then return to the Braintree App Licenses.

 ![activate2](./img/image-1.png)

1.	Select the PowerFlow entry
2.	Click Update License Key
3.	Enter the key on the page that opens and click Ok. You should get a message that states “Thank you for registering”

## 3. Process

### 3.1 PowerFlow Setup

![search-setup](./img/image-2.png)

Review setups

![alt text](./img/image-3.png)

Each Type can be configured with a default PowerAutomate flow that will copy to the Power Workflow Definitions.
Click Edit to modify the Authentication for the Flow Setup.

> Note: The authentication is to match the PowerAutomate authentication method. Only users in my tenant relates to the Any user in my tenant option in PowerAutomate. If this is selected, you need to create a app registration in Azure, with the PowerAutomate User permission.
>
> ![alt text](./img/image-4.png)


Open Power Workflow Definitions
 
![alt text](./img/image-5.png)


### 3.2 Create a new Record Change Power Workflow Definition

![alt text](./img/image-6.png)

Enter **Workflow Description**
![alt text](./img/image-7.png)

Set **Type** to *Record Change*
![alt text](./img/image-8.png)

Select Customer table and lookup Page
![alt text](./img/image-9.png)

Select Customer Card
![alt text](./img/image-10.png)

Select the **Power Automate Flow Id** from lookup or click the **Use default Flow URL and ID **action
![alt text](./img/image-11.png)

Set **Event Selection** to *New*
Add **Event Description** and click in the Field Name cell under Record Change Conditions
![alt text](./img/image-12.png)

Select fields
![alt text](./img/image-13.png)
![alt text](./img/image-14.png)

Selected fields are populated in the Record Change Conditions
![alt text](./img/image-15.png)

Add approvers
![alt text](./img/image-16.png)

You can make use of Security Groups, Mail Groups and individual Users. 
It will sequentially send to everyone in the group. Everyone in the group must approve. If someone in the group rejects it, it will not go to the next person in that group and or to any subsequent approvers setup in this sequence.

![alt text](./img/image-17.png)

Click the Approval conditions assist edit button
![alt text](./img/image-18.png)

Add approver conditions
![alt text](./img/image-19.png)

Add conditions for when this approver will be used.
The approvers on this line will only be used, if the Customer Posting Group on the Customer card is FOREIGN

Add second approver conditions, for when this approver will be used
![alt text](./img/image-20.png)
![alt text](./img/image-21.png)

Click the Create Workflow action
![alt text](./img/image-22.png)

Duplicate Approver Warning
![alt text](./img/image-23.png)

This is just a warning that potential duplicates have been detected, and you have to ensure that the conditions are setup correctly so that the same approver isn't used twice in an approval run.

Click the Yes to create new Run and Cancel Event Codes
![alt text](./img/image-24.png)

Review and enable workflow
![alt text](./img/image-25.png)

Open a DOMESTIC customer card
![alt text](./img/image-26.png)

Change Name 2, Address and VAT Registration No.
![alt text](./img/image-27.png)
![alt text](./img/image-28.png)

Change to View mode
![alt text](./img/image-29.png)

Changes have been reverted. Click the OK button
![alt text](./img/image-30.png)

Open the Your Approval Required for changes made to email
![alt text](./img/image-31.png)
![alt text](./img/image-32.png)
![alt text](./img/image-33.png)

Verify changes have been applied
![alt text](./img/image-34.png)
![alt text](./img/image-35.png)


### 3.3 Create a new Approval workflow for custom tables

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

## 4. Extending

Events have been added in strategic places to allow you extend workflows by focusing on the business logic and less on the where and how to add the code.

Here is a list of events available to use:

| Object | Event | Usage Scenario |
| --- | --- | --- |
| codeunit 72449784 "PowerFlow Management BTR"    | OnBeforeRunWorkflow   |   Perform additional checks before a custom workflow is executed by a Workflow Trigger type.  |
|     |  OnBeforeCancelWorkflow   |   Perform additional checks before a custom workflow cancellation is executed by a Workflow Trigger type.  |
|     |   OnExecuteRunWorkflowOnAfterCheckApprovalPossible  |  For each matching workflow definition that is linked to the Workflow Trigger, after the Approval is Possible Check is performed, handle custom checks.   |
| codeunit 72449775 "Approval Management BTR"   |   OnCheckApprovalPossibleOnAfterCalcShowNothingToApproveError  |   Perform additional checks, e.g. if the document should go for approval, check if the lines on the document satisfies a custom condition, and return true if “Nothing to approve” error should then be raised.  |
|     |  OnAfterCheckApprovalPossible   |  Custom logic to execute or retain record detail when approval is possible.   |
| codeunit 72449776 "Record Approval Management BTR"   | OnBeforeCreateApprovalStatus    |   When status is managed by PowerFlow, before the new status record is inserted into the database, allows the for custom logic to be added.  |
|     | OnBeforeUpdateApprovalStatus    |   Before status is changed from one value to the next, allow for custom logic to be added. E.g. allowed status movements.  |
| codeunit 72449777 "Field Change Management BTR"   | OnApplyNewValuesFindWorkflowRecordChange    |  Allows for custom implementation of the ApplyNewValues event if executed by a function using a table other than the Workflow Webhook Entry   |
|     | OnDiscardNewValuesFindWorkflowRecordChange    |  Allows for custom implementation of the DiscardNewValues event if executed by a function using a table other than the Workflow Webhook Entry   |
| codeunit 72449778 "WF Webhook Notification BTR"   |   OnPrepareWebhookPayloadOnBeforeWriteToText  |  Add additional data to the Json Payload being sent to PowerAutomate   |
| codeunit 72449779 "WF Webhook Notify Task BTR"    |  OnFetchWorkflowWebhookNotificationInitParams   | Allows overriding of the RetryCount and WaitTime parameters    |
| codeunit 72449780 "Workflow Webhook Mgmt BTR"    |  OnFindTaskSchedulerAllowed   | Allow override of using the Task Scheduler when sending webhook notifications.    |
|     |  OnPrepareWebhookPayloadWithxRecOnBeforeCompareField   | Add custom content or skip content from being added (like sensitive information) to the field changed array information.    |
|     |  OnBeforeReturnValidateApproverConditionsResult   | Perform custom checks when determining if this approver (or approver set) should be used in the approval process.    |
| codeunit 72449781 "Modification Handler BTR" | 	OnBeforeShouldHandleWorkflowEvent | Determine if a worklow event should be executed based on custom logic |
|     |	OnShouldHandleWorkflowEventOnBeforeCompareField | 	Before a field change is compared to the original value, perform custom checks on a field. |
| codeunit 72449785 "Workflow Condition Eval. BTR" | OnBeforeEvaluateCustomConditions | Enable evaluation custom conditions for a record. |
|     |	OnBeforeEvaluateCondition | Perform Custom implementation logic before record conditions are evaluated. |
|     |	OnCustomEvaluateConditionOnTable | 	Implement custom logic to determine if the execution of the event should trigger a workflow instance or not. See Example Code section for implementation example. |
|     |	OnBeforeEvaluateRecordChangeCondition | Custom implementation of Record Change Condition checks |
| codeunit 72449787 "Workflow Response Handling BTR" | 	OnSetStatusToRejected | Handle approval outcome for when a document is rejected and not using the PowerFlow Status management. |

## 5. Example Code

### 5.1 OnCustomEvaluateConditionOnTable


    [EventSubscriber(ObjectType::Codeunit, Codeunit::"Workflow Condition Eval. BTR", OnCustomEvaluateConditionOnTable, '', false, false)]
    local procedure OnCustomEvaluateConditionOnTable(_LookupRecRef: RecordRef; _RecRef: RecordRef; _TempBlob: Codeunit "Temp Blob"; var _IsHandled: Boolean; var _Result: Boolean)
    var
         ItemJnlBatch: Record "Item Journal Batch";
         tempItemJnlLine: Record "Item Journal Line" temporary;
    begin

        /// Use to allow custom checks for specific tables or conditions. 
        /// Example: to check if the total amount in a Item Journal Batch is zero.
        case LookupRecRef.Number of
            Database::"Item Journal Batch":
                begin
                    LookupRecRef.SetTable(ItemJnlBatch);
                    // Custom field added to ItemJournalBatch to use as filter
                    amountFilter := ItemJnlBatch.GetFilter("Total Amount (LCY) Filter");
                   ItemJnlBatch.SetRange("Total Amount (LCY) Filter");
        
                    if ItemJnlBatch.Find() then begin
                        // function to get the total batch amount
                        tempItemJnlLine."Amount (LCY)" := ItemJnlBatch.GetAbsJournalTotalAmount(); 
                        tempItemJnlLine.Insert(false);
                        // apply filter the check if amount satisfies the condition
                        tempItemJnlLine.SetFilter("Amount (LCY)", amountFilter); 
                        exit(not tempItemJnlLine.IsEmpty());
                    end;
                end;
        end;
    end;


### 5.2 Custom Record Change implementations.

Either update table’s OnModify() trigger or subscribe to OnAfterModifyEvent() in a codeunit and add below call to RunPowerFlowOnModifyEvents().
It is sometimes necessary to add it in places other than the OnModify() or OnAfterModifyEvent() as field validations can trigger a modify at sometimes, undesirable times.

    [EventSubscriber(ObjectType::Table, Database::"SharePoint Attachment BTR", OnAfterModifyEvent, '', false, false)]
    local procedure "SPAttachment_OnAfterModifyEvent"(var Rec: Record "SharePoint Attachment BTR"; var xRec: Record "SharePoint Attachment BTR"; RunTrigger: Boolean)
    var
        ModificationHandler: Codeunit Braintree.PowerFlow.Monitoring."Modification Handler BTR";
    begin
        ModificationHandler.RunPowerFlowOnModifyEvents(Rec, xRec);
    end;


## 6 Troubleshooting
### 6.1 Common errors

#### 6.1.1 Record type <name> is not supported by this workflow response.
This can occur when you have created an approval workflow but have not implemented status management code.
![alt text](./img/image-69.png)

**Solution:**
implemented status management code. or you have forgotten to set the PowerFlow Manages Status field to Yes on the Power Workflow Definition.

### 6.2 Other
If you encounter any issues or errors while using the PowerFlow extension please contact Braintree support, providing details such as error messages and the steps leading to the problem for efficient troubleshooting.

Email: bcsupport@braintree.co.za
