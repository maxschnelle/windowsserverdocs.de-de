---
title: Entfernen von Servern in Direkte Speicherplätze
ms.assetid: 9d8499a7-1307-473d-9f00-8a051164fad2
ms.prod: windows-server
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
description: Wie entferne ich Server aus einem Direkte Speicherplätze-Cluster in Windows Server.
ms.date: 2/5/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce8caef2b51279c97cc012045750b7a73d97a4ba
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322312"
---
# <a name="removing-servers-in-storage-spaces-direct"></a>Entfernen von Servern in Direkte Speicherplätze

>Gilt für: Windows Server 2019, Windows Server 2016

In diesem Thema wird beschrieben, wie Server in [Direkte Speicherplätze](storage-spaces-direct-overview.md) mithilfe von PowerShell entfernt werden.

## <a name="remove-a-server-but-leave-its-drives"></a>Entfernen eines Servers, aber Beibehalten der Laufwerke

Wenn Sie den Server bald wieder dem Cluster hinzufügen möchten oder wenn Sie die Laufwerke behalten möchten, indem Sie sie auf einen anderen Server verschieben, können Sie den Server aus dem Cluster entfernen, *ohne* seine Laufwerke aus dem Speicherpool zu entfernen. Dies ist das Standardverhalten bei Verwendung des Failovercluster-Managers zum Entfernen des Servers.

Verwenden Sie das [Remove-ClusterNode](https://technet.microsoft.com/library/hh847251.aspx)-Cmdlet in PowerShell:

```PowerShell
Remove-ClusterNode <Name>
```

Dieses Cmdlet ist schnell erfolgreich, unabhängig von allen Kapazitätsaspekten, weil sich der Speicherpool die fehlenden Laufwerke merkt und erwartet, dass sie zurückkehren. Es werden keine Daten von den fehlenden Laufwerken verschoben. Während sie nicht vorhanden sind, wird für **OperationalStatus**"Verbindung unterbrochen" angezeigt, und für die Volumes wird "Unvollständig" angezeigt.

Wenn die Laufwerke zurückkehren, werden sie automatisch erkannt und dem Pool neu zugeordnet, auch wenn sie sich jetzt auf einem neuen Server befinden.

   >[!WARNING]
   > Verteilen Sie keine Laufwerke mit Pooldaten von einem Server auf mehrere andere Server. Beispiel: Wenn ein Server mit zehn Laufwerke ausfällt (beispielsweise weil bei der Hauptplatine oder dem Startlaufwerk ein Fehler auftritt), **können** Sie alle zehn Laufwerke auf einen neuen Server verschieben, aber Sie **können sie nicht** separat auf verschiedene andere Server verschieben.

## <a name="remove-a-server-and-its-drives"></a>Entfernen eines Servers und seiner Laufwerke

Wenn Sie einen Server endgültig aus dem Cluster entfernen möchten (auch als horizontales Herunterskalieren bezeichnet), können Sie den Server aus dem Cluster *und* seine Laufwerke aus dem Speicherpool entfernen.

Verwenden Sie das **Remove-ClusterNode**-Cmdlet mit dem optionalen **-CleanUpDisks**-Flag:

```PowerShell
Remove-ClusterNode <Name> -CleanUpDisks
```

Die Ausführung dieses Cmdlet kann lange dauern (manchmal auch viele Stunden), da Windows alle auf dem Server gespeicherten Daten auf andere Servern im Cluster verschieben muss. Nachdem dieser Vorgang abgeschlossen ist, werden die Laufwerke dauerhaft aus dem Speicherpool entfernt und der fehlerfreie Zustand der betroffenen Volumes wiederhergestellt.

### <a name="requirements"></a>Voraussetzungen

Zum dauerhaften horizontalen Herunterskalieren (Entfernen eines Servers *und* der Laufwerke) muss der Cluster die folgenden zwei Kriterien erfüllen. Ist dies nicht der Fall, gibt das Cmdlet **Remove-ClusterNode -CleanUpDisks** sofort einen Fehler zurück, bevor die Datenverschiebung beginnt, um Störungen zu minimieren.

#### <a name="enough-capacity"></a>Ausreichend Kapazität

Zunächst müssen Sie über ausreichend Speicherkapazität für die verbleibenden Server verfügen, um alle Volumes aufnehmen zu können.

Wenn Sie beispielsweise vier Server mit jeweils zehn 1-TB-Laufwerken besitzen, haben Sie insgesamt 40 TB physische Speicherkapazität. Nach dem Entfernen eines Servers und aller seiner Laufwerke sind 30 TB Kapazität übrig. Wenn der Speicherbedarf Ihrer Volumes zusammen mehr als 30 TB beträgt, passen sie nicht auf die verbleibenden Server, daher gibt das Cmdlet einen Fehler zurück, und es werden keine Daten verschoben.

#### <a name="enough-fault-domains"></a>Genügend Fehlerdomänen

Zweitens benötigen Sie genügend Fehlerdomänen (in der Regel Server), um die Resilizenz Ihrer Volumes bereitzustellen.

Wenn beispielsweise die Volumes Drei-Wege-Spiegelung auf Serverebene für Resilizenz verwenden, können sie nur fehlerfrei sein, wenn Sie mindestens drei Server besitzen. Wenn Sie genau drei Server haben und dann versuchen, einen Server and alle seine Laufwerke zu entfernen, gibt das Cmdlet einen Fehler zurück, und es werden keine Daten verschoben.

In der folgenden Tabelle wird die Mindestanzahl der Fehlerdomänen gezeigt, die für jeden Resilienztyp erforderlich ist.

|    Resilienz          |    Mindestens erforderliche Fehlerdomänen   |
|------------------------|-------------------------------------|
|    Zwei-Wege-Spiegelung      |    2                                |
|    Drei-Wege-Spiegelung    |    3                                |
|    Duale Parität         |    4                                |

   >[!NOTE]
   > Es ist in Ordnung, kurzzeitig weniger Server zu haben, z. B. bei Ausfällen oder Wartung. Damit die Volumes wieder zurück in einen vollständig fehlerfreien Status wechseln, müssen Sie jedoch die minimale Anzahl von Servern besitzen, die oben aufgeführt ist.

## <a name="see-also"></a>Siehe auch

- [Übersicht über direkte Speicherplätze](storage-spaces-direct-overview.md)
