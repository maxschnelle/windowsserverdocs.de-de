---
title: In der Windows-Authentifizierung verwendete Gruppenrichtlinieneinstellungen
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847931"
---
# <a name="group-policy-settings-used-in-windows-authentication"></a>In der Windows-Authentifizierung verwendete Gruppenrichtlinieneinstellungen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Referenzthema für IT-Experten beschreibt die Verwendung und die Auswirkungen der Einstellungen für Gruppenrichtlinien bei der Authentifizierung.

Sie können die Authentifizierung in Windows-Betriebssystemen durch Hinzufügen von Benutzer-, Computer- und Dienstkonten zu Gruppen, und klicken Sie dann durch Anwenden von Authentifizierungsrichtlinien zu diesen Gruppen verwalten. Diese Richtlinien werden als lokale Sicherheitsrichtlinien sowie administrative Vorlagen, auch bekannt als Einstellungen für Gruppenrichtlinien definiert. Beide können konfiguriert und in Ihrer Organisation mithilfe von Gruppenrichtlinien verteilt werden.

> [!NOTE]
> Funktionen in Windows Server 2012 R2, ermöglichen Ihnen das Konfigurieren von Authentifizierungsrichtlinien für gezielte Dienste oder Anwendungen, häufig authentifizierungssilos, mithilfe geschützter Benutzerkonten. Informationen dazu, wie Sie dies in Active Directory durchführen, finden Sie unter [konfigurieren geschützter Konten](how-to-configure-protected-accounts.md).

Beispielsweise können Sie die folgenden Richtlinien für Gruppen, die basierend auf ihrer Funktion in der Organisation anwenden:

-   Melden Sie sich lokal oder in eine Domäne

-   Melden Sie sich über ein Netzwerk

-   Zurücksetzen der Konten

-   Erstellen von Konten

In der folgende Tabelle sind Richtliniengruppen, die relevant für die Authentifizierung sowie Links zu Dokumentationen, mit denen Sie können diese Richtlinien konfigurieren.

|Gruppenrichtlinie|Pfad|Beschreibung|
|--------|------|--------|
|**Kennwortrichtlinie**|Lokalen Computer Policy\Computer Computerkonfiguration\Windows-Einstellungen\sicherheitseinstellungen\kontorichtlinien|Kennwortrichtlinien Auswirkungen auf die Merkmale und Verhalten von Kennwörtern. Kennwortrichtlinien werden für Domänenkonten oder lokalen Benutzerkonten verwendet. Sie bestimmen die Einstellungen für Kennwörter, z. B. Erzwingungsrichtlinie für Netzwerkzugriffsschutz und der Lebensdauer.<br /><br />Weitere Informationen zu bestimmten Einstellungen finden Sie unter [Kennwortrichtlinie](https://technet.microsoft.com/itpro/windows/keep-secure/password-policy).|
|**Kontosperrungsrichtlinie**|Lokalen Computer Policy\Computer Computerkonfiguration\Windows-Einstellungen\sicherheitseinstellungen\kontorichtlinien|Account Lockout Richtlinienoptionen deaktivieren Konten nach einer bestimmten Anzahl fehlgeschlagener Anmeldeversuche. Diese Optionen können Sie die erkennen und Blockieren von versucht, Kennwörter zu unterbrechen.<br /><br />Informationen zu Konto Lockout Policy-Optionen finden Sie unter [Kontosperrungsrichtlinie](https://technet.microsoft.com/itpro/windows/keep-secure/account-lockout-policy).|
|**Kerberos-Richtlinie**|Lokalen Computer Policy\Computer Computerkonfiguration\Windows-Einstellungen\sicherheitseinstellungen\kontorichtlinien|Ressourcenkontofehler in Verbindung mit den Einstellungen gehören Ticket-Lebensdauer und die Durchsetzung der Regeln. Kerberos-Richtlinie gilt nicht für lokale Datenbanken, da das Kerberos-Authentifizierungsprotokoll nicht verwendet wird, um lokale Konten zu authentifizieren. Aus diesem Grund können die Kerberos-Richtlinieneinstellungen nur mit der Standarddomäne (Group Policy Object, GPO) konfiguriert werden, in dem sie sich auf domänenanmeldungen auswirkt.<br /><br />Weitere Informationen zu Optionen für die Kerberos-Richtlinie für den Domänencontroller, finden Sie unter [Kerberos-Richtlinie](https://technet.microsoft.com/itpro/windows/keep-secure/kerberos-policy).|
|**Überwachungsrichtlinie**|Lokalen Computer Policy\Computer Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\überwachungsrichtlinie|Überwachungsrichtlinie können Sie steuern und den Zugriff auf Objekte, z. B. Dateien und Ordner, und klicken Sie zum Verwalten von Benutzer- und Gruppenkonten und benutzeranmeldungen und Abmeldevorgänge zu verstehen. Überwachungsrichtlinien können die Kategorien der Ereignisse angeben, die Sie verwenden möchten, überwachen und legen Sie die Größe und das Verhalten des Sicherheitsprotokolls zu bestimmen, welche Objekte zum Überwachen des Zugriffs werden sollen und welche Art von Zugriff, die Sie überwachen möchten.<br /><br />|
|**Zuweisen von Benutzerrechten**|Lokalen Computer Policy\Computer Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Benutzerrechten|Benutzerrechte werden in der Regel auf der Grundlage der Sicherheitsgruppen zugewiesen, die ein Benutzer, z. B. Administratoren, Hauptbenutzer oder Benutzer angehört. Die Einstellungen in dieser Kategorie werden in der Regel zum gewähren oder Verweigern von Berechtigungen auf einem Computer, auf der Grundlage der Methode der Gruppenmitgliedschaften von Zugriff und Sicherheit.|
|**Sicherheitsoptionen**|Lokalen Computer Policy\Computer Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\sicherheitsoptionen|Richtlinien für die Authentifizierung relevant sind:<br /><br />-Geräte<br />-Domänencontroller<br />: Domänenmitglied<br />-Interaktive Anmeldung<br />-Microsoft-Netzwerkserver<br />-Netzwerkzugriff<br />-Netzwerksicherheit<br />-Recovery-Konsole<br />– Herunterfahren<br /><br />|
|**Delegierung von Anmeldeinformationen**|Computer Configuration\Administrative Templates\System\Credentials Delegierung|Die Delegierung von Anmeldeinformationen ist ein Mechanismus, mit der lokale Anmeldeinformationen, die auf anderen Systemen, insbesondere bei Mitgliedsservern und Domänencontrollern innerhalb einer Domäne verwendet werden kann. Diese Einstellungen gelten für Anwendungen mithilfe der Credential Security Support Provider (SSP Cred). Remotedesktop-Verbindung ist ein Beispiel.|
|**KDC**|Computer Configuration\Administrative Templates\System\KDC|Diese Richtlinieneinstellungen beeinflussen, wie das Schlüsselverteilungscenter (KDC), einem Dienst auf dem Domänencontroller, die Kerberos-authentifizierungsanforderungen verarbeitet.|
|**Kerberos**|Computer Configuration\Administrative Templates\System\Kerberos|Diese Richtlinieneinstellungen beeinflussen, wie Kerberos konfiguriert ist, um Unterstützung für Ansprüche, Kerberos-hochrüstung, Verbundauthentifizierung, identifizierende webanwendungsproxy-Server und andere Konfigurationen zu behandeln.|
|**Logon**|Computerkonfiguration\Administrative Vorlagen\System\Anmeldung|Diese Einstellungen steuern, wie das System die anmeldeerfahrung für Benutzer zeigt.|
|**Anmeldedienst**|Computer Configuration\Administrative Templates\System\Net Anmeldung|Diese Richtlinieneinstellungen steuern, wie das System Netzwerk anmeldeanforderungen, einschließlich der Domänencontrollerlocator Verhalten behandelt.<br /><br />Weitere Informationen darüber, wie der Domänencontrollerlocator in Replikationsprozessen einfügt, finden Sie unter [Grundlegendes zur Replikation zwischen Standorten](https://technet.microsoft.com/library/cc771251.aspx).|
|**Biometrie**|Computer Configuration\Administrative Templates\Windows Components\Biometrics|Mit diesen Richtlinieneinstellungen wird im Allgemeinen zulassen oder verweigern die Verwendung der Biometrie als Authentifizierungsmethode.<br /><br />Informationen über die Windows-Implementierung der Biometrie finden Sie in der Windows-Biometrieframework: Übersicht.|
|**Anmeldeinformationen-Benutzeroberfläche**|Computer Computerkonfiguration\Administrative Vorlagen\Windows-Komponenten\benutzerschnittstelle|Diese Richtlinieneinstellungen steuern, wie die Anmeldeinformationen zum Zeitpunkt der Eintrag verwaltet werden.|
|**Die Synchronisierung von Kennwörtern**|Computer Configuration\Administrative Templates\Windows Components\Password Synchronisierung|Diese Richtlinieneinstellungen bestimmen, wie das System für die Synchronisierung von Kennwörtern zwischen Windows und UNIX-basierten Betriebssystemen verwaltet werden.<br /><br />Weitere Informationen finden Sie unter [Kennwortsynchronisierung](https://technet.microsoft.com/library/cc732609.aspx).|
|**Smartcard**|Computer Configuration\Administrative Templates\Windows Components\Smart-Karte|Mit diesen Richtlinieneinstellungen wird steuern, wie das System smartcardanmeldungen verwaltet.<br /><br />|
|**Windows-Anmeldeoptionen**|Computer Computerkonfiguration\Administrative Vorlagen\Windows-Komponenten\Windows-Anmeldeoptionen|Diese Richtlinieneinstellungen steuern, wann und wie Anmeldung Möglichkeiten zur Verfügung stehen.|
|**Strg + Alt + Entf-Optionen**|Computer Configuration\Administrative Templates\Windows Components\Ctrl + Alt + Entf-Optionen|Diese Richtlinieneinstellungen Auswirkungen auf die Darstellung und der Zugriff auf Funktionen, die auf die Anmeldebenutzeroberfläche (sicheren Desktop), z. B. Task-Manager und die Sperre der Tastatur des Computers.|
|**Logon**|Computer Configuration\Administrative Templates\Windows Components\Logon|Diese Richtlinieneinstellungen bestimmen, ob oder welche Prozesse bei der Anmeldung des Benutzers ausgeführt werden.|

## <a name="see-also"></a>Siehe auch
[Technische Übersicht über Windows-Authentifizierung](windows-authentication-technical-overview.md)


