---
layout: post
title:  "My First Final Product: Grant Tracker"
date:   2015-08-04 09:10:41
categories: rails ruby project update week-ten
---

Today, I am wrapping up my involvement in the Grant Tracker.  Some of the front end has not been finished by Sam, and some parts that were requested by the client (Zapier support, Notes) have not been implemented.  But we have too many questions to build these out without further client input.  

But I am also excited, because it totally works!

So right now, this is what our application does:

- A user can perform all CRUD operations for...
  - an organization
  - an organization material (file stored in Google Drive)
  - a proposal
  - a proposal material (file stored in Google Drive)
  - a task (generating automatic/emailed reminders)
  - a reminder (although reminders are meant mostly to be in the background and are auto-generated when a task is created)
- Reminder emails are sent as a scheduled task on Heroku from the Google account
- Users can export data for organizations and proposals to a Google Spreadsheet.  The spreadsheet belongs to the user (via Google's shared privileges) and can be edited by the user.  It has links back to the proposal/organization page on the web app.
- Admins can import organizations from a Google Spreadsheet.

The code is private, but below you can find more information about the site and how we built it.

#Live Site

The site is deployed on Heroku, but I will not share the url here.

#Set Up Information

### Secret Environmental Variables
During collaboration and development, we need to store passwords and other secret information in a file that is not committed to git.  We need to share the variables among our collaborators.  To do this, we use a gem called Figaro.

Install Figaro, if it is not already installed.

On command line, type:

```
  $ bundle exec figaro install
```

This command will create a config/application.yml file and update .gitignore to ignore this file.  You should type Environmental variables into this file.

This project needs the following Environmental Variables.  Type these names (and their real values) into your local application.yml file.


```ruby
  development_username: 'something@gmail.com'
  development_password: 'something'
  `production_username`: 'something_else@gmail.com'
  `production_password`: 'something_else'
  `host_url`: 'http://localhost:3000'
  `deployment_url`: 'some_url'


  development_client_id: 'some_clientid'
  development_client_secret: 'some_secret'
  development_refresh_token: 'some_token'

  production_client_id: 'some_other_id'
  production_client_secret: 'some_other_secret'
  production_refresh_token: 'some_other_token'
  import_spreadsheet_id: 'some_id'

```

Then in my development.rb and and production.rb files, I set the variables to global ENV variables that we use throughout our code.

```ruby
 #config/development.rb
  ENV['url'] = ENV['host_url']  
  ENV['gmail_username'] = ENV['development_username']
  ENV['gmail_password'] = ENV['development_password']
  
  ENV['google_drive_client_id'] = ENV['development_client_id']
  ENV['google_drive_client_secret'] = ENV['development_client_secret']
  ENV['google_drive_refresh_token'] = ENV['development_refresh_token']
  
  
  #config/production.rb
  ENV['url'] = ENV['host_url']  
  ENV['gmail_username'] = ENV['production_username']
  ENV['gmail_password'] = ENV['production_password']
  
  ENV['google_drive_client_id'] = ENV['production_client_id']
  ENV['google_drive_client_secret'] = ENV['production_client_secret']
  ENV['google_drive_refresh_token'] = ENV['production_refresh_token']
```


To use the environmental variables, it's like we have a Hash called ENV, and the key is the items on the left hand side of the application.yml file.  The value is on the right-hand side.

As an example:

```ruby
>  ENV['gmail_username']
=> 'some_username@something.com'
```


In deployment mode, [follow Figaro documentation for how to deploy](https://github.com/laserlemon/figaro).  The only difference is that the documentation does not mention that you need to precede any figaro command in command line with 'bundle exec', as of this writing (8-3-15).

##Major Models
 - Organization
 - Proposal
 - OrganizationMaterial
 - ProposalMaterial
 - Task
 - Reminder
 - User
 - Spreadsheet


##Helper Models with seeded records

We have a few helper models that are only intended to be used.  Regular CRUD operations should not be available to the users.  These models and their default records are:

###StatusReminder
- Sent (default)
- Not Sent
- Not Needed

###StatusTask
 - Not Started (default)
 - In Progress
 - Completed

###StatusProposal
 - Not Started (default)
 - In Progress
 - Submitted
 - Awarded
 - Denied
 - Archived
 
###GrantType 
 - Earmark
 - Block
 - Categorical
(no default)

###Export
 - Organization

##Admin User
To start, only one user will be the Admin. The Admin is determined by the `is_admin` Boolean field in the users table.

New users will be created as `is_admin` == false.  From the web interface, there is no way to create a new Admin user.  The only way to add new Admins is for the current Admin to change a user to an Admin also.  The current Admin(s) will have access to a list of all users, and they can change any user to an Admin.

##CRUD availability

Only Admins have access to Create, Update, or Delete objects from the following models:
 
 - StatusReminder
 - StatusTask
 - StatusProposal
 - GrantType

Only Admins can Delete objects from the following models:

 - User (and Admin rights for any User)
 - Organization
 - OrganizationMaterial
 - ProposalMaterial
 - Proposal
 - Task
 - ProposalTemplate (TODO)

Any User can Delete objects that belong to them from the following models:

 - Task (association only)
 - Reminder (association & object)
 - Spreadsheet

Any User can Create, Read, and Edit objects that belong to them from the following models:

 - User
 - ProposalTemplate
 - UserSetting (TODO)
 - Task
 - Reminder

Any User can Create, Read, and Edit objects (whether they belong to them or not) from the following models:

 - Organization
 - OrganizationMaterial
 - ProposalMaterial
 - Proposal

Any User can Read objects (whether they belong to them or not) from the following models:

 - ProposalTemplate
 - StatusReminder
 - StatusTask
 - StatusProposal
 
Key to Table
<table>
  <thead>
    <tr>
      <th>Model</th>
      <th>Symbol</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Any User</td>
      <td>U</td>
    </tr>
    <tr>
      <td>Collaborating User</td>
      <td>C</td>
    </tr>
    <tr>
      <td>Owning User</td>
      <td>O</td>
    </tr>
    <tr>
      <td>Admin</td>
      <td>A</td>
    </tr>
  </tbody>
</table>

These permissions are cascading.  So if Any User can do it, so can a Collaborating User, an Owning User, and an Admin.  But if A Collaborating User can do it, Any User cannot.

<table>
  <thead>
    <tr>
      <th>Model</th>
      <th>Create</th>
      <th>Read</th>
      <th>Update</th>
      <th>Destroy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>User</td>
      <td>U</td>
      <td>O</td>
      <td>O</td>
      <td>A</td>
    </tr>
    <tr>
      <td>UserSetting</td>
      <td>U</td>
      <td>O</td>
      <td>O</td>
      <td>A</td>
    </tr>
    <tr>
      <td>Organization</td>
      <td>U</td>
      <td>U</td>
      <td>U</td>
      <td>A</td>
    </tr>
    <tr>
      <td>OrganizationMaterial</td>
      <td>U</td>
      <td>U</td>
      <td>U</td>
      <td>A</td>
    </tr>
    <tr>
      <td>ProposalMaterial</td>
      <td>U</td>
      <td>U</td>
      <td>U</td>
      <td>A</td>
    </tr>
    <tr>
      <td>Proposal</td>
      <td>U</td>
      <td>U</td>
      <td>U</td>
      <td>A</td>
    </tr>
    <tr>
      <td>Task-User Association</td>
      <td>O</td>
      <td>C</td>
      <td>O</td>
      <td>O</td>
    </tr>
    <tr>
      <td>Task</td>
      <td>U</td>
      <td>C</td>
      <td>C</td>
      <td>A</td>
    </tr>
    <tr>
      <td>Reminder</td>
      <td>U</td>
      <td>O</td>
      <td>U</td>
      <td>O</td>
    </tr>
    <tr>
      <td>StatusReminder</td>
      <td>A</td>
      <td>U</td>
      <td>A</td>
      <td>A</td>
    </tr>
    <tr>
      <td>StatusProposal</td>
      <td>A</td>
      <td>U</td>
      <td>A</td>
      <td>A</td>
    </tr>
    <tr>
      <td>StatusTask</td>
      <td>A</td>
      <td>U</td>
      <td>A</td>
      <td>A</td>
    </tr>
    <tr>
      <td>GrantType</td>
      <td>A</td>
      <td>U</td>
      <td>A</td>
      <td>A</td>
    </tr> 
    <tr>
      <td>ProposalTempalte</td>
      <td>U</td>
      <td>U</td>
      <td>?</td>
      <td>A</td>
    </tr>  
    <tr>
      <td>Spreadsheets</td>
      <td>U</td>
      <td>U</td>
      <td>U</td>
      <td>U</td>
    </tr> 
    <tr>
      <td>Export</td>
      <td>-</td>
      <td>U</td>
      <td>-</td>
      <td>-</td>
    </tr>
  </tbody>
</table>

## Creating Helper Model Default Records and Admin

The default admin user is seeded in the database.

Run rake db:seed to seed the database initially.  It can be run as many times as you want.  If the records have been created, they will not be created again.


##How Tasks/Reminders/Users work together
 - The user who creates the task is assigned to the task
 - Any user can assign him or herself (or others) to any task 
 - When a new user is assigned to a task, the users’s reminders are created, according to the user's default reminder settings
 - When a user is removed from a task, the user’s reminders for that task are deleted
 - When a user is removed from a task and there are no more users, the task is also deleted
 - A user cannot create a reminder for a task unless they are already assigned to the task
 - Default reminders are not created if the reminder date is in the past or if the user already has a reminder for that task on the default day
 - A user can still create multiple reminders for a single task on the same day. (For example, to set a reminder at 8:00 am and then again at noon on the same day.)
 - To add/update/read/or delete reminders, go to the Task page.  To change how reminders are created by default, go to the Settings page. (This feature is TODO)
 - If a task is marked complete, all reminders are deleted for all users. (Note: if you mark a task complete and then undo that back to a previous status, your reminders will be gone.)
 

## How default tasks are created for a proposal
 - The user has stored the default tasks they want to create when they make a proposal (This customization is TOOD)
 - The user can change the default tasks on their settings page (This feature is TODO)
 - When a user creates a new proposal, the default tasks for a proposal will pre-populate.  They can add/edit/delete these default tasks before submitting a proposal
 - When a user creates a proposal, any tasks created will be assigned to that user
 
## File Repository Notes
 - Files can be uploaded to, downloaded from, copied over, and deleted from the designated Google Drive account
 - Access to the Google Drive via the app requires OAuth 2.0 authorization (see https://console.developers.google.com/)
 - Access requires a client ID # and a client secret
 - The code for the file repository can be found in the application helper file
 - When an organization or proposal is created a new sub-collection is generated on the Google drive using the (create_sub_collection method) to store that organization's/proposal's materials
 - New files are uploaded to the drive using the (`upload_to_google_drive` method), this method also calls the (`add_file_to_folder` method) to move the file to the appropriate sub_collection
    -to do this the controller needs to send as arguments: the path to the file(`make_path` method)
      -the filename(`make_filename` method)
      -the id number for the `sub_collection`(`make_folder_id` method)
      -and the collection name(collection method)
 - Downloading, copying over, and deleting files occurs in a similar fashion using the sub-methods in the controller and the main methods in the application helper


## Debugging
The Heroku site is set up to log app data for debugging.  Anything that you send to STDOUT (ie - puts) will appear in the heroku log.

To look at the logs (if you are a collaborator), go to command line of the repository and type in...

```
$ heroku logs --source app
```

Amidst the other stuff, should be your stuff.

NOTE: this is a config setting which can be changed.  So if it stops working, check if the production logging settings are still set, as below.

```ruby
 #config/production.rb
 
 # somewhere within the Rails config loop
  config.log_formatter = ::Logger::Formatter.new
  config.logger = Logger.new(STDOUT)
  
```


## Record Exporting

For now a Spreadsheet can only belong to a single user, not multiple users.

Spreadsheet
-name
-googleid #must not be google_id because it confused activerecord
-google_url
-export_id
-last_updated
-user_id


Export  
-name

(This is a Helper model. The available types are hard-coded in as db:seeds.  Even the admin does not have access to change the values of this class because unless the models have the right code, data can not be exported.  Therefore, routes don't even exist.)

Files are shared with users at the time of being created.  Files belong to the user.  When you edit a file, you automatically refresh its contents.

The content being exported is hard-coded (by Model) and is not able to be changed.  However, sensitive data, like EINs, are removed, and joins are created if they  make sense.

A user can edit the file in any way he/she wants. Links to the objects are available as one of the columns in the file.

## Record Importing
There is a single file in Google Drive in the development account that is set up to Import Organization records. The ID is secret.  (It is not necessary to use separate files for deployment vs. production necessarily but this can be done.)

The Admin is the only person who has access to the import page.  There is a link to the file where records can be added.  The user should not change anything about the records.  Any person with the url to the spreadsheet can access/edit it.

Once records have been added, the Admin can hit a link to Import the records.  Failed records are displayed for the user after running, which is an important notification because all records are deleted from the spreadsheet after uploading to prevent duplication.

## Possible Security Issues

EINs of Foundations are not currently encrypted or Hashed.  However, they are not available for Exporting.

There are two google accounts, one for development, one for production.

Sensitive, private information should *not* be stored in Google Drive. Sensitive information can be stored in the database.

The import spreadsheet link is shareable with anyone who has the link.  The import happens as a post method and must be authenticated using the user's admin session.  It may be desirable to remove sharing and disable the post import route after the client has uploaded their records and turn that off after it is done.  It is anticipated that this feature is only needed during set up.