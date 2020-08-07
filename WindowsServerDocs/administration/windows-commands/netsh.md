---
title: Netsh
description: Referenz Artikel für den Befehl netsh, bei dem es sich um ein Befehlszeilen-Skript Programm handelt, mit dem Sie die Netzwerkkonfiguration eines derzeit ausgelaufenden Computers entweder lokal oder Remote anzeigen oder ändern können.
ms.topic: article
ms.assetid: 96fc069d-53c0-4d0a-9f7f-f9f3d49a02bd carmonmills
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 366c7a21f44dc6545de7ba81cba8fe152c245b6b
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886032"
---
# <a name="netsh"></a>Netsh

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Das Befehlszeilen-Skript Hilfsprogramm für die Netzwerk Shell, mit dem Sie die Netzwerkkonfiguration eines derzeit ausgelaufenden Computers entweder lokal oder Remote anzeigen oder ändern können. Sie können dieses Hilfsprogramm an der Eingabeaufforderung oder in Windows PowerShell starten.

## <a name="syntax"></a>Syntax

```
netsh [-a <Aliasfile>][-c <Context>][-r <Remotecomputer>][-u [<domainname>\<username>][-p <Password> | [{<NetshCommand> | -f <scriptfile>}]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| -a `<Aliasfile>` | Gibt an, dass Sie nach dem Ausführen von aliasfile und dem Namen der Textdatei, die mindestens einen netsh-Befehl enthält, an die Netsh-Eingabeaufforderung zurückgegeben werden. |
| -c`<Context>` | Gibt an, dass netsh den angegebenen Netsh-Kontext und den Netsh-Kontext für die Eingabe eingibt. |
| -r`<Remotecomputer>` | Gibt den zu konfigurier-Remote Computer an.<p>**Wichtig:** Wenn Sie diesen Parameter verwenden, müssen Sie sicherstellen, dass der Remote Registrierungsdienst auf dem Remote Computer ausgeführt wird. Wenn er nicht ausgeführt wird, zeigt Windows die Fehlermeldung "Netzwerkpfad nicht gefunden" an. |
| -u`<domainname>\<username>` | Gibt den Domänen-und Benutzerkonto Namen an, der beim Ausführen des Netsh-Befehls unter einem Benutzerkonto verwendet werden soll. Wenn Sie die Domäne weglassen, wird die lokale Domäne standardmäßig verwendet. |
| -p`<Password>` | Gibt das Kennwort für das Benutzerkonto an, das durch den-Parameter angegeben wird `-u <username>` . |
| `<NetshCommand>` | Gibt den Befehl netsh an, der ausgeführt werden soll. |
| -f`<scriptfile>` | Beendet den Netsh-Befehl, nachdem die angegebene Skriptdatei ausgeführt wurde. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Wenn Sie **-r** angeben, gefolgt von einem anderen Befehl, führt netsh den Befehl auf dem Remote Computer aus und kehrt dann zur Cmd.exe Eingabeaufforderung zurück. Wenn Sie **-r** ohne einen anderen Befehl angeben, wird Netsh im Remote Modus geöffnet. Das Verfahren ist ähnlich wie die Verwendung von **set machine** an der Netsh-Eingabeaufforderung. Wenn Sie **-r**verwenden, legen Sie den Bereitstellungs Zielcomputer nur für die aktuelle Instanz von netsh fest. Nachdem du Netsh beendet und erneut eingegeben hast, wird der Zielcomputer als lokaler Computer zurückgesetzt. Du kannst Netsh-Befehle auf einem Remotecomputer ausführen, indem du einen in WINS gespeicherten Computernamen, einen UNC-Namen, einen vom DNS-Server aufzulösenden Internetnamen oder eine IP-Adresse angibst.

- Wenn der Zeichen folgen Wert Leerzeichen zwischen Zeichen enthält, müssen Sie den Zeichen folgen Wert in Anführungszeichen einschließen. Zum Beispiel, `-r "contoso remote device"`

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
