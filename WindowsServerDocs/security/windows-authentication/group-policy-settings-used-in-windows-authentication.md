---
title: In der Windows-Authentifizierung verwendete Gruppenrichtlinieneinstellungen
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 352e67dead6e22085a8e7350dd7e5c18c6d74676
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403256"
---
# <a name="group-policy-settings-used-in-windows-authentication"></a>In der Windows-Authentifizierung verwendete Gruppenrichtlinieneinstellungen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Referenz Thema für IT-Experten werden die Verwendung und Auswirkung von Gruppenrichtlinie Einstellungen im Authentifizierungsprozess beschrieben.

Sie können die Authentifizierung in Windows-Betriebssystemen verwalten, indem Sie Benutzer-, Computer-und Dienst Konten zu Gruppen hinzufügen und anschließend Authentifizierungs Richtlinien für diese Gruppen anwenden. Diese Richtlinien werden als lokale Sicherheitsrichtlinien und als administrative Vorlagen definiert, auch als Gruppenrichtlinie Einstellungen bezeichnet. Beide Sätze können mit Gruppenrichtlinie in ihrer gesamten Organisation konfiguriert und verteilt werden.

> [!NOTE]
> Mithilfe der in Windows Server 2012 R2 eingeführten Features können Sie Authentifizierungs Richtlinien für gezielte Dienste oder Anwendungen, die häufig als Authentifizierungs Silos bezeichnet werden, mithilfe geschützter Konten konfigurieren. Informationen dazu, wie Sie dies in Active Directory tun, finden Sie unter [Konfigurieren geschützter Konten](how-to-configure-protected-accounts.md).

Beispielsweise können Sie die folgenden Richtlinien auf Grundlage ihrer Funktion in der Organisation auf Gruppen anwenden:

-   Lokal oder in einer Domäne anmelden

-   Anmelden über ein Netzwerk

-   Konten zurücksetzen

-   Erstellen von Konten

In der folgenden Tabelle sind die für die-Authentifizierung relevanten Richtlinien Gruppen aufgeführt. es enthält Links zu Dokumentationen, mit denen Sie diese Richtlinien konfigurieren können.

|Richtlinien Gruppe|Speicherort|Beschreibung|
|--------|------|--------|
|**Kenn Wort Richtlinie**|Lokaler Computer policy\computerkonfiguration\windows-einstellungen\sicherheitseinstellungen\konto Richtlinien|Kenn Wort Richtlinien beeinflussen die Merkmale und das Verhalten von Kenn Wörtern. Kenn Wort Richtlinien werden für Domänen Konten oder lokale Benutzerkonten verwendet. Sie bestimmen Einstellungen für Kenn Wörter, z. b. Erzwingung und Lebensdauer.<br /><br />Informationen zu bestimmten Einstellungen finden Sie unter Kenn [Wort Richtlinie](https://technet.microsoft.com/itpro/windows/keep-secure/password-policy).|
|**Konto Sperr Richtlinie**|Lokaler Computer policy\computerkonfiguration\windows-einstellungen\sicherheitseinstellungen\konto Richtlinien|Optionen für die Konto Sperrungs Richtlinie deaktivieren Sie Konten nach einer festgelegten Anzahl fehlerhafter Anmeldeversuche. Mithilfe dieser Optionen können Sie Versuche zum Unterbrechen von Kenn Wörtern erkennen und blockieren.<br /><br />Informationen zu den Optionen für die Konto Sperrungs Richtlinie finden Sie unter [Konto Sperr Richtlinie](https://technet.microsoft.com/itpro/windows/keep-secure/account-lockout-policy).|
|**Kerberos-Richtlinie**|Lokaler Computer policy\computerkonfiguration\windows-einstellungen\sicherheitseinstellungen\konto Richtlinien|Die Kerberos-bezogenen Einstellungen umfassen die Ticket Lebensdauer und Erzwingungs Regeln. Die Kerberos-Richtlinie gilt nicht für lokale Konto Datenbanken, da das Kerberos-Authentifizierungsprotokoll nicht verwendet wird, um lokale Konten zu authentifizieren. Aus diesem Grund können die Kerberos-Richtlinien Einstellungen nur mithilfe des standardmäßigen Domänen Gruppenrichtlinie Objekts (GPO) konfiguriert werden, wo es sich auf Domänen Anmeldungen auswirkt.<br /><br />Informationen zu Kerberos-Richtlinien Optionen für den Domänen Controller finden Sie unter [Kerberos-Richtlinie](https://technet.microsoft.com/itpro/windows/keep-secure/kerberos-policy).|
|**Überwachungsrichtlinie**|Lokaler Computer policy\computerkonfiguration\windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien \ Überwachungsrichtlinie|Mithilfe der Überwachungsrichtlinie können Sie den Zugriff auf Objekte, wie z. b. Dateien und Ordner, Steuern und verstehen sowie Benutzer-und Gruppenkonten sowie Benutzeranmeldungen und-Abrechnungen verwalten. Mit Überwachungs Richtlinien können die Kategorien von Ereignissen angegeben werden, die Sie überwachen möchten, die Größe und das Verhalten des Sicherheitsprotokolls festlegen und bestimmen, welche Objekte der Zugriff überwacht werden sollen und welche Art von Zugriff Sie überwachen möchten.<br /><br />|
|**Zuweisung von Benutzerrechten**|Lokale Computer policy\computerkonfiguration\windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Benutzerrechten|Benutzerrechte werden in der Regel auf Basis der Sicherheitsgruppen zugewiesen, zu denen ein Benutzer gehört, z. b. Administratoren, Hauptbenutzer oder Benutzer. Die Richtlinien Einstellungen in dieser Kategorie werden in der Regel verwendet, um Berechtigungen für den Zugriff auf einen Computer basierend auf der Zugriffs-und Sicherheitsgruppen Mitgliedschaften zu erteilen oder zu verweigern.|
|**Sicherheitsoptionen**|Lokale Computer policy\computerkonfiguration\windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Sicherheitsoptionen|Zu den für die Authentifizierung relevanten Richtlinien gehören:<br /><br />-Geräte<br />-Domänen Controller<br />-Domänen Mitglied<br />-Interaktive Anmeldung<br />-Microsoft-Netzwerkserver<br />-Netzwerk Zugriff<br />-Netzwerksicherheit<br />-Wiederherstellungskonsole<br />-Herunterfahren<br /><br />|
|**Delegierungs Delegierungen**|Computerkonfiguration\Administrative vorlagen\system\anmeldeinformationen Delegierung|Bei der Delegierung von Anmelde Informationen handelt es sich um einen Mechanismus, mit dem lokale Anmelde Informationen auf anderen Systemen verwendet werden können, insbesondere Mitglieds Server und Domänen Controller innerhalb einer Domäne. Diese Einstellungen gelten für Anwendungen mithilfe des Credential Security Support Provider (SSP). Remotedesktopverbindung ist ein Beispiel.|
|**KDC**|Computerkonfiguration\Administrative vorlagen\system\kdc|Diese Richtlinien Einstellungen wirken sich darauf aus, wie die Schlüsselverteilungscenter (KDC), bei der es sich um einen Dienst auf dem Domänen Controller handelt, Kerberos-Authentifizierungsanforderungen verarbeitet.|
|**Kerberos**|Computerkonfiguration\Administrative vorlagen\system\kerberos|Diese Richtlinien Einstellungen beeinflussen, wie Kerberos für die Unterstützung von Ansprüchen, Kerberos armoring, Verbund Authentifizierung, Identifizierung von Proxy Servern und anderen Konfigurationen konfiguriert ist.|
|**Anmelden**|Computerkonfiguration\Administrative Vorlagen\System\Anmeldung|Mit diesen Richtlinien Einstellungen wird gesteuert, wie das System den Anmeldevorgang für Benutzer anzeigt.|
|**Anmelde Namen**|Computerkonfiguration\Administrative vorlagen\system\net-Anmeldung|Mit diesen Richtlinien Einstellungen wird gesteuert, wie das System Netzwerk Anmelde Anforderungen behandelt, einschließlich der Art des Domänen Controller-Locators.<br /><br />Weitere Informationen zur Funktionsweise des Domänen Controller-Locators in Replikations Prozesse finden Sie Untergrund Legendes zur [Replikation Zwischenstand Orten](https://technet.microsoft.com/library/cc771251.aspx).|
|**Biometrie**|Computerkonfiguration\Administrative Vorlagen\Windows-komponents\biometrie|Diese Richtlinien Einstellungen erlauben oder verweigern die Verwendung von Biometrie als Authentifizierungsmethode.<br /><br />Weitere Informationen zur Windows-Implementierung von Biometrie finden Sie unter Windows-Biometrieframework Übersicht.|
|**Anmelde Informationen-Benutzeroberfläche**|Computerkonfiguration\Administrative Vorlagen\Windows-komponents\benutzerbenutzerschnittstelle|Diese Richtlinien Einstellungen steuern, wie Anmelde Informationen zum Zeitpunkt des Eintrags verwaltet werden.|
|**Kenn Wort Synchronisierung**|Computerkonfiguration\Administrative Vorlagen\Windows-komponents\kenn Wort Synchronisierung|Mit diesen Richtlinien Einstellungen wird festgelegt, wie das System die Synchronisierung von Kenn Wörtern zwischen Windows-und UNIX-basierten Betriebssystemen verwaltet.<br /><br />Weitere Informationen finden Sie unter Kenn [Wort Synchronisierung](https://technet.microsoft.com/library/cc732609.aspx).|
|**Smartcard**|Computerkonfiguration\Administrative Vorlagen\Windows-komponents\smartcard|Mit diesen Richtlinien Einstellungen wird gesteuert, wie Smartcardanmeldungen vom System verwaltet werden.<br /><br />|
|**Windows-Anmelde Optionen**|Computerkonfiguration\Administrative Vorlagen\Windows-komponents\windows-Anmelde Optionen|Diese Richtlinien Einstellungen steuern, wann und wie Anmelde Chancen verfügbar sind.|
|**STRG + ALT + ENTF-Optionen**|Computerkonfiguration\Administrative Vorlagen\Windows-komponents\strg + ALT + ENTF-Optionen|Diese Richtlinien Einstellungen wirken sich auf die Darstellung von und den Zugriff auf Funktionen auf der Anmelde Benutzeroberfläche (sicherer Desktop) aus, z. b. Task-Manager und die Tastatursperre des Computers.|
|**Anmelden**|Computerkonfiguration\Administrative Vorlagen\Windows-komponents\logon|Mit diesen Richtlinien Einstellungen wird festgelegt, ob oder welche Prozesse ausgeführt werden können, wenn sich der Benutzer anmeldet.|

## <a name="see-also"></a>Siehe auch
[Windows-Authentifizierung: Technische Übersicht](windows-authentication-technical-overview.md)


