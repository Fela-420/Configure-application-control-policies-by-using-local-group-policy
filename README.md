# Configure-application-control-policies-by-using-local-group-policy
Select Type here to search from the taskbar, type regedit, then select Registry Editor from the results.

Select Yes on the User Account Control window.
![2025-03-14 (1)](https://github.com/user-attachments/assets/90ec9b23-8698-4df2-8580-5d13b83e88c3)

Once the Registry Editor window is visible. Close it.

This confirms that you are currently able to open the Registry Editor.

Select Type here to search from the taskbar, type powershell, right-click Windows PowerShell from the results, then select Run as administrator.

Select Yes on the User Account Control window.

Enter the following command to start the Application Identification service:

net start appidsvc
Select Type here to search from the taskbar, type secpol.msc, then select secpol.msc from the results.

The Local Security Policy window should be displayed.
![2025-03-14 (2)](https://github.com/user-attachments/assets/c3e50cbf-e30c-47fd-8ac2-0ab56123dd0a)

Maximize the Local Security Policy window and adjust the left pane to right pane divider by using the click-hold-drag-release method to move the divider to about one-third the width of the screen from the left. This will allow you to display the full names of the items in the left pane.

In the left pane, select the arrow to expand Application Control Policies.

Select the arrow to expand AppLocker then select AppLocker.
![2025-03-14 (5)](https://github.com/user-attachments/assets/dd4b1df2-82a4-47a5-a26d-2073d6c7c779)

In the right pane, select Configure rule enforcement in the Configure Rule Enforcement section.

On the AppLocker Properties window, mark all 4 (four) of the Configured checkboxes, then verify that Enforce rules is selected in all 4 (four) of the pull-down lists, select Apply, then select OK.
![2025-03-14 (6)](https://github.com/user-attachments/assets/1289de77-db70-4bc1-abbf-908abc3ef4bd)

This operation enables AppLocker rule enforcement. Next, you will create an AppLocker executable rule to deny Regedit execution based on Path.

In the left pane, select Executable Rules

In the right pane, right-click the empty space and then select Create New Rule….

On the Create Executable Rule window, on the Before You Begin page, select Next.
![2025-03-14 (7)](https://github.com/user-attachments/assets/4afe7a5b-dbc1-4920-ac9e-015a9eafebfa)

On the Permissions page, under Action, select Deny, leave the User or group: value set at Everyone, and then select Next.

On the Conditions page, select Path, and then select Next.

On the Path page, under Path, type %WINDIR%\regedit.exe, then Create.
![2025-03-14 (8)](https://github.com/user-attachments/assets/ca5e6be6-1cda-490d-8b78-cd30a022e2af)

If an AppLocker pop-up window is displayed regarding creating default rules, select Yes.

A Path rule simply denies the application from running based on the name and location of the file. If the file is moved or renamed, it will execute. The Hash rule generates a hash of the file, so even if the file is renamed or moved, it will still not execute. Hash rules use more overhead but are more restrictive.

Switch back to the PowerShell window.

Force a Group Policy update by entering the following command:

gpupdate /force
Wait for the messages indicating that both the Computer Policy and User Policy updates have completed.
![2025-03-14 (10)](https://github.com/user-attachments/assets/0f30ed04-00e1-4968-8777-8aa3456af10b)

Enter regedit to test the AppLocker policy enforcement from the PowerShell CLI.

You should see an error indicating the program failed to run since it is blocked by group policy.
![2025-03-14 (11)](https://github.com/user-attachments/assets/34956fe2-578e-41ca-a7c3-f916fea4cd7c)

Test the AppLocker policy enforcement from the GUI. Select Type here to search from the taskbar, type regedit, then select Registry Editor from the results.

A notification window should appear stating "This app has been blocked by your system administrator".

Select Close to close the notification window.

Leave the Local Security Policy and PowerShell windows open.

Return to the Local Security Policy window.

THe Application Control Policies section in the left pane should still be expanded showing AppLocker and its sub-elements, including Executable Rules.

In the left pane, select Executable Rules.

In the right pane, right-click and then select Create New Rule.

On the Create Executable Rule window, on the Before You Begin page, select Next.
![2025-03-14 (12)](https://github.com/user-attachments/assets/28e8792a-3159-4e68-b106-99a872a7eeb1)

On the Permissions page, under Action, select Deny and then select Next.

On the Conditions page, select File hash, and then select Next.

On the File Hash page, select Browse Files….
![2025-03-14 (13)](https://github.com/user-attachments/assets/05242387-316e-4d77-85fb-4e4ae337032b)

Select This PC in the left pane, then double-click Local Disk (C:) in the right pane.

Double-click Program Files, then double-click Mozilla Firefox.

Select firefox and then select Open.

You are returned to the File Hash page, select Create.

You should now see the firefox.exe | File Hash Deny rule.
![2025-03-14 (15)](https://github.com/user-attachments/assets/076d56b0-b985-4ad9-a863-3e24df75adf3)

A Path rule simply denies the application from running based on the name and location of the file. If the file is moved or renamed, it will execute. The Hash rule generates a hash of the file so even if the file is renamed or moved, it will still not execute. Hash rules use more overhead but are more restrictive.

Which of the following statements are true in regards to AppLocker rules? (Select all that apply).

A path rule denies execution if the file is moved to another directory.
A hash rule denies execution if the file is renamed.
A path rule denies execution if the file is renamed.
A hash rule denies execution if the file is moved to another directory.
Congratulations, you have answered the question correctly.

Switch back to the PowerShell window.

Force a Group Policy update by entering the following command:

gpupdate /force
Wait for the messages indicating that both the Computer Policy and User Policy updates have completed.

Select Type here to search from the taskbar, type Firefox, then select Firefox from the results

A notification window should appear stating "This app has been blocked by your system administrator".

Select Close to close the notification window.


