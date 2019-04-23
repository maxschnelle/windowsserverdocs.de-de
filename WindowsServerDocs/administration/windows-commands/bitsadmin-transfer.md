---
title: bitsadmin Übertragung
description: Windows-Befehle Thema **Bitsadmin Übertragung** -überträgt eine oder mehrere Dateien.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe302141-b33a-4a05-835e-dc4fc4db7d5a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2ef29a242a834fae42d1de3994a82aedcf87ec2d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852461"
---
# <a name="bitsadmin-transfer"></a>bitsadmin Übertragung

Überträgt eine oder mehrere Dateien. Um mehrere Dateien gleichzeitig übertragen werden, geben Sie mehrere \<RemoteFileName\>-\<LocalFileName\> Paare. Die Paare sind durch Leerzeichen getrennt.

## <a name="syntax"></a>Syntax

```
bitsadmin /Transfer <Name> [<Type>] [/Priority <Job_Priority>] [/ACLFlags <Flags>] [/DYNAMIC] <RemoteFileName> <LocalFileName>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Name|Der Name des Auftrags. Im Gegensatz zu den meisten Befehlen **Namen** kann nur einen Namen und nicht auf eine GUID sein.|
|Typ|Optional: Geben Sie den Typ des Auftrags. Verwendung **/herunterladen** (Standard) für einen Auftrag herunterladen oder **/hochladen** für einen Auftrag hochladen.|
|Priority|Optional – die Job_priority auf einen der folgenden Werte festgelegt:</br>: VORDERGRUND</br>– HIGH</br>-   NORMAL</br>– NIEDRIG|
|ACLFlags|Optional: Gibt an, dass Sie den Besitzer und die ACL-Informationen mit den herunterzuladenden Datei beibehalten möchten. Um den Besitzer und die Gruppe mit der Datei zu gewährleisten, legen Sie z. B. Flags auf `OG`. Geben Sie eine oder mehrere der folgenden Flags:</br>-O: Kopieren Sie Informationen über den sperrbesitzer-Datei.</br>-   G: Kopieren Sie Informationen zur Datei.</br>-   D: Kopieren Sie DACL-Informationen, mit der Datei.</br>-   S: Kopieren Sie SACL-Informationen, mit der Datei.|
|\/DYNAMIC|Konfiguriert den Auftrag mit [ **BITS_JOB_PROPERTY_DYNAMIC_CONTENT**](/windows/desktop/api/bits5_0/ne-bits5_0-bits_job_property_id), die lockert der serverseitige Anforderungen.|
|RemoteFileName|Der Name der Datei bei der Übertragung an den Server.|
|LocalFileName|Der Name der Datei, die lokal vorliegen.|

## <a name="remarks"></a>Hinweise

Der Dienst BITSAdmin erstellt standardmäßig einen Downloadauftrag, der ausgeführt wird **NORMAL** Priorität und das Befehlsfenster mit Statusinformationen aktualisiert werden, bis die Übertragung abgeschlossen ist, oder bis ein schwerwiegender Fehler auftritt. Der Dienst wird der Auftrag abgeschlossen, wenn er erfolgreich alle Dateien übertragen und bricht den Auftrag ab, wenn ein schwerwiegender Fehler auftritt. Der Dienst nicht den Auftrag erstellen, wenn es keine Dateien hinzufügen, um den Auftrag ist oder wenn Sie angeben, dass einen ungültigen Wert für *Typ* oder *Job_Priority*. Um mehrere Dateien gleichzeitig übertragen werden, geben Sie mehrere *RemoteFileName*-*LocalFileName* Paare. Die Paare sind durch Leerzeichen getrennt.

> [!NOTE]
> Der Befehl BITSAdmin weiter ausgeführt werden, wenn ein vorübergehender Fehler auftritt. Um den Befehl zu beenden, drücken Sie STRG + C.

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel beginnt, die eine Übertragung-Auftrags mit mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /Transfer myDownloadJob http://prodserver/audio.wma c:\downloads\audio.wma
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)