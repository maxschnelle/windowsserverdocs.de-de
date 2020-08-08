---
title: Entfernen von Servern in direkte Speicherplätze
ms.assetid: 9d8499a7-1307-473d-9f00-8a051164fad2
ms.author: cosdar
manager: eldenc
ms.topic: article
author: cosmosdarwin
description: Entfernen von Servern aus einem direkte Speicherplätze-Cluster in Windows Server.
ms.date: 2/5/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc6ca368be71b24b8a552051c6edc2b7220dd57b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971067"
---
# <a name="removing-servers-in-storage-spaces-direct"></a>Entfernen von Servern in direkte Speicherplätze

>Gilt für: Windows Server 2019, Windows Server 2016

In diesem Thema wird beschrieben, wie Sie Server in [direkte Speicherplätze](storage-spaces-direct-overview.md) mithilfe von PowerShell entfernen.

## <a name="remove-a-server-but-leave-its-drives"></a>Entfernen eines Servers, belassen der Laufwerke

Wenn Sie den Server in Kürze wieder dem Cluster hinzufügen möchten, oder wenn Sie beabsichtigen, seine Laufwerke beizubehalten, indem Sie Sie auf einen anderen Server verschieben, können Sie den Server aus dem Cluster entfernen, *ohne* seine Laufwerke aus dem Speicherpool zu entfernen. Dies ist das Standardverhalten, wenn Sie Failovercluster-Manager verwenden, um den Server zu entfernen.

Verwenden Sie das [Remove-clusternode-](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831694(v=ws.11)) Cmdlet in PowerShell:

```PowerShell
Remove-ClusterNode <Name>
```

Dieses Cmdlet ist unabhängig von den Kapazitäts Überlegungen schnell erfolgreich, da der Speicherpool die fehlenden Laufwerke "speichert" und davon ausgeht, dass Sie zurückkehren. Es gibt keine Daten Verschiebung von den fehlenden Laufwerken. Obwohl Sie weiterhin fehlen, wird Ihr **OperationalStatus** als "verlorene Kommunikation" angezeigt, und auf Ihren Volumes wird "unvollständig" angezeigt.

Wenn die Laufwerke wieder zurückgegeben werden, werden Sie automatisch erkannt und erneut dem Pool zugeordnet, auch wenn Sie sich jetzt auf einem neuen Server befinden.

   >[!WARNING]
   > Verteilen Sie keine Laufwerke mit Pooldaten von einem Server auf mehrere andere Server. Wenn z. b. ein Server mit zehn Laufwerken ausfällt (weil z. b. die Platine oder das Start Laufwerk fehlgeschlagen ist), **können** Sie alle zehn Laufwerke auf einen neuen Server verschieben, aber Sie können Sie **nicht** einzeln auf andere Server verschieben.

## <a name="remove-a-server-and-its-drives"></a>Entfernen eines Servers und seiner Laufwerke

Wenn Sie einen Server dauerhaft aus dem Cluster entfernen möchten (manchmal auch als "Skalierung" bezeichnet), können Sie den Server aus dem Cluster entfernen *und* seine Laufwerke aus dem Speicherpool entfernen.

Verwenden Sie das **Remove-clusternode** -Cmdlet mit dem optionalen **-cleanupdisks-** Flag:

```PowerShell
Remove-ClusterNode <Name> -CleanUpDisks
```

Das Ausführen dieses Cmdlets kann einige Zeit in Anspruch nehmen, da Windows alle auf diesem Server gespeicherten Daten auf andere Server im Cluster verschieben muss. Nach Abschluss dieses Vorgangs werden die Laufwerke dauerhaft aus dem Speicherpool entfernt, und die betroffenen Volumes werden wieder in einen fehlerfreien Zustand versetzt.

### <a name="requirements"></a>Anforderungen

Zum permanenten horizontalen Herunterskalieren (Entfernen eines Servers *und* seiner Laufwerke) muss Ihr Cluster die folgenden beiden Anforderungen erfüllen. Wenn dies nicht der Fall ist, wird vom Cmdlet " **Remove-clusternode-cleanupdisks** " sofort ein Fehler zurückgegeben, bevor eine Daten Verschiebung begonnen wird, um die Unterbrechung zu minimieren.

#### <a name="enough-capacity"></a>Genügend Kapazität

Zunächst müssen Sie über ausreichend Speicherkapazität für die verbleibenden Server verfügen, um alle Volumes aufnehmen zu können.

Wenn Sie z. b. über vier Server mit jeweils 10 x 1 TB-Laufwerken verfügen, verfügen Sie über 40 TB gesamte physische Speicherkapazität. Nach dem Entfernen eines Servers und aller zugehörigen Laufwerke haben Sie noch 30 TB Kapazität. Wenn die Spuren Ihrer Volumes mehr als 30 TB gleich sind, werden Sie nicht in die restlichen Server integriert, sodass das Cmdlet einen Fehler zurückgibt und keine Daten verschiebt.

#### <a name="enough-fault-domains"></a>Genügend Fehler Domänen

Zweitens müssen Sie über genügend Fehler Domänen (in der Regel Server) verfügen, um die Resilienz Ihrer Volumes zu gewährleisten.

Wenn Ihre Volumes z. b. die drei-Wege-Spiegelung auf Serverebene für Resilienz verwenden, können Sie nur dann voll funktionsfähig sein, wenn Sie über mindestens drei Server verfügen. Wenn Sie genau drei Server haben und dann versuchen, eine und alle zugehörigen Laufwerke zu entfernen, gibt das Cmdlet einen Fehler zurück und verschiebt keine Daten.

Diese Tabelle zeigt die Mindestanzahl von Fehler Domänen, die für jeden resilienztyp erforderlich sind.

|    Resilienz          |    Mindestens erforderliche Fehlerdomänen   |
|------------------------|-------------------------------------|
|    Zwei-Wege-Spiegelung      |    2                                |
|    Drei-Wege-Spiegelung    |    3                                |
|    Duale Parität         |    4                                |

   >[!NOTE]
   > Es ist in Ordnung, kurz weniger Server zu haben, z. b. bei Fehlern oder Wartungs Tasks. Damit Volumes in einen vollständig fehlerfreien Status zurückversetzt werden können, müssen Sie jedoch über die Mindestanzahl der oben aufgeführten Server verfügen.

## <a name="additional-references"></a>Weitere Verweise

- [Direkte Speicherplätze – Übersicht](storage-spaces-direct-overview.md)
