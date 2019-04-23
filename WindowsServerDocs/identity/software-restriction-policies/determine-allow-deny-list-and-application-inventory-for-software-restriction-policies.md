---
title: Festlegen der Zulassen bzw. Verweigern-Liste und des Anwendungsinventars für Richtlinien für die Softwareeinschränkung
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-software-restriction-policies
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0abb73b6-b5d8-4505-8ab1-2f29e4bf0411
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 60e78912284715649938567d66ffb90b9890b1b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847291"
---
# <a name="determine-allow-deny-list-and-application-inventory-for-software-restriction-policies"></a>Festlegen der Zulassen bzw. Verweigern-Liste und des Anwendungsinventars für Richtlinien für die Softwareeinschränkung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema für IT-Experten bietet Anleitungen wie Erstellen zulassen und verweigern-Liste für Anwendungen, für die Verwaltung mit Windows Server 2008 und Windows Vista (Software Restriction Policies, SRP) ab.

## <a name="introduction"></a>Einführung
Die Richtlinien für Softwareeinschränkung (Software Restriction Policies, SRP) sind ein auf der Gruppenrichtlinie basierendes Feature, das Softwareprogramme identifiziert, die auf Computern in einer Domäne ausgeführt werden, und die Fähigkeit zur Ausführung dieser Programme steuert. Sie können Richtlinien für Softwareeinschränkung auch verwenden, um eine stark eingeschränkte Konfiguration für Computer zu erstellen, in der Sie ausschließlich die Ausführung explizit angegebener Anwendungen zulassen. Diese in Microsoft Active Directory-Domänendienste und Gruppenrichtlinien integriert sind, aber auch auf eigenständigen Computern konfiguriert werden. Ausgangspunkt für Richtlinien für Softwareeinschränkung, finden Sie unter den [Richtlinien für Softwareeinschränkung](software-restriction-policies.md).

Ab Windows Server 2008 R2 und Windows 7, Windows AppLocker anstelle oder zusammen mit Richtlinien für Softwareeinschränkung für einen Teil Ihrer anwendungssteuerungsstrategie dienen.

Informationen zum Ausführen bestimmte Aufgaben mithilfe von Richtlinien für Softwareeinschränkung finden Sie hier:

-   [Arbeiten Sie mit Richtlinien für die Softwareeinschränkungsregeln](work-with-software-restriction-policies-rules.md)

-   [Verwenden von Richtlinien für Softwareeinschränkungen zum Schutz Ihres Computers vor einem e-Mail-Virus](use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus.md)

### <a name="what-default-rule-to-choose-allow-or-deny"></a>Welche Standardregel auswählen: Zulassen oder verweigern
Richtlinien für softwareeinschränkung können in zwei Modi bereitgestellt werden, die die Grundlage für Ihre Standardregel sind: Liste der zugelassenen oder Verweigerungsliste. Sie können eine Richtlinie erstellen, die jede Anwendung identifiziert, die in Ihrer Umgebung ausgeführt werden darf; die Standardregel in Ihrer Richtlinie ist eingeschränkt, und wird blockiert alle Anwendungen, die nicht explizit zuzulassen ausgeführt. Oder Sie erstellen eine Richtlinie, die jede Anwendung identifiziert, die nicht ausgeführt werden kann; die Standardregel ist nicht eingeschränkt und nur die Anwendungen, die Sie explizit aufgelistet haben beschränkt.

> [!IMPORTANT]
> Der Modus für die verweigern-Liste möglicherweise eine hohe-Wartungsstrategie für Ihre Organisation in Bezug auf die anwendungssteuerung. Erstellen und verwalten eine wachsende Liste, die verhindert, sämtlicher Malware und anderer problematischen Anwendungen dass wäre zeitaufwendig und anfällig für Fehler.

### <a name="create-an-inventory-of-your-applications-for-the-allow-list"></a>Erstellung eines Inventars aus Ihrer Anwendung in der Zulassungsliste
Um die Standard-Zulassungsregel effektiv nutzen zu können, müssen Sie bestimmen, welche Anwendungen in Ihrer Organisation erforderlich sind. Es gibt Tools, die zum Erzeugen eines Anwendungsbestands, z. B. dem Inventory Collector in die Microsoft Application Compatibility Toolkit entworfen. Jedoch SRP verfügt über ein Feature zur erweiterten Protokollierung können Sie entnehmen, genau wie die Anwendungen in Ihrer Umgebung ausgeführt werden.

##### <a name="to-discover-which-applications-to-allow"></a>Welche Anwendungen zu ermitteln.

1.  Bereitstellen Sie in einer testumgebung der Richtlinie für Softwareeinschränkung mit dem Standard-Regelsatz, um eine uneingeschränkte aus, und entfernen Sie alle zusätzlichen Regeln. Wenn Sie Richtlinien für Softwareeinschränkung aktivieren, ohne dass sie alle Anwendungen zu beschränken, werden SPR überwachen, welche Anwendungen ausgeführt werden, sind.

2.  Erstellen Sie den folgenden Registrierungswert, um das Feature zur erweiterten Protokollierung zu aktivieren, und legen Sie den Pfad, in dem die Protokolldatei geschrieben werden soll.

    **"HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Safer\ CodeIdentifiers"**

    String-Wert: *NameLogFile Pfad NameLogFile*

    Da Softwareeinschränkungsrichtlinien bei der Ausführung aller Anwendungen auswertet, wird ein Eintrag in die Protokolldatei geschrieben *NameLogFile* jedes Mal, die Anwendung ausgeführt wird.

3.  Auswerten der Protokolldatei.

    Jeder Protokolleintrag gibt:

    -   der Aufrufer der Softwareeinschränkungsrichtlinie und die Prozess-ID (PID) des aufrufenden Prozesses

    -   Das Ziel ausgewertet wird

    -   die SRP-Regel, die aufgetreten ist, wenn die Anwendung ausgeführt wurde

    -   Ein Bezeichner für die SRP-Regel.

    Ein Beispiel für die Ausgabe in eine Protokolldatei geschrieben:

**Explorer.exe (PID = 4728) identifiedC:\Windows\system32\onenote.exe uneingeschränkten Usingpath gilt, Guid = {320bd852-aa7c-4674-82c5-9a80321670a3}** alle Anwendungen und den zugehörigen Code, der Richtlinien für Softwareeinschränkung überprüft und blockieren in das Protokoll angegeben Datei, die Sie verwenden können, um zu bestimmen, welche ausführbare Dateien, die für die Liste der zulässigen berücksichtigt werden sollen.


