---
title: How to prepare HANA, express edition environment for tutorials
description: This how-to shows you how to prepare your HANA, express edition for executing the other Tutorials.
tags: [  tutorial>beginner, products>sap-hana\,-express-edition, tutorial>how-to ]
---

## Prerequisites  
 - Proficiency: beginner
 - Setup: This tutorial provides the details on creating required users for other `HANA, express edition` "Tutorials"

## Next Steps
 - Go to the [SAP HANA, express edition tutorials page](http://www.sap.com/developer/topics/sap-hana-express.tutorials.html)

## NOTE: SAP HANA, express edition version 2.0 implications on 'How-Tos' and 'Tutorials'

The available HANA, express edition versions (1.0 SP12 and 2.0 SP00) have different default instance numbers. The publishes Tutuorials and How-Tos refer to the default 1.0 SP12 instance numbers. When using the 2.0 version please use the new default instance number and port (3`<instance number>`15):

HANA Express Version  | Default Instance ID | Port
:-------------------  | :------------------ | :---------------
1.0 SP12              |  00                 | 30015
2.0 SP00              |  90                 | 39015

## How-To Details
The HANA, express edition "Tutorials" reference a set of users. This set of instructions assures all required users and passwords are available and correct before attempting the other `HANA, express edition` "Tutorials".

The passwords referred to in the "Tutorials" will not match the passwords chosen by the user. For example, any reference to the password `"HANARocks2016"` should be replaced by the user provided password (see below).

### Time to Complete
**5 Min**.

---

1. Review default system configuration for `HANA, express edition`:

Field Name  | Value
:---------- | :---------------
System Host | `hxehost`
SID         | `HXE`
System Instance Number | `00` (version 2 SP00 `90`)
XSA Organization | `HANAExpress`
XSA Space   | `SAP`
ALL passwords | <user defined> (referred to as `HANAROCKS2016` in tutorials)



2. Create `WORKSHOP_01` user for `SAP HANA, express edition` "How-To" tutorials:

    - Login to `HANA` as `hxeadm`  (you may need to change system password if not already done) and create `WORKSHOP_01` user:

    ```
    % sudo su - hxeadm

    % xs login -u xsa_admin -p <password>

Reminder version 2.0 SP00 default instance number is 90, in below hdbsql command, replace "00" with "90".

    % hdbsql -i 00 -n localhost:30013 -u SYSTEM -p <SYSTEM user password>  "CREATE USER WORKSHOP_01 PASSWORD <password> NO FORCE_FIRST_PASSWORD_CHANGE SET PARAMETER XS_RC_XS_CONTROLLER_USER = 'XS_CONTROLLER_USER' , XS_RC_DEVX_DEVELOPER = 'DEVX_DEVELOPER', XS_RC_XS_AUTHORIZATION_ADMIN = 'XS_AUTHORIZATION_ADMIN'"
    ```

3. Add XSA "space role" for workshop user:

    ```
    % xs set-space-role WORKSHOP_01 HANAExpress SAP SpaceDeveloper
    ```

4. Verify the new `WORKSHOP_01` user can connect to `HANA, express edition`:

    ```
    % hdbsql -u WORKSHOP_01 -p <password> -d SystemDB
    ```

    Expected result:

    ![image 1](1.PNG)

5. Verify the `WORKSHOP_01` user can connect to XSA:

    ```
    % xs login -u WORKSHOP_01 -p <password>
    ```

    Expected result:

    ![image 1](2.PNG)

## Next Steps
 - Go to the [SAP HANA, express edition tutorials page](http://www.sap.com/developer/topics/sap-hana-express.tutorials.html)
