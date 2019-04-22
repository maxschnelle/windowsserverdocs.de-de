---
ms.assetid: 2a5d5271-6ac6-4c1b-b4ef-9b568932a55a
title: Active Directory Domain-Wide-Schema-updates
description: Domänenweite schemaaktualisierungen von Adprep/domainprep ausgeführt wird, wenn es sich bei einem Domänencontroller heraufstufen
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 10/29/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 20598431b9c2376051247fd7ba14e33af00968cc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812321"
---
# <a name="domain-wide-schema-updates"></a>Domänenweite-Schema-updates

>Gilt für: Windows Server

Sie können überprüfen, dass die folgende Gruppe von Änderungen, um zu verstehen und Vorbereiten für die Schemaupdates, die von Adprep/domainprep / in Windows Server ausgeführt werden.

Ab Windows Server 2012 führen Adprep-Befehlen automatisch nach Bedarf während der AD DS-Installation. Sie können auch separat im Voraus über AD DS-Installation ausgeführt werden. Weitere Informationen finden Sie unter [Ausführen von Adprep.exe](https://technet.microsoft.com/library/dd464018(v=ws.10).aspx).

Weitere Informationen zur Interpretation dieser Access Control Entry (ACE) Zeichenfolgen, finden Sie unter [ACE Zeichenfolgen](https://msdn.microsoft.com/library/aa374928(VS.85).aspx). Weitere Informationen zur Interpretation der Zeichenfolgen-ID (SID) Sicherheit finden Sie unter [SID-Zeichenfolgen](https://msdn.microsoft.com/library/aa379602(VS.85).aspx).

## <a name="windows-server-semi-annual-channel-domain-wide-updates"></a>WindowsServer (Halbjährlicher Kanal): Domänenweite updates

Nach dem die Vorgänge, die ausgeführt werden **Domainprep** in Windows Server 2016 (Vorgänge-89) abgeschlossen ist, die **Revision** -Attribut für CN = ActiveDirectoryUpdate, CN = DomainUpdates, CN = System, DC = Gesamtstruktur-Stammdomäne Objekt nastaven NA hodnotu **16**.

|Anzahl der Vorgänge und GUID|Beschreibung|Berechtigungen|
|------------------------------|---------------|--------------|---------------|
|**Operation 89**: {A0C238BA-9E30-4EE6-80A6-43F731E9A5CD}|Löschen Sie den ACE, der Vollzugriff auf Unternehmensadministratoren für die Schlüssel zu gewähren, und fügen Sie ein ACE gewähren der Unternehmen Schlüssel Administratoren-Vollzugriff auf das MsdsKeyCredentialLink-Attribut hinzu.|(A; löschen CI; RPWPCRLCLOCCDCRCWDWOSDDTSW;; Wichtige Organisations-Admins) <br /> <br />Fügen Sie (OA; hinzu CI; RPWP; 5b47d60f-6090-40b2-9f37-2a4de88f3063; Wichtige Organisations-Admins)|

## <a name="windows-server-2016-domain-wide-updates"></a>Windows Server 2016: Domänenweite updates

Nach dem die Vorgänge, die ausgeführt werden **Domainprep** in Windows Server 2016 (82-88-Vorgänge) abgeschlossen ist, die **Revision** -Attribut für CN = ActiveDirectoryUpdate, CN = DomainUpdates, CN = System, DC = Objekt, um festgelegt wird Gesamtstruktur-Stammdomäne **15**.

|Anzahl der Vorgänge und GUID|Beschreibung|Attribute|Berechtigungen|
|------------------------------|---------------|--------------|---------------|
|**Vorgang 82**: {83C53DA7-427E-47A4-A07A-A324598B88F7}|Erstellen von CN = Schlüsselcontainer am Stamm der Domäne|-"objectClass": Container<br />-Beschreibung: Standardcontainer für schlüsselanmeldeinformation-Objekte<br />- ShowInAdvancedViewOnly: TRUE|(A;CI;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;EA)<br />(A;CI;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;DA)<br />(A;CI;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)<br />(A;CI;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;DD)<br />(A;CI;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;ED)|
|**Operation 83**: {C81FC9CC-0130-4FD1-B272-634D74818133}|Fügen Sie Vollzugriff auf zulassen-Aces in CN = Schlüsselcontainer für "Domain\Key Administratoren" und "Rootdomain\Enterprise Schlüsseladministratoren".|Nicht zutreffend|(A; CI; RPWPCRLCLOCCDCRCWDWOSDDTSW;; Key-Admins)<br />(A; CI; RPWPCRLCLOCCDCRCWDWOSDDTSW;; Wichtige Organisations-Admins)|
|**Operation 84**: {E5F9E791-D96D-4FC9-93C9-D53E1DC439BA}|Ändern des OtherWellKnownObjects-Attributs, zeigen Sie auf den CN = Schlüsselcontainer.|-OtherWellKnownObjects: B:32:683A24E2E8164BD3AF86AC3C2CF3F981:CN=Keys,%ws|Nicht zutreffend|
|**Vorgang 85**: {e6d5fd00-385d-4e65-b02d-9da3493ed850}|Ändern der Domänen-NC zum Zulassen von "Domain\Key Administratoren" und "Rootdomain\Enterprise Schlüsseladministratoren" So ändern Sie das Attribut Msds-KeyCredentialLink. |Nicht zutreffend|(OA; CI; RPWP; 5b47d60f-6090-40b2-9f37-2a4de88f3063; Key-Admins)<br />(OA; CI; RPWP; 5b47d60f-6090-40b2-9f37-2a4de88f3063; Unternehmensadministratoren Schlüssel in der Stammdomäne, aber in nicht-Root-Domänen führte dazu, dass eine falsche Domäne relativer ACE mit einer nicht auflösbaren-527-SID)|
|**Operation 86**: {3a6b3fbf-3168-4312-a10d-dd5b3393952d}|Gewähren von AUTOS DS-überprüft-schreiben-Computer für Ersteller-Besitzer und Self-Service|Nicht zutreffend|(OA;CIIO;SW;9b026da6-0d3c-465c-8bee-5199d7165cba;bf967a86-0de6-11d0-a285-00aa003049e2;PS)<br />(OA;CIIO;SW;9b026da6-0d3c-465c-8bee-5199d7165cba;bf967a86-0de6-11d0-a285-00aa003049e2;CO)|
|**Operation 87**: {7F950403-0AB3-47F9-9730-5D7B0269F9BD}|Löschen Sie den ACE, der Vollzugriff auf die falsche Domäne relativer Schlüssel Organisations-Admins-Gruppe gewähren, und fügen Sie einen ACE, der Vollzugriff auf Schlüssel Organisations-Admins-Gruppe zu gewähren. |Nicht zutreffend|(A; löschen CI; RPWPCRLCLOCCDCRCWDWOSDDTSW;; Wichtige Organisations-Admins)<br /> <br />Fügen Sie (A; hinzu CI; RPWPCRLCLOCCDCRCWDWOSDDTSW;; Wichtige Organisations-Admins)|
|**Vorgang 88**: {434bb40d-dbc9-4fe7-81d4-d57229f7b080}|Hinzufügen von "MsDS-ExpirePasswordsOnSmartCardOnlyAccounts" für das Domänen-NC-Objekt, und standardmäßig ist der Wert auf "false" festgelegt|Nicht zutreffend|Nicht zutreffend|

Die Schlüssel-Unternehmensadministratoren und Schlüsseladministratoren Gruppen werden nur erstellt, nach einem Windows Server 2016-Domänencontroller höher gestuft wird und die Rolle des PDC-Emulator-FSMO-Funktion übernimmt.

## <a name="windows-server-2012-r2-domain-wide-updates"></a>Windows Server 2012 R2: Domänenweite updates

Obwohl keine Vorgänge, indem ausgeführt werden **Domainprep** in Windows Server 2012 R2, wenn der Befehl abgeschlossen ist, die **Revision** -Attribut für CN = ActiveDirectoryUpdate, CN = DomainUpdates, CN = System, DC = Objekt, um festgelegt wird Gesamtstruktur-Stammdomäne **10**.

## <a name="windows-server-2012-domain-wide-updates"></a>Windows Server 2012: Domänenweite updates

Nach dem die Vorgänge, die ausgeführt werden **Domainprep** in Windows Server 2012 (Vorgänge 78, 79, 80 und 81) abgeschlossen ist, die **Revision** -Attribut für CN = ActiveDirectoryUpdate, CN = DomainUpdates, CN = System, DC = Objekt, um festgelegt wird Gesamtstruktur-Stammdomäne **9**.

|Anzahl der Vorgänge und GUID|Beschreibung|Attribute|Berechtigungen|
|------------------------------|---------------|--------------|---------------|
|**Operation 78**: {c3c927a6-cc1d-47c0-966b-be8f9b63d991}|Erstellen eines neuen Objekts CN = TPM-Geräten in der Domänenpartition.|Object-Klasse: MsTPM-InformationObjectsContainer|Nicht zutreffend|
|**Operation 79**: {54afcfb9-637a-4251-9f47-4d50e7021211}|Erstellt einen Zugriffssteuerungseintrag für den TPM-Dienst.|Nicht zutreffend|(OA;CIIO;WP;ea1b7b93-5e48-46d5-bc6c-4df4fda78a35;bf967a86-0de6-11d0-a285-00aa003049e2;PS)|
|**Vorgang 80**: {f4728883-84dd-483c-9897-274f2ebcf11e}|Erteilen Sie "Klonen DC" für erweiterte **Klonbare Domänencontroller** Gruppe|Nicht zutreffend|(OA; CR; 3e0f7e18-2c7a-4c10-ba82-4d926db99a3e; *Domänen-SID*-522)|
|**Operation 81**: {ff4f9d27-7157-4cb0-80a9-5d6f2b14c8ff}|Gewähren Sie ms-DS-Allowed-To-Act-On-Behalf-Of-Other-Identity Prinzipal Self für alle Objekte.|Nicht zutreffend|(OA;CIOI;RPWP;3f78c3e5-f79a-46bd-a0b8-9d18116ddc79;;PS)|
