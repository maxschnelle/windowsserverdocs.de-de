---
title: Problembehandlung bei der Aktivierung von OTP
description: Dieses Thema ist Teil des Handbuchs Bereitstellen des Remote Zugriffs mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: b58252ca-4c1d-4664-a3c4-7301e2121517
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a01a52be4ce755c57297ba825be249b9b6853c7d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87958298"
---
# <a name="troubleshooting-enabling-otp"></a>Problembehandlung bei der Aktivierung von OTP

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Dieses Thema enthält Informationen zur Problembehandlung bei Problemen im Zusammenhang mit dem Aktivieren der DirectAccess-OTP-Authentifizierung über das PowerShell-Cmdlet " **enable-daotpauthentication** " oder über die Remote Zugriffs-Verwaltungskonsole.

## <a name="failed-to-enroll-the-otp-signing-certificate"></a>Fehler beim Registrieren des OTP-Signatur Zertifikats.
**Fehler** (Server Ereignisprotokoll). Ein OTP-Signaturzertifikat kann nicht mithilfe der Zertifikat Vorlage <OTP_signing_template_name registriert werden>

**Ursache**

Für diesen Fehler gibt es drei mögliche Ursachen:

-   Die Vorlage ist nicht vorhanden.

-   Die in der Vorlage festgelegten Berechtigungen lassen nicht zu, dass sich der DirectAccess-Server registrieren kann.

-   Es ist keine Netzwerkverbindung mit der ausstellenden Zertifizierungsstelle (Certification Authority, ca) vorhanden.

**Lösung**

1.  Stellen Sie sicher, dass die OTP-Signaturzertifikat Vorlage mit dem angegebenen Namen lautet:

    1.  Ist vorhanden und verfügt über die entsprechenden Berechtigungen.

    2.  Ist so festgelegt, dass Sie von mindestens einer Zertifizierungsstelle ausgestellt wird, die Zertifikate an den DirectAccess-Server ausstellen kann.

2.  Wenn die Vorlage nicht vorhanden ist, erstellen Sie Sie wie in 3,3 Planen des Registrierungsstellen Zertifikats beschrieben. Wenn eine andere entsprechende Vorlage vorhanden ist, konfigurieren Sie DirectAccess OTP mit dem neuen Vorlagen Namen neu.

## <a name="failed-to-enable-directaccess-otp-when-webdav-is-installed"></a>Fehler beim Aktivieren von DirectAccess OTP, wenn WebDAV installiert ist.
**Szenario**. Beim Versuch, die Konfiguration von DirectAccess OTP in der Remote Zugriffs-Verwaltungskonsole oder mithilfe des `Enable-DAOtpAuthentication` PowerShell-Cmdlets anzuwenden, schlägt der Vorgang fehl.

**Fehler** (Server Ereignisprotokoll). DirectAccess-OTP-Einstellungen können nicht angewendet werden, weil die WebDAV-IIS-Erweiterung auf dem Server ausgeführt wird. Entfernen Sie WebDAV, und wenden Sie die Einstellungen erneut an.

**Ursache**

Der DirectAccess-OTP-Dienst ist nicht mit der WebDAV-Veröffentlichungs Funktion kompatibel und kann nicht aktiviert werden, während WebDAV installiert ist.

**Lösung**

Deinstallieren Sie die WebDAV-Rolle:

1.  Klicken Sie in der Server-Manager Konsole im linken Bereich auf **IIS**.

2.  Scrollen Sie im Hauptbereich zu **Rollen und Features**.

3.  Klicken Sie mit der rechten Maustaste auf **WebDAV-Veröffentlichung**, und klicken Sie dann auf **Rolle oder Feature entfernen**.

4.  Vervollständigen Sie den Assistenten zum Entfernen von Rollen und Features.

5.  Wenden Sie die Konfiguration von DirectAccess OTP erneut an.

## <a name="no-templates-available-in-the-remote-access-management-console"></a>In der Remote Zugriffs-Verwaltungskonsole sind keine Vorlagen verfügbar.
**Szenario**. Beim Konfigurieren von OTP-oder Registrierungsstellen-Zertifikat Vorlagen mithilfe der Remote Zugriffs-Verwaltungskonsole fehlen einige oder alle Vorlagen in den Auswahl Fenstern.

**Ursache**

Für diesen Fehler gibt es zwei mögliche Ursachen:

-   Die Vorlage ist nicht gemäß den Anforderungen des DirectAccess-OTP konfiguriert und kann daher nicht ausgewählt werden.

-   Die ausgewählten Zertifizierungsstellen unter den **OTP** -Zertifizierungsstellen Servern sind nicht so konfiguriert, dass die erforderlichen Vorlagen ausgestellt werden.

**Lösung**

1.  Stellen Sie sicher, dass die OTP-Anmeldevorlage und die OTP-Signaturzertifikat Vorlage ordnungsgemäß konfiguriert sind, wie in 3,2 Planen der OTP-Zertifikat Vorlage und 3,3 Planen des Registrierungsstellen Zertifikats beschrieben.

2.  Stellen Sie sicher, dass die konfigurierten Zertifizierungsstellen in der Liste der **OTP** -Zertifizierungsstellen Server so konfiguriert sind, dass Sie die relevanten Vorlagen

    1.  Öffnen Sie auf dem Zertifizierungsstellen Server die Konsole Zertifizierungsstelle.

    2.  Erweitern Sie im linken Bereich den ausgewählten Zertifizierungsstellen Server.

    3.  Klicken Sie auf **Zertifikat Vorlagen** , und stellen Sie sicher, dass die erforderlichen Vorlagen aktiviert sind. Falls nicht, klicken Sie mit der rechten Maustaste auf **Zertifikat Vorlagen**, klicken Sie auf **neu**, dann auf Auszustellende **Zertifikat Vorlage**, und wählen Sie dann die Vorlagen aus, die Sie aktivieren möchten.

## <a name="cannot-set-renewal-period-of-otp-template-to-1-hour"></a>Erneuerungs Zeitraum der OTP-Vorlage kann nicht auf 1 Stunde festgelegt werden.
**Szenario**. Bei der Konfiguration der DirectAccess OTP-Anmeldevorlage mithilfe von Windows 2003 ca ist es nicht möglich, den Erneuerungs Zeitraum der Vorlage auf 1 Stunde festzulegen.

**Ursache**

Mit dem MMC-Snap-in "Zertifikat Vorlagen" in Windows Server 2003 können Sie den Erneuerungs Zeitraum einer Vorlage nicht auf eine Stunde festlegen.

**Lösung**

Installieren Sie das Zertifikat Vorlagen-Snap-in auf einem Post-Windows Server 2003-Server, und verwenden Sie es zum Konfigurieren der OTP-Anmeldevorlage. Weitere Informationen finden Sie unter [Installieren des Zertifikat Vorlagen-Snap-Ins](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732445(v=ws.11))

