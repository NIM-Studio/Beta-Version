Installation
============

This guide applies to **NIM Studio v0.1.0-beta**. The beta is available
only to approved testers and is governed by the included licence,
rights notice, and beta policy.

The application is available to selected users upon request. 

Available packages
--------------------------

.. list-table::
   :header-rows: 1
   :widths: 18 18 42 22

   * - Operating system
     - Architecture
     - Package
     - Notes
   * - Windows 10/11
     - 64-bit (x86_64)
     - ``NIM-Studio-v0.1.0-beta-Windows-x64.zip``
     - Portable application; Python is not required.
   * - macOS
     - Intel (x86_64)
     - ``NIM-Studio-v0.1.0-beta-macOS-Intel-unsigned.dmg``
     - For Intel-based Macs.
   * - macOS
     - Apple Silicon (arm64)
     - ``NIM-Studio-v0.1.0-beta-macOS-AppleSilicon-unsigned.dmg``
     - For Macs with an M-series chip.

To identify your Mac, select **Apple menu > About This Mac**. Choose
Apple Silicon if an Apple M-series chip is listed. Choose Intel if an
Intel processor is listed.

Before installation
-------------------

#. Obtain the package only through the official private beta channel.
#. Confirm that the filename matches one of the packages listed above.
#. If a SHA-256 checksum was provided, verify it before opening the package.
#. On an institutionally managed computer, confirm that installation is
   permitted by your institution's IT and security policies.

.. warning::

   The beta packages are currently unsigned. Windows or macOS may therefore
   display a security warning. Continue only if you received the package
   through the approved NIM Studio beta channel and your device policy permits
   unsigned beta software.

Windows 10/11
-------------

#. Download ``NIM-Studio-v0.1.0-beta-Windows-x64.zip``.
#. Right-click the ZIP file and select **Extract All**.
#. Keep the extracted folder intact. Do not move ``NIM Studio.exe`` away
   from its accompanying ``_internal`` folder.
#. Open the extracted folder and double-click ``NIM Studio.exe``.
#. You may save the icon on the desktop, start or toolbar for easy findability. 
#. If Microsoft Defender SmartScreen appears, select **More info** and then
   **Run anyway**, provided your device policy permits the beta.
#. On first launch, review and accept the displayed licence, rights notice,
   and beta policy.

NIM Studio is distributed as a portable Windows application. It does not use
a traditional installer and does not require Python.

macOS — Intel or Apple Silicon
-------------

#. Download ``NIM-Studio-v0.1.0-beta-macOS-Intel-unsigned.dmg`` OR ``NIM-Studio-v0.1.0-beta-macOS-AppleSilicon-unsigned.dmg``.
#. Double-click the DMG to mount it.
#. Drag **NIM Studio** onto the **Applications** shortcut (this works only if the user has administrator rights on the machine)
#. Open NIM Studio by double clicking the app icon. 
#. You may save the icon on the desktop, start or toolbar for easy findability. 
#. If macOS blocks the application, open **Apple menu > System Settings >
   Privacy & Security**.
#. Under **Security**, select **Open Anyway**, authenticate, and confirm
   **Open**.
#. On first launch, review and accept the displayed licence, rights notice,
   and beta policy.

If you cannot write to the system Applications folder, you may run NIM Studio
from the mounted DMG or copy it to ``~/Applications``, provided your device
policy allows this.

The Apple Silicon package runs natively on M-series Macs and does not require
Rosetta 2.


Troubleshooting
---------------

Windows cannot find a DLL or ``_internal`` file
   Extract the complete ZIP again. Keep ``NIM Studio.exe`` together with the
   entire ``_internal`` folder.

macOS cannot verify the developer
   Follow the **Privacy & Security > Open Anyway** procedure above. Do not
   disable Gatekeeper globally.

The application is blocked on a managed device
   Contact your institution's IT department. Do not attempt to bypass
   organizational security controls.

Legal documents or interface assets are missing
   Stop using the package and report the problem through the private beta
   support channel.

The application does not start
   Record your operating-system version, package filename, and complete error
   message, then send them through the beta support channel.

Uninstalling NIM Studio
-----------------------

Windows
~~~~~~~

Close NIM Studio and delete the extracted application folder.

macOS
~~~~~

Close NIM Studio and move ``NIM Studio.app`` from ``Applications`` or
``~/Applications`` to the Bin. Eject and delete the downloaded DMG if it is
no longer needed.

The locally stored acceptance record may remain in the current user's
application-data or application-support directory.

Beta support
------------

Report installation problems through the private feedback and support channel
provided during beta onboarding.

Do not publicly share beta packages, access links, internal documentation, or
screenshots containing sensitive information.