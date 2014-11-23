# bugzilla_custom

A Bugzilla template that presents "fake" custom ticket types and fields without actually requiring custom ticket types or fields in the data model.

TABLE OF CONTENTS:
* WHAT IS THIS?
* HOW DO I INSTALL IT?
* HOW DOES IT WORK? (BASIC DESCRIPTION)
* HOW DOES IT WORK? (DETAILED DESCRIPTION)
* TERMINOLOGY: BUG VS TICKET
* RELATED OFFICIAL DOCUMENTATION FROM MOZILLA

## What's this?
A Bugzilla template that presents "fake" custom ticket types and fields without actually requiring custom ticket types or fields in the data model.

The custom ticket types are "fake" in that they are just GUI buttons which are not actually wired to anything in the data model and the custom ticket fields are "fake" in that they are just GUI fields which are actually wired to the standard Description field in the data model. The advantages of this are several:

* Tickets are of the default and standard format and use the standard default data model. Real custom types and fields in the data model are not necessary. This keeps your tickets easy to work with and export etc.

* Allows distinguishing between different types of tickets, and presents different fields appropriate to the selected ticket type.

* Users are forced to enter tickets in a sane format which makes the tickets easier to understand. This makes sure that all users (even those who are not familiar with good practices) file great tickets.

## How do I install it?
Installing is very simple and takes only a minute. Go to your bugzilla template folder, example path:

`/var/lib/bugzilla3/template/en`

and add the folder structure 

`custom/bug/create`

so that you get a folder structure as so

`<bugzilla folder>/template/en/custom/bug/create`

Then, put the files 

`create.html.tmpl`
`comment.txt.tmpl`

inside the create folder.

Make sure that all the folders and files you just created have the necessary permissions set on them in order for bugzilla to be able to reach and use them. Note that the /en/ in this instruction stands for English language templates. It is possible to put the files in folders for other languages as well, but since they are in English, if so the create.html.tmpl should be translated first.

Then, go to your bugzilla home and then press "New". When you reach the ticket entry form, it should be using the template.

## How does it work? (basic)
The files

`create.html.tmpl`
`comment.txt.tmpl`

make up a custom ticket template for Bugzilla that distinguishes between bugs, feature requests and other kinds of tickets. When filing a new ticket, the user is first presented three buttons: "Bug", "Feature request" or "Other". Depending on which button the user presses, different ticket fields are presented.

If the user presses the "Bug" button, instead of just displaying the standard "Description" field, the user is presented the fields "Steps to reproduce", "Actual result" and "Expected result". Behind the scenes, these fields are actually wired to the standard "Description" field in the data model.

If the user presses the "Feature request" button, instead of just displaying the standard "Description" field, the user is presented the fields "As a ...", "I want ..." and "So that ...". Behind the scenes, these fields are actually wired to the standard "Description" field in the data model.

If the user presses the "Other" button, the standard "Description" field is displayed along with a warning to only use this option if absolutely sure that the ticket can't be filed as a bug or feature request instead, and a reminder not to write sloppy tickets.

## How does it work? (detailed)

`CREATE.HTML.TMPL`

The file create.html.tmpl is the file that shows the ticket entry form. It uses JavaScript to present the three custom ticket type buttons. The buttons are wired to the JavaScript method "setupFields", which is used to change the visibility of the sections containing the custom ticket fields. Each custom ticket field has a name, which is used to identify that field and its contents in the comment.txt.tmpl file.

`COMMENT.TXT.TMPL`

This file controls what happens when the user presses the submit button. It uses IF statements to check whether the custom fields actually contain anything and combines the contents of them appropriately to prepare the contents to actually be stored as the standard "Description" field.

Hacking around with these files is relatively straightforward. If you want to present more or other "fake" custom ticket types or fields, or improve something in the files, just hack away! Please don't forget to notify the author about improvements, contact details can be found at the top of this file.

## Terminology: "bug" vs "ticket"
Bugzilla uses the term "bug" per default. This is unfortunate, because Bugzilla can handle- and does in most cases handle- not only bugs also feature requests, support questions etc.

In fact, Bugzilla even comes with an "importance" option called "enhancement" which can be used to signal that a bug is really not a bug, but rather an "enhancement" (we prefer using the term "feature request" over the term "enhancement").

The good news is that Bugzilla allows us to use another term than bug if we want to. The file 

`variables.none.tmpl`

Example path: 

`/var/lib/bugzilla3/template/en/default/global/variables.none.tmpl` 

allows us to switch to another term. A more fitting term, that is often used in other similar software, is "ticket". Make a backup copy of this file and simply edit the original file to switch to another term (we strongly recommend the term "ticket").

## Related official documentation from Mozilla
https://wiki.mozilla.org/Bugzilla:Customization_Guidelines
http://www.bugzilla.org/docs/tip/en/html/cust-templates.html
