## Sample Code

### OnCustomEvaluateConditionOnTable

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


### Custom Record Change implementations.

Either update table’s OnModify() trigger or subscribe to OnAfterModifyEvent() in a codeunit and add below call to RunPowerFlowOnModifyEvents().
It is sometimes necessary to add it in places other than the OnModify() or OnAfterModifyEvent() as field validations can trigger a modify at sometimes, undesirable times.

    [EventSubscriber(ObjectType::Table, Database::"SharePoint Attachment BTR", OnAfterModifyEvent, '', false, false)]
    local procedure "SPAttachment_OnAfterModifyEvent"(var Rec: Record "SharePoint Attachment BTR"; var xRec: Record "SharePoint Attachment BTR"; RunTrigger: Boolean)
    var
        ModificationHandler: Codeunit Braintree.PowerFlow.Monitoring."Modification Handler BTR";
    begin
        ModificationHandler.RunPowerFlowOnModifyEvents(Rec, xRec);
    end;

## Troubleshooting

### Common errors

#### Record type <name> is not supported by this workflow response.
This can occur when you have created an approval workflow but have not implemented status management code.
![alt text](./img/image-69.png)

**Solution:**
implemented status management code. or you have forgotten to set the PowerFlow Manages Status field to Yes on the Power Workflow Definition.


[**⬆️ Back to Top**](#sample-code) &nbsp;&nbsp;&nbsp;&nbsp; [**🏠 Home**](/PowerFlow)