---
ms.assetid: 155abe09-6360-4913-8dd9-7392d71ea4e6
title: Konfigurieren eines Computers für die Problembehandlung
ms.author: daveba
author: iainfoulds
manager: daveba
ms.date: 08/07/2018
ms.topic: article
ms.openlocfilehash: f340cd9608eec21110efe7d10e936c5320d6e303
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93070462"
---
# <a name="configuring-a-computer-for-troubleshooting"></a>Konfigurieren eines Computers für die Problembehandlung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Bevor Sie erweiterte Problem Behandlungstechniken verwenden, um Active Directory Probleme zu identifizieren und zu beheben, konfigurieren Sie Ihre Computer für die Problembehandlung. Außerdem sollten Sie über grundlegende Kenntnisse der Problem Behandlungskonzepte, Verfahren und Tools verfügen.

Informationen zu Überwachungstools für Windows Server finden Sie in der Schritt-für-Schritt-Anleitung für die [Leistungs-und Zuverlässigkeits Überwachung in Windows Server](https://go.microsoft.com/fwlink/?LinkId=123737) .

## <a name="configuration-tasks-for-troubleshooting"></a>Konfigurationsaufgaben für die Problembehandlung

Führen Sie die folgenden Aufgaben aus, um den Computer für die Problembehandlung Active Directory Domain Services (AD DS) zu konfigurieren:

### <a name="install-remote-server-administration-tools-for-ad-ds"></a>Installieren Sie Remoteserver-Verwaltungstools für AD DS

Wenn Sie AD DS zum Erstellen eines Domänen Controllers installieren, werden die Verwaltungs Tools, die Sie zum Verwalten von AD DS verwenden, automatisch installiert. Wenn Sie Domänen Controller Remote von einem Computer verwalten möchten, der kein Domänen Controller ist, können Sie die Remoteserver-Verwaltungstools (RSAT) auf einem Mitglieds Server oder einer Arbeitsstation installieren, auf dem eine unterstützte Version von Windows ausgeführt wird. RSAT ersetzt Windows-Support Tools von Windows Server 2003.

Weitere Informationen zum Installieren von RSAT finden Sie im Artikel [Remoteserver-Verwaltungstools](../../../../remote/remote-server-administration-tools.md).

### <a name="configure-reliability-and-performance-monitor"></a>Konfigurieren der Zuverlässigkeit und des Leistungs Monitors

Windows Server enthält den Windows-Zuverlässigkeits-und Leistungs Monitor, bei dem es sich um ein MMC-Snap-in (Microsoft Management Console) handelt, das die Funktionalität vorheriger eigenständiger Tools, einschließlich Leistungsprotokolle und-Warnungen, Server Performance Advisor und System Monitor, kombiniert. Dieses Snap-in stellt eine grafische Benutzeroberfläche (GUI) zum Anpassen von Datensammler Sätzen und Ereignis Ablauf Verfolgungs Sitzungen bereit.

Die Zuverlässigkeits-und Leistungsüberwachung umfasst auch die Zuverlässigkeits Überwachung, ein MMC-Snap-in, das Änderungen am System nachverfolgt und Sie mit Änderungen in der Systemstabilität vergleicht und eine grafische Ansicht der Beziehung bietet.

### <a name="set-logging-levels"></a>Festlegen der Protokolliergrade

Wenn die Informationen, die Sie im Verzeichnisdienst Protokoll in Ereignisanzeige erhalten, für die Problembehandlung nicht ausreichen, erhöhen Sie die Protokollierungs Stufen mithilfe des entsprechenden Registrierungs Eintrags in **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Diagnostics** .

Standardmäßig sind die Protokollierungs Ebenen für alle Einträge auf **0** festgelegt, was die minimale Menge an Informationen liefert. Der höchste Protokolliergrad ist **5** . Das Erhöhen der Ebene für einen Eintrag bewirkt, dass zusätzliche Ereignisse im Verzeichnisdienst-Ereignisprotokoll protokolliert werden.

Verwenden Sie das folgende Verfahren, um den Protokolliergrad für einen diagnoseeintrag zu ändern. Zum Durchführen dieses Verfahrens ist mindestens die Mitgliedschaft in **Domänen-Admins** oder eine entsprechende Berechtigung erforderlich.

> [!WARNING]
> Es wird empfohlen, die Registrierung nur dann direkt zu bearbeiten, wenn es keine andere Alternative gibt. Änderungen an der Registrierung werden weder vom Registrierungs-Editor noch von Windows überprüft, bevor Sie angewendet werden. Daher können falsche Werte gespeichert werden. Dies kann zu nicht BEHEB baren Fehlern im System führen. Verwenden Sie nach Möglichkeit Gruppenrichtlinie oder andere Windows-Tools, z. b. MMC-Snap-Ins, um Aufgaben auszuführen, anstatt die Registrierung direkt zu bearbeiten. Wenn Sie die Registrierung bearbeiten müssen, gehen Sie äußerst umsichtig vor.
>

So ändern Sie den Protokolliergrad für einen diagnoseeintrag

1. Klicken Sie auf **Start**  >  **Ausführen** > geben Sie **Regedit** ein > klicken Sie auf **OK** .
2. Navigieren Sie zu dem Eintrag, für den Sie die Protokollierung festlegen möchten.
   * Beispiel: HKEY_LOCAL_MACHINESYSTEMCurrentControlSetServicesNTDSDiagnostics
3. Doppelklicken Sie auf den Eintrag, und klicken Sie in **Basis** auf **Dezimal** .
4. Geben Sie unter **Wert** eine ganze Zahl zwischen **0** und **5** ein, und klicken Sie dann auf **OK** .
