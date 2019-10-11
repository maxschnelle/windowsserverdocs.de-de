---
title: Neuerstellen der Tokens.dat-Datei
description: Informationen zum Neuerstellen der Tokens.dat-Datei bei der Behandlung von Windows-Aktivierungsproblemen
ms.topic: troubleshooting
ms.date: 09/18/2019
ms.technology: server-general
author: Teresa-Motiv
ms.author: v-tea
manager: dcscontentpm
ms.localizationpriority: medium
ms.openlocfilehash: 8a5835cd601b2eb327c8605d70bf075e6c8e8414
ms.sourcegitcommit: 9855d6b59b1f8722f39ae74ad373ce1530da0ccf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/04/2019
ms.locfileid: "71962996"
---
# <a name="rebuild-the-tokensdat-file"></a>Neuerstellen der Tokens.dat-Datei

Wenn Sie Probleme bei der Windows-Aktivierung behandeln, müssen Sie möglicherweise die Datei „Tokens.dat“ neu erstellen. In diesem Artikel wird ausführlich beschrieben, wie dies geschieht.

## <a name="resolution"></a>Auflösung

Führen Sie die folgenden Schritte aus, um die Tokens.dat-Datei neu zu erstellen:

1. Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten:  
   **Für Windows 10**

   1. Öffnen Sie das **Startmenü**, und geben Sie **cmd** ein.
   1. Klicken Sie in den Suchergebnissen mit der rechten Maustaste auf **Eingabeaufforderung**, und wählen Sie dann **Als Administrator ausführen** aus.  

   **Für Windows 8.1**
   1. Wischen Sie vom rechten Bildschirmrand aus nach innen, und tippen Sie dann auf **Suchen**. Wenn Sie eine Maus verwenden, zeigen Sie auf die untere rechte Ecke des Bildschirms, und wählen Sie dann **Suchen** aus.
   1. Geben Sie im Suchfeld **cmd** ein.
   1. Wischen Sie über das angezeigte Symbol **Eingabeaufforderung**, oder klicken Sie mit der rechten Maustaste darauf.
   1. Tippen oder klicken Sie auf **Als Administrator ausführen**.

   **Für Windows 7**
   1. Öffnen Sie das **Startmenü**, und geben Sie **cmd** ein.
   1. Klicken Sie in den Suchergebnissen mit der rechten Maustaste auf **cmd.exe**, und wählen Sie **Als Administrator ausführen** aus.

1. Geben Sie die Liste der Befehle ein, die für Ihr Betriebssystem geeignet sind.  

   Geben Sie für Windows 10, Windows Server 2016 und höhere Versionen von Windows nacheinander die folgenden Befehle ein:
   ```cmd
   net stop sppsvc
   cd %windir%\system32\spp\store\2.0
   ren tokens.dat tokens.bar
   net start sppsvc
   cscript.exe %windir%\system32\slmgr.vbs /rilc
   ```
   Geben Sie für Windows 8.1, Windows Server 2012 und Windows Server 2012 R2 nacheinander die folgenden Befehle ein:
   ```cmd
   net stop sppsvc
   cd %windir%\ServiceProfiles\LocalService\AppData\Local\Microsoft\WSLicense
   ren tokens.dat tokens.bar
   net start sppsvc
   cscript.exe %windir%\system32\slmgr.vbs /rilc
   ```
   Geben Sie für Windows 7, Windows Server 2008 und Windows Server 2008 R2 nacheinander die folgenden Befehle ein:
   ```cmd
   net stop sppsvc
   cd %windir%\ServiceProfiles\NetworkService\AppData\Roaming\Microsoft\SoftwareProtectionPlatform
   ren tokens.dat tokens.bar
   net start sppsvc
   cscript.exe %windir%\system32\slmgr.vbs /rilc
   ```
1. Starten Sie den Computer neu.

## <a name="more-information"></a>Weitere Informationen

Nachdem Sie die Datei „Tokens.dat“ neu erstellt haben, müssen Sie Ihren Product Key mit einer der folgenden Methoden erneut installieren:

- Geben Sie an der gleichen Eingabeaufforderung mit erhöhten Rechten den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:

   ```cmd
   cscript.exe %windir%\system32\slmgr.vbs /ipk <Product key>
   ```

  > [!IMPORTANT]
  > Verwenden Sie nicht den Schalter **/upk** zum Deinstallieren eines Product Keys. Verwenden Sie den Schalter **/ipk**, um einen Product Key über einen vorhandenen Product Key zu installieren.
- Klicken Sie mit der rechten Maustaste auf **Arbeitsplatz**, wählen Sie **Eigenschaften** und dann **Product Key ändern** aus.

Weitere Informationen zu KMS-Clientsetupschlüsseln finden Sie unter [KMS-Clientsetupschlüssel](kmsclientkeys.md).
