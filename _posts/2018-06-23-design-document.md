---
layout: post
title: Windows Server Administration - Design Document
img: //i.imgur.com/iye3IS2.jpg
author: Raymond Piller
comments: true
tags:
- LTEC5210
- Information Design
- ProjectA
---
# ­­TAPF

|||
| --- | --- |
| Topic | Roles and Responsibilities of the Windows Server Manager (WSM). _Familiarization with the daily tasks of the WSM; in order to allow co-workers of the same expertise but different skill set be cross-trained for coverage when the WSM is out of the office for an extended period of time; such as on vacation._ |
| Audience | System Administrators on the Infrastructure Team working at [Computing for Arts and Sciences (CAS)](https://its.cas.unt.edu) here at the [University of North Texas (UNT)](https://unt.edu). The students/learners in this training are seasoned veterans in their discipline of I.T. administration; such as: Windows workstation management, Linux server management, Linux workstation management, Apple workstation management, and process and workflow automation; to name a few. The learners are Tier-5 support for helpdesk. Some learners will already be familiar with some or most of the tasks in this training, but only the WSM is considered an expert in all the tasks. This is individualized, self-paced training for a small team, so the audience size will likely only ever be one or two learners at a given time. Additionally, all or part of this training may be able to be used to train Tier-3 and 4 technicians to advance along their desired career path; this is not the intended audience and may require reworking of the training regimen. |
| Purpose | Train colleagues in the day to day work of the WSM; including request handling, VM management, printer management, AD management, network share management, and Windows server management. We routinely get requests for new software or hardware support that we have never seen before. Likely, we did not pre-approve the purchase, and now the request has been approved above our heads. We are told to figure it out. In cases like this, there is no Subject Matter Expert (SME) on premises and we must turn towards the internet and our vast experience/expertise with tinkering systems into functioning properly. The learners will be guided through implementation of several real-life examples from our request history. They will be expected to navigate through the lack of information to find out what the customer is trying to accomplish. Upon completion, learners will be able to fulfill 90% of requests while the SME (Windows Desktop Manager) is unavailable. Failure to complete tasks will result in more remedial, formalized training on the topic at hand. |
| Format | This self-paced asynchronous training will utilize: online documentation, videos, and practical exercises that invoke meaningful and active learning. Real-life examples will be pulled from our archives, in the form of an emailed in request. These examples will be used to facilitate the learning experience to show the learners how a seemingly simple request unravels into a multi-phase solution requiring collaboration with other teams around campus. The learner will be allowed to question the customer for more details, and |

The training is designed to be asynchronous to mimic the way requests come into our office. When we get a request, there&#39;s no a lecturer at the front of the office telling us how to address that request. If the request is for software we&#39;ve never heard of before, we start by searching for that software on the internet and seeing if it&#39;s well-documented. We then assert what the software is truly used for, and we assess what the customer is trying to accomplish. We then correlate the request to the software or other software we already support, and we present an alternative solution if its available. This requires searching our internal documentation and communicating with our colleagues to determine if we already support something that provides an identical or comparable service/solution.

This course will be no different. The learner will assume the role of SME (the WSM) and will figure it out. Searching the internet, documentation, existing requests, and communicating with the customer and colleagues are all expected parts of this training.

This lesson will be designed as a one-week training session to allow colleagues and new employees familiarity with the roles and responsibilities of the WSM from a technological perspective. It will be an online asynchronous course that will discuss various problems encountered in the field, as well as explore effective methodologies to implement solutions to issues that arise for the WSM. There will be a final formative and summative assessment at the end of the term.

# Problem

When the WSM wants to take time off work, most of his responsibilities wait for him to return. This fact remains in the back of his head for the duration of his vacation, and he cannot truly enjoy the time off knowing he will face a heavy load when he returns to the office. More importantly, it is not okay for us to tell our customers that they must wait for him to return to get a seemingly simple request fulfilled.

There is no existing official training regimen established as part of onboarding or cross-training. We are expected to cover one another using past knowledge and experience to resolve issues and fulfill requests. Any knowledge currently received is &quot;learn as you go.&quot; The creation of this program will allow employees without any previous experience with Windows servers to temporarily field requests and resolve issues while the WSM is engaged elsewhere.

# Learning Expectations

## Lesson Goals and Objectives

1. **The Learner Will (TLW) create and manage VMware VMs.** This is the core of the work done by the WSM.
  1. **Use virtual lab to manage VCenter.** We don&#39;t play or test on production systems.
    1. **Create virtual lab via pre-created**  **Vagrantfiles****.** This will create all the necessary servers for working through this training. This process _should be_ automated after starting but could take several hours to complete.
  2. **Manage VM Snapshots.** Creating a VM snapshot is crucial for testing a configuration and being able to easily and instantly revert those changes if something goes wrong. We create snapshots before touching a production server for any reason. Unfortunately, too many snapshots can also cause IOPs issues. As such, we must ensure we delete snapshots that are no longer needed.
  3. **Manage VM Disk expansion.** To keep our systems running lean, we configure the servers with a minimum amount of local storage. When allocating storage to a server, we [prefer fixed disk size, as opposed to dynamic](https://communities.vmware.com/thread/88747). The performance hit for a dynamic disk is minimal when you&#39;re running only a few servers. However, when there are have thousands of servers all running dynamic disks, the [IOPS](https://en.wikipedia.org/wiki/IOPS) performance hit adds up. Occasionally, the size of the disk exceeds what we originally planned and needs to be expanded. This is usually a service outage event, and not a change that can wait a week for the WMS to return for vacation.
2. **TLW create and manage network printers.** The WSM manages the Windows Print Server (WPS) which allows centralized control of network accessible printers.
  1. **Set up new printers.** We often get need to setup new printers as our fleet is expanded by departmental growth. Sometimes, those printers are replacing older printers, but are a different brand and need different drivers associated with it; transferring the name of the replaced printer to the new printer.
    1. **Add them to the network.** Unlike most devices on the network, printers require a static IP address. This needs a specific configuration in our DHCP server. This process has been automated, but familiarity with this step is a must.
    2. **Add them to the Windows print server.** In order for the WPS to control the new printer, it must have several things configured on the server: IP, port, driver, and the printer object. After that, it can be shared to computers that we manage, and the computers print to the server and the server hands the job off to the printer.
    3. **Manage security, locking the printer down.** The printers themselves are typically wide open, and they need to be locked down. Locked down includes allowing the printer to only communicate on the network to the WPS and change the remote administrative password(s).
    4. **Manage print codes issuing.** Some printers support the use of a print code that&#39;s required for printing. This is an enterprise feature and allows print jobs to be associated to a print code, that&#39;s assigned to a specific person. This is typically for accounting purposes, and required by some departments for some printers.
    5. **Manage scan to email/network-share.** Multi-Function Printers (MFPs) can do more than just printing; such as: scanning, binding, stapling, and more. Since it&#39;s a network printer, we typically need to configure an end-point for the scanned documents. This may be one or more email addresses or a network storage location that acts as a drop box. Either way, the options are typically controlled by the WPS and need to be configured by the WSM.
    6. **Evaluate printing functionality from Windows and OS X.** Now that everything is configured, test the work that you did. Simple print a test page from the two main desktop operating systems that we support: Windows 10 and OS X.
3. **TLW create and manage Active Directory (AD) Accounts and Groups.** CAS supports the largest number of faculty and staff in the [UNT System (UNTS)](https://www.untsystem.edu/). As such, we get new account and access permission requests daily. In today&#39;s technological age, we must resolve these request within the working day, if not within the hour that they were requested. Not having access to work systems is a typically critical error for any of our faculty and staff.
  1. **Create new AD accounts.** If we have a new faculty or staff member, we usually have their accounts create long before they get to campus. This is through years of process optimization and automation as we get notifications telling us about new hires. Occasionally, all the pieces to the puzzle don&#39;t fall into place and manual intervention is required. In this event, the WSM needs to intimately familiar with the account creation script and how to troubleshoot it.
  2. **Assess access issues.** Almost daily, we get a call or an email telling us that someone can&#39;t access something. Our job isn&#39;t to just grant those rights as they come in. Our job is to determine if the requestor is the has the authority to make the request and if not ensure the request is routed to the proper authority. After that, granting access is typically as easy as adding a user to a new AD group. If not, we need to ensure that it&#39;s configured that way to uphold he standards that should have already been in place.
  3. **Create new AD groups.** Occasionally, requests come in for granting more specific permissions to a subset of customers to a more specific task, server, or service. These permission changes need to be granted using the standards that have been implemented for the relevant task, server, or service. Familiarity with where these standards are documented and how to apply these standards are required.
4. **TLW manage network shares.** Networks storage locations are a centralized and backed up file storage spaced. These locations are often used for shared documents and data repositories. Additionally, there are private locations available to every user that offer a limited amount of backed up storage.
  1. **Manage quotas.** Quotas are designed to prevent users from filling up network storage by implementing a maximum usage size. This quota is often exceeded and if the user calls to request more storage, we audit usage and grant additional storage if usage seems justifiable. This political barrier just helps us ensure we&#39;re not storing and backing up a customer&#39;s entire music collection.
  2. **Manage permissions.** Obviously, users need proper permissions to either just see files in a location or make changes to those files. It&#39;s important to grant permissions with the principal of least privilege in mind. As an educational institution, we fall under FERPA regulations, and must also be familiar with the types of data that is intended on being accessed.
5. **TLW be able to find, review, and resolve issues in a timely manner.** Just like work expectations, all tasks must be resolved in a timely fashion. Some tasks will be more complex, requiring more time. These tasks will have additional time afforded to the solution.
6. **TLW will be able to communicate technical information in a clear, non-technical manner.** Just like with a real request, the solution must be communicated to the customer in a clear and concise manner; without the use of unnecessary technical jargon.

## Lesson Components

### Learners

- **Performance computer system access.**
  - The learner will need to run a virtual lab on their computer. The lab will be configured with Vagrant.
    - Multiple VMs (at least two) acting as VMware ESX Hypervisors
    - 60-Day VSphere/VCenter will be installed for lab
- **Network/internet access.**
  - Searching the internet (aka googling) for assistance is encouraged, but the learner should start with internal documentation.
- **Proficient knowledge of:**
  - AD objects. These acronyms should be second nature: DN, FQDN, GPO, GPP, DC, etc.
  - Network design and communication protocols. These acronyms should be second nature: DNS, DHCP, TCP, UDP, IPSEC, TCP/IP, VLAN, MAC, etc.
- **Familiarity with:**
  - OTRS Ticketing System
  - VMware Web Management Console
  - Principal of Least Privilege
  - Coding: PowerShell, VBScript, and AutoIt.
- **Troubleshoot their own computer issues.**

### Instructors

In addition to the expectations of the learners, the instructors are expected to have the following qualifications:

- **Expert knowledge of:**
  - VMware VM configuration.
  - Windows Servers.
  - Active Directory.
  - Group Policy Objects and Group Policy Preferences.
  - Printer Management.
  - Network Share Management.
- **Proficient knowledge of:**
  - PowerShell, PowerShell Best Practices, and PowerShell Coding Standards.

# Learning Activities

There will be an introductory video and/or documentation that must be reviewed before any tasks are started. Learner should discuss clarification points on anything before the tasks begin. Once the tasks begin, the instructor will assume the role of the customer, and the leaner will assume the role of the WSM.

Each task will have a basic request that will require the learner to communicate with the customer to get clarification. Proper communication skills must always be exhibited. Each task has a scriptable solution equivalent. At least 25% of all work done must be done using PowerShell (or another scripting language).

Learner will submit screen recording to the instructor for each task completed. Screen must be recorded from the time the learner reads the request until the moment before linking the recording into the email submitted to the instructor. All internet searches should be done within view of the screen recorder. Learner will submit a compressed archive (such as ZIP or 7zip) of any code written to complete the task. The training environment will be saved in its state and review of the completed task will be done before the learner can proceed to the next task.

- Learner will use the _Vagrantfiles_ to create their learning and testing environment. (1.a.i)
  - Download and install Vagrant.
  - Download and execute the _Vagrantfiles_ for this course; _this could take several hours to complete and should be completed before the training begins_.
  - Download and install a Screen Recorder for use when working on a task.
- Learner will review introductory videos and documentation to gain a broad understanding of the work done by the WMS.
  - After the introduction, the learner will get face-to-face time with the instructor to ask any questions and get clarification on anything that wasn&#39;t clear in the introduction.
  - After the face-to-face time, the instructor will assume the role of the customer, and the learner will assume the role of the WSM. Instructor and learner respective roles will be assumed during assessment of each task.
- Learner will be given a new infrastructure (Windows Server) request to look over. (1)
  - Clarification questions can be asked of the customer (the instructor) via e-mail.
- Learner will fulfill the request and provide customer with usage information in a formal e-mail. (1, 6)
- Learner will be given a new printer request to look over. (2)
  - Clarification questions can be asked of the customer (the instructor) via e-mail.
- Learner will fulfill the request and provide customer with usage information in a formal e-mail. (2, 6)
- Learner will be given a new AD Learner account and group request to look over. (3)
  - Clarification questions can be asked of the customer (the instructor) via e-mail.
- Learner will fulfill the request and provide customer with usage information in a formal e-mail. (3, 6)
- Learner will be given a new network share request to look over. (4)
  - Clarification questions can be asked of the customer (the instructor) via e-mail.
- Learner will fulfill the request and provide customer with usage information in a formal e-mail. (4, 6)
- Learner will be given several real examples of simple and complex requests that dive deeper into the skills learned throughout this training. (4, 6)
  - Clarification questions can be asked of the customer (the instructor) via e-mail.
  - Will resolve (if applicable) the request/issue and communicate technical information back to the customer in a clear, non-technical manner.

# Assessment

The learner will have the opportunity to e-mail back and forth with the customer (instructor) to clarify anything; ensuring a firm understanding of the requirements. During the tasks, the internet is available for assistance. All searching should be done within view of the screen recorder; we want to understand how the solution was obtained as well as if the solution is correct. The instructor will review the screen recordings made by the learner for each task to see how the task was completed and ensuring the task was fully completed. The screen recordings will also assist the instructor on assessing knowledgeability and whether the learner should get a supplemental task of the same type.

All the tasks require a specific solution; however, there are often several ways to implement a solution. If that solution works without security vulnerabilities, then the task was successful. If the task works, but with security vulnerabilities, we need to address that with the learners, and they may be given a follow-up task. All learners are seasoned I.T. Administrators, so they should be able to think about the security implications of their decisions without being walked through the thought process in this training.

At least 25% of all work done must be done using PowerShell (or another scripting language). The learner will earn a free custom pizza, courtesy of the instructor, if 100% of all work is done using PowerShell.

The SME will determine if the tasks are done to completion. However, the Team Manager will be the final judge on whether the learner is fully cross-trained, or if the learner requires remedial training.

# Evaluation

If most learners can complete the assigned tasks, then I know the instructional design was successful. If there is a task that cannot be regularly completed, then I have an area for improvement. I expect to have to tweak the timeline, but I&#39;ve deliberately kept it short to add pressure to the task.

The training is task-based, and the goals/objectives can be measured by the completeness of tasks. The learners will have completed the task successfully if the outcome of all tasks is satisfactory and result in usable and secure implementation of the requested service. If we consistently have goals/objectives not met, then maybe this training expects to much knowledge in advance.

There are several potential areas of improvement that need to be closely monitored to determine if adjustments need to be made to allow for a more comfortable training experience:

- How much time did it take to complete the task?
  - Was the solution too rushed because of time constraints?
  - Was the student focused more on completion and less on solution exploration?
- Are the goals met to 100% satisfaction?
  - Do we need to spend more time discussing how to pull &quot;what are you trying to accomplish&quot; out of a customer?

# Timeline

The training will be asynchronous, but it is expected to take no longer than a week. The average amount of time should be 15 hours; three hours per day. After the first day, a basic understanding of all goals is expected. The second day will start with a one-hour session with the instructor; the instructor is also the SME. This will confirm a firm understanding of all training goals. After day two&#39;s introduction, the rest of the training will occur asynchronously; at the learner&#39;s pace.

- Learner will use the _Vagrantfiles_ to create their learning and testing environment. (1.a.i) (30 minutes; Task is automated and might take several hours to complete.)
- Learner will review introductory videos and documentation to gain a broad understanding of the work done by the WMS. (3 hours)
- The learner will get face-to-face time with the instructor to ask any questions and get clarification on anything that wasn&#39;t clear in the introduction. (30 minutes)
- Learner will be given a new infrastructure (Windows Server) request to look over. (1) (30 minutes)
- Learner will fulfill the request and provide customer with usage information in a formal e-mail. (1, 6) (2 hours)
- Learner will be given a new printer request to look over. (2) (30 minutes)
- Learner will fulfill the request and provide customer with usage information in a formal e-mail. (2, 6) (1 hour)
- Learner will be given a new AD account and group request to look over. (3) (30 minutes)
- Learner will fulfill the request and provide customer with usage information in a formal e-mail. (3, 6) (1 hours)
- Learner will be given a new network share request to look over. (4) (30 minutes)
- Learner will fulfill the request and provide customer with usage information in a formal e-mail. (4, 6) (2 hours)
- Learner will be given several real examples of simple and complex requests that dive deeper into the skills learned throughout this training. (4, 6) (3 hours)