.. title:: Nutanix Core Workshop

.. |br| raw:: html

    <br>

.. toctree::
  :maxdepth: 2
  :caption: workshop
  :name: _workshop
  :hidden:



.. _Getting_Started:

---------------
Getting Started
---------------

Welcome to the Nutanix Core Workshop! This workshop may accompany an instructor-led session that introduces Nutanix Core technologies and many common management tasks.

You will explore Prism Element and become familiar with its features and navigation. You will use Prism to perform basic cluster administration tasks, including storage and networking. You will also walk through basic VM deployment and management tasks with Prism and AHV. Finally, you will explore VM data protection, including snapshots and replication. The instructor explains the exercises and answers any additional questions that you may have.

At the end of the bootcamp, attendees should understand the Core concepts and technologies that make up the Nutanix Enterprise Cloud stack.

What's New
++++++++++

..

 * Workshop updated for the following software versions:
    
    * AOS & PC 5.11.x

 * Optional Lab Updates:

    * This Workshop has been done with the 1-Click-Demo 


Agenda
++++++

- Introductions
- Nutanix Technology Overview
- Nutanix Configuration
- Deploying and Managing Workloads
- Security Compliance

Introductions
+++++++++++++

- Name
- Familiarity with Nutanix
- Expectations

Initial Setup
+++++++++++++

There will be a handout with all the information you need to connect to the Lab

Environment Details
+++++++++++++++++++

Nutanix Workshops are intended to be run in the Nutanix Hosted POC environment. Your cluster will be provisioned with all necessary images, networks, and VMs required to complete the exercises.

Networking
..........

Hosted POC clusters follow a standard naming convention:

=================== ====================
**Cluster Name**    POC\ *XYZ*
**Subnet**          10.*XYZ*.\ *XYZ*\ .0
**Cluster IP**      10.*XYZ*.\ *XYZ*\ .7
=================== ====================

For example:

=================== ==========
**Cluster Name**    POC055
**Subnet**          10.21.55.0
**Cluster IP**      10.21.55.7
=================== ==========

Throughout the Workshop there are multiple instances where you will need to substitute *XYZ* with the correct octet for your subnet, for example:


===================== ==============================================
IP Address            Description
===================== ==============================================
10.*XYZ*.\ *XYZ*\ .7  Nutanix Cluster Virtual IP
10.*XYZ*.\ *XYZ*\ .10 **PC** VM IP, Prism Central
10.*XYZ*.\ *XYZ*\ .15 **DC1** VM IP, nutanix.local Domain Controller
10.*XYZ*.\ *XYZ*\ .16 **DC2** VM IP, nutanix.local Domain Controller
===================== ==============================================


Each cluster is configured with 1 VLAN which can be used for VMs:


================= ========================= ====== ============================================
Network Name      Address                   VLAN   DHCP Scope
================= ========================= ====== ============================================
Network-01        10.*XYZ*.\ *XYZ*\ .1/26   0      10.*XYZ*.\ *XYZ*\ .33-10.*XYZ*.\ *XYZ*\ .61
Unmanaged Network                           10
Managed Network   10.*XYZ*.\ *XYZ*\ .65/26  0      10.*XYZ*.\ *XYZ*\ .65-10.*XYZ*.\ *XYZ*\ .127
================= ========================= ====== ============================================



Credentials
...........

.. note::

  The *<Cluster Password>* is the Same for all

============= ========== ====================
Credential    Username   Password
============= ========== ====================
Prism Element admin      *<Cluster Password>*
Prism Central admin      *<Cluster Password>*
Controller VM nutanix    *<Cluster Password>*
Prism Central VM nutanix *<Cluster Password>*
============= ========== ====================



Each cluster has a dedicated domain controller VM, **DC1**, **DC2** responsible for providing AD services for the **nutanix.local** domain. The domain is populated with the following Users and Groups:

================================ ============================================================================================== ====================
Group                            Username(s)                                                                                    Password
================================ ============================================================================================== ====================
Customer-A-Admin-Account-Group   adm-User-1-A, adm-User-2-A, adm-User-3-A, adm-User-4-A, adm-User-5-A                           *<Cluster Password>*
Customer-A-Service-Account-Group ntnx-bck-svc-A, ntnx-exc-svc-A, ntnx-ntx-svc-A, ntnx-psr-svc-A, ntnx-sql-svc-A, ntnx-xda-svc-A *<Cluster Password>*
Customer-A-User-Account-Group    user-1-A, user-2-A, user-3-A, user-4-A, user-5-A                                               *<Cluster Password>*
Customer-B-Admin-Account-Group   adm-User-1-B, adm-User-2-B, adm-User-3-B, adm-User-4-B, adm-User-5-B                           *<Cluster Password>*
Customer-B-Service-Account-Group ntnx-bck-svc-B, ntnx-exc-svc-B, ntnx-ntx-svc-B, ntnx-psr-svc-B, ntnx-sql-svc-B, ntnx-xda-svc-B *<Cluster Password>*
Customer-B-User-Account-Group    user-1-B, user-2-B, user-3-B, user-4-B, user-5-B                                               *<Cluster Password>*
Customer-C-Admin-Account-Group   adm-User-1-C, adm-User-2-C, adm-User-3-C, adm-User-4-C, adm-User-5-C                           *<Cluster Password>*
Customer-C-Service-Account-Group ntnx-bck-svc-C, ntnx-exc-svc-C, ntnx-ntx-svc-C, ntnx-psr-svc-C, ntnx-sql-svc-C, ntnx-xda-svc-C *<Cluster Password>*
Customer-C-User-Account-Group    user-1-C, user-2-C, user-3-C, user-4-C, user-5-C                                               *<Cluster Password>*
Customer-D-Admin-Account-Group   adm-User-1-D, adm-User-2-D, adm-User-3-D, adm-User-4-D, adm-User-5-D                           *<Cluster Password>*
Customer-D-Service-Account-Group ntnx-bck-svc-D, ntnx-exc-svc-D, ntnx-ntx-svc-D, ntnx-psr-svc-D, ntnx-sql-svc-D, ntnx-xda-svc-D *<Cluster Password>*
Customer-D-User-Account-Group    user-1-D, user-2-D, user-3-D, user-4-D, user-5-D                                               *<Cluster Password>*
================================ ============================================================================================== ====================


Access Instructions
+++++++++++++++++++

The Nutanix Hosted POC environment can be accessed a number of different ways:


Parallels VDI this is slow and shoudl only be used if any thing else dose not work.
...................................................................................

Login to: https://xld-uswest1.nutanix.com (for PHX) or https://xld-useast1.nutanix.com (for RTP)

**Nutanix Employees** - Use your NUTANIXDC credentials
**Non-Employees** - **Username:** POCxxx-User01 (up to POCxxx-User20), **Password:** *<Provided by Instructor>*

Employee Pulse Secure VPN
.........................

To download the client: login to https://xlv-uswest1.nutanix.com or https://xlv-useast1.nutanix.com - **Username:** POCxxx-User01 (up to POCxxx-User20), **Password:** *<Provided by Instructor>*

Download and install the client.

In Pulse Secure Client, **Add** a connection:

For PHX:

============== ========================================
**Type**       Policy Secure (UAC) or Connection Server
**Name**       X-Labs - PHX
**Server URL** xlv-uswest1.nutanix.com
============== ========================================

For RTP:

============== ========================================
**Type**       Policy Secure (UAC) or Connection Server
**Name**       X-Labs - RTP
**Server URL** xlv-useast1.nutanix.com
============== ========================================

Bootcamp WLAN Connection
........................

============ ==========
ntnx_hpoc_5G nutanix/4u
ntnx_hpoc    nutanix/4u
============ ==========


Nutanix Version Info
++++++++++++++++++++

- **AHV Version** - AHV 20170830.301  (5.11+/5.11+)
- **AOS Version** - 5.11.1
- **PC Version** - 5.11.1

----------------------
**Indices and tables**
----------------------

* :ref:`genindex`
* :ref:`search`
