---
title: Festlegen der Zulassen bzw. Verweigern-Liste und des Anwendungsinventars für Richtlinien für die Softwareeinschränkung
description: Windows Server-Sicherheit
ms.prod: windows-server
ms.technology: security-software-restriction-policies
ms.topic: article
ms.assetid: 0abb73b6-b5d8-4505-8ab1-2f29e4bf0411
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 7609ebb0fdcb6d429cd40d99399eaaedb732df08
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855093"
---
# <a name="determine-allow-deny-list-and-application-inventory-for-software-restriction-policies"></a>Festlegen der Zulassen bzw. Verweigern-Liste und des Anwendungsinventars für Richtlinien für die Softwareeinschränkung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema für IT-Experten wird beschrieben, wie Sie eine Zulassungs-und Verweigerungs Liste für Anwendungen erstellen, die mit Software Einschränkungs Richtlinien (SRP) ab Windows Server 2008 und Windows Vista verwaltet werden.

## <a name="introduction"></a>Einführung
Die Richtlinien für Softwareeinschränkung (Software Restriction Policies, SRP) sind ein auf der Gruppenrichtlinie basierendes Feature, das Softwareprogramme identifiziert, die auf Computern in einer Domäne ausgeführt werden, und die Fähigkeit zur Ausführung dieser Programme steuert. Sie können Richtlinien für Softwareeinschränkung auch verwenden, um eine stark eingeschränkte Konfiguration für Computer zu erstellen, in der Sie ausschließlich die Ausführung explizit angegebener Anwendungen zulassen. Diese sind in Microsoft Active Directory Domain Services und Gruppenrichtlinie integriert, können aber auch auf eigenständigen Computern konfiguriert werden. Einen Ausgangspunkt für SRP finden Sie in den [Richtlinien für Software Einschränkung](software-restriction-policies.md).

Ab Windows Server 2008 R2 und Windows 7 kann Windows AppLocker anstelle von oder in zusammen mit SRP für einen Teil ihrer Anwendungs Steuerungsstrategie verwendet werden.

Informationen zum Ausführen bestimmter Aufgaben mithilfe von SRP finden Sie in den folgenden Bereichen:

-   [Arbeiten mit Regeln der Richtlinien für Softwareeinschränkung](work-with-software-restriction-policies-rules.md)

-   [Verwenden von Richtlinien für Software Einschränkung zum Schutz Ihres Computers vor einem e-Mail-Virus](use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus.md)

### <a name="what-default-rule-to-choose-allow-or-deny"></a>Folgende Standardregel auswählen: zulassen oder verweigern
Software Einschränkungs Richtlinien können in einem von zwei Modi bereitgestellt werden, die die Basis ihrer Standardregel sind: Zulassungsliste oder Verweigerungs Liste. Sie können eine Richtlinie erstellen, die jede Anwendung identifiziert, die in Ihrer Umgebung ausgeführt werden darf. die Standardregel in der Richtlinie ist eingeschränkt und blockiert alle Anwendungen, die nicht explizit ausgeführt werden dürfen. Oder Sie können eine Richtlinie erstellen, die jede Anwendung identifiziert, die nicht ausgeführt werden kann. die Standardregel ist uneingeschränkt und schränkt nur die Anwendungen ein, die Sie explizit aufgelistet haben.

> [!IMPORTANT]
> Der Ablehnungs Listenmodus ist möglicherweise eine hoch Wartungsstrategie für Ihre Organisation in Bezug auf die Anwendungssteuerung. Das Erstellen und Verwalten einer sich entwickelnden Liste, die alle Malware und andere problematische Anwendungen untersagt, wäre zeitaufwändig und anfällig für Fehler.

### <a name="create-an-inventory-of-your-applications-for-the-allow-list"></a>Erstellen eines Inventars Ihrer Anwendungen für die Zulassungsliste
Um die Zulassungs Standardregel effektiv verwenden zu können, müssen Sie genau feststellen, welche Anwendungen in Ihrer Organisation erforderlich sind. Es gibt Tools, die entwickelt wurden, um ein Anwendungs Inventar zu entwickeln, z. b. den Inventur Sammler im Microsoft Application Compatibility Toolkit. SRP verfügt jedoch über eine erweiterte Protokollierungsfunktion, mit der Sie genau verstehen können, welche Anwendungen in Ihrer Umgebung ausgeführt werden.

##### <a name="to-discover-which-applications-to-allow"></a>So ermitteln Sie, welche Anwendungen zugelassen werden

1.  Stellen Sie in einer Testumgebung die Software Einschränkungs Richtlinie mit der Standardregel auf uneingeschränkt bereit, und entfernen Sie alle zusätzlichen Regeln. Wenn Sie SRP aktivieren, ohne dies zu erzwingen, um Anwendungen einzuschränken, kann SPR überwachen, welche Anwendungen ausgeführt werden.

2.  Erstellen Sie den folgenden Registrierungs Wert, um das Feature erweiterte Protokollierung zu aktivieren, und legen Sie den Pfad auf den Speicherort der Protokolldatei fest.

    **"HKEY_LOCAL_MACHINE \software\policies\microsoft\windows\safer\codeidentifiers"**

    Zeichen folgen Wert: *namelogfile-Pfad zu namelogfile*

    Da SRP alle Anwendungen evaluiert, wenn diese ausgeführt werden, wird jedes Mal, wenn die Anwendung ausgeführt wird, ein Eintrag in die Protokolldatei *namelogfile* geschrieben.

3.  Auswerten der Protokolldatei

    Jeder Protokolleintrag lautet:

    -   der Aufrufer der Software Einschränkungs Richtlinie und die Prozess-ID (PID) des aufrufenden Prozesses.

    -   Das auszuwertende Ziel

    -   die SRP-Regel, die gefunden wurde, als diese Anwendung ausgeführt wurde.

    -   ein Bezeichner für die SRP-Regel.

    Ein Beispiel für die Ausgabe, die in eine Protokolldatei geschrieben wird:

**Explorer. exe (PID = 4728) identifiedc: \ windows\system32\onenote.exe als unbeschränkte usingpath-Regel, GUID = {320bd852-AA7C-4674-82c5-9a80321670a3}**    Alle Anwendungen und zugeordneten Code, die von SRP überprüft und auf Block festgelegt werden, werden in der Protokolldatei vermerkt. Diese können Sie dann verwenden, um zu bestimmen, welche ausführbaren Dateien für die zulässige Liste berücksichtigt werden sollen.


