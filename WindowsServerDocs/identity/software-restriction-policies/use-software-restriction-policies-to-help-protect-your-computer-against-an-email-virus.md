---
title: "Verwenden von Richtlinien für Softwareeinschränkung zum Schutz Ihres Computers vor einem E-Mail-Virus"
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-software-restriction-policies
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 02f23979-f832-4e46-bdea-21fd77db35b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 41b4c2399a86ef96d34b62295eda4a1ce9300609
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus"></a>Verwenden von Richtlinien für Softwareeinschränkung zum Schutz Ihres Computers vor einem E-Mail-Virus

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Dieses Thema enthält Informationen, wie ein Steuerelement Anwendung von Sicherheitsrichtlinien (Software Restriction Policies, SRP) zum Schutz Ihres Computers vor e-Mail-Virus ab Windows Server 2008 und Windows Vista verwenden.

## <a name="introduction"></a>Einführung in
(Software Restriction Policies, SRP) ist der Gruppenrichtlinie basierendes Feature, das Softwareprogramme identifiziert, die auf Computern in einer Domäne ausgeführt, und die Fähigkeit zur Ausführung dieser Programme steuert. Mithilfe von Softwareeinschränkungsrichtlinien um eine stark eingeschränkte Konfiguration für Computer zu erstellen, in dem Sie nur explizit angegebene Anwendungen ausführen können. Diese sind mit Microsoft Active Directory-Domänendienste und Gruppenrichtlinien integriert, aber auch auf eigenständigen Computern konfiguriert werden. Ausgangspunkt für SRP finden Sie unter der [Softwareeinschränkungsrichtlinien](software-restriction-policies.md).

Ab Windows Server 2008 R2 und Windows 7, kann Windows AppLocker anstelle von oder zusammen mit SRP für einen Teil Ihrer anwendungssteuerungsstrategie verwendet werden. 

#### <a name="configure-srp-to-help-protect-against-an-e-mail-virus"></a>Konfigurieren von SRP zum Schutz vor einem e-Mail-virus

1.  Überprüfen Sie die bewährten Methoden für Softwareeinschränkungsrichtlinien zum Verständnis der Funktionsweise von SRP.

    -   [Bewährte Methoden](software-restriction-policies-technical-overview.md#BKMK_Best_Practices)

    -   [Funktionsweise von Softwareeinschränkungsrichtlinien](https://technet.microsoft.com/library/cc786941(v=WS.10).aspx)

2.  Öffnen Sie die Richtlinien für Softwareeinschränkung.

    -   [Für den lokalen computer](administer-software-restriction-policies.md#BKMK_1)

    -   [Sind für eine Domäne Site oder Organisationseinheit, und Sie ein, auf einem Mitgliedsserver oder einer Arbeitsstation, die einer Domäne angehört](administer-software-restriction-policies.md#BKMK_2)

3.  Wenn Sie Richtlinien für softwareeinschränkung nicht definiert haben, erstellen Sie neue Softwareeinschränkungsrichtlinien.

    -   [Zum Erstellen neuer Softwareeinschränkungsrichtlinien](administer-software-restriction-policies.md#BKMK_Create_SRP)

4.  Erstellen Sie eine Pfadregel für den Ordner, der Ihr e-Mail-Programm verwendet wird, um e-Mail-Anlagen ausführen, und legen Sie die Sicherheit auf **nicht erlaubt**.

    -   [Arbeiten mit Pfadregeln](work-with-software-restriction-policies-rules.md#BKMK_Path_Rules)

5.  Geben Sie die Dateitypen, die für die die Regel gilt.

    -   [Hinzufügen oder Löschen eines designierten Dateityps](administer-software-restriction-policies.md#BKMK_Add_Del)

6.  Ändern Sie Einstellungen, sodass sie gelten für die Benutzer und Gruppen:

    -   Geben Sie Benutzer oder Gruppen, Sie die Gruppenrichtlinienobjekts (GPO möchten) Richtlinieneinstellungen angewendet.

    -   Lokale Administratoren von den Softwareeinschränkungsrichtlinien für eine bestimmte Einstellung in der Gruppenrichtlinie ausgeschlossen ist und noch immer den Rest der Gruppenrichtlinie für die Administratoren gelten.

        -   [Um zu verhindern, dass Softwareeinschränkungsrichtlinien für lokale Administratoren](administer-software-restriction-policies.md#BKMK_Prevent_Admin)

7.  Testen der Richtlinie.


