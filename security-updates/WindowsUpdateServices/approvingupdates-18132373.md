---
TOCTitle: Approving Updates
Title: Approving Updates
ms:assetid: '7276f84d-429e-4a39-8ef8-be3bff47b45e'
ms:contentKeyID: 18132373
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Cc708458(v=WS.10)'
---

Approving Updates
=================

After updates have been synchronized to your WSUS server, you must approve them to initiate a deployment action. When you approve an update, you are essentially telling WSUS what to do with it (for example, your choices are **Install**, **Detect only**, **Remove**, or **Decline update**). When approving an update, you specify a default approval setting for the **All Computers** group, and any necessary settings for each computer group in the **Approve Updates** dialog box. If you do not approve an update, its approval status remains **Not approved** and your WSUS server performs no action for the update. The exceptions to this are in the **Critical Updates** and **Security Updates** classifications, which by default are automatically approved for detection after they are synchronized.

The **Updates** page is the central access point in the WSUS console for approving updates. On the **Updates** page, you can specify the action you want WSUS to exercise for the update by computer group. You do this by selecting one of the options under **Tasks**. The following provides more information about the different approvals you can enable on the **Updates** page.

If your WSUS server is running in replica mode, you will not be able to approve updates on your WSUS server. For more information about replica mode, see [Running in Replica Mode](https://technet.microsoft.com/d143c886-30b6-4034-80a2-182171ac8f8b).

Approving Updates for Detection
-------------------------------

When you approve an update for detection, the update is not installed. Instead, WSUS checks whether the update is compliant with or needed by computers in the groups you specify for the **Detect only approval** option in the **Approve Updates** dialog box. The detection occurs at the scheduled time that the client computer communicates with the WSUS server. You can see the result of the detection either in the Status of Updates report or on the **Updates** page, by clicking the **Status** tab for a specific update. In either case, the information you need will appear in the **Needed** column, which represents the number of computers that have been detected as needing a particular update. If the client computer does not need the update, the number in **Needed** is zero.

By default, Critical Updates and Security Updates are automatically approved for detection.

**To approve updates for detection**
1.  On the WSUS console toolbar, click **Updates**.

2.  In the list of updates, click one or more updates that you want to approve for detection.

3.  Under **Update Tasks**, click **Change** approval.

4.  In the **Approve Updates** dialog box, verify that **Approval** is set to **Detect only** for the All Computers group.

5.  If you want to set a different default approval setting for one or more groups, under **Group approval settings for the selected updates**, find the group(s) for which you want to set the special approval setting, and then, in the **Approval** column, select an approval setting.

Approving Updates for Installation
----------------------------------

You can select one or multiple updates; if you select multiple updates, you can approve them for installation at once; you can also approve installation by computer group. This would be the **Install approval** option in the **Approve Updates** dialog box. In addition, when you specify this approval action, you can do one of the following:

-   Use the settings on the client computers to determine when to install updates. When you select this option, users in the targeted computer group will receive a notification dialog box and an **Automatic Updates** icon on their taskbar when updates are ready to be installed on their computers. They can then install the updates immediately, or at a later time, by clicking the **Automatic Updates** icon. If you have configured Automatic Updates, either by Group Policy or locally, to notify the user before installation, these notifications will be offered to any non-administrator who logs onto the computer in the targeted computer group.
-   Set a deadline for automatic installation. When you select this option, you set specific times and dates to install updates, overriding any settings on the client computers. In addition, you can specify a past date for the deadline if you want to run an approval action immediately (that is, when the client computers next contact the WSUS server).

| ![](images/Cc708458.Important(WS.10).gif)Importante                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| You cannot set a deadline for automatic installation for an update if user input is required (for example, accepting a license agreement or specifying a setting relevant to the update). If you set a deadline for such an installation synchronization will fail. To determine whether an update will require user input, look at the **May request user input** field in the update properties for an update displayed on the **Updates** page. Also check for a message in the **Approve Updates** box which says "**The selected update requires user input and does not support and installation deadline**." |

**To approve updates for installation**
1.  On the WSUS console toolbar, click **Updates**.

2.  In the list of updates, click one or more updates that you want to approve for installation.

3.  Under **Update Tasks**, click **Change approval**.

4.  In the **Approve Updates** dialog box, verify that **Approval** is set to **Install** for the All Computers group.

5.  To specify how and when the update will be installed for computers in the computer group, next to **Deadline**, click **None**, and then click one of the following options:

    -   If you want to enable users to determine when to install the updates, click **Use client settings to determine update installation time**, and then click **OK**. If you have configured Automatic Updates, either by domain-based or local Group Policy, to notify the user before installation, these notifications will be offered to any non-administrator who logs onto the computer in the targeted computer group.
    -   If you want the update to be installed automatically, click **Install the update by the selected date and time**, specify the date and time of the deadline, and then click **OK**. If you want the install to occur immediately (that is, when the client computers next contact the WSUS server), you can specify a past date for the deadline.

6.  If you want to set a different default approval setting for one or more groups, under **Group approval settings for the selected updates**, find the group(s) for which you want to set the special approval setting, and then, in the **Approval** column, click an approval setting.

| ![](images/Cc708458.note(WS.10).gif)Nota                                                                                                                        |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| For more information about downloading and installing updates, see [Best Practices with Windows Server Update Services](https://technet.microsoft.com/b4ff7f56-45b5-4f2b-82e7-283903d23c26). |

Declining Updates
-----------------

This option is available as a task under **Update Tasks** on the **Updates** page. If you select this option, the update is removed from the list of available updates. Declined updates will appear in the updates list only if you select either **Declined** or **All updates** in the **Approval** list when specifying the filter for the update list under **View**.

**To decline updates**
1.  On the WSUS console toolbar, click **Updates**.

2.  In the list of updates, click one or more updates that you want to decline.

3.  In **Update Tasks**, click **Decline update** or **Decline selected updates**, depending on whether you have selected one or multiple updates to decline.

Approving Updates for Removal
-----------------------------

You can approve an update for removal (that is, approve uninstalling the update). This option is only available if the update supports uninstalling, and you would choose the **Remove approval** option in the **Approve Updates** dialog box. You can specify a deadline for the update to be uninstalled, as well as specify a past date for the deadline if you want to run an approval action immediately (that is, when the client computers next contact the WSUS server).

**To approve updates for removal**
1.  On the WSUS console toolbar, click **Updates**.

2.  In the list of updates, click one or more updates that you want to approve for removal.

3.  Under **Update Tasks**, click **Change approval**.

4.  In the **Approve Updates** dialog box, verify that **Approve** is set to **Remove** for the All Computers group.

5.  If you want to set a deadline for the update(s) to be automatically removed, next to **Deadline**, click **None**, specify the date and time for the deadline, and then click **OK**. If you want the update removal to occur immediately (that is, when the client computers next contact the WSUS server), you can specify a past date for the deadline.

6.  If you want to set a different default approval setting for one or more groups, under **Group approval settings for the selected updates**, find the group(s) for which you want to set the special approval setting, and then, in the Approval column, click an approval setting.

Approving Updates Automatically
-------------------------------

On the **Automatic Approval Options** page, you can configure your WSUS server to automatically approve installation or detection for updates and associated metadata when they are downloaded to the WSUS server during synchronization. This is different from approving updates on the **Updates** page, where, by default, updates are approved for detection.

You can configure automatic approval for updates by update classifications and groups. If the installation and detection rules you set conflict, your WSUS server will follow the installation rules.

On the **Automatic Approval Options** page, you can also select an option to automatically approve revisions to existing updates as they become available. This option is selected by default. A revision is a version of an update that has had changes made to it (for example, it might have expired, or UI text, the EULA, or applicability rules for computers might have changed). If you do not choose to automatically approve the revised version of an update, WSUS will use the older version, and you must manually approve the update revision.

Automatically Approving Updates for Detection
---------------------------------------------

When you select this option, you can create a rule that your WSUS server will automatically apply during synchronization. For the rule, you specify what updates you want to automatically approve for detection, by update classification and by computer group. This applies only to new updates, as opposed to revised updates. This setting is available on the **Automatic Approval Options** page.

On this page, you can also set a rule for automatically approving updates for installation. In the event that rules conflict (for example, you have specified the same update classification and same computer group combination in both the rule to automatically approve for detection and automatically approve for installation), then your WSUS server applies the rule to automatically approve for installation.

**To automatically approve updates for detection**
1.  On the WSUS console toolbar, click **Options**, and then click **Automatic Approval Options**.

2.  In **Updates**, under **Approve for Detection**, select the **Automatically approve updates for detection by using the following rule** check box (if it is not already selected).

3.  If you want to specify update classifications to automatically approve during synchronization, do the following:

    -   Next to **Classifications**, click **Add/Remove Classifications**.
    -   In the **Add/Remove Classifications** dialog box, select the update classifications that you want to automatically approve, and then click **OK**.

4.  If you want to specify the computer groups for which to automatically approve updates during synchronization:

    -   Next to **Computer groups**, click **Add/Remove Computer Groups**.
    -   In the **Add/Remove Computer Groups** dialog box, select the computer groups for which you want to automatically approve updates, and then click **OK**.

5.  Under **Tasks**, click **Save settings**, and then click **OK**.

Automatically Approve Updates for Installation
----------------------------------------------

When you select this option, you can create a rule that your WSUS server will automatically apply during synchronization. For the rule, you specify what updates you want to automatically approve for installation, by update classification and by computer group. This applies only to new updates, as opposed to revised updates. This setting is available on the **Automatic Approval Options** page.

On this page, you can also set a rule for automatically approving updates for detection. In the event that rules conflict (for example, you have specified the same update classification and same computer group combination in both the rule to automatically approve for installation and automatically approve for detection), then your WSUS server applies the rule to automatically approve for installation.

**To automatically approve updates installation**
1.  On the WSUS console toolbar, click **Options**, and then click **Automatic Approval Options**.

2.  In **Updates**, under **Approve for Installation**, select the **Automatically approve updates for installation by using the following rule** check box (if it is not already selected).

3.  If you want to specify update classifications to automatically approve during synchronization, do the following:

    -   Next to **Classifications**, click **Add/Remove Classifications**.
    -   In the **Add/Remove Classifications** dialog box, select the update classifications that you want to automatically approve, and then click **OK**.

4.  If you want to specify the computer groups for which to automatically approve updates during synchronization:

    -   Next to **Computer groups**, click **Add/Remove Computer Groups**.
    -   In the **Add/Remove Computer Groups** dialog box, select the computer groups for which you want to automatically approve updates, and then click **OK**.

5.  Under **Tasks**, click **Save settings**, and then click **OK**.

Automatically Approving Revisions to Updates
--------------------------------------------

The **Automatic Approval Options** page contains an option to automatically approve revisions to existing updates as they become available. This option is selected by default. A revision is a version of an update that has changes (for example, it might have expired, or have an updated EULA, UI text, or applicability rules for computers). If you configure your WSUS server to automatically approve new revisions of an update but an expired revision for the update is synchronized, your WSUS server will automatically decline the update. If you choose not to automatically approve the revised version of an update, your WSUS server will use the older revision, and you must manually approve the update revision.

**To automatically approve revisions to updates**
1.  On the WSUS console toolbar, click **Options**, and then click **Automatic Approval Options**.

2.  Under **Revisions to Updates**, click **Automatically approve the latest revision of the update**.

3.  Under **Tasks**, click **Save settings**, and then click **OK**.

Approving Superseding or Superseded Updates
-------------------------------------------

Typically, an update that *supersedes* other updates does one or more of the following:

-   Enhances, improves, and/or adds to the fix provided by one or more previously released updates.
-   Improves the efficiency of its update file package, which is installed on client computers if the update is approved for installation. For example, the superseded update might contain files that are no longer relevant to the fix, or to the operating systems now supported by the new update, so those files are not included in the superseding update's file package.
-   Updates newer versions of operating systems. It is also important to note that the superseding update might not support earlier versions of operating systems.

Conversely, an update that is *superseded* by another update does the following:

-   Fixes a similar vulnerability to the update that supersedes it. However, the update that supersedes it might enhance the fix that the superseded update provides.
-   Updates earlier versions of operating systems—in some cases these versions of operating systems are no longer updated by the superseding update.

In the list of updates on the **Updates** page, an icon next to the update indicates that it has a supersedure relationship to another update. The **Details** tab in the properties for the update tells you whether the update supersedes or is superseded by another update. In addition, you can determine which updates supersede or are superseded by the update by looking at the **Supersedes** and **Superseded by** entries. The properties box for the update is available at various locations in the WSUS console (for example, on the **Updates** page, on the **Computers** page).

WSUS does not automatically decline superseded updates, and it is recommended that you do not assume that superseded updates should be declined in favor of the new, superseding update. Before declining a superseded update, make sure that it is no longer needed by any of your client computers. Following are examples of scenarios where you might need to install a superseded update:

-   If a superseding update supports only newer versions of an operating system, and some of your client computers run earlier versions of the operating system.
-   If a superseding update has more restricted applicability than the update it supersedes, which would make it inappropriate for some client computers.
-   If an update no longer supersedes a previously released update due to new changes. It is possible that through changes at each release, an update no longer supersedes an update it previously superseded in an earlier version. In this scenario, you will still see a message on the **Details** tab for the superseded update that it has been superseded, even though the update that supersedes it has been replaced by an update that does not.

#### Recommended Process for Approving a Superseding Update

Because a superseding update typically enhances a fix provided by a previously released, superseded update, it is recommended that you first see how many client computers will be compliant with the new update, and work backward from there. Use the following process.

**To approve a superseding update**
1.  Approve the superseding update for **Install** on all computers where the fix provided by the update is appropriate.

2.  Check the resulting status of the approval action on your computers. Note which computers show status as **Not needed** for the update, and then compare the properties of those computers with the properties of the update.

3.  Use the information available in the update properties to help you determine which previously released version of the updates are available. For example, look under **Supersedes** on the **Details** tab, and check the **Description** and **KB article number** entries if appropriate.

4.  Get information about the superseded, previously released versions of the updates; for example, view their properties.

5.  When you find a superseded update that seems appropriate for the remaining client computers, approve the update for installation.

6.  Repeat this process until all of your client computers are updated with the intended fix.
