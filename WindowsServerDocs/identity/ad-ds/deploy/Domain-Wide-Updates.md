---
ms.assetid: 2a5d5271-6ac6-4c1b-b4ef-9b568932a55a
title: Active Directory Domänen weiten Schema Aktualisierungen
description: Domänen weite Schema Updates, die von adprep/domainprep bei der herauf Stufung eines Domänen Controllers ausgeführt werden
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 10/29/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 3b82958471e5292f202aa338aee7f4f5863459af
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80825213"
---
# <a name="domain-wide-schema-updates"></a>Domänen weite Schema Aktualisierungen

>Gilt für: Windows Server

Sie können die folgenden Änderungen überprüfen, um die Schema Aktualisierungen zu verstehen und vorzubereiten, die von adprep/domainprep in Windows Server ausgeführt werden.

Ab Windows Server 2012 werden adprep-Befehle bei Bedarf bei der AD DS Installation automatisch ausgeführt. Sie können auch separat im Voraus AD DS Installation ausgeführt werden. Weitere Informationen finden Sie unter [Ausführen von Adprep.exe](https://technet.microsoft.com/library/dd464018(v=ws.10).aspx).

Weitere Informationen zum Interpretieren der ACE-Zeichen folgen (Access Control Entry, Zugriffs Steuerungs Eintrag) finden Sie unter [ACE](https://msdn.microsoft.com/library/aa374928(VS.85).aspx)-Zeichen folgen. Weitere Informationen zum Interpretieren der Sicherheits-ID (SID)-Zeichen folgen finden Sie unter [sid](https://msdn.microsoft.com/library/aa379602(VS.85).aspx)-Zeichen folgen.

## <a name="windows-server-semi-annual-channel-domain-wide-updates"></a>Windows Server (halbjährlicher Kanal): Domänen weite Updates

Nachdem die von **domainprep** in Windows Server 2016 (Operation 89) ausgeführten Vorgänge beendet wurden, wird das **Revisions** Attribut für das Objekt CN = ActiveDirectoryUpdate, CN = DomainUpdates, CN = System, DC = ForestRootDomain auf **16**festgelegt.

|Vorgangs Nummer und GUID|Beschreibung|Berechtigungen|
|------------------------------|---------------|--------------|---------------|
|**Vorgang 89**: {A0C238BA-9E30-4EE6-80A6-43F731E9A5CD}|Löschen Sie den ACE, der Vollzugriff auf Organisations Schlüssel-Administratoren gewährt, und fügen Sie einen ACE hinzu, der Enterprise Key-Administratoren die vollständige Kontrolle über das msdskeykredentiallink-Attribut gewährt.|Löschen (A; RKI Rpwpcrlcloccdcrcwdwosddzw;;; Enterprise Key-Administratoren) <br /> <br />Hinzufügen (OA; RKI Rpwp; 5b47d60f -6090-40b2-9F 37-2a4debug-Datei Enterprise Key-Administratoren)|

## <a name="windows-server-2016-domain-wide-updates"></a>Windows Server 2016: Domänen weite Updates

Nachdem die von **domainprep** in Windows Server 2016 (Operations 82-88) ausgeführten Vorgänge beendet wurden, wird das **Revisions** Attribut für das Objekt CN = ActiveDirectoryUpdate, CN = DomainUpdates, CN = System, DC = ForestRootDomain auf **15**festgelegt.

|Vorgangs Nummer und GUID|Beschreibung|Attribute|Berechtigungen|
|------------------------------|---------------|--------------|---------------|
|**Vorgang 82**: {83c53da7-427E-47a4-a07a-a324598b88b88f|Create CN = Keys-Container im Stammverzeichnis der Domäne|-objectClass: Container<br />-Description: Standardcontainer für Schlüssel Anmelde Informationsobjekte<br />-ShowInAdvancedViewOnly: true|Ein RKI Rpwpcrlcloccdcrcwdwosddzw;;; Erkrankungen<br />Ein RKI rpwpcrlcloccdcrcwdwosddzw;;;D Ein<br />Ein RKI Rpwpcrlcloccdcrcwdwosddzw;;; Mütter<br />Ein RKI rpwpcrlcloccdcrcwdwosddzw;;;D D<br />Ein RKI Rpwpcrlcloccdcrcwdwosddzw;;; Über|
|**Vorgang 83**: {C81FC9CC-0130-4FD1-B272-634D74818133}|Fügen Sie den Container "Full Control allow ACEs to CN = Keys" für "domain\key Admins" und "rootdomain\enter Prise Key Admins" hinzu.|N/V|Ein RKI Rpwpcrlcloccdcrcwdwosddzw;;; Haupt Administratoren)<br />Ein RKI Rpwpcrlcloccdcrcwdwosddzw;;; Enterprise Key-Administratoren)|
|**Vorgang 84**: {E5F9E791-D96D-4FC9-93C9-D53E1DC439BA}|Ändern Sie das OtherWellKnownObjects-Attribut so, dass es auf den Container CN = Keys verweist.|-otherWellKnownObjects: b:32:683a24e2e8164bd3af86ac3c2cf3f981: CN = Keys,% WS|N/V|
|**Vorgang 85**: {e6d5fd00-385d-4e65-B02D-9da3493ed850}|Ändern Sie den Domänen-NC, um "domain\key Admins" und "rootdomain\enter Prise Key Admins" zu ändern, um das msDS-keykredentiallink-Attribut zu ändern. |N/V|OA RKI Rpwp; 5b47d60f -6090-40b2-9F 37-2a4debug-Datei Haupt Administratoren)<br />OA RKI Rpwp; 5b47d60f -6090-40b2-9F 37-2a4debug-Datei Enterprise Key-Administratoren in der Stamm Domäne, aber in nicht Stamm Domänen führte zu einem gefälschte-Domänen relativen ACE mit einer nicht auflösbaren 527-sid.|
|**Vorgang 86**: {3a6b3f BF-3168-4312-a10d-dd5b3393952d}|Gewähren Sie dem Besitzer "DS-validieren-Write-Computer" und selbst|N/V|OA Ciio; SW; 9b026da6-0d3c-465c-8bee-5199d7165cba; bf967a86-0de6-11D0-A285-00aa003049e2; PS)<br />OA Ciio; SW; 9b026da6-0d3c-465c-8bee-5199d7165cba; bf967a86-0de6-11D0-A285-00aa003049e2; Co)|
|**Vorgang 87**: {7F 950403-0ab3-47F 9-9730-5d7b0269f 9 BD}|Löschen Sie den ACE, der Vollzugriff auf die Gruppe der falschen Domänen bezogenen Organisations Schlüssel-Administratoren gewährt, und fügen Sie einen ACE hinzu, der der Gruppe "Organisations Schlüssel-Admins" Vollzugriff gewährt. |N/V|Löschen (A; RKI Rpwpcrlcloccdcrcwdwosddzw;;; Enterprise Key-Administratoren)<br /> <br />Hinzufügen (A; RKI Rpwpcrlcloccdcrcwdwosddzw;;; Enterprise Key-Administratoren)|
|**Vorgang 88**: {434bb40 d-dbc9-4fe7-81d4-d57229f7b080}|Fügen Sie "msDS-expirepasswordsonsmartcardonlyaccounts" für das Domänen-NC-Objekt hinzu, und legen Sie Standardwert auf false fest.|N/V|N/V|

