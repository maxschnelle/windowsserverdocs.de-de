---
title: manage-bde-Schutzvorrichtungen
description: Referenz Artikel für den Befehl manage-bde Protector, der die Schutzmethoden verwaltet, die für den BitLocker-Verschlüsselungsschlüssel verwendet werden.
ms.topic: reference
ms.assetid: 1f9b22c5-cc93-45df-9165-bedee94998da
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 08/06/2018
ms.openlocfilehash: 0461edcb2e1177f1a72ec7e4a1c893c80cd70698
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89027568"
---
# <a name="manage-bde-protectors"></a>manage-bde-Schutzvorrichtungen

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Verwaltet die Schutzmethoden, die für den BitLocker-Verschlüsselungsschlüssel verwendet werden.

## <a name="syntax"></a>Syntax

```
manage-bde -protectors [{-get|-add|-delete|-disable|-enable|-adbackup|-aadbackup}] <drive> [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ----------- | ----------- |
| -Get | Zeigt alle auf dem Laufwerk aktivierten Schlüsselschutz Methoden an und gibt ihren Typ und Bezeichner (ID) an. |
| -Hinzufügen | Fügt mit zusätzlichen **Add-** Parametern Schlüsselschutz Methoden hinzu. |
| -delete | Löscht Schlüsselschutz Methoden, die von BitLocker verwendet werden. Alle Schlüssel Schutzvorrichtungen werden von einem Laufwerk entfernt, es sei denn, die Parameter " **-Delete** " werden verwendet, um anzugeben, welche Schutzvorrichtungen gelöscht werden sollen. Wenn die letzte Schutzvorrichtung auf einem Laufwerk gelöscht wird, wird der BitLocker-Schutz des Laufwerks deaktiviert, um sicherzustellen, dass der Zugriff auf die Daten nicht versehentlich verloren geht. |
| -disable | Deaktiviert den Schutz, mit dem jeder auf verschlüsselte Daten zugreifen kann, indem der Verschlüsselungsschlüssel auf dem Laufwerk nicht gesichert wird. Es werden keine Schlüssel Schutzvorrichtungen entfernt. Der Schutz wird beim nächsten Start von Windows fortgesetzt, es sei denn, mit den optionalen Parametern " **-Deaktivieren** " können Sie die Neustart Anzahl angeben. |
| -enable | Ermöglicht den Schutz, indem der unsichere Verschlüsselungsschlüssel vom Laufwerk entfernt wird. Alle konfigurierten Schlüssel Schutzvorrichtungen auf dem Laufwerk werden erzwungen. |
| -adbackup | Sichert alle Wiederherstellungs Informationen für das angegebene Laufwerk Active Directory Domain Services (AD DS). Wenn Sie nur einen einzelnen Wiederherstellungs Schlüssel in AD DS sichern möchten, fügen Sie den Parameter **-ID** an, und geben Sie die ID eines bestimmten Wiederherstellungs Schlüssels an, der gesichert werden soll. |
| -aadbackup | Sichert alle Wiederherstellungs Informationen für das angegebene Laufwerk Azure Active Directory (Azure AD). Wenn Sie nur einen einzelnen Wiederherstellungs Schlüssel in Azure AD sichern möchten, fügen Sie den Parameter **-ID** an, und geben Sie die ID eines bestimmten Wiederherstellungs Schlüssels an, der gesichert werden soll. |
| `<drive>` | Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar. |
| -Computername | Gibt an, dass manage-bde.exe zum Ändern des BitLocker-Schutzes auf einem anderen Computer verwendet wird. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

#### <a name="additional--add-parameters"></a>Zusätzliche Parameter hinzufügen

Der Parameter-Add kann auch diese gültigen zusätzlichen Parameter verwenden.

```
manage-bde -protectors -add [<drive>] [-forceupgrade] [-recoverypassword <numericalpassword>] [-recoverykey <pathtoexternalkeydirectory>]
[-startupkey <pathtoexternalkeydirectory>] [-certificate {-cf <pathtocertificatefile>|-ct <certificatethumbprint>}] [-tpm] [-tpmandpin]
[-tpmandstartupkey <pathtoexternalkeydirectory>] [-tpmandpinandstartupkey <pathtoexternalkeydirectory>] [-password][-adaccountorgroup <securityidentifier> [-computername <name>]
[{-?|/?}] [{-help|-h}]
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `<drive>` | Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar. |
| -wiederherstellungkennwort | Fügt eine numerische Kennwort-Schutzvorrichtung hinzu. Sie können auch **-RP** als abgekürzte Version dieses Befehls verwenden. |
| `<numericalpassword>` | Stellt das Wiederherstellungs Kennwort dar. |
| -Wiederherstellungsschlüssel | Fügt eine externe Schlüssel Schutzvorrichtung für die Wiederherstellung hinzu. Sie können " **-RK** " auch als abgekürzte Version dieses Befehls verwenden. |
| `<pathtoexternalkeydirectory>` | Stellt den Verzeichnispfad zum Wiederherstellungs Schlüssel dar. |
| -startupkey | Fügt eine externe Schlüssel Schutzvorrichtung zum Starten hinzu. Sie können auch **-SK** als abgekürzte Version dieses Befehls verwenden. |
| `<pathtoexternalkeydirectory>` | Stellt den Verzeichnispfad zum Systemstart Schlüssel dar. |
| -Zertifikat | Fügt eine Schutzvorrichtung für ein öffentliches Schlüssel für ein Daten Laufwerk hinzu. Sie können auch **-CERT** als abgekürzte Version dieses Befehls verwenden. |
| -cf | Gibt an, dass eine Zertifikatsdatei verwendet wird, um das Zertifikat für öffentliche Schlüssel bereitzustellen. |
| <pathtocertificatefile> | Stellt den Verzeichnispfad zur Zertifikatsdatei dar. |
| -CT | Gibt an, dass ein Zertifikat Fingerabdruck verwendet wird, um das Zertifikat für öffentliche Schlüssel zu identifizieren. |
| `<certificatethumbprint>` | Gibt den Wert der Eigenschaft "Fingerabdruck" des Zertifikats an, das Sie verwenden möchten. Beispielsweise sollte der Wert des Zertifikat Fingerabdrucks A9 09 50 2D D8 2a E4 14 33 E6 F8 38 86 B0 0d 42 77 a3 2a 7B als a909502dd82ae41433e6f83886b00d4277a32a7b angegeben werden. |
| -TPMAndPIN | Fügt ein Trusted Platform Module (TPM) und eine PIN-Schutzvorrichtung (Personal Identification Number) für das Betriebssystem Laufwerk hinzu. Sie können auch **-tp** als abgekürzte Version dieses Befehls verwenden. |
| -TPMAndStartupKey | Fügt ein TPM und eine Systemstart Schlüssel-Schutzvorrichtung für das Betriebssystem Laufwerk hinzu. Sie können auch **-TSK** als abgekürzte Version dieses Befehls verwenden. |
| -tpmandpinandstartupkey | Fügt ein TPM, eine PIN und eine Start Schlüsselschutzvorrichtung für das Betriebssystem Laufwerk hinzu. Sie können auch **-tpsk** als abgekürzte Version dieses Befehls verwenden. |
| -password | Fügt eine Kenn Wort Schlüssel-Schutzvorrichtung für das Daten Laufwerk hinzu. Sie können auch **-PW** als abgekürzte Version dieses Befehls verwenden. |
| -adaccountorgroup | Fügt eine Sicherheits-ID (SID)-basierte Identitäts Schutzvorrichtung für das Volume hinzu. Sie können auch **-sid** als abgekürzte Version dieses Befehls verwenden. **Wichtig:** Standardmäßig können Sie eine adaccountorgroup-Schutzvorrichtung nicht remote mithilfe von WMI oder manage-bde hinzufügen. Wenn Ihre Bereitstellung die Möglichkeit erfordert, diese Schutzvorrichtung Remote hinzuzufügen, müssen Sie die eingeschränkte Delegierung aktivieren. |
| -Computername | Gibt an, dass "Manage-BDE" verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

#### <a name="additional--delete-parameters"></a>Zusätzliche Parameter löschen

```
manage-bde -protectors -delete <drive> [-type {recoverypassword|externalkey|certificate|tpm|tpmandstartupkey|tpmandpin|tpmandpinandstartupkey|Password|Identity}]
[-id <keyprotectorID>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `<drive>` | Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar. |
| -Typ | Identifiziert die zu löschende Schlüssel Schutzvorrichtung. Sie können auch **-t** als abgekürzte Version dieses Befehls verwenden. |
| RecoveryPassword | Gibt an, dass alle Schutz Kennwort-Schlüssel Schutzvorrichtungen gelöscht werden sollen. |
| ExternalKey | Gibt an, dass alle dem Laufwerk zugeordneten externen Schlüsselschutz Vorrichtungen gelöscht werden sollen. |
| Zertifikat | Gibt an, dass alle dem Laufwerk zugeordneten Zertifikat Schlüsselschutz Vorrichtungen gelöscht werden sollen. |
| TPM | Gibt an, dass alle dem Laufwerk zugeordneten TPM-Schlüsselschutz Vorrichtungen gelöscht werden sollen. |
| TPMAndStartupKey | Gibt an, dass alle dem Laufwerk zugeordneten TPM-und systemeigenen Schlüsselschutz Vorrichtungen gelöscht werden sollen. |
| TPMAndPIN | Gibt an, dass alle dem Laufwerk zugeordneten TPM-und PIN-basierten Schlüsselschutz Vorrichtungen gelöscht werden sollen. |
| tpmandpinandstartupkey | Gibt an, dass alle dem Laufwerk zugeordneten TPM-, PIN-und Start Schlüssel-Schlüssel Schutzvorrichtungen gelöscht werden sollen. |
| password | Gibt an, dass alle dem Laufwerk zugeordneten Kennwort-Schlüsselschutz Vorrichtungen gelöscht werden sollen. |
| identity | Gibt an, dass alle dem Laufwerk zugeordneten Identitätsschlüssel Schutzvorrichtungen gelöscht werden sollen. |
| -ID | Identifiziert die zu löschende Schlüssel Schutzvorrichtung mithilfe des Schlüssel Bezeichners. Dieser Parameter ist eine alternative Option für den **-Type-** Parameter. |
| `<keyprotectorID>` | Identifiziert eine einzelne Schlüssel Schutzvorrichtung auf dem zu löschenden Laufwerk. Schlüsselschutzschutzids können mithilfe des Befehls **manage-bde-Protector-Get** angezeigt werden. |
| -Computername | Gibt an, dass manage-bde.exe zum Ändern des BitLocker-Schutzes auf einem anderen Computer verwendet wird. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

#### <a name="additional--disable-parameters"></a>Zusätzliche Parameter deaktivieren

```
manage-bde -protectors -disable <drive> [-rebootcount <integer 0 - 15>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `<drive>` | Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar. |
| rebootcount | Gibt an, dass der Schutz für das Betriebssystem Volume angehalten wurde und fortgesetzt wird, sobald Windows neu gestartet wurde, und zwar so oft wie im Parameter " **rebootcount** " angegeben. Geben Sie **0** an, um den Schutz unbegrenzt anzuhalten. Wenn dieser Parameter nicht angegeben wird, wird der BitLocker-Schutz nach dem Neustart von Windows automatisch fortgesetzt. Sie können auch **-RC** als abgekürzte Version dieses Befehls verwenden. |
| -Computername | Gibt an, dass manage-bde.exe zum Ändern des BitLocker-Schutzes auf einem anderen Computer verwendet wird. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine durch eine Zertifikatsdatei identifizierte Zertifikat Schlüssel Schutzvorrichtung hinzuzufügen:

```
manage-bde -protectors -add E: -certificate -cf c:\File Folder\Filename.cer
```

Geben Sie Folgendes ein, um eine **adaccountorgroup** -Schlüssel Schutzvorrichtung hinzuzufügen, die von Domäne und Benutzername identifiziert wird:

```
manage-bde -protectors -add E: -sid DOMAIN\user
```

Um den Schutz zu deaktivieren, bis der Computer dreimal neu gestartet wurde, geben Sie Folgendes ein:

```
manage-bde -protectors -disable C: -rc 3
```

Geben Sie Folgendes ein, um alle TPM-und Start Schlüssel-basierten Schlüssel Schutzvorrichtungen auf Laufwerk C zu löschen:

```
manage-bde -protectors -delete C: -type tpmandstartupkey
```

Geben Sie Folgendes ein, um alle Wiederherstellungs Informationen für das Laufwerk C in AD DS zu sichern:

```
manage-bde -protectors -adbackup C:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Manage-BDE"](manage-bde.md)
