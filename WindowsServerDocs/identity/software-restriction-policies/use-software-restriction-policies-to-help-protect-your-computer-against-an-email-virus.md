---
title: Verwenden von Richtlinien für die Softwareeinschränkung zum Schutz Ihres Computers vor einem E-Mail-Virus
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850671"
---
# <a name="use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus"></a>Verwenden von Richtlinien für die Softwareeinschränkung zum Schutz Ihres Computers vor einem E-Mail-Virus

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema enthält Informationen, die die anwendungssteuerung festlegen-Richtlinien mithilfe von Windows-Verwaltungsinstrumentation (Software Restriction Policies, SRP) zum Schutz Ihres Computers vor der e-Mail-Virus ab Windows Server 2008 und Windows Vista.

## <a name="introduction"></a>Einführung
Die Richtlinien für Softwareeinschränkung (Software Restriction Policies, SRP) sind ein auf der Gruppenrichtlinie basierendes Feature, das Softwareprogramme identifiziert, die auf Computern in einer Domäne ausgeführt werden, und die Fähigkeit zur Ausführung dieser Programme steuert. Sie können Richtlinien für Softwareeinschränkung auch verwenden, um eine stark eingeschränkte Konfiguration für Computer zu erstellen, in der Sie ausschließlich die Ausführung explizit angegebener Anwendungen zulassen. Diese in Microsoft Active Directory-Domänendienste und Gruppenrichtlinien integriert sind, aber auch auf eigenständigen Computern konfiguriert werden. Ausgangspunkt für Richtlinien für Softwareeinschränkung, finden Sie unter den [Richtlinien für Softwareeinschränkung](software-restriction-policies.md).

Ab Windows Server 2008 R2 und Windows 7, Windows AppLocker anstelle oder zusammen mit Richtlinien für Softwareeinschränkung für einen Teil Ihrer anwendungssteuerungsstrategie dienen. 

#### <a name="configure-srp-to-help-protect-against-an-e-mail-virus"></a>Konfigurieren von Richtlinien für Softwareeinschränkung zum Schutz vor einem e-Mail-virus

1.  Überprüfen Sie die bewährten Methoden für Richtlinien für softwareeinschränkung zu verstehen, wie Richtlinien für Softwareeinschränkung funktioniert.

    -   [Empfohlene Methoden](software-restriction-policies-technical-overview.md#BKMK_Best_Practices)

    -   [Wie funktionieren Richtlinien für Softwareeinschränkung](https://technet.microsoft.com/library/cc786941(v=WS.10).aspx)

2.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

    -   [Für den lokalen computer](administer-software-restriction-policies.md#BKMK_1)

    -   [Sind für eine Domäne Standort oder die Organisationseinheit, und Sie ein, auf einem Mitgliedsserver oder einer Arbeitsstation, die mit einer Domäne verknüpft ist](administer-software-restriction-policies.md#BKMK_2)

3.  Wenn Sie Richtlinien für softwareeinschränkung nicht zuvor definiert haben, erstellen Sie neue Richtlinien für softwareeinschränkung.

    -   [Erstellen Sie neue Richtlinien für softwareeinschränkung](administer-software-restriction-policies.md#BKMK_Create_SRP)

4.  Erstellen Sie eine Pfadregel für den Ordner, der das e-Mail-Programm verwendet wird, um e-Mail-Anlagen auszuführen, und legen Sie die Sicherheit auf **nicht erlaubt**.

    -   [Arbeiten mit Pfadregeln](work-with-software-restriction-policies-rules.md#BKMK_Path_Rules)

5.  Geben Sie die Dateitypen, die für die die Regel gilt.

    -   [Hinzufügen oder Löschen eines designierten Dateityps](administer-software-restriction-policies.md#BKMK_Add_Del)

6.  Ändern Sie die Richtlinieneinstellungen, damit sie gelten für die Benutzer und Gruppen, die Sie möchten:

    -   Geben Sie Benutzern oder Gruppen, Sie nicht das Gruppenrichtlinienobjekt des (Gruppenrichtlinienobjekt GPO möchten) die Richtlinieneinstellungen angewendet.

    -   Lokale Administratoren von Richtlinien für softwareeinschränkung einer Einstellung für die spezifische Richtlinie in der Gruppenrichtlinie ausschließen und den Rest der Gruppenrichtlinie für die Administratoren gelten immer noch.

        -   [Um zu verhindern, dass Softwareeinschränkungsrichtlinien für lokale Administratoren](administer-software-restriction-policies.md#BKMK_Prevent_Admin)

7.  Testen der Richtlinie an.


