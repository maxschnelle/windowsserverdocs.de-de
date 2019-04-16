---
title: Gruppenrichtlinien Sie in Windows-Authentifizierung verwendete
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9e237f89-45b1-4a4e-9b72-11dc7d6a470b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 38df2033b57c0394b96f539f54efe6a3579500f2
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="group-policy-settings-used-in-windows-authentication"></a>Gruppenrichtlinien Sie in Windows-Authentifizierung verwendete

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Referenzthema für IT-Experten beschreibt die Verwendung und die Auswirkungen der Gruppenrichtlinien-Einstellungen bei der Authentifizierung.

Sie können die Authentifizierung in Windows-Betriebssystemen durch Benutzer, Computer und Dienstkonten zu Gruppen hinzufügen und dann durch Anwenden von Authentifizierungsrichtlinien für diese Gruppen verwalten. Diese Richtlinien werden als lokale Sicherheitsrichtlinien und administrativen Vorlagen, auch bekannt als Gruppenrichtlinien-Einstellungen definiert. Beide werden konfiguriert und in der gesamten Organisation mithilfe von Gruppenrichtlinien verteilt.

> [!NOTE]
> In Windows Server 2012 R2 eingeführte Funktionen können Sie Authentifizierungsrichtlinien für zielgerichtete Dienste konfigurieren oder Anwendungen, der so genannte authentifizierungssilos, mithilfe von geschützter Benutzerkonten. Informationen dazu, wie Sie hierzu in Active Directory finden Sie unter [How to Configure Protected Accounts](how-to-configure-protected-accounts.md).

Beispielsweise können Sie die folgenden Richtlinien für Gruppen, basierend auf deren Funktion in der Organisation anwenden:

-   Melden Sie sich lokal oder mit einer Domäne

-   Melden Sie sich über ein Netzwerk

-   Zurücksetzen von Konten

-   Erstellen von Konten

In der folgende Tabelle sind für die Authentifizierung relevant Richtliniengruppen sowie Links zur Dokumentation, die Ihnen helfen, diese Richtlinien konfigurieren.