Die Gruppen Enterprise Key Admins und Key Admins werden erst erstellt, nachdem ein Windows Server 2016-Domänen Controller herauf gestuft und die PDC-Emulator-FSMO-Rolle übernommen wurde.

## <a name="windows-server-2012-r2-domain-wide-updates"></a>Windows Server 2012 R2: Domänen weite Updates

Obwohl keine Vorgänge von **domainprep** in Windows Server 2012 R2 ausgeführt werden, wird nach Abschluss des Befehls das **Revisions** Attribut für das Objekt CN = ActiveDirectoryUpdate, CN = DomainUpdates, CN = System, DC = ForestRootDomain auf **10**festgelegt.

## <a name="windows-server-2012-domain-wide-updates"></a>Windows Server 2012: Domänen weite Updates

Nachdem die von **domainprep** in Windows Server 2012 (Operations 78, 79, 80 und 81) ausgeführten Vorgänge beendet wurden, wird das **Revisions** Attribut für das Objekt CN = ActiveDirectoryUpdate, CN = DomainUpdates, CN = System, DC = ForestRootDomain auf **9**festgelegt.

|Vorgangs Nummer und GUID|Beschreibung|Attribute|Berechtigungen|
|------------------------------|---------------|--------------|---------------|
|**Vorgang 78**: {c3c927a6-cc1d-47c0-966B-be8f9b63d991}|Erstellen Sie ein neues Objekt "CN = TPM-Geräte" in der Domänen Partition.|Objektklasse: mstpm-informationobjectcontainer|N/V|
|**Vorgang 79**: {54afcfb9-637a-4251-9f47-4d50e7021211}|Es wurde ein Zugriffs Steuerungs Eintrag für den TPM-Dienst erstellt.|N/V|OA Ciio; WP; ea1b7b93-5e48-46d5-bc6c-4df4fda78a35; bf967a86-0de6-11D0-A285-00aa003049e2; PS)|
|**Vorgang 80**: {f4728883-84dd-483c-9897-274f2ebcf11e}|Erteilen Sie für die Gruppe " **klonbare Domänen Controller** " Erweiterte Rechte "Klon-DC".|N/V|(OA;; CR; 3e0f 7E18-2c7a-4c10-ba82-4d926db99a3e;; *Domänen-SID*-522)|
|**Vorgang 81**: {ff4f9d27-7157-4cb0-80a9-5d6f2b14c8ff}|Erteilen Sie dem Prinzipal selbst für alle Objekte ms-DS-allowed-to-act-on-Namen-of-other-Identity.|N/V|OA CIOI; Rpwp; 3b78c3e5-b-46bd-a0b8-9d18116ddc79;; Psel|
