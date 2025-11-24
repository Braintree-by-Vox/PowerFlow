## Extending

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


[**⬆️ Back to Top**](#Extending) &nbsp;&nbsp;&nbsp;&nbsp; [**🏠 Home**](/Braintree-theme)