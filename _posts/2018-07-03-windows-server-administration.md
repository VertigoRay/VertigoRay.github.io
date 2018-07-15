---
layout: post
title: Windows Server Administration - Cross-Training Job Aid
img: //i.imgur.com/JwAcelr.png
author: Raymond Piller
comments: true
tags:
- LTEC5210
- Information Design
- ProjectA
---
<small><i><a href="https://github.com/VertigoRay/LTEC5210.ray.pillers.us/raw/master/download/2018-07-03-windows-server-administration.pdf">Download PDF</a></i></small>
- [Introduction](#introduction)
- [Main Course Outcomes](#main-course-outcomes)
- [Preparing for Training](#preparing-for-training)
  - [Definitions](#definitions)
  - [Pre-Installation](#pre-installation)
  - [Lab Preparation](#lab-preparation)
- [Training Session](#training-session)
  - [AD Objects](#ad-objects)
    - [AD User Requests Task Set](#ad-user-requests-task-set)
      - [Account Request - lc00001](#account-request---lc00001)
      - [Account Request – sd00001](#account-request-%E2%80%93-sd00001)
      - [Account Request - wm00001](#account-request---wm00001)
      - [Account Request – nm00001](#account-request-%E2%80%93-nm00001)
      - [Account Request – pd00001](#account-request-%E2%80%93-pd00001)
    - [AD Group Requests Task Set](#ad-group-requests-task-set)
      - [Share Access](#share-access)
      - [RDP Request – Add User](#rdp-request-%E2%80%93-add-user)
      - [Technician Leaving – Chucky Dobi](#technician-leaving-%E2%80%93-chucky-dobi)
      - [New Technician – KVM Access](#new-technician-%E2%80%93-kvm-access)
      - [Restricted Printer Access](#restricted-printer-access)
    - [Assess Access/Permission Issues Task Set](#assess-accesspermission-issues-task-set)
      - [Network Access Denied](#network-access-denied)
      - [Cannot RDP to Desktop](#cannot-rdp-to-desktop)
      - [Cannot Print – Access Denied](#cannot-print-%E2%80%93-access-denied)
      - [Network Share Inaccessible](#network-share-inaccessible)
      - [Cannot Log In to Website](#cannot-log-in-to-website)
  - [Network Shares](#network-shares)
    - [Quota Management Task Set](#quota-management-task-set)
      - [Home Drive is Out of Space](#home-drive-is-out-of-space)
      - [Departmental Share Full – Chemistry](#departmental-share-full-%E2%80%93-chemistry)
      - [Departmental Share Full – Psychology](#departmental-share-full-%E2%80%93-psychology)
      - [Need More Space](#need-more-space)
      - [Need More Space on Home Drive](#need-more-space-on-home-drive)
    - [Permission Management Task Set](#permission-management-task-set)
      - [Staff Member Needs Access](#staff-member-needs-access)
      - [Student Employee Needs Access](#student-employee-needs-access)
      - [Staff Member No Longer Needs Access](#staff-member-no-longer-needs-access)
      - [New Department Needs All Things](#new-department-needs-all-things)
      - [Unable to Access Network Location](#unable-to-access-network-location)
- [Instructor and Learner Resources](#instructor-and-learner-resources)
- [Credits](#credits)
- [Appendix](#appendix)
  - [Computer Naming Convention](#computer-naming-convention)
  - [Learner Evaluation](#learner-evaluation)

# Introduction

The goal of this cross-training is to allow any of the Windows Server Manager's (WSM) colleagues to partially fill in for him/her while he/she is out of the office. If the WSM wants to take a week for a vacation, the WSM's colleagues need to pick up the slack so the WSM doesn't return to the office with a heavy workload. Additionally, the WSM may only be out for an hour for an off-site appointment. Some things affect learning and need to be fixed immediately.

The WSM handles all the Windows server requests that come in. Most of the time, these requests are simple tasks and just require familiarity with the systems. These tasks are perfect candidates to cross-train for several reasons:

- There are a lot of current examples that we have available to us.
- They are relatively simple tasks, that come in frequent enough that they become a burden.
- They can be quickly trained and re-trained as needed.

As we work through the training remember one important thing. Although the learners are experts in their field, that doesn't make them an expert WSM.

# Main Course Outcomes

1. Proficiency with creation and management of Active Directory (AD) objects.
2. Proficiency with creation and management of Windows networked printers.
3. Proficiency with creation and management of Windows network shares.
4. Comfortable with written technical communication to non-technical people.

# Preparing for Training

Before you go any farther, you will want to start setting up your computer for the training. The virtual lab that we'll be using is free and easy to set up. However, it can take an hour or more to automatically run through all the steps; the speed mostly depends on your internet speed and the speed of your computer. Let's get the lab creation process started so we can let it run while you read through this document.

## Definitions

I'll attempt to define some common definitions for this document. Definition details will be linked.

- **CLI:** [Command-Line Interface](https://en.wikipedia.org/wiki/Command-line_interface)
  - Any text/commands in `code font` should be typed into your CLI.

## Pre-Installation

We will need a few pieces of software to set up the training lab. The lab will run in VirtualBox VMs. The VMs are configured with Vagrant so setup is easy; even if it takes a while. The Vagrant files are stored on [GitHub](https://github.com) so we might want a git client installed to make getting the files a breeze. You're expected to know how to run and walk through an installer on your own. For the purposes of this lab, the default installation options are fine.

1. [VirtualBox](https://www.virtualbox.org):
  1. [Download VirtualBox](https://www.virtualbox.org/wiki/Downloads). _The page isn't the prettiest, but the download links are at the top._
     - **Windows:** Click the _Windows hosts_ link, near the top of that page.
     - **OS X:** Click the _OS X hosts_ link, near the top of that page.
  2. Install VirtualBox.
2. [Vagrant](https://www.vagrantup.com):
  1. [Download Vagrant](https://www.vagrantup.com/downloads.html). _Choose the download appropriate for your OS._
  2. Install Vagrant.
3. **Optional:** [Git](https://git-scm.com):
  1. Download [Git](https://git-scm.com/downloads). _Choose the download appropriate for your OS._
     - **OS X:** OS X comes with Git, but it's likely not the latest version. Feel free to take this time to upgrade it.
  2. Install Git.

## Lab Preparation

<img alt="VirtualBox VMs" src="//i.imgur.com/o2tOKmJ.png" style="clear: right; float: right; margin: 10px;" />

You're expected to already be familiar with using git, GitHub, and Vagrant. If you're not, you may want to find and run through the tutorials on those. However, you don't need to run through the tutorials to get this started, I'll cover everything with enough detail to do it, even if you don't understand how it's working. Understanding these pieces is beyond the scope of this document and the training.

1. Open your CLI. _We will work from_ _C:\Temp__. If you decide to change that path or you're not using Windows, you will need to adapt future commands that reference the path that you're using._
   1. Change into that folder: cd C:\Temp
2. Download the Vagrant files from GitHub: [https://github.com/UNT-CAS/adfs2](https://github.com/UNT-CAS/adfs2)
   2. **If you have git installed:**
      1. `git clone https://github.com/UNT-CAS/adfs2.git`
   3. **If you _do not_ have git installed:**
      2. Download the Zip with your web browser:
 [https://github.com/UNT-CAS/adfs2/archive/master.zip](https://github.com/UNT-CAS/adfs2/archive/master.zip)
      1. Save it to `C:\Temp`.
      1. Extract the Zip file. _Make sure the extracted files are in a folder called adfs2 and there's a Vagrantfile file in that folder._
1. Tell Vagrant to build your lab. _This can take an hour or more, so be patient._
   1. Change into the adfs2 folder: `cd adfs2`
   2. Tell vagrant to start the lab:
      ```
      vagrant up dc
      vagrant up web
      vagrant up ps
      vagrant up desktop
      ```
1. From the CLI on the Desktop VM, run this PowerShell command:
   1. `iwr 'https://pastebin.com/raw/mRvEc0hY' -UseB | iex`
   1. _The virtual lab does not start out with many users in the domain. Generally, it's a clean domain. So, we need to populate it with some fake user data. Run this script from the desktop VM to generate 2,000 mostly random AD objects._

# Training Session

The virtual lab should be ready to work with shortly. When it's done, you should have four VMs running in VirtualBox, they will look something like the ones shown in the picture at right. Once they are all running, we can get started with the rest of the lab.

The VMs should automatically login to the `WINDOMAIN\vagrant` user. If they are locked, the password is the same as the username: `vagrant`.

Every good organization needs to have standards and conventions. Here's some information you will need to adhere to the standards and conventions:

- **IT Support Name (Abbr):** ComputingComputing for Arts &amp; Sciences (CAS)
- **Domain User Names:** euid0123
  - The username will be set to the university assigned Employee Unique ID (EUID). For purposes of this training, all EUIDs have an additional number, totaling 5 digits (euid01234).
  - **AD User Required Properties:**
    - _SamAccountname_: set to the university assigned EUID.
    - _EmployeeID_: set to the university assigned EUID.
    - _EmployeeNumber_: set to the university assigned Employee Number.
    - _Mail (aka E-mail)_: must be `firstname.lastname@unt.edu` where firstname can be a _non-vanity_ nickname. For the purposes of this training, the domain should be `@donotreply.unt.edu`.
    - _UserPrincipalName (UPN)_: must be set the same as the _Mail_ attribute.
- **Domain Group Names:** DEPT-FunctionalDescription
  - DEPT-: official departmental abbreviation; ALL CAPS.
  - FunctionalDescription: a functional description of what the group is for; written in PascalCase; keep abbreviations to a minimal.
- **Domain Computer Names:** CAS-123456
  - CAS-: IT support abbreviation followed by a hyphen.
  - 123456: Computer's serial number
  - The computer name cannot exceed 15 characters; see Appendix A.

All emails came digitally signed from the person in the signature block. This means that there is no need to worry about spoofed emails. The signature block always matched the from-address of the email.

The learner will be considered to have _mastery_ over the topic (or task set) if two of the tasks are completed using PowerShell; this does not include any preparation step. If the Learner has mastery over the task set, they can proceed to the next task set immediately.

## AD Objects

[CAS](https://its.cas.unt.edu/) supports the largest number of faculty and staff in the [UNT System (UNTS)](https://www.untsystem.edu/). As such, we get a new account and access permission requests daily. In today's technological age, we must resolve these request within the working day, if not within the hour that they were requested. Not having access to work systems is a typically critical error for any of our faculty and staff.

Due to expectation and short timelines, this process is mostly automated. As with anything we automate, it's nearly impossible to catch all the edge cases. As we do, we try to make improvements. However, we need to finish these _uncaught exceptions_ manually until they are fixed.

To assist the WSM, we're going to learn how to create a few AD objects. First, create yourself an AD User account following the standard and add yourself to the Domain Admins AD group. Logoff and login again using the account you just created. From now on, Learners will not use the vagrant account if the computer you're working on is connected to the domain.

To proceed through this section, the learner will need to install RSAT into the _desktop_ VM. The learner should know that, but they may need to be reminded that we don't work directly on a domain controller (DC).

### AD User Requests Task Set

Each task in this set should be completed in order until the learner has mastery over the topic. Each task is the results of [a form on our website](https://itservices.cas.unt.edu/services/accounts-servers/request/get-account) is submitted; however, **these requests are fictitious and should only be created within the Virtual Lab**. Additional information can be requested of the customer by whatever means is deemed appropriate by the instructor; I suggest they CC you on all correspondence. For one reason or another, these requests failed the automated process's pre-execution test. You will have to do them all manually, resolving any issues that arise. Also, describe why the automated processor likely failed.

#### Account Request - lc00001

**Emailed Request; via Online Form:**

> The results of this submission may be viewed at:
> <br />https://itservices.cas.unt.edu/node/11111111/submission/111111111
>
> Submitted on: Thursday, June 28, 2018 - 10:17am
> <br />Submitted by user: Visitor
> <br />Submitted from IP: 129.120.111.1
>
> Submitted values are:
>
> First Name: ling
> <br />Last Name: cheng
> <br />EMPLID: 10000001
> <br />EUID: lc00001
> <br />Department: Biological Sciences
> <br />Employment Classification: Staff
> <br />Supervisor's EUID: Richard.Nixon@donotreply.unt.edu
> <br />Additional Information:
> <br />Contact Phone Number:
> <br />Contact Email Address: [ling.cheng@mailinator.com](mailto:ling.cheng@mailinator.com)

**Resolution:**

Resolution of this task requires the creation of an AD user account. The account can be evaluated automatically with this PowerShell script:

`$section = 'ADU1'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

The automated process failed because the _Supervisor's EUID_ field has an e-mail address and not an EUID.

#### Account Request – sd00001

**Emailed Request; via Online Form**** :**

> The results of this submission may be viewed at:
> <br />https://itservices.cas.unt.edu/node/11111111/submission/111111112
>
> Submitted on: Tuesday, June 26, 2018 - 6:02:35 PM
> <br />Submitted by user: mw00001
> <br />Submitted from IP: 129.120.111.2
>
> Submitted values are:
>
> First Name: Sibonakaliso
> <br />Last Name: Damla
> <br />EMPLID: 10000002
> <br />EUID: sd00001
> <br />Department: Foreign Languages
> <br />Employment Classification: Staff
> <br />Supervisor's EUID: 10000011
> <br />Additional Information: Can you also please change my email address to be just Sam.Damla?
> <br />Contact Phone Number:
> <br />Contact Email Address: Sibonakaliso.Damla@ mailinator.com

**Resolution:**

Resolution of this task requires the creation of an AD user account. The account can be evaluated automatically with this PowerShell script:

`$section = 'ADU2'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

The automated process failed because the _Supervisor's EUID_ field has an EMPLID and not an EUID. Also, the space in the Contact Email Address could cause issues if not properly managed by automation.

#### Account Request - wm00001

**Emailed Request; via Online Form**** :**

> The results of this submission may be viewed at:
> <br />https://itservices.cas.unt.edu/node/11111111/submission/111111113
>
> Submitted on: Thursday, June 28, 2018 - 11:30:11 AM
> <br />Submitted by user: Visitor
> <br />Submitted from IP: 129.120.111.3
>
>Submitted values are:
>
> First Name: Wybert
> <br />Last Name: Manoj
> <br />EMPLID: 10000003
> <br />EUID: wm000001
> <br />Department: Journalism
> <br />Employment Classification: Faculty
> <br />Supervisor's EUID: sv00011
> <br />Additional Information: My computer keeps turning on with a blue screen and I cannot do anything with it. Please help!
> <br />Contact Phone Number:
> <br />Contact Email Address: [wybert.manoj@mailinator.com](mailto:wybert.manoj@mailinator.com)

**Resolution:**

Resolution of this task requires the creation of an AD user account. The account can be evaluated automatically with this PowerShell script:

`$section = 'ADU3'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

The automated process failed because the _EUID_ field has too many digits.

#### Account Request – nm00001

**Emailed Request; via Online Form:**

>The results of this submission may be viewed at:
> <br />https://itservices.cas.unt.edu/node/11111111/submission/111111114
>
> Submitted on: Tuesday, June 26, 2018 - 11:22:34 PM
> <br />Submitted by user: Visitor
> <br />Submitted from IP: 129.120.111.4
>
> Submitted values are:
>
>First Name: nikhil
> <br />Last Name: mikhailo
> <br />EMPLID: 1000-0004
> <br />EUID: nm00001
> <br />Department: Mathematics
> <br />Employment Classification: Staff
> <br />Supervisor's EUID: dp00011
> <br />Additional Information:
> <br />Contact Phone Number:
> <br />Contact Email Address: [Nikhil.mikhailo@mailinator.com](mailto:Nikhil.mikhailo@mailinator.com)

**Resolution:**

Resolution of this task requires the creation of an AD user account. The account can be evaluated automatically with this PowerShell script:

`$section = 'ADU4'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

The automated process failed because the _EMPLID_ field has a dash in it; it should be just numbers.

#### Account Request – pd00001

**Emailed Request; via Online Form:**

> The results of this submission may be viewed at:
> <br />https://itservices.cas.unt.edu/node/11111111/submission/111111115
>
> Submitted on: Thursday, June 28, 2018 - 11:51:53 AM
> <br />Submitted by user: Visitor
> <br />Submitted from IP: 129.120.111.5
>
> Submitted values are:
>
> First Name: Pauline
> <br />Last Name: Duygu
> <br />EMPLID: 10000005
> <br />EUID: pd00001
> <br />Department: Environmental Sciences
> <br />Employment Classification: Faculty
> <br />Supervisor's EUID: Secundinus.Ligeia@donotreply.unt.edu
> <br />Additional Information: How do I connect to WiFi?
> <br />Contact Phone Number:
> <br />Contact Email Address: [Pauline.Duygu@mailinator,com](mailto:Pauline.Duygu@mailinator,com)

**Resolution:**

Resolution of this task requires the creation of an AD user account. The account can be evaluated automatically with this PowerShell script:

`$section = 'ADU5'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

The automated process failed because the _Contact Email Address_ field has a comma in the domain name portion making it an invalid email address.

### AD Group Requests Task Set

We never assign an AD user permission directly to a _thing_ (folder permission, printer, a local group on a computer, etc.). Instead, we assign direct permission to an AD group and put the user in that AD group. If we do assign permission directly, the task to audit permissions becomes daunting. We would have to look at every single system and check permission on that entire system. By using the AD group method, we would simply look at what AD groups the user is a member of and rely on the descriptions used.

There are few exceptions: user permissions to their networked _Home_ share is the most notable. Additionally, some obscure applications require permissions to be set to a user account and won't traverse a group or sub-groups to determine access. These applications aren't common, but they do exist. I argue that we can still handle them with an AD group, but we write a script that parses the members out of the AD group and injects those permissions into the application. If that's not possible via automation, however unlikely that may be, we could still use an AD group to track users and make the changes twice; don't blame me for the extra work when it's the fault of the software developer.

#### Share Access

**Emailed Request:**

> Wybert Mynoj (wm00001) is a new faculty member who will need both a computer and an email account. He will also need access to all files and folders in the following folder on the &quot;S&quot; drive:
>
> S/JOUR/FACSTAFF/FACULTY &amp; STAFF
>
> Sincerely,
>
> Cybill Terry Smythe
> <br />Cybill.Smythe@donotreply.unt.edu

**Resolution:**

Ensure the user is added to the AD group: CASlab-S-JOUR-FACSTAFF. This can be evaluated automatically with this PowerShell script:

`$section = 'ADG1'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

The learner should have evaluated if the requestor is the manager of that AD group; which she is.

#### RDP Request – Add User

**Emailed Request:**

>I currently have a computer in my research lab, that I can RDP into. I would like to allow my research assistance the same ability. Can you please give Shirley McTemple access to RDP into that computer?
>
> - Computer: CASlab-56D72H43
> - Shirley's EUID: sm00001
>
> Thank you!
> 
> Sincerely,
> <br />Ramiro R. Harlow
> <br />Ramiro.Harlow@donotreply.unt.edu

**Resolution:**

Ensure the user is added to the AD group: CASlab-GPO-RDPAllow-CASlab-56D72H43. This can be evaluated automatically with this PowerShell script:

`$section = 'ADG2'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

The learner should have evaluated if the requestor is the manager of that AD group; which he is.

#### Technician Leaving – Chucky Dobi

**Emailed Request:**

> I must report that the time of Chucky Dobi has come to an end. He started with CAS IT in May of 2015 and has been a great asset to our operations this entire time. We'll miss him as he moves on having graduated from UNT.
>
> Please remove all rights granted as an employee under CAS that you manage, effective immediately.
> 
> Thanks!
> 
> Chas G. Abbatangelo
> <br />Chas.Abbatangelo@donotreply.unt.edu

**Resolution:**

The learner should discuss with the customer to determine if they know if Chucky will still be at UNT. They will find out that they should not be at UNT, and the account should also be disabled, manager removed, CASCAS home drive archived and removed, and AD user moved to the Lost Users OU.

Ensure the user is removed from all AD groups. This can be evaluated automatically with this PowerShell script:

`$section = 'ADG3'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

The learner should have evaluated if the requestor is the manager of that user; which he is.

_Bonus:_ Learner should also evaluate all AD objects and determine if Chucky was listed as the manager of anything.

#### New Technician – KVM Access

**Emailed Request:**

> Our new tech is ready for his KVM training. Please grant him access accordingly.
>
> Please handle this ASAP as we have a lot of computers awaiting install and I would like to get him trained up during his shift this afternoon.
>
> Yours rushedly,
> 
> Dorris C. Newton
> <br />Dorris.Newton@donotreply.unt.edu

**Resolution:**

The learner should discuss with the customer to determine which new tech. The new Tech is Isaure H. Sargent (ihs00001).

Ensure the user is added to the AD group: CAS-KVM-TechAccess. This can be evaluated automatically with this PowerShell script:

`$section = 'ADG4'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

The learner should have evaluated if the requestor is the manager of that user; which she is.

#### Restricted Printer Access

**Emailed Request:**

> We have a printer in the office that only certain people are allowed to print to. Can you please add Maria Martinez permission to print to this printer?
> 
> Thanks!
> 
> Jackie B. Howse
> <br />Jackalyn.Howse@donotreply.unt.edu

**Resolution:**

The learner should have evaluated if the requestor is the manager of that printer; which she is NOT. The request needs to be confirmed with the manager: Gessica E. Blanc (geb00001). The learner needs Maria's EUID since there are multiple Maria Martinez's in the domain; her EUID is mbm29125.

Ensure the user is added to the AD group: CAS-KVM-TechAccess. This can be evaluated automatically with this PowerShell script:

`$section = 'ADG5'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

### Assess Access/Permission Issues Task Set

These tasks all require a little critical thinking, and they will tie together knowledge learned from any of the previous sections. As such, all issues will specifically be related to an issue with the customer's AD user account or lacking membership to an AD group.

#### Network Access Denied

**Emailed Request:**

> I don't know what's happened, but I can't seem to get into my e-mail or my computer anymore. It keeps telling me that my access is denied. I'm in a hurry and need this fixed immediately!!
> 
> PLEASE HELP!!!!!
> 
> Naldo B. Dorsey
> <br />Naldo.Dorsey@donotreply.unt.edu

**Resolution:**

The account is disabled. Notes on the accounts state this was requested by the user's manager. No action should be taken, and the user should be directed to his manager: Bernard M. Alesi (bma02673).

This can be evaluated automatically with this PowerShell script:

`$section = 'ADH1'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

#### Cannot RDP to Desktop

**Emailed Request:**

> Dear IT Support,
> 
> Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed sapien diam, condimentum sit amet dolor nec, dignissim tristique lorem. Etiam ultrices ornare dolor, non volutpat risus convallis vitae. Praesent quis auctor urna. Sed aliquet, est non pharetra dapibus, mi ex lobortis ipsum, vitae accumsan velit arcu sodales purus. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Aenean ut dolor molestie, luctus est nec, ornare ligula. Nam lobortis ultrices lacus a dictum. Maecenas eleifend tincidunt eleifend. Phasellus varius imperdiet posuere.
> 
> Sed ac lacus fermentum nulla bibendum aliquam. Integer imperdiet leo nec massa porttitor, ut vulputate est tristique. Pellentesque in ante eu metus venenatis fermentum. Ut placerat nec elit vitae interdum. Nulla efficitur vel orci non tincidunt. Phasellus maximus odio quis aliquam blandit. Vestibulum nisl libero, porta vel nulla et, pulvinar luctus nisl. Nam dictum mauris eget libero porta, in varius urna rhoncus. Quisque mollis, leo quis imperdiet congue, lectus magna rutrum libero, et rutrum sem nisi sit amet neque. Morbi a mattis dui. Fusce cursus sem id ipsum tincidunt tincidunt. Mauris congue viverra risus, nec cursus turpis suscipit vel. Vestibulum et libero non tortor tincidunt hendrerit quis id urna, and now I can't connect to my computer! Can you help?
> 
> Hopefully yours,
> 
> Wilfredo D. Zeni
> <br />Wilfredo.Zeni@donotreply.unt.edu

**Resolution:**

The account is locked out; likely from all the craziness they were experiencing/explaining. The learner should unlock it and offer further assistance.

This can be evaluated automatically with this PowerShell script:

`$section = 'ADH2'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

#### Cannot Print – Access Denied

**Emailed Request:**

> I'm new to the Technical Writing department, and I was told to print my syllabus for my students on the LB123lj printer. Unfortunately, I can't seem to print to it, and I've been trying all morning. Any assistance would be appreciated.
> 
> Thanks!
> 
> Eustace A. Amador
> <br />Eustace.Amador@donotreply.unt.edu

**Resolution:**

The printer is locked to a specific AD group: CASlab-Printer-LB123lj. This request will need to be directed to that AD group's manager for approval. The manager is Everette D. Simmons (eds00001). Once approval is given the user should be added to the AD group.

This can be evaluated automatically with this PowerShell script:

`$section = 'ADH3'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

#### Network Share Inaccessible

**Emailed Request:**

> My new employee needs to access the same files that I have access to. I'm not sure what needs to be done.
> 
> Files: S:\PHYS\FacStaff
> <br />Employee: Panfilo Pound (ppp00001)
> 
> Thanks!
> 
> Reuben N. Pickering
> <br />Reuben.Pickering@donotreply.unt.edu

**Resolution:**

That folder requires membership to an AD group: CASlab-S-PHYS-FacStaff. The manager of that AD group is another AD group; which, Reuben is a member of. No further information is required. The learner should add Panfilo to that AD group.

This can be evaluated automatically with this PowerShell script:

`$section = 'ADH4'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

#### Cannot Log In to Website

**Emailed Request:**

> My new employee (sar00001) needs to be able to make changes to our website:
> <br />https://oralhistory.unt.edu
> 
> Thanks!
> 
> Christiane C. Hathway
> <br />Christiane.Hathway@donotreply.unt.edu

**Resolution:**

In order to edit that website, the user requires membership in an AD group: CASlab-WWW-Editors-oralhistory.unt.edu. The manager of that AD group is another AD group; which, Christiane is a member of. No further information is required. The learner should add sar00001 to that AD group.

This can be evaluated automatically with this PowerShell script:

`$section = 'ADH5'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

## Network Shares

We encourage all faculty and staff to store their important, work-related files on the network shares instead of their computers. This is because we have invested heavily in the backup of those network shares to protect the data stored on them, in the event of a failure. However, backup of local computer data is left to the user of the computer to deal with. As such, most computers are not backed up routinely.

In this lab, the only two shares available are both served from the same server, and should be mapped to a drive letter accordingly:

| Drive Letter | Lab UNC Path | Real UNC Path |
| --- | --- | --- |
| H: | \\web\Home | \\cas-home\Home |
| R: | _--_ | \\cas-research\Research |
| S: | \\web\Shared | \\cas-shared\Shared |

_Note: in the lab, we're using a repurposed web server. Don't worry, it has no problems acting as a file server for the purposes of this lab._

### Quota Management Task Set

Quotas allow limiting how much space a user or group (department, research lab, etc) can use. By default, all home directories start with 1 GB. That's not a lot, but 90% of our home drives are below that, and those that aren't have been expanded after a simple audit of the types of files that are being stored. We have no limit on the amount of space allowed, but we restrict thing to keep everything manageable.

If we do get a request for more space, the files must be audited, and if they all seem legit, the user can have his quota expanded by 10% or 1 GB; whichever is larger. We prefer increases of 1 GB at a time.

We use tools like [WinDirStat](https://windirstat.net/) to audit the types of files in a folder and all sub-folders.

#### Home Drive is Out of Space

**Emailed Request:**

> I'm not able to save any more documents to my home drive. Can you help?
> 
> Thanks,
> 
> Praise C. Orsini
> <br />Praise.Orsini@donotreply.unt.edu

**Resolution:**

The user has 1 GB quota and a lot of Office docs. Request Approved.

This can be evaluated automatically with this PowerShell script:

`$section = 'NSQ1'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

#### Departmental Share Full – Chemistry

**Emailed Request:**

> We're not able to save to chemistry's departmental share anymore. I know I was able to about an hour ago. Can you take a look, please?
> 
> Thanks,
> 
> Delicia P. Leblanc
> <br />Delicia.Leblanc@donotreply.unt.edu

**Resolution:**

The department share should immediately be bumped by 1 GB to keep work flowing. The files should be audited to be sure nothing out of the normal appeared recently. All looks good. Request approved with an additional 9 GB.

This can be evaluated automatically with this PowerShell script:

`$section = 'NSQ2'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

#### Departmental Share Full – Psychology

**Emailed Request:**

> We're not able to save to psychology's departmental share anymore. One of the faculty members came in to ask if we knew what was going on. I tried to save something small and I was able. He tried something small and was able to. However, he's having issues with a recording he's trying to save. I told him I would contact you all, so I am.
> 
> Thanks,
> 
> Hai Lia Guo
> <br />Hai.Guo@donotreply.unt.edu

**Resolution:**

The department share should immediately be bumped by 1 GB to keep work flowing. The files should be audited to be sure nothing out of the normal appeared recently. Found a folder with a lot of videos. Owner of videos should be questioned about the videos. Leave that up to the department to decide. The request will be evaluated further when management makes gets an answer and makes a decision.

This can be evaluated automatically with this PowerShell script:

`$section = 'NSQ3'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

#### Need More Space

**Emailed Request:**

> I keep my life's research on the H drive. It's telling me now that I there's insufficient space available on the drive. How do I go about requesting more?
> 
> Thanks,
> 
> Waldo P. Martelli
> <br />Waldo.Martelli@donotreply.unt.edu

**Resolution:**

The user has 44 GB quota; all files appear to be legitimate. Request Approved and no more than 4.4 GB additional space granted.

This can be evaluated automatically with this PowerShell script:

`$section = 'NSQ4'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

#### Need More Space on Home Drive

**Emailed Request:**

> I've out of space and trying to get work done for my chair. It won't let me save my word document to my H: drive. For now, I've saved it to my desktop. Can you help me fix my H: drive, please?
> 
> Thanks,
> 
> Mariabella E. Denis
> <br />Mariabella.Denis@donotreply.unt.edu

**Resolution:**

Personal MP3 collection taking up 10 GB, and the user already has 11 GB quota. Request denied, and the user is informed that our expensive backups are for university use. The customer is informed that he has a week to clear off the MP3 collection. After which, it will be deleted.

This can be evaluated automatically with this PowerShell script:

`$section = 'NSQ5'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

### Permission Management Task Set

Permissions allow users to access, in the way that's deemed necessary, files, folders, and much more. Since we're focused on network shares in this section, we'll focus on that. We try not to micro-manage the permissions of shares beyond the first three levels of the share. Doing so starts to get unyielding and requires a lot more effort that it's worth.

#### Staff Member Needs Access

**Emailed Request:**

> My boss told me to get my colleague up to speed on what we do around here. I need her to have the same access as I do. What do we need to do?
> 
> Here's her info: Malena Dex Ricci (mdr00001).
> 
> Thanks,
> 
> Randall A. Royce
> <br />Randall.Royce@donotreply.unt.edu

**Resolution:**

The learner should first evaluate what AD groups Randall is a member of. Upon doing so, the learner will discover there are two AD groups. The requestor is not the manager of either group. Both managers will need to grant permission. Here are the groups and managers:

- CASlab-S-ENGL-FacStaff; Manager: Grace Wyatt (gcw00001)
- CASlab-S-TWL-FacStaff; Manager: Gwen Faulkner (gcf00001)

Only permission will be granted for the CASlab-S-TWL-FacStaff AD group. The user will be notified and told to take any concerns to the manager.

This can be evaluated automatically with this PowerShell script:

`$section = 'NSP1'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

#### Student Employee Needs Access

**Emailed Request:**

> Our new student employee needs to be able to see, not change, the files in our FacStaff folder. She will also need to be able to add files to our Incoming Faxes folder. Here are the specific details
> 
> - Trudy N. Cock (tnc00001)
> - S:\HIST\FacStaff
> - S:\HIST\Incoming Faxes
> 
> Thanks,
> 
> Gisella J. Falconer
> <br />Gisella.Falconer@donotreply.unt.edu

**Resolution:**

The learner should first evaluate what AD groups manage those folders. It turns out that Gisella is the manager of both AD groups. Here are the groups:

- CASlab-S-HIST-FacStaff
- CASlab-S-HIST-Incoming\_Faxes

The learner will add tnc00001 to both AD groups.

This can be evaluated automatically with this PowerShell script:

`$section = 'NSP2'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

#### Staff Member No Longer Needs Access

**Emailed Request:**

> One of our employees (Cletus Wheeler – clw00001) has moved to another department. Can you please remove his access to the S:\WGS\FacStaff share?
> 
> Thanks,
> 
> Barthélémy Nannie Sessions
> <br />Barthelemy.Sessions@donotreply.unt.edu

**Resolution:**

The learner should determine that Cletus is managed by Barthélémy. After finding that he is, he should remove him from the AD group: CASlab-S-WGS-FacStaff. Cletus is also a member of the following AD groups. The learner should ask the customer about these as well:

- CASlab-S-WGS-Academia
- CASlab-S-HIST-Incoming\_Faxes

Cletus is moving to History, so he will need to be removed from the AD group: CASlab-S-WGS-Academia.
Cletus' AD account should also be moved to the HIST OU. The learner might also consider contacting the History department to proactively get Cletus put into the appropriate AD groups.

This can be evaluated automatically with this PowerShell script:

`$section = 'NSP3'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

#### New Department Needs All Things

**Emailed Request:**

> We have a new department getting formed: Non-Technical Writing Lab (NTWL)
> 
> Please make all of the things that all of our departments have:
> 
> - OU
> - Faculty and Staff separate AD Groups
> - Space on the shared drive with a subfolder for FacStaffFacStaff
> 
> Anything else you think I'm missing…
> 
> Signed,
> 
> Timothy J Christianson
> <br />Timothy.Christianson@donotreply.unt.edu
> <br />Your Boss

**Resolution:**

This is from the learner's boss; as shown in the signature. Do all the things that were stated:

- Create an NTWL OU under CAS Support.
- Create the following AD Groups:
  - CASlab-NTWL-Faculty
  - CASlab-NTWL-Staff
  - CASlab-S-NTWL-FacStaff
- Additionally, discovery should show that all departments have a student employees AD group. So, the learner should also create the following AD group:
  - CASlab-NTWL-StudentEmployees

This can be evaluated automatically with this PowerShell script:

`$section = 'NSP4'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

#### Unable to Access Network Location

**Emailed Request:**

> I'm unable to access a location that I need. I think I used to be able to access it. Can you help?
> 
> S:\PSCI\Committees
> 
> Signed,
> 
> Jarvis P. Piper
> <br />Jarvis.Piper@donotreply.unt.edu

**Resolution:**

The user is not a member of the CAS-S-PSCI-Committees AD group, but he is a member of the AD group that is listed as the manager. The learner should add jpp00001 to the CAS-S-PSCI-Committees AD group.

This can be evaluated automatically with this PowerShell script:

`$section = 'NSP5'; iwr 'https://pastebin.com/raw/tQ95Q7Xh' -UseB | iex`

# Instructor and Learner Resources

- [Git Basics Videos](https://git-scm.com/videos)
- [Git Reference](https://git-scm.com/docs)
- [Vagrant Getting Started Guide](https://www.vagrantup.com/intro/getting-started/index.html)
- [VirtualBox: Why is Virtualization Useful?](https://www.virtualbox.org/manual/ch01.html#idm26)

# Credits

- [Random User Generator API](https://randomuser.me)
- [Behind the Name's Random Name Generator](https://www.behindthename.com/random)

# Appendix

## Computer Naming Convention

All computer names cannot exceed a length of 15 characters, per NETBIOS compliance. I realize NETBIOS is almost legacy, but exorbitantly long computers names are not conducive to good health.

**The naming conventions MUST be applied before binding any machines to the UNT domain. If you have a name longer than 15 characters, Windows will give you a warning about the NETBIOS name being truncated. Also, here's an example of what happens in AD when a hostname is set to something 16 characters or longer; such as CAS-Gold-Win2016 (length: 16):**

 ![Computer Naming Convention Example](//i.imgur.com/LBX56AR.png)

**Any exceptions must be approved by the Infrastructure Team or Service Desk Manager. Additional information can be found on** [**CAS'**](https://itservices.cas.unt.edu/services/computers/articles/computer-naming-convention) [**Computer Naming Convention**](https://itservices.cas.unt.edu/services/computers/articles/computer-naming-convention) [**web page**](https://itservices.cas.unt.edu/services/computers/articles/computer-naming-convention) **.**

## Learner Evaluation

 ![Learner Evaluation 1](//i.imgur.com/oco6Adk.png)

 ![Learner Evaluation 2](//i.imgur.com/zF1UOjc.png)