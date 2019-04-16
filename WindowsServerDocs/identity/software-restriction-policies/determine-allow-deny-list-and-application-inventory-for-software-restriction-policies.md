---
title: "Bestimmen Sie zulassen bzw. verweigern-Liste und des Anwendungsinventars für Richtlinien für Softwareeinschränkung"
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="determine-allow-deny-list-and-application-inventory-for-software-restriction-policies"></a>Bestimmen Sie zulassen bzw. verweigern-Liste und des Anwendungsinventars für Richtlinien für Softwareeinschränkung

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema für IT-Spezialisten enthält eine Anleitung zum Erstellen einer zulassen und Negativliste für Apps für die Verwaltung durch (Software Restriction Policies, SRP) ab Windows Server2008 und Windows Vista.

## <a name="introduction"></a>Einführung in
(Software Restriction Policies, SRP) ist der Gruppenrichtlinie basierendes Feature, das Softwareprogramme identifiziert, die auf Computern in einer Domäne ausgeführt, und die Fähigkeit zur Ausführung dieser Programme steuert. Mithilfe von Softwareeinschränkungsrichtlinien um eine stark eingeschränkte Konfiguration für Computer zu erstellen, in dem Sie nur explizit angegebene Anwendungen ausführen können. Diese sind mit Microsoft Active Directory-Domänendienste und Gruppenrichtlinien integriert, aber auch auf eigenständigen Computern konfiguriert werden. Ausgangspunkt für SRP finden Sie unter der [Softwareeinschränkungsrichtlinien](software-restriction-policies.md).

Ab Windows Server 2008 R2 und Windows 7, kann Windows AppLocker anstelle von oder zusammen mit SRP für einen Teil Ihrer anwendungssteuerungsstrategie verwendet werden.

Informationen dazu, wie Sie bestimmte Aufgaben mit SRP finden Sie in der folgenden:

-   [Arbeiten Sie mit Software Restriction Policies Regeln](work-with-software-restriction-policies-rules.md)

-   [Verwenden von Richtlinien für Softwareeinschränkung zum Schutz Ihres Computers vor einem E-Mail-Virus](use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus.md)

### <a name="what-default-rule-to-choose-allow-or-deny"></a>Welche Standardregel auswählen: gewähren oder verweigern
Richtlinien für Softwareeinschränkung in einem von zwei Modi, die die Grundlage für die Standardregel bereitgestellt werden können: Liste zulassen oder verweigern. Sie können eine Richtlinie erstellen, die jede Anwendung identifiziert, die in Ihrer Umgebung ausgeführt werden darf. die Standardregel in Ihrer Richtlinie ist eingeschränkt blockieren Sie alle Anwendungen, die nicht ausdrücklich zulassen ausgeführt. Oder Sie können eine Richtlinie, die jede Anwendung identifiziert, die ausgeführt werden kann; die Standard-Regel ist nicht eingeschränkt und lässt nur die Anwendungen, die Sie explizit aufgeführt sind.

> [!IMPORTANT]
> Der Verweigerungsliste Modus möglicherweise eine Strategie hohem Verwaltungsaufwand für Ihre Organisation hinsichtlich der Anwendungskontrolle. Erstellen und Verwalten von einer sich entwickelnden Liste, die verhindert, alle Schadsoftware und andere problematische Anwendung dass wäre zeitaufwändig und anfällig für Fehler.

### <a name="create-an-inventory-of-your-applications-for-the-allow-list"></a>Erstellen Sie eine Anwendung für die Liste "zulassen"
Um die Standard-Zulassungsregel effektiv zu verwenden, müssen Sie bestimmen, genau welche Anwendungen in Ihrer Organisation erforderlich sind. Es gibt Tools, die eine Anwendungsinventur, z.B. die Inventur-Sammlung in der Microsoft Application Compatibility Toolkit zu erstellen. Aber SRP hat eine erweiterte Protokollierung-Feature, mit Ihnen zu verstehen, genau welche Anwendungen in Ihrer Umgebung ausgeführt werden können.

##### <a name="to-discover-which-applications-to-allow"></a>Welche Anwendungen zu ermitteln.

1.  Bereitstellen Sie in einer Testumgebung Softwareeinschränkungsrichtlinie mit dem Standard-Regelsatz nicht eingeschränkt, und entfernen Sie keine zusätzlichen Regeln. Wenn Sie SRP aktivieren, ohne dass es für alle Anwendungen zu beschränken, werden SPR überwachen, welche Anwendungen werden ausgeführt.

2.  Erstellen Sie den folgenden Registrierungswert, damit das Feature zur erweiterten Protokollierung zu aktivieren, und legen Sie den Pfad an, in dem die Protokolldatei geschrieben werden soll.

    **"HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Safer\ CodeIdentifiers"**

    Zeichenfolgenwert: *NameLogFile Pfad zur NameLogFile*

    Da SRP alle Anwendungen bewertet, wenn sie ausgeführt werden, wird ein Eintrag in die Protokolldatei geschrieben *NameLogFile* jedes Mal, wenn die Anwendung ausgeführt wird.

3.  Bewerten Sie die Protokolldatei

    Jeder Eintrag angibt:

    -   Der Aufrufer der Softwareeinschränkungsrichtlinien und die Prozess-ID (PID) des der aufrufende Prozess

    -   Das Ziel ausgewertet werden

    -   Die SRP-Regel, die aufgetreten ist, wenn die Anwendung ausgeführt haben

    -   Ein Bezeichner für die SRP-Regel.

    Ein Beispiel der Ausgabe in eine Protokolldatei geschrieben:

**Explorer.exe (PID = 4728) identifiedC:\Windows\system32\OneNote.exe uneingeschränkten Usingpath gilt, GUID = {320bd852-aa7c-4674-82c5-9a80321670a3}** alle Anwendungen und zugehörigen Code, der SRP überprüft und blockieren, weitere Maßnahmen in der Protokolldatei, die Sie dann verwenden können, um zu bestimmen, welche ausführbare Dateien für Ihre Liste der zulässigen Apps berücksichtigt werden sollen.


