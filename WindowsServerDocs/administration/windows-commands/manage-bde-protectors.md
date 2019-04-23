---
title: Verwalten von-Bde-protectors
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1f9b22c5-cc93-45df-9165-bedee94998da
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 08/06/2018
ms.openlocfilehash: c804fe6fa4aca8c55bd6a312536cc453962b3c1c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852841"
---
# <a name="manage-bde-protectors"></a>Verwalten von-Bde: IRM-Schutz

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Verwaltet die Schutzmethoden, die für die BitLocker-Verschlüsselungsschlüssel verwendet. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).
## <a name="syntax"></a>Syntax
```
manage-bde -protectors [{-get|-add|-delete|-disable|-enable|-adbackup|-aadbackup}] <Drive> [-computername <Name>] [{-?|/?}] [{-help|-h}]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|-get|Zeigt alle Schlüsselschutz-Methoden, die auf dem Laufwerk aktiviert, und stellt Sie bereit, ihren Typ und den Bezeichner (ID).|
|-Hinzufügen|Fügt Schlüsselschutz-Methoden wie angegeben mit zusätzlichen [ Hinzufügen von Parametern](manage-bde-protectors.md#BKMK_addprotectors).|
|-Löschen|Löscht Schlüsselschutz-Methoden, die von BitLocker verwendet wird. Alle Schlüsselschutzvorrichtungen werden von einem Laufwerk entfernt werden, es sei denn, das optionale [-Löschparametern](manage-bde-protectors.md#BKMK_deleteprotectors) werden verwendet, um die Schutzvorrichtungen löschen angeben. Wenn die letzte-Schutzvorrichtung auf einem Laufwerk gelöscht wird, ist der BitLocker-Schutz des Laufwerks deaktiviert, um sicherzustellen, dass der Zugriff auf Daten nicht versehentlich verloren geht.|
|-Deaktivieren|Schutz, sodass auf die verschlüsselten Daten zugreifen, indem Sie den Verschlüsselungsschlüssel verfügbar auf Laufwerk ungesichert für alle Benutzer deaktiviert. Es werden keine Schlüsselschutzvorrichtungen entfernt. Schutz wird fortgesetzt, wenn Sie das nächste Mal Windows gestartet wird, es sei denn, das optionale [-Parameter deaktivieren](manage-bde-protectors.md#BKMK_disableprot) werden verwendet, um die Anzahl der Neustart angeben.|
|-Aktivieren|Ermöglicht den Schutz durch das Entfernen des nicht gesicherten Verschlüsselungsschlüssels aus dem Laufwerk. Alle konfigurierten Schlüsselschutzvorrichtungen auf dem Laufwerk werden erzwungen.|
|-adbackup|Sichert alle Wiederherstellungsinformationen für das Laufwerk angegeben, um Active Directory Domain Services (AD DS). Um nur einen einzigen Wiederherstellungsschlüssel in AD DS zu sichern, fügen Sie der **-Id** Parameter, und geben Sie die ID der einen bestimmten Wiederherstellungsschlüssel gesichert werden.|
|-aadbackup|Sichert alle Wiederherstellungsinformationen für das Laufwerk angegeben, um Azure Active Directory (Azure Ad). Fügen Sie in Azure AD können nur einen einzigen Wiederherstellungsschlüssel zu sichern, die **-Id** Parameter, und geben Sie die ID der einen bestimmten Wiederherstellungsschlüssel gesichert werden.|
|<Drive>|Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.|
|-computername|Gibt an, dass diese verwalten-bde.exe verwendet wird, um die BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **- Cn** als eine verkürzte Version des mit diesem Befehl.|
|<Name>|Stellt den Namen des Computers, auf dem BitLocker-Schutz zu ändern. Akzeptierte Werte sind die NetBIOS-Namen des Computers und die IP-Adresse des Computers.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung.|
|---Help oder-h|Zeigt Hilfe an der Eingabeaufforderung abgeschlossen werden.|
### <a name="BKMK_addprotectors"></a>-Syntax und Parameter hinzufügen
```
manage-bde  protectors  add [<Drive>] [-forceupgrade] [-recoverypassword <NumericalPassword>] [-recoverykey <pathToExternalKeydirectory>]
[-startupkey <pathToExternalKeydirectory>] [-certificate {-cf <pathToCertificateFile>|-ct <CertificateThumbprint>}] [-tpm] [-tpmandpin] 
[-tpmandstartupkey <pathToExternalKeydirectory>] [-tpmandpinandstartupkey <pathToExternalKeydirectory>] [-password][-adaccountorgroup <securityidentifier> [-computername <Name>] 
[{-?|/?}] [{-help|-h}]
```
|Parameter|Beschreibung|
|-------|--------|
|<Drive>|Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.|
|-recoverypassword|Fügt eine Schutzvorrichtung numerisches Kennwort hinzu. Sie können auch **- Rp** als eine verkürzte Version des mit diesem Befehl.|
|<NumericalPassword>|Stellt die Eingabe eines Wiederherstellungskennworts dar.|
|-recoverykey|Fügt eine externe Schlüsselschutzvorrichtung für die Wiederherstellung an. Sie können auch **- Rk** als eine verkürzte Version des mit diesem Befehl.|
|<pathToExternalKeydirectory>|Stellt den Verzeichnispfad für den Wiederherstellungsschlüssel dar.|
|-Startschlüssel|Fügt eine externe Schlüsselschutzvorrichtung für den Start. Sie können auch **-sk** als eine verkürzte Version des mit diesem Befehl.|
|<pathToExternalKeydirectory>|Stellt den Verzeichnispfad für den Schlüssel zum Systemstart dar.|
|-Zertifikat|Fügt einer öffentlichen Schlüsselschutzvorrichtung für ein Laufwerk hinzu. Sie können auch **-Cert** als eine verkürzte Version des mit diesem Befehl.|
|-cf|Gibt an, dass eine Zertifikatdatei, geben Sie das öffentliche Schlüsselzertifikat verwendet wird.|
|<pathToCertificateFile>|Stellt den Pfad zur Zertifikatdatei dar.|
|-ct|Gibt an, dass der Fingerabdruck eines Zertifikats verwendet wird, um das Zertifikat für öffentliche Schlüssel zu identifizieren.|
|<CertificateThumbprint>|Gibt den Wert der Eigenschaft "Fingerabdruck" des Zertifikats, die Sie verwenden möchten. Z. B. ein Zertifikat Fingerabdruckwert des "a9 09 50 2d d8 2a e4 14 33 e6 f8 38 86 b0 0d 42 77 a3 2a 7" muss angegeben werden, als "a909502dd82ae41433e6f83886b00d4277a32a7b".|
|-tpmandpin|Fügt ein Trusted Platform Module (TPM) und das personal Identification Number (PIN)-Schutzvorrichtung für das Betriebssystemlaufwerk. Sie können auch **- Tp** als eine verkürzte Version des mit diesem Befehl.|
|-tpmandstartupkey|Fügt eine TPM- und -Systemstart-Schlüsselschutzvorrichtung für das Betriebssystemlaufwerk. Sie können auch **-tsk** als eine verkürzte Version des mit diesem Befehl.|
|-tpmandpinandstartupkey|Fügt eine TPM-PIN und Startup-Schlüsselschutzvorrichtung für das Betriebssystemlaufwerk. Sie können auch **- Tpsk** als eine verkürzte Version des mit diesem Befehl.|
|-Kennwort|Fügt eine Kennwort-Schlüsselschutzvorrichtung für das Datenlaufwerk an. Sie können auch **- kW** als eine verkürzte Version des mit diesem Befehl.|
|-adaccountorgroup|Fügt eine Sicherheits-ID (SID)-basierte Identitätsschutz für das Volume.  Sie können auch **-Sid** als eine verkürzte Version des mit diesem Befehl. **WICHTIG:** Standardmäßig können nicht Sie eine Remoteverbindung mit WMI oder verwalten-Bde ADAccountOrGroup-Schutzvorrichtung hinzufügen.  Wenn Ihre Bereitstellung die Möglichkeit, diese Schutzvorrichtung Remote hinzuzufügen erfordert, müssen Sie eingeschränkten Delegierung aktivieren.|
|-computername|Gibt an, dass diese verwalten-Bde verwendet wird, um die BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **- Cn** als eine verkürzte Version des mit diesem Befehl.|
|<Name>|Stellt den Namen des Computers, auf dem BitLocker-Schutz zu ändern. Akzeptierte Werte sind die NetBIOS-Namen des Computers und die IP-Adresse des Computers.|
### <a name="BKMK_deleteprotectors"></a>-Syntax und Parameter löschen
```
manage-bde  protectors  delete <Drive> [-type {recoverypassword|externalkey|certificate|tpm|tpmandstartupkey|tpmandpin|tpmandpinandstartupkey|Password|Identity}] 
[-id <KeyProtectorID>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```
|Parameter|Beschreibung|
|-------|--------|
|<Drive>|Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.|
|-type|Identifiziert die Schlüsselschutzvorrichtung zu löschen. Sie können auch **-t** als eine verkürzte Version des mit diesem Befehl.|
|recoverypassword|Gibt an, dass alle Wiederherstellungskennwort-Schutzvorrichtungen Schlüssel gelöscht werden soll.|
|ExternalKey|Gibt an, dass alle externen Schlüsselschutzvorrichtungen verknüpft ist, mit dem Laufwerk gelöscht werden soll.|
|Zertifikat|Gibt an, dass alle Schlüsselschutzvorrichtungen Zertifikat, das Laufwerk zugeordnet, die gelöscht werden soll.|
|tpm|Gibt an, dass nur-TPM-Schlüsselschutzvorrichtungen, die das Laufwerk zugeordnet, die gelöscht werden soll.|
|TPMAndStartupKey|Gibt an, dass alle TPM- und -Startup Key basierenden Schlüsselschutzvorrichtungen das Laufwerk zugeordnet, die gelöscht werden soll.|
|TPMAndPIN|Gibt an, dass alle TPM und PIN Schlüsselschutzvorrichtungen dem Laufwerk zugeordneten basiert, sollten gelöscht werden.|
|tpmandpinandstartupkey|Gibt an, dass alle TPM und PIN beim Start wichtigsten basierenden Schlüsselschutzvorrichtungen verknüpft ist, mit dem Laufwerk gelöscht werden soll.|
|Kennwort|Gibt an, dass alle Schlüsselschutzvorrichtungen Kennwort, das Laufwerk zugeordnet, die gelöscht werden soll.|
|Identität|Gibt an, dass alle Schlüsselschutzvorrichtungen Identität, der dem Laufwerk zugeordnet, die gelöscht werden soll.|
|-id|Identifiziert die Schlüsselschutzvorrichtung zu löschen, indem Sie mit den Schlüsselbezeichner an. Dieser Parameter ist eine alternative Option aus, um die **-Typ** Parameter.|
|<KeyProtectorID>|Gibt eine einzelne Kennwortschlüssel-Schutzvorrichtung auf dem Laufwerk zu löschen. Schlüsselschutzvorrichtung IDs kann angezeigt werden, mithilfe der **verwalten-Bde-Protectors-erhalten** Befehl.|
|-computername|Gibt an, dass diese verwalten-bde.exe verwendet wird, um die BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **- Cn** als eine verkürzte Version des mit diesem Befehl.|
|<Name>|Stellt den Namen des Computers, auf dem BitLocker-Schutz zu ändern. Akzeptierte Werte sind die NetBIOS-Namen des Computers und die IP-Adresse des Computers.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung.|
|---Help oder-h|Zeigt Hilfe an der Eingabeaufforderung abgeschlossen werden.|
### <a name="BKMK_disableprot"></a>– Deaktivieren Sie die Syntax und Parameter
```
manage-bde  protectors  disable <Drive> [-RebootCount <integer 0 - 15>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```
|Parameter|Beschreibung|
|-------|--------|
|<Drive>|Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.|
|RebootCount|Gibt an, beginnend mit Windows 8, Schutz von Volume des Betriebssystems wurde angehalten und wird fortgesetzt, nachdem Windows wurde neu gestartet wie oft im RebootCount-Parameter angegeben. Geben Sie 0 an, um den Schutz auf unbestimmte Zeit angehalten. Wenn dieser Parameter nicht angegeben ist, dass die BitLocker-Schutz werden automatisch fort, wenn es sich bei Windows neu gestartet wird. Sie können auch **-rc** als eine verkürzte Version des mit diesem Befehl.|
|-computername|Gibt an, dass diese verwalten-bde.exe verwendet wird, um die BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **- Cn** als eine verkürzte Version des mit diesem Befehl.|
|<Name>|Stellt den Namen des Computers, auf dem BitLocker-Schutz zu ändern. Akzeptierte Werte sind die NetBIOS-Namen des Computers und die IP-Adresse des Computers.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung.|
|---Help oder-h|Zeigt Hilfe an der Eingabeaufforderung abgeschlossen werden.|
## <a name="BKMK_Examples"></a>Beispiele für
Das folgende Beispiel veranschaulicht die Verwendung der **-Schutzvorrichtungen** Befehl zum Hinzufügen einer schlüsselschutzkomponente Zertifikat, identifiziert anhand einer Zertifikatsdatei auf Laufwerk e:.
```
manage-bde  protectors  add E: -certificate  cf "c:\File Folder\Filename.cer"
```
Das folgende Beispiel veranschaulicht die Verwendung der **-Schutzvorrichtungen** Befehl zum Hinzufügen einer **Adaccountorgroup** Schlüsselschutzvorrichtung identifizierte Domäne und den Namen auf Laufwerk e:.
```
manage-bde  protectors  add E: -sid DOMAIN\user
```
Das folgende Beispiel veranschaulicht die Verwendung der ** Schutzvorrichtungen **-Befehl, um den Schutz zu deaktivieren, bis der Computer die 3 Mal neu gestartet wurde.
```
manage-bde  protectors  disable C: -rc 3
```
Das folgende Beispiel veranschaulicht die Verwendung der **-Schutzvorrichtungen** Befehl zum Löschen aller TPM und Schlüssel zum Systemstart basierend Schlüsselschutzvorrichtungen auf Laufwerk C.
```
manage-bde  protectors  delete C: -type tpmandstartupkey
```
Das folgende Beispiel veranschaulicht die Verwendung der **-Schutzvorrichtungen** Befehl aus, um alle Wiederherstellungsinformationen für Laufwerk C: in AD DS zu sichern.
```
manage-bde  protectors  adbackup C:
```
## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [manage-bde](manage-bde.md)
