---
title: Verwalten von NPS-Vorlagen
description: Dieses Thema enthält Anweisungen zum Erstellen, anzuwenden, exportieren und importieren Sie die NPS-Vorlagen für Netzwerkrichtlinienserver unter Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 989b00c5-4767-4081-ace5-6321f8b2c55e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 170a0e86f7dcca77c6efe841318b522554f8e78e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845131"
---
# <a name="manage-nps-templates"></a>Verwalten von NPS-Vorlagen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Können Sie Netzwerkrichtlinienserver \(NPS\) Vorlagen zum Erstellen der Konfigurationselemente, z. B. Remote Authentication Dial-in User Service \(RADIUS\) Clients oder freigegebene geheime Daten, die auf dem lokalen wiederverwendet werden können NPS und Export für die Verwendung auf anderen NPSs. 

Vorlagenverwaltung stellt einen Knoten in der NPS-Konsole, in denen Sie können erstellen, ändern, löschen, duplizieren, und zeigen Sie die Verwendung von NPS-Vorlagen, bereit. NPS-Vorlagen dienen zum Verringern der Anzahl der Zeit- und Kostenaufwand, die zum Konfigurieren von NPS auf einem oder mehreren Servern benötigt.

Die folgenden Typen der NPS-Vorlagen sind für die Konfiguration in der Verwaltung von Vorlagen verfügbar.

- **Gemeinsamer geheimer**. Diese Vorlagentyp macht es möglich, dass Sie einen gemeinsamen geheimen Schlüssel angeben, die Sie wiederverwenden können (durch Auswählen der Vorlage in die entsprechende Position in der NPS-Konsole) Wenn Sie die RADIUS-Clients und Servern konfigurieren. 

- **RADIUS-Clients**. Solche Vorlage ermöglicht es, für die Sie zum Konfigurieren von RADIUS-Clienteinstellungen, die Sie wiederverwenden können, durch Auswählen der Vorlage in die entsprechende Position in der NPS-Konsole.

- **Remote-RADIUS-Servern**. Diese Vorlage ermöglicht es, für das remote-RADIUS-Server-Einstellungen konfigurieren, die Sie durch Auswählen der Vorlage in die entsprechende Position in der NPS-Konsole wiederverwenden können. 

- **IP-Filter**. Diese Vorlage ermöglicht es Ihnen die Erstellung von Internet Protocol, Version 4 (IPv4) und Internetprotokoll Version 6 \(IPv6\) Filter, die Sie wiederverwenden können \(durch Auswählen der Vorlage in die entsprechende Position in der NPS Konsole\) beim Netzwerkrichtlinien konfigurieren.

## <a name="create-an-nps-template"></a>Erstellen Sie eine NPS-Vorlage

Konfigurieren einer Vorlage unterscheidet sich von den NPS direkt konfigurieren. Erstellen einer Vorlage wirkt sich nicht auf den NPS Funktionen aus. Es ist nur, wenn Sie die Vorlage in die entsprechende Position in der NPS-Konsole auswählen und wenden Sie die Vorlage an, dass die Vorlage die NPS-Funktionalität auswirkt. 

Angenommen, konfigurieren Sie einen RADIUS-Client in der Konsole "NPS" unter **RADIUS-Clients und Servern**, Sie ändern die NPS-Konfiguration, und wird bei der Konfiguration von NPS für die Kommunikation mit einem der Server für den Netzwerkzugriff. \(Der nächste Schritt ist so konfigurieren Sie Netzwerkzugriffsserver \(NAS\) mit NPS kommunizieren.\) 

Jedoch wenn Sie ein neues konfigurieren **RADIUS-Clients** Vorlage in der Konsole "NPS" unter **Vorlagenverwaltung** anstatt zu einer neuen RADIUS-Clients unter Erstellen **RADIUS-Clients und Servern**, Sie haben eine Vorlage erstellt, aber Sie haben nicht die NPS-Funktionalität noch geändert. Um die NPS-Funktionalität ändern, müssen Sie die Vorlage von der richtigen Position in der NPS-Konsole anwenden.

Das folgende Verfahren enthält Anweisungen zum Erstellen einer neuen Vorlage.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.

### <a name="to-create-an-nps-template"></a>So erstellen Sie eine NPS-Vorlage


1. Klicken Sie auf den NPS, im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet. 

2. Erweitern Sie in der Konsole "NPS" **Vorlagenverwaltung**, mit der rechten Maustaste wie z. B. auf eines Vorlagentyp **RADIUS-Clients**, und klicken Sie dann auf **neu**.

3. Ein neues Vorlage Eigenschaften-Dialogfeld wird geöffnet, die Sie verwenden können, um Ihre Vorlage zu konfigurieren.

## <a name="apply-an-nps-template"></a>Wenden Sie eine NPS-Vorlage

Sie können eine Vorlage, die Sie erstellt haben **Vorlagenverwaltung** durch Navigieren zu einem Speicherort in der NPS-Konsole, in dem Sie die Vorlage anwenden können. Wenn Sie eine Vorlage für freigegebene geheime Schlüssel in eine RADIUS-Client-Konfiguration anwenden möchten, können Sie z. B. das folgende Verfahren verwenden.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.

### <a name="to-apply-an-nps-template"></a>So wenden Sie eine NPS-Vorlage

1. Klicken Sie auf den NPS, im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet.

2. Erweitern Sie in der Konsole "NPS" **RADIUS-Clients und Servern**, und erweitern Sie dann **RADIUS-Clients**.

3. Wählen Sie in **RADIUS-Clients**, im Detailbereich mit der Maustaste des RADIUS-Clients, der Sie die NPS-Vorlage anwenden, und klicken Sie dann auf möchten **Eigenschaften**.

4. Im Dialogfeld "Eigenschaften" das Feld für den RADIUS-Client in **auswählen eine vorhandene Vorlage für freigegebene geheime Schlüssel**, wählen Sie die Vorlage, die Sie aus der Liste der Vorlagen anwenden möchten.

## <a name="export-or-import-nps-templates"></a>Exportieren oder importieren NPS-Vorlagen

Sie können Vorlagen für die Verwendung auf anderen NPSs exportieren werden soll, oder Sie können Vorlagen in importieren **Vorlagenverwaltung** für die Verwendung auf dem lokalen Computer. 

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.

### <a name="to-export-or-import-nps-templates"></a>Zum Exportieren oder importieren die NPS-Vorlagen

1. So exportieren Sie die NPS-Vorlagen, in der Konsole "NPS" Maustaste **Vorlagenverwaltung**, und klicken Sie dann auf **Vorlagen in eine Datei exportieren**.

2. So importieren Sie die NPS-Vorlagen, in der Konsole "NPS" Maustaste **Vorlagenverwaltung**, und klicken Sie dann auf **Vorlagen importieren, von einem Computer** oder **Vorlagen aus Datei importieren**.


