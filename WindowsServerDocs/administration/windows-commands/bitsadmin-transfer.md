---
title: bitsadmin Übertragung
description: Windows-Befehls Thema für die bitionadmin-Übertragung, bei der eine oder mehrere Dateien übertragen werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fe302141-b33a-4a05-835e-dc4fc4db7d5a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4e960b4d94416d57e6c42ec27057dafef5e44516
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849003"
---
# <a name="bitsadmin-transfer"></a>bitsadmin Übertragung

Überträgt eine oder mehrere Dateien. Um mehr als eine Datei zu übertragen, geben Sie mehrere \<remotefilename-\>-\<localfilename\>-Paare an. Die Paare sind durch Leerzeichen begrenzt.

## <a name="syntax"></a>Syntax

```
bitsadmin /Transfer <Name> [<Type>] [/Priority <Job_Priority>] [/ACLFlags <Flags>] [/DYNAMIC] <RemoteFileName> <LocalFileName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Name|Der Name des Auftrags. Im Gegensatz zu den meisten Befehlen darf **Name** nur ein Name und keine GUID sein.|
|Typ|Optional – geben Sie den Typ des Auftrags an. Verwenden Sie **/Download** (Standardeinstellung) für einen Download Auftrag oder **"/Upload"** für einen Uploadauftrag.|
|Priority|Optional – legen Sie den job_priority auf einen der folgenden Werte fest:</br>-Vordergrund</br>-Hoch</br>-NORMAL</br>-Niedrig|
|Aclflags|Optional – gibt an, dass Sie den Besitzer und die ACL-Informationen mit der heruntergeladenen Datei verwalten möchten. Um z. b. den Besitzer und die Gruppe mit der Datei beizubehalten, legen Sie Flags auf `OG`fest. Geben Sie mindestens eines der folgenden Flags an:</br>-O: Besitzer Informationen in Datei kopieren.</br>-G: Kopieren von Gruppeninformationen mit der Datei.</br>-D: DACL-Informationen werden mit der Datei kopiert.</br>-S: Kopieren Sie SACL-Informationen mit der Datei.|
|/DYNAMIC|Konfiguriert den Auftrag mit [**BITS_JOB_PROPERTY_DYNAMIC_CONTENT**](/windows/desktop/api/bits5_0/ne-bits5_0-bits_job_property_id), wodurch die serverseitigen Anforderungen entspannt werden.|
|Remotefilename|Der Name der Datei, wenn Sie auf den Server übertragen wird.|
|Localfilename|Der Name der lokalen Datei.|

## <a name="remarks"></a>Hinweise

Standardmäßig erstellt der bitadmin-Dienst einen Download Auftrag, der mit **normaler** Priorität ausgeführt wird, und aktualisiert das Befehlsfenster mit Statusinformationen, bis die Übertragung abgeschlossen ist oder ein kritischer Fehler auftritt. Der Dienst schließt den Auftrag ab, wenn er alle Dateien erfolgreich überträgt und den Auftrag abbricht, wenn ein kritischer Fehler auftritt. Der Dienst erstellt den Auftrag nicht, wenn dem Auftrag keine Dateien hinzugefügt werden können oder wenn Sie einen ungültigen Wert für *Typ* oder *Job_Priority*angeben. Um mehr als eine Datei zu übertragen, geben Sie mehrere *remotefilename* --*localfilename* -Paare an. Die Paare sind durch Leerzeichen begrenzt.

> [!NOTE]
> Der bitionsadmin-Befehl wird weiterhin ausgeführt, wenn ein vorübergehender Fehler auftritt. Um den Befehl zu beenden, drücken Sie STRG + C.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird ein Übertragungs Auftrag mit dem Namen *mydownloadjob*gestartet.
```
C:\>bitsadmin /Transfer myDownloadJob http://prodserver/audio.wma c:\downloads\audio.wma
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)