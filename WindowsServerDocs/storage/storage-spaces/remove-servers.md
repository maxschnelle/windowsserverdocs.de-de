---
title: Entfernen von Servern in Direkte Speicherplätze
ms.assetid: 9d8499a7-1307-473d-9f00-8a051164fad2
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
description: Wie entferne ich Server aus einem Direkte Speicherplätze-Cluster in Windows Server.
ms.date: 2/5/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fcb67b3c5fbcff0ca2a48ee9a1d2e109af3e9a8
ms.sourcegitcommit: bb626d8626ef47426b781925ea588755dbe2e403
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/28/2018
ms.locfileid: "7871603"
---
# Entfernen von Servern in Direkte Speicherplätze

>Gilt für: WindowsServer 2019, WindowsServer 2016

In diesem Thema wird beschrieben, wie Server in [Direkte Speicherplätze](storage-spaces-direct-overview.md) mithilfe von PowerShell entfernt werden.

## Entfernen eines Servers, aber Beibehalten der Laufwerke

Wenn Sie den Server bald wieder dem Cluster hinzufügen möchten oder wenn Sie die Laufwerke behalten möchten, indem Sie sie auf einen anderen Server verschieben, können Sie den Server aus dem Cluster entfernen, *ohne* seine Laufwerke aus dem Speicherpool zu entfernen. Dies ist das Standardverhalten bei Verwendung des Failovercluster-Managers zum Entfernen des Servers.

Verwenden Sie das [Remove-ClusterNode](https://technet.microsoft.com/library/hh847251.aspx)-Cmdlet in PowerShell:

```PowerShell
Remove-ClusterNode <Name>
```

Dieses Cmdlet ist schnell erfolgreich, unabhängig von allen Kapazitätsaspekten, weil sich der Speicherpool die fehlenden Laufwerke merkt und erwartet, dass sie zurückkehren. Es werden keine Daten von den fehlenden Laufwerken verschoben. Während sie nicht vorhanden sind, wird für **OperationalStatus**"Verbindung unterbrochen" angezeigt, und für die Volumes wird "Unvollständig" angezeigt.

Wenn die Laufwerke zurückkehren, werden sie automatisch erkannt und dem Pool neu zugeordnet, auch wenn sie sich jetzt auf einem neuen Server befinden.

   >[!WARNING]
   > Verteilen Sie keine Laufwerke mit Pooldaten von einem Server auf mehrere andere Server. Beispiel: Wenn ein Server mit zehn Laufwerke ausfällt (beispielsweise weil bei der Hauptplatine oder dem Startlaufwerk ein Fehler auftritt), **können** Sie alle zehn Laufwerke auf einen neuen Server verschieben, aber Sie **können sie nicht** separat auf verschiedene andere Server verschieben.

## Entfernen eines Servers und seiner Laufwerke

Wenn Sie einen Server endgültig aus dem Cluster entfernen möchten (auch als horizontales Herunterskalieren bezeichnet), können Sie den Server aus dem Cluster *und* seine Laufwerke aus dem Speicherpool entfernen.

Verwenden Sie das **Remove-ClusterNode**-Cmdlet mit dem optionalen **-CleanUpDisks**-Flag:

```PowerShell
Remove-ClusterNode <Name> -CleanUpDisks
```

Die Ausführung dieses Cmdlet kann lange dauern (manchmal auch viele Stunden), da Windows alle auf dem Server gespeicherten Daten auf andere Servern im Cluster verschieben muss. Nachdem dieser Vorgang abgeschlossen ist, werden die Laufwerke dauerhaft aus dem Speicherpool entfernt und der fehlerfreie Zustand der betroffenen Volumes wiederhergestellt.

### Anforderungen

Zum dauerhaften horizontalen Herunterskalieren (Entfernen eines Servers *und* der Laufwerke) muss der Cluster die folgenden zwei Kriterien erfüllen. Ist dies nicht der Fall, gibt das Cmdlet **Remove-ClusterNode -CleanUpDisks** sofort einen Fehler zurück, bevor die Datenverschiebung beginnt, um Störungen zu minimieren.

#### Ausreichend Kapazität

Zunächst benötigen Sie genügend Speicherkapazität auf den verbleibenden Servern für alle Ihre Volumes.

Wenn Sie beispielsweise vier Server mit jeweils zehn 1-TB-Laufwerken besitzen, haben Sie insgesamt 40 TB physische Speicherkapazität. Nach dem Entfernen eines Servers und aller seiner Laufwerke sind 30 TB Kapazität übrig. Wenn der Speicherbedarf Ihrer Volumes zusammen mehr als 30TB beträgt, passen sie nicht auf die verbleibenden Server, daher gibt das Cmdlet einen Fehler zurück, und es werden keine Daten verschoben.

#### Genügend Fehlerdomänen

Zweitens benötigen Sie genügend Fehlerdomänen (in der Regel Server), um die Resilizenz Ihrer Volumes bereitzustellen.

Wenn beispielsweise die Volumes Drei-Wege-Spiegelung auf Serverebene für Resilizenz verwenden, können sie nur fehlerfrei sein, wenn Sie mindestens drei Server besitzen. Wenn Sie genau drei Server haben und dann versuchen, einen Server and alle seine Laufwerke zu entfernen, gibt das Cmdlet einen Fehler zurück, und es werden keine Daten verschoben.

In der folgenden Tabelle wird die Mindestanzahl der Fehlerdomänen gezeigt, die für jeden Resilienztyp erforderlich ist.

|    Resilienz          |    Mindestens erforderliche Fehlerdomänen   |
|------------------------|-------------------------------------|
|    Zwei-Wege-Spiegelung      |    2                                |
|    Drei-Wege-Spiegelung    |    3                                |
|    Duale Parität         |    4                                |

   >[!NOTE]
   > Es ist in Ordnung, kurzzeitig weniger Server zu haben, z.B. bei Ausfällen oder Wartung. Damit die Volumes wieder zurück in einen vollständig fehlerfreien Status wechseln, müssen Sie jedoch die minimale Anzahl von Servern besitzen, die oben aufgeführt ist.

## Weitere Informationen

- [Direkte Speicherplätze – Übersicht](storage-spaces-direct-overview.md)
