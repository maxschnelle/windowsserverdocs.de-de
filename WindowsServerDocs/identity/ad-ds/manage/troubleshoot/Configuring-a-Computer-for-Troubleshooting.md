---
ms.assetid: 155abe09-6360-4913-8dd9-7392d71ea4e6
title: Konfigurieren eines Computers für die Problembehandlung
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 1acb5f7d309d58ed4a5a3aca6bb89f01c0cbf933
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854121"
---
# <a name="configuring-a-computer-for-troubleshooting"></a>Konfigurieren eines Computers für die Problembehandlung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Vor der Verwendung fortgeschrittenen Techniken der Problembehandlung erkennen und beheben Probleme bei der Active Directory konfigurieren Sie Ihre Computer für die Problembehandlung. Sie sollten auch ein grundlegendes Verständnis der Konzepte, Verfahren und Tools zur haben.

Informationen zum Überwachen von Tools für Windows Server finden Sie in der schrittweisen Anleitung für [Leistungs- und Zuverlässigkeitsüberwachung in Windows Server](https://go.microsoft.com/fwlink/?LinkId=123737)

## <a name="configuration-tasks-for-troubleshooting"></a>Konfigurationsaufgaben für die Problembehandlung

Führen Sie zum Konfigurieren des Computers zur Problembehandlung der Active Directory Domain Services (AD DS) die folgenden Aufgaben aus:

### <a name="install-remote-server-administration-tools-for-ad-ds"></a>Installieren Sie Remoteserver-Verwaltungstools für AD DS

Bei der Installation von AD DS auf einen Domänencontroller zu erstellen, werden die Verwaltungstools, die Sie verwenden, um das Verwalten von AD DS automatisch installiert. Wenn Sie möchten die Domänencontroller remote auf einem Computer verwalten, die nicht auf einem Domänencontroller ist, können Sie die Remote Server-Verwaltungstools (RSAT) installieren, auf einem Mitgliedsserver oder einer Arbeitsstation, auf denen eine unterstützte Version von Windows ausgeführt wird. Remoteserver-Verwaltungstools wird die Windows-Supporttools von Windows Server 2003 ersetzt.

Informationen zum Installieren der Remoteserver-Verwaltungstools, finden Sie im Artikel [Remoteserver-Verwaltungstools](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools).

### <a name="configure-reliability-and-performance-monitor"></a>Konfigurieren der Zuverlässigkeits- und Leistungsüberwachung

Windows Server enthält, die Windows-Zuverlässigkeit und die Performance Monitor, der ein Microsoft Management Console (MMC)-Snap-in, die die Funktionalität vorheriger eigenständiger Tools ist, einschließlich Leistungsprotokolle und Warnungen, Server Performance Advisor kombiniert, und zum Systemmonitor. Dieses Snap-In bietet eine grafische Benutzeroberfläche (GUI) für die Anpassung Datensammlersätze und Ereignisablaufverfolgungssitzungen.

Zuverlässigkeits- und Leistungsüberwachung umfasst auch Reliability Monitor, ein MMC-Snap-in, die verfolgt Änderungen an das System und vergleicht diese Änderungen in der Systemstabilität, bietet eine grafische Darstellung der ihre Beziehung an.

### <a name="set-logging-levels"></a>Protokollieren von Ebenen festlegen

Wenn die Informationen, die in das Verzeichnisdienst-Protokoll in der Ereignisanzeige Sie erhalten für die Problembehandlung nicht ausreicht, lösen die Protokolliergrade mit dem entsprechenden Registrierungseintrag in **HKEY_LOCAL_ MACHINESYSTEMCurrentControlSetServicesNTDSDiagnostics**.

Standardmäßig werden die Protokolliergrade für alle Einträge festgelegt, um **0**, die die minimale Menge an Informationen bereitstellt. Der höchste Protokolliergrad ist **5**. Erhöhen die Ebene nach einem Eintrag bewirkt, dass weitere Ereignisse im Verzeichnisdienst-Ereignisprotokoll protokolliert werden.

Verwenden Sie das folgende Verfahren, um den Protokolliergrad für ein diagnoseeintrag zu ändern. Grundvoraussetzung für die Ausführung dieses Vorgangs ist die Mitgliedschaft in **Domänen-Admins** oder einer gleichwertigen Gruppe.

> [!WARNING]
> Es wird empfohlen, die Registrierung nur dann direkt zu bearbeiten, wenn es keine andere Alternative gibt. Änderungen an der Registrierung werden nicht überprüft, indem Sie den Registrierungs-Editor oder Windows, bevor sie angewendet werden, und daher falsche Werte gespeichert werden können. Dies kann zu nicht behebbaren Fehlern im System führen. Verwenden Sie nach Möglichkeit Gruppenrichtlinien oder anderen Windows-Tools, z. B. MMC-Snap-ins zum Ausführen von Aufgaben, anstatt die direkte Bearbeitung der Registrierung. Wenn Sie die Registrierung bearbeiten müssen, gehen Sie äußerst umsichtig vor.
>

So ändern Sie den Protokolliergrad für ein diagnoseeintrag

1. Klicken Sie auf **starten** > **ausführen** > Typ **"regedit"** > Klicken Sie auf **OK**.
2. Navigieren Sie zu dem Eintrag für den Sie festlegen, anmelden möchten.
   * BEISPIEL: HKEY_LOCAL_MACHINESYSTEMCurrentControlSetServicesNTDSDiagnostics
3. Doppelklicken Sie auf den Eintrag, und klicken Sie in **Base**, klicken Sie auf **Decimal**.
4. In **Wert**, geben Sie eine ganze Zahl zwischen **0** über **5**, und klicken Sie dann auf **OK**.
