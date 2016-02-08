# Prerequisites #

The script uses the the [Domain Shared Contacts API](http://code.google.com/googleapps/domain/shared_contacts/gdata_shared_contacts_api_reference.html), which is only available to Google Apps **Premier** and **Education Editions** domains. To enable the API, log in to your admin account, and click the **User accounts** tab. Then click the **Settings** subtab, select the checkbox to enable the Provisioning API and save your changes. Please note changes can take up to 24 hours to be reflected in the email address auto-complete and the contact manager.

# Importing Microsoft Outlook contacts into the shared contact list of a domain #

  1. Export your Microsoft Outlook contacts to CSV file in Windows format.
  1. [Install the script and its dependencies.](Installation.md)
  1. Run the script with:
<pre>
cd google-shared-contacts-client<br>
python shared_contacts_profiles.py --admin=*your-admin-login@your-domain.com* --import=*your-ms-outlook-contacts-file.csv* --output=*output-file.csv*</pre>

OR (only **Windows**, using **Win32 release**)

<pre>
cd google-shared-contacts-client<br>
shared_contacts_profiles.exe --admin=*your-admin-login@your-domain.com* --import=*your-ms-outlook-contacts-file.csv* --output=*output-file.csv*</pre>


The script will ask for the admin password.

Note that the script will print the contacts before and after the loading of contacts.<br>The contacts should be viewable in the Contact Manager within 24 hours, at this address: <code>http://www.google.com/contacts/a/your-domain.com</code>

The output file will contain all added or updated contacts with their ID, so that you can later update or delete them. The output format is suitable for input to another invocation.<br>
<br>
<h1>Imported CSV file format</h1>

The Zip file includes an example file: <code>outlook.csv</code>.<br>
<br>
The file is a comma-separated CSV file. The first line should contain the name of each column. Accepted columns are:<br>
<ul><li>Action: the action to perform on the contact, as one of: add, update, delete.<br>
</li><li>ID: the ID of the contact; must be left empty for add action, set for update and delete actions. You can retrieve contact IDs from the output of an <code>--import</code> or <code>--export</code> command.<br>
</li><li>contact fields: <a href='SupportedContactFields.md'>full list of accepted fields</a>.</li></ul>

Example:<br>
<pre><code>Action,ID,Name,E-mail Address,Business Phone<br>
add,,Adam Glacius,adam.glacius@anycom.com,+1 555 3227 8543<br>
update,241a444f0b330b22,Daniel Ireland,danielireland@restty.com,+1 555 3227 8544<br>
delete,527fbda08922b018,Duncan Amey,duncanamey@dreamt.com,+1 555 3227 8545<br>
</code></pre>

<h1>Other features</h1>

The script also enables you to:<br>
<ul><li><b>export</b> the existing contacts to a CSV file, with <code>--export=exported-file.csv</code><br>Please note that not all fields are supported by this feature: only the first home/work/other email addresses/phone numbers/postal addresses are retained. We recommend not using this feature to synchronize your address list back to your Outlook repository.<br>
</li><li><b>delete all contacts</b>, with: <code>--clear</code></li></ul>

If you specify several commands at the same time, they are executed in the following order: <code>--clear</code>, <code>--import</code>, <code>--export</code> <b>regardless of the order of the parameters in the command line</b>. In particular:<br>
<ul><li><code>--clear</code> is executed first because it asks for confirmation. If you specify <code>--clear</code> with another command, the script is guaranteed to execute without interruption after <code>--clear</code> prompt.<br>
</li><li>If you specify <code>--clear --export</code>, all contacts are deleted first, hence <code>--export</code> generates an empty file.<br>
</li><li>If you specify <code>--import --export</code>, the new contacts are imported first, then <code>--export</code> generates a file containing all contacts of the domain including the new ones.</li></ul>

<h1>Example invocations</h1>

Imports the contacts of your-ms-outlook-contacts-file.csv into the domain. Writes the added or updated contacts to <code>output-file.csv</code>:<br>
<code>python shared_contacts_profiles.py --admin=your-admin-login@your-domain.com --import=your-ms-outlook-contacts-file.csv --output=output-file.csv</code>

Exports all contacts of the domain to <code>export-file.csv</code>:<br>
<code>python shared_contacts_profiles.py --admin=your-admin-login@your-domain.com --export=export-file.csv</code>

Deletes all contacts of the domain:<br>
<code>python shared_contacts_profiles.py --admin=your-admin-login@your-domain.com --clear</code>