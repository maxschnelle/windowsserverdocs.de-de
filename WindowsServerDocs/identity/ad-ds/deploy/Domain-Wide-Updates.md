---
ms.assetid: 2a5d5271-6ac6-4c1b-b4ef-9b568932a55a
title: "Active Directory-domänenweite Schema-Updates"
description: "Domänenweite Schema-Updates, die von Adprep ausgeführt /domainprep beim Heraufstufen eines Domänencontrollers"
author: MicrosoftGuyJFlo
ms.author: joflore
manager: femila
ms.date: 07/14/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 59efb7c854b7f3693776bf9a1a371f98c2206d60
ms.sourcegitcommit: 79c1359232bece2e5c3ee5507f1e4bf19b44f487
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/19/2018
---
# <a name="domain-wide-schema-updates"></a>Domänenweite Schema-Updates

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Sie können überprüfen, die folgende Gruppe von Änderungen, um zu verstehen und Vorbereiten von Schemaupdates, die von Adprep ausgeführt werden /domainprep in Windows Server. 

Adprep-Befehle ab Windows Server 2012, während der Installation von AD DS nach Bedarf automatisch ausgeführt. Sie können auch separat vor der AD DS-Installation ausgeführt werden. Weitere Informationen finden Sie unter [Running Adprep.exe](https://technet.microsoft.com/library/dd464018(v=ws.10).aspx).

Weitere Informationen zur Interpretation der Access-Steuerelement (Entry, ACE) Zeichenfolgen finden Sie unter [ACE Zeichenfolgen](https://msdn.microsoft.com/library/aa374928(VS.85).aspx). Weitere Informationen zur Interpretation dieser Sicherheits-ID (SID) Zeichenfolgen finden Sie unter [SID-Zeichenfolgen](https://msdn.microsoft.com/library/aa379602(VS.85).aspx).

## <a name="windows-server-semi-annual-channel-domain-wide-updates"></a>Windows Server (Semikolons jährlichen Channel): Domänenweite aktualisiert

Nach den Vorgängen, die vom ausgeführt werden, **Domainprep** in Windows Server2016 (Vorgang 89) abgeschlossen ist, die **Revision** -Attribut für das CN = ActiveDirectoryUpdate, CN = DomainUpdates, CN = System, DC = Stammdomäne der Gesamtstruktur -Objekt **16**.

|Anzahl der Vorgänge und die GUID|Beschreibung|Berechtigungen|
|------------------------------|---------------|--------------|---------------|
|**Vorgang 89**: {A0C238BA-9E30-4EE6-80A6-43F731E9A5CD}|Löschen Sie den ACE Gewähren von Vollzugriff für Unternehmensadministratoren Schlüssel, und fügen Sie einen ACE gewähren Enterprise Schlüssel Administratoren Vollzugriff auf das MsdsKeyCredentialLink-Attribut.|(A; löschen CI; RPWPCRLCLOCCDCRCWDWOSDDTSW;; Wichtige Organisations-Admins) <br /> <br />Fügen Sie hinzu (OA; CI; RPWP; 5b47d60f-6090-40b2-9f37-2a4de88f3063; Wichtige Organisations-Admins)|

## <a name="windows-server-2016-domain-wide-updates"></a>Windows Server 2016: Domänenweite Updates

Nach den Vorgängen, die vom ausgeführt werden, **Domainprep** in Windows Server2016 (Vorgänge 82 88) abgeschlossen ist, die **Revision** -Attribut für das CN = ActiveDirectoryUpdate, CN = DomainUpdates, CN = System, DC = Stammdomäne Objekt festgelegt ist **15**.

|Anzahl der Vorgänge und die GUID|Beschreibung|Attribute|Berechtigungen|
|------------------------------|---------------|--------------|---------------|
|**Vorgang 82**: {83C53DA7-427E-47A4-A07A-A324598B88F7}|Erstellen von CN = Schlüssel Container am Stamm der Domäne|-ObjectClass: Container<br />-Beschreibung: Standard-Container für wichtige Anmeldeinformationen Objekte<br />-ShowInAdvancedViewOnly: TRUE|(A; CI; RPWPCRLCLOCCDCRCWDWOSDDTSW;; EA)<br />(A; CI; RPWPCRLCLOCCDCRCWDWOSDDTSW;; D A)<br />(A; CI; RPWPCRLCLOCCDCRCWDWOSDDTSW;; SY)<br />(A; CI; RPWPCRLCLOCCDCRCWDWOSDDTSW;; D D)<br />(A; CI; RPWPCRLCLOCCDCRCWDWOSDDTSW;; ED)|
|**Vorgang 83**: {C81FC9CC-0130-4FD1-B272-634D74818133}|Hinzufügen von Vollzugriff zulassen Aces, CN = Schlüssel Container für "Domain\Key Admins" und "Rootdomain\Enterprise Schlüssel-Admins".|N/V|(A; CI; RPWPCRLCLOCCDCRCWDWOSDDTSW;; Wichtige Administratoren)<br />(A; CI; RPWPCRLCLOCCDCRCWDWOSDDTSW;; Wichtige Organisations-Admins)|
|**Vorgang 84**: {E5F9E791-D96D-4FC9-93C9-D53E1DC439BA}|Ändern Sie OtherWellKnownObjects-Attribut auf CN = Schlüssel Container.|-OtherWellKnownObjects: B:32:683A24E2E8164BD3AF86AC3C2CF3F981:CN = %ws-Schlüssel|N/V|
|**Vorgang 85**: {e6d5fd00-385d-4e65-b02d-9da3493ed850}|Ändern der Domäne NC gestatten "Domain\Key Admins" und "Rootdomain\Enterprise Schlüssel-Admins" zum Ändern des Msds-KeyCredentialLink-Attributs. |N/V|(OA; CI; RPWP; 5b47d60f-6090-40b2-9f37-2a4de88f3063; Wichtige Administratoren)<br />(OA; CI; RPWP; 5b47d60f-6090-40b2-9f37-2a4de88f3063; Unternehmensadministratoren Schlüssel in der Stammdomäne, aber in Nicht-Stamm-Domänen führte dazu, dass eine gefälschte Domäne relativer ACE mit einer nicht auflösbaren-527 SID)|
|**Vorgang 86**: {3a6b3fbf-3168-4312-a10d-dd5b3393952d}|Erteilen Sie der DS-überprüft-Write-Computer Auto Ersteller-Besitzer und den aktuellen|N/V|(OA; CIIO;SW;9b026da6-0d3c-465c-8bee-5199d7165cba;bf967a86-0de6-11D0-a285-00aa003049e2;PS)<br />(OA; CIIO;SW;9b026da6-0d3c-465c-8bee-5199d7165cba;bf967a86-0de6-11D0-a285-00aa003049e2;CO)|
|**Vorgang 87**: {7F950403-0AB3-47F9-9730-5D7B0269F9BD}|Löschen Sie den ACE zu gewähren der falschen Gruppe der Domäne relativer Unternehmensadministratoren Schlüssel, und fügen Sie einen ACE Schlüssel Unternehmensadministratorgruppe Vollzugriff erteilen. |N/V|(A; löschen CI; RPWPCRLCLOCCDCRCWDWOSDDTSW;; Wichtige Organisations-Admins)<br /> <br />(A; hinzufügen CI; RPWPCRLCLOCCDCRCWDWOSDDTSW;; Wichtige Organisations-Admins)|
|**Vorgang 88**: {434bb40d-dbc9-4fe7-81d4-d57229f7b080}|Hinzufügen von "MsDS-ExpirePasswordsOnSmartCardOnlyAccounts" für die Domäne NC-Objekt und Standardwert auf "false" festgelegt|N/V|N/V|

Die Gruppen Schlüssel Unternehmensadministratoren und Schlüssel Admins werden nur erstellt, nachdem ein Windows Server2016-Domänencontroller heraufgestuft wird und der PDC-Emulator-FSMO-Rolle übernimmt.

## <a name="windows-server-2012-r2-domain-wide-updates"></a>Windows Server 2012 R2: Domänenweite aktualisiert

Zwar keine Vorgänge ausgeführt werden, indem Sie **Domainprep** in Windows Server2012 R2, nachdem der Befehl abgeschlossen ist, die **Revision** -Attribut für das CN = ActiveDirectoryUpdate, CN = DomainUpdates, CN = System, DC = Stammdomäne Objekt festgelegt ist **10**.

## <a name="windows-server-2012-domain-wide-updates"></a>Windows Server 2012: Domänenweite Updates

Nach den Vorgängen, die vom ausgeführt werden, **Domainprep** in Windows Server2012 (Vorgänge 78, 79, 80 und 81) abgeschlossen ist, die **Revision** -Attribut für das CN = ActiveDirectoryUpdate, CN = DomainUpdates, CN = System, DC = Stammdomäne Objekt festgelegt ist **9**.

|Anzahl der Vorgänge und die GUID|Beschreibung|Attribute|Berechtigungen|
|------------------------------|---------------|--------------|---------------|
|**Vorgang 78**: {c3c927a6-cc1d-47c0-966b-be8f9b63d991}|Erstellen Sie ein neues Objekt CN = TPM-Geräte in der Domänenpartition.|Object-Klasse: MsTPM-InformationObjectsContainer|N/V|
|**Vorgang 79**: {54afcfb9-637a-4251-9f47-4d50e7021211}|Erstellt einen Eintrag für den TPM-Dienst.|N/V|(OA; CIIO; WP;ea1b7b93-5e48-46d5-bc6c-4df4fda78a35;bf967a86-0de6-11D0-a285-00aa003049e2;PS)|
|**Vorgang 80**: {f4728883-84dd-483c-9897-274f2ebcf11e}|Erteilen Sie "Klon-DC" Erweitertes Recht, mit **Klonbare Domänencontroller** Gruppe|N/V|(OA; CR; 3e0f7e18-2c7a-4c10-ba82-4d926db99a3e; *Domänen-SID*-522)|
|**Vorgang 81**: {ff4f9d27-7157-4cb0-80a9-5d6f2b14c8ff}|Erteilen Sie für alle Objekte ms-DS-Allowed-To-Act-On-Behalf-Of-Other-Identity Prinzipal selbst.|N/V|(OA; CIOI; RPWP; 3f78c3e5-f79a-46bd-a0b8-9d18116ddc79; PS)|
