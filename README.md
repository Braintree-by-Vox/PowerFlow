# PowerFlow
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
- In Standard Business Central, you either the approval is triggered either on everything, or on individual fields. I.e. if you wanted to track a change on 5 fields, you had to maintain 5 different workflows.
- You also had to add code if it was for a table other than those provided for by Business Central.
- With PowerFlow, you can enable change tracking for any (non-system) table in your database, without development.
- Only track the changes to your specified fields: You specify all the fields you want to monitor, and maintain 1 workflow.
- Restore previous values if needed
- Configurable field change conditions
  
> **NOTE:**
> 1. Suggest not using standard BC events like `A customer record is changed` for `Record Change` flows, as it will cause the trigger to be executed by standard BC and then by Power Flow.
> 2. Turn off the "Feature Update: Auto-save with every field change" feature, as this will cause `Record Change` flows to trigger on every field change.
> 3. We introduced page extensions for the Customer and Vendor cards that disables the immidiate save when modifying the **Name** fields. Otherwise it causes 2 approvals kicking off, one for the name change and then another one for any other monitored fields that have changed.

> **TECHNICAL NOTE**: 
> From #3 in the notes above, the Customer and Vendor cards has `CurrPage.Update()` code on the `Name.OnValidate()` which causes the save of the record.

**Multi-Level Approval Management**
- Support for multiple approver types:
  - Security Groups
  - Mailing Groups
  - Individual Users
- Sequential approval routing
- Conditional approvers – This allows you to maintain 1 workflow, and have separate approvers for different conditions on a record. E.g. send Purchase Order approvals to different branch managers, regardless of the user, using just 1 workflow.
- Duplicate approver detection
- Approval status tracking

