---
Order: 12
Area: editor
TOCTitle: Settings Sync
ContentId: 6cb84e60-6d90-4137-83f6-bdab3438b8f5
PageTitle: Settings Sync in Visual Studio Code
DateApproved: 7/9/2020
MetaDescription: Synchronize your user settings across all your Visual Studio Code instances.
---
# Settings Sync

>**Note**: Settings Sync is still in Preview and only available on VS Code [Insiders](/insiders).

## Turning on Settings Sync

You can turn on Settings Sync using the **Turn On Preferences Sync...** entry in the **Manage** gear menu at the bottom of the Activity Bar.

![Turn on Sync command](images/settings-sync/turn-on-sync.png)

You will be asked to sign in and what preferences you would like to sync; currently Settings, Keyboard Shortcuts, Extensions, User Snippets, and UI State are supported.

![Settings Sync configure dialog](images/settings-sync/sync-configure.png)

Selecting the **Sign in & Turn on** button will ask you to choose between signing in with your Microsoft or GitHub account.

![Settings Sync configure dialog](images/settings-sync/sync-accounts.png)

After making this selection, the browser will open so that you can sign in to your Microsoft or GitHub account. When a Microsoft account is chosen, you can use either personal accounts, such as Outlook accounts, or Azure accounts, and you can also link a GitHub account to a new or existing Microsoft account.

After signing in, Settings Sync will be turned on and continue to synchronize your preferences automatically in the background.

## Configuring synced data

Machine settings (with `machine` or `machine-overridable` [scopes](/updates/v1_34.md#machinespecific-settings)) are not synchronized by default, since their values are specific to a given machine. You can also add or remove settings you want to this list from the Settings editor or using the setting `sync.ignoredSettings`.

![Settings Sync ignored settings](images/settings-sync/sync-ignored-settings.png)

Keyboard Shortcuts are synchronized per platform by default. If your keyboard shortcuts are platform-agnostic, you can synchronize them across platforms by disabling the setting `sync.keybindingsPerPlatform`.

All built-in and installed extensions are synchronized along with their global enablement state. You can skip synchronizing an extension, either from the Extensions view (`kb(workbench.view.extensions)`) or using the setting `sync.ignoredExtensions`.

![Settings Sync ignored settings](images/settings-sync/sync-ignored-extensions.png)

Following UI State is synchronized currently:

* Display Language
* Activity Bar entries
* Panel entries
* Views layout and visibility
* Recently used commands
* Do not show again notifications

You can always change what is synced via the **Preferences Sync: Configure** command or by opening the **Manage** gear menu, selecting **Preferences Sync is On**, and then **Preferences Sync: Configure**.

## Conflicts

When synchronizing settings between multiple machines, there may occasionally be conflicts. Conflicts can happen when first setting up sync between machines or when settings change while a machine is offline. When conflicts occur, you will be presented with the following options:

* **Accept Local**: Selecting this option will overwrite **remote** settings in the cloud with your local settings.
* **Accept Remote**: Selecting this option will overwrite **local** settings with remote settings from the cloud.
* **Show Conflicts**: Selecting this will display a diff editor similar to the Source Control diff editor, where you can preview the local and remote settings and choose to either accept local or remote or manually resolve the changes in your local settings file and then accept the local file.

## Switching Accounts

If at any time you want to sync your data to a different account, you can turn off and turn on Settings Sync again with different account.

## Restoring data

VS Code always stores local and remote backups of your preferences while syncing and provides views for accessing these. In case something goes wrong, you can restore your data from these views.

![Settings Sync backup views](images/settings-sync/sync-backup-views.png)

You can open these views using **Preferences Sync: Show Synced Data** command from the Command Palette. The Local Sync activity view is hidden by default and you can enable it using **Views** submenu under **Preferences Sync** view overflow actions.

![Settings Sync enable local backup views](images/settings-sync/sync-enable-local-activity-view.png)

Local backups folder in the disk can be accessed via the **Preferences Sync: Open Local Backups Folder** command. The folder is organized by the type of preference and contains versions of your JSON files, named with a timestamp of when the backup occurred. These backups are automatically deleted after 30 days.

## Synced Machines

VS Code keeps track of the machines synchronizing your preferences and provides a view to access them. Every machine is given a default name based on the type of VS Code (Insiders or Stable) and the platform it is on. You can always update the machine name using the edit action available on the machine entry in the view. You can also disable sync on another machine using **Turn off Preferences Sync** context menu action on the machine entry in the view.

![Settings Sync machines views](images/settings-sync/sync-machines-view.png)

You can open this view using **Preferences Sync: Show Synced Data** command from the Command Palette.

## Reporting issues

Settings Sync activity can be monitored in the **Log (Preferences Sync)** output view. If you experience a problem with Settings Sync, please include this log when creating the issue. If your problem is related to authentication, also include the log from the **Account** output view.

## How do I delete my data?

If you want to remove all your data from our servers, just turn off sync via **Preferences Sync is On** menu available under **Manage** gear menu and select the checkbox to clear all cloud data. If you choose to re-enable sync, it will be as if you're signing in for the first time.

## Next steps

* [User and Workspace settings](/docs/getstarted/settings.md) - Learn how to configure VS Code to your preferences through user and workspace settings.

## Common questions

## Troubleshooting keychain issues

Settings Sync persists authentication information to the system keychain. Writing to the keychain can fail in some cases if the keychain is misconfigured.

### macOS

If the keychain throws the error "The user name or passphrase you entered is not correct.", open the Keychain Access app, right-click on the `login` keychain, and lock and unlock it again. This error was first reported in [issue #76](https://github.com/atom/node-keytar/issues/76) as a problem after upgrading to macOS High Sierra, but it has also been reported on more recent macOS versions.

### Linux

If the keychain throws the error "No such interface "org.freedesktop.Secret.Collection" on object at path /org/freedesktop/secrets/collection/login", try following the steps described in [issue #92972](https://github.com/microsoft/vscode/issues/92972#issuecomment-625751232) to create a new keyring.