|Richtliniengruppe|Speicherort|Beschreibung|
|--------|------|--------|
|**Kennwortrichtlinie**|Lokaler Computer Policy\Computer Computerkonfiguration\Windows-Einstellungen\sicherheitseinstellungen\kontorichtlinien|Kennwortrichtlinien Einfluss auf die Merkmale und Verhalten von Kennwörtern. Kennwortrichtlinien werden für Domänenkonten oder lokale Benutzerkonten verwendet. Sie bestimmen die Einstellungen für Kennwörter, z. B. erzwingungseinstellungen und die Lebensdauer.<br /><br />Weitere Informationen zu bestimmten Einstellungen finden Sie unter [Kennwortrichtlinie](https://technet.microsoft.com/itpro/windows/keep-secure/password-policy).|
|**Kontosperrungsrichtlinie**|Lokaler Computer Policy\Computer Computerkonfiguration\Windows-Einstellungen\sicherheitseinstellungen\kontorichtlinien|Optionen für Konto-Sperre deaktivieren Sie Konten nach einer festgelegten Anzahl von fehlgeschlagenen Anmeldeversuchen. Mit diesen Optionen können Sie erkennen und blockieren versucht, Kennwörter zu unterbrechen.<br /><br />Informationen zum Konto Sperre Richtlinienoptionen finden Sie unter [Kontosperrungsrichtlinie](https://technet.microsoft.com/itpro/windows/keep-secure/account-lockout-policy).|
|**Kerberos-Richtlinie**|Lokaler Computer Policy\Computer Computerkonfiguration\Windows-Einstellungen\sicherheitseinstellungen\kontorichtlinien|Kerberos-bezogene Einstellungen umfassen Ticket-Lebensdauer und Erzwingung. Kerberos-Richtlinie gilt nicht für lokales Kontodatenbanken, da das Kerberos-Authentifizierungsprotokoll nicht verwendet wird, um lokale Konten zu authentifizieren. Daher können die Kerberos-Richtlinieneinstellungen nur mit der Standarddomäne (Group Policy Object, GPO) konfiguriert werden, in dem sie domänenanmeldungen beeinflusst.<br /><br />Informationen zu den Optionen der Kerberos-Richtlinie für den Domänencontroller, finden Sie unter [Kerberos-Richtlinie](https://technet.microsoft.com/itpro/windows/keep-secure/kerberos-policy).|
|**Überwachungsrichtlinie**|Lokaler Computer Policy\Computer Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\überwachungsrichtlinie|Überwachungsrichtlinien können Sie steuern und den Zugriff auf Objekte, z. B. Dateien und Ordner, und klicken Sie zum Verwalten von Benutzer- und Gruppenkonten und benutzeranmeldungen und Abmeldevorgänge zu verstehen. Überwachungsrichtlinien können die Kategorien der Ereignisse angeben, die Sie verwenden möchten, überwachen, die Größe und das Verhalten des Sicherheitsprotokolls festlegen und bestimmen, welche Objekte zum Überwachen des Zugriffs werden sollen und welche Art von Zugriff, die Sie überwachen möchten.<br /><br />|
|**Zuweisen von Benutzerrechten**|Lokaler Computer Policy\Computer Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Benutzerrechten|Benutzerrechte werden in der Regel auf der Grundlage der Sicherheitsgruppen zugewiesen, die ein Benutzer, z. B. Administratoren, Hauptbenutzer oder Benutzer angehört. Die Richtlinieneinstellungen in dieser Kategorie werden in der Regel zum gewähren oder Verweigern von Zugriff auf einen Computer anhand der Methode der Gruppenmitgliedschaft für den Zugriff und Sicherheit verwendet.|
|**Sicherheitsoptionen**|Lokaler Computer Policy\Computer Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\sicherheitsoptionen|Richtlinien für die Authentifizierung relevant sind:<br /><br />-Geräte<br />-Domänencontroller<br />-Domänenmitglieder sind<br />-Interaktive Anmeldung<br />-Microsoft Netzwerkserver<br />-Netzwerkzugriff<br />-Netzwerk Sicherheit<br />-Wiederherstellungskonsole<br />-Herunterfahren<br /><br />|
|**Delegierung von Anmeldeinformationen**|Computer Configuration\Administrative Templates\System\Credentials Delegierung|Die Delegierung von Anmeldeinformationen ist ein Mechanismus, der mit lokale Anmeldeinformationen auf anderen Systemen, insbesondere auf Mitgliedsservern und Domänencontrollern innerhalb einer Domäne verwendet werden können. Diese Einstellungen gelten für Anwendungen mit dem Credential Security Support Provider (SSP Cred). Remotedesktopverbindung ist ein Beispiel.|
|**KDC**|Computer Configuration\Administrative Templates\System\KDC|Diese Einstellungen beeinflussen, wie die Schlüsselverteilungscenter (KDC), die einen Dienst auf dem Domänencontroller ist, Kerberos-authentifizierungsanforderungen verarbeitet.|
|**Kerberos**|Computer Configuration\Administrative Templates\System\Kerberos|Diese Einstellungen beeinflussen, wie Kerberos für die Behandlung von Unterstützung für Ansprüche, Kerberos-hochrüstung, Verbundauthentifizierung, identifizierende Proxyservern und andere Konfigurationen konfiguriert ist.|
|**Anmeldung**|Benutzerkonfiguration|Diese Richtlinieneinstellungen steuern, wie das System den Anmeldevorgang für Benutzer zeigt.|
|**Der Anmeldedienst**|Computer Configuration\Administrative Templates\System\Net Anmeldung|Diese Richtlinieneinstellungen steuern, wie das System Netzwerk anmeldeanforderungen, die das Verhalten der Domänencontrollerlocator einschließlich behandelt.<br /><br />Weitere Informationen dazu, wie der Domänencontrollerlocator in Replikationsvorgänge passt, finden Sie unter [Grundlegendes zur Replikation zwischen Standorten](https://technet.microsoft.com/library/cc771251.aspx).|
|**Biometrische Daten**|Computer Configuration\Administrative Templates\Windows Components\Biometrics|Diese Einstellungen in der Regel zulassen oder Verweigern der Verwendung biometrischer Daten als Authentifizierungsmethode.<br /><br />Informationen zu Windows-Implementierung von biometrischen Daten finden Sie in der Windows-Biometrieframework: Übersicht.|
|**Anmeldeinformationen-Benutzeroberfläche**|Computer Computerkonfiguration\Administrative Vorlagen\Windows-Komponenten\benutzerschnittstelle|Diese Richtlinieneinstellungen steuern, wie Anmeldeinformationen zum Zeitpunkt der Eintrag verwaltet werden.|
|**Synchronisierung von Kennwörtern**|Computer Configuration\Administrative Templates\Windows Components\Password Synchronisierung|Diese Einstellungen bestimmen, wie das System die Synchronisierung von Kennwörtern zwischen Windows- und UNIX-basierten Betriebssystemen verwaltet.<br /><br />Weitere Informationen finden Sie unter [Kennwortsynchronisierung](https://technet.microsoft.com/library/cc732609.aspx).|
|**Smartcard**|Computer Configuration\Administrative Templates\Windows Components\Smart Karte|Diese Richtlinieneinstellungen steuern, wie das System die Smartcard-Anmeldung verwaltet.<br /><br />|
|**Windows-Anmeldeoptionen**|Computer Computerkonfiguration\Administrative Vorlagen\Windows-Komponenten\Windows-Anmeldeoptionen|Diese Richtlinieneinstellungen steuern, wann und wie Anmeldung Möglichkeiten zur Verfügung stehen.|
|**Strg + Alt + Entf-Optionen**|Computerkonfiguration\Administrative Vorlagen\Windows-Components\Ctrl + Alt + Entf-Optionen|Diese Richtlinieneinstellungen wirken sich auf die Darstellung von und den Zugriff auf Funktionen auf der Anmeldebenutzeroberfläche (sicheren Desktop), z. B. Task-Manager und die Tastatur Sperren des Computers.|
|**Anmeldung**|Computer Configuration\Administrative Templates\Windows Components\Logon|Diese Einstellungen bestimmen, ob oder welche Prozesse bei der Anmeldung des Benutzers ausgeführt werden.|

## <a name="see-also"></a>Siehe auch
[Technische Übersicht über Windows-Authentifizierung](windows-authentication-technical-overview.md)


