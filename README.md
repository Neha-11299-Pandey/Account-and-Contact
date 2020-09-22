# Account-and-Contact

When a new Account is created, create a new Contact that has the following data points:
First Name = “Info”
Last Name = “Default”
Email = “info@websitedomain.tld”
Only_Default_Contact = TRUE
When the Account has more than 1 Contact, update Only_Default_Contact to FALSE.

trigger createAccount on Account (after insert,before update)
{
á

 áList<Contact> lst = new List<Contact>();
á 
 Contact con = new Contact();
á 
á if(trigger.isAfter && trigger.isInsert)
á
 {
á á
for(Account acc:trigger.new)
á 
á{
á á 
ácon.AccountId = acc.Id;
á á 
ácon.FirstName = 'Info';
á á 
ácon.LastName = 'Default';
á á á
 con.Email = 'info@websitedomain.tld';
á á 
 á álst.add(con); á á
á 
á }
á
 }
á á
if(!lst.isEmpty())
á
 á{
á 
á á insert lst;
á 
á
á á}
á á
á á
á 
áif(trigger.isBefore && trigger.isUpdate)
á á
{
á 
áList<Account> ls = [Select
 Only_Default_Contact__c from Account];

á áfor(Account a: trigger.new)
á 
á á{
á á
 á if(lst.size()==1)
á á á
á {
á á 
 á a.Only_Default_Contact__c = TRUE;
á á á á
 update a;

á á á á }
á á á 
á else
á á á
 á {
á á á á 
á   a.Only_Default_Contact__c = FALSE;
á á á á
 á  update a;
á á á 
á   }
á
 
 á}
á 
á }



