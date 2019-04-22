---
title: Problembehandlung bei der Aktivierung von OTP
description: Dieses Thema ist Teil des Leitfadens Bereitstellen von Remotezugriff mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b58252ca-4c1d-4664-a3c4-7301e2121517
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d789671a0425974e560e5f4a43ebcba4c1741c76
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819461"
---
# <a name="troubleshooting-enabling-otp"></a>Problembehandlung bei der Aktivierung von OTP

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema enthält Problembehandlungsinformationen für Probleme beim Aktivieren von DirectAccess-OTP-Authentifizierung, die entweder die **aktivieren-DAOtpAuthentication** PowerShell-Cmdlets oder die Remotezugriffs-Verwaltungskonsole.
  
## <a name="failed-to-enroll-the-otp-signing-certificate"></a>Fehler bei der Registrierung des OTP-Signaturzertifikats  
**Fehler** (Server-Ereignisprotokoll). Ein OTP-Signaturzertifikat kann nicht mit der Zertifikatvorlage < OTP_signing_template_name > registriert werden  
  
**Ursache**  
  
Es gibt drei mögliche Ursachen für diesen Fehler aus:  
  
-   Die Vorlage ist nicht vorhanden.  
  
-   Die Berechtigungen für die Vorlage lassen sich nicht auf den DirectAccess-Server für die Registrierung aus.  
  
-   Es ist keine Netzwerkkonnektivität und die ausstellende Zertifizierungsstelle (CA).  
  
**Lösung**  
  
1.  Stellen Sie sicher, dass das Codesignaturzertifikat OTP-Vorlage mit dem angegebenen Namen:  
  
    1.  Vorhanden ist und über die richtigen Berechtigungen verfügt.  
  
    2.  Wird von mindestens eine Zertifizierungsstelle ausgestellt werden, die Zertifikate, auf dem DirectAccess-Server ausstellen können festgelegt.  
  
2.  Wenn die Vorlage nicht vorhanden, erstellen Sie ihn der registrierungsstellenzertifikats 3.3 Plan unter oder wenn eine andere entsprechende Vorlage vorhanden ist, konfigurieren DirectAccess-OTP mit dem neuen Vorlagennamen.  
  
## <a name="failed-to-enable-directaccess-otp-when-webdav-is-installed"></a>Fehler beim Aktivieren von DirectAccess-OTP wenn WebDAV installiert ist  
**Szenario**. Beim Versuch, die zum Anwenden der DirectAccess-OTP-Konfiguration in der Remotezugriffs-Verwaltungskonsole oder mithilfe der `Enable-DAOtpAuthentication` PowerShell-Cmdlet, schlägt der Vorgang fehl.  
  
**Fehler** (Server-Ereignisprotokoll). DirectAccess-OTP-Einstellungen können nicht angewendet werden, da die WebDAV IIS-Erweiterung auf dem Server ausgeführt wird. Entfernen Sie WebDAV, und wenden Sie die Einstellungen erneut.  
  
**Ursache**  
  
Der DirectAccess-OTP-Dienst ist nicht kompatibel mit der WebDAV-Veröffentlichung-Funktion und kann nicht aktiviert werden, während WebDAV installiert wird.  
  
**Lösung**  
  
Deinstallieren Sie die WebDAV-Rolle:  
  
1.  Klicken Sie in der Server-Manager-Konsole in den linken Bereich auf **IIS**.  
  
2.  Im Hauptfenster einen Bildlauf zu **von Rollen und FEATURES**.  
  
3.  Mit der rechten Maustaste **WebDAV-Veröffentlichung**, und klicken Sie dann auf **Rolle oder Feature entfernen**.  
  
4.  Führen Sie das Entfernen von Rollen und Features-Assistenten.  
  
5.  Wenden Sie die DirectAccess-OTP-Konfiguration an.  
  
## <a name="no-templates-available-in-the-remote-access-management-console"></a>Keine Vorlagen verfügbar, in der Remotezugriffs-Verwaltungskonsole  
**Szenario**. Beim Konfigurieren von OTP oder Registrierung Zertifikatsvorlagen verwenden die Remotezugriffs-Verwaltungskonsole, einige oder alle Vorlagen aus dem Fenster fehlen.  
  
**Ursache**  
  
Es gibt zwei mögliche Ursachen für diesen Fehler aus:  
  
-   Die Vorlage ist nicht gemäß den Anforderungen für DirectAccess-OTP konfiguriert, und daher nicht ausgewählt werden.  
  
-   Die ausgewählten Zertifizierungsstellen unter **OTP-Zertifizierungsstellenserver** sind nicht so konfiguriert, dass die erforderlichen Vorlagen ausgeben.  
  
**Lösung**  
  
1.  Stellen Sie sicher, dass die OTP-anmelden-Vorlage und der OTP-Zertifikatvorlage Signieren ordnungsgemäß konfiguriert sind wie beschrieben in 3.2 Plan für die OTP-Zertifikatvorlage und 3.3 der registrierungsstellenzertifikats planen.  
  
2.  Stellen Sie sicher, dass die konfigurierten Zertifizierungsstellen in der **OTP-Zertifizierungsstellenserver** Liste sind so konfiguriert, dass die Probleme die relevanten Vorlagen:  
  
    1.  Öffnen Sie auf dem Zertifizierungsstellenserver die Zertifizierungsstellenkonsole.  
  
    2.  Erweitern Sie im linken Bereich ausgewählte ZS-Servers ein.  
  
    3.  Klicken Sie auf **Zertifikatvorlagen** und stellen Sie sicher, dass die erforderlichen Vorlagen aktiviert sind. Falls nicht, mit der rechten Maustaste **Zertifikatvorlagen**, klicken Sie auf **neu**, klicken Sie auf **Auszustellende Zertifikatvorlage ausstellen**, und wählen Sie dann die Vorlagen, die Sie aktivieren möchten.  
  
## <a name="cannot-set-renewal-period-of-otp-template-to-1-hour"></a>Erneuerungszeitraums der OTP-Vorlage kann nicht auf 1 Stunde festgelegt werden.  
**Szenario**. Wenn die DirectAccess-OTP-anmelden-Vorlage mithilfe von Windows 2003-Zertifizierungsstelle zu konfigurieren, ist es nicht möglich, den Erneuerungszeitraum der Vorlage auf 1 Stunde festgelegt.  
  
**Ursache**  
  
Das Zertifikatvorlagen-MMC-Snap-in in Windows Server 2003 kann nicht den Erneuerungszeitraum einer Vorlage auf 1 Stunde festlegen.  
  
**Lösung**  
  
Zertifikatvorlagen-Snap-in auf einem nach der Windows Server 2003-Server installieren und verwenden sie zum Konfigurieren der OTP-anmelden-Vorlage finden Sie unter [installieren, die Zertifikatvorlagen-Snap-Ins](https://technet.microsoft.com/library/cc732445.aspx).  
  


