# Decommission and Deletion of a Shared Mailbox

!!! note
    Typically what is done when a person reaches out and says that a mailbox is no longer in-use and can be deleted is the following:

1.  Place an out-of-office on the message for ~30 days letting anyone who sends to it know that the mailbox will be going away and, if applicable, all inquiries should be directed to another shared mailbox or individual user (ask the requestor where they would like these messages to be sent before setting the OoO).
2.  After 30 days, disable the mailbox and remove access to it.
3.  Either remove all members from the .MBAccess and .webAdmin groups attached to the mailbox and leave the empty groups as having access to the mailbox as a reminder that they should be deleted when the mailbox is deleted OR you can empty and delete the groups when the mailbox gets disabled with the understanding that you may need to re-create them if access is needed again.
4.  Keep the mailbox around for ~2 more weeks just in case the user or another person in their department say "Oh, we forgot we need to get X, Y, and Z messages out of the mailbox before it gets deleted!"
5.  After 30 days + 2 weeks has passed, you may or may not want to create a .pst export of the mailbox's data from the Compliance/Purview admin center to store for a period of time on the Z: drive.
6.  Place the .pst file on the Z: drive if necessary.
7.  Delete the ExG-XXYYZZ.MBaccess and ExG-XXYYZZ.webAdmin groups, if not already done.
8.  Delete the ExS-XXYYZZ or ExR-XXYYZZ mailbox user in AD and this will delete the mailbox on the back end.
