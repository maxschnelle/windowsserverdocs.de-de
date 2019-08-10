---
title: DNS-Client seitiges Zwischenspeichern auf DNS-Clients deaktivieren
description: In diesem Artikel wird beschrieben, wie Sie das Client seitige DNS-Zwischenspeichern auf DNS-Clients deaktivieren.
manager: willchen
ms.prod: ''
ms.technology: networking-dns
ms.topic: article
ms.author: delhan
ms.date: 8/8/2019
author: Deland-Han
ms.openlocfilehash: 0b20400029b462798587c2291431b5a7c3d61775
ms.sourcegitcommit: 0e3c2473a54f915d35687d30d1b4b1ac2bae4068
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68917807"
---
# <a name="disable-dns-client-side-caching-on-dns-clients"></a>DNS-Client seitiges Zwischenspeichern auf DNS-Clients deaktivieren

Windows enthält einen Client seitigen DNS-Cache. Das Client seitige DNS-Cache-Feature generiert möglicherweise einen falschen Eindruck, dass der DNS-Lastenausgleich "Roundrobin" nicht vom DNS-Server zum Windows-Client Computer stattfindet. Wenn Sie den Ping-Befehl verwenden, um nach demselben A-Datensatz-Domänen Namen zu suchen, verwendet der Client möglicherweise dieselbe IP-Adresse.  

## <a name="how-to-disable-client-side-caching"></a>Deaktivieren der Client seitigen Zwischenspeicherung

Führen Sie einen der folgenden Befehle aus, um die DNS-Zwischenspeicherung zu verhindern:

```cmd
net stop dnscache
```

```cmd
sc servername stop dnscache
```


Um den DNS-Cache dauerhaft in Windows zu deaktivieren, verwenden Sie das Service Controller-Tool oder das Tool Dienste, um den Starttyp des DNS-Client Diensts auf **deaktiviert**festzulegen. Beachten Sie, dass der Name des Windows DNS-Client diensdienstanens auch als "dnscache" angezeigt wird. 

> [!NOTE]
> Wenn der DNS-resolvercache deaktiviert ist, wird die Gesamtleistung des Client Computers verringert, und der Netzwerk Datenverkehr für DNS-Abfragen wird erhöht. 

Der DNS-Client Dienst optimiert die Leistung der DNS-Namensauflösung, indem zuvor aufgelöste Namen im Arbeitsspeicher gespeichert werden. Wenn der DNS-Client Dienst ausgeschaltet ist, kann der Computer weiterhin DNS-Namen mithilfe der DNS-Server des Netzwerks auflösen. 

Wenn der Windows-Konflikt Löser eine Antwort (positiv oder negativ) an eine Abfrage empfängt, wird diese Antwort dem Cache hinzugefügt und ein DNS-Ressourcen Daten Satz erstellt. Der Konflikt Löser überprüft den Cache immer, bevor er einen DNS-Server abfragt. Wenn sich ein DNS-Ressourcen Daten Satz im Cache befindet, verwendet der Konflikt Löser den Datensatz aus dem Cache, anstatt einen Server abzufragen. Dieses Verhalten beschleunigt Abfragen und reduziert den Netzwerk Datenverkehr für DNS-Abfragen. 

Sie können das Tool ipconfig verwenden, um den DNS-Konflikt Löser-Cache anzuzeigen und zu leeren. Um den DNS-Konflikt Löser-Cache anzuzeigen, führen Sie den folgenden Befehl an einer Eingabeaufforderung aus:

```cmd
ipconfig /displaydns 
```

Mit diesem Befehl wird der Inhalt des DNS-resolvercaches angezeigt, einschließlich der DNS-Ressourcen Einträge, die aus der Hostdatei vorab geladen werden, und aller vor kurzem abgefragten Namen, die vom System aufgelöst wurden. Nach einiger Zeit verwirft der Konflikt Löser den Datensatz aus dem Cache. Der Zeitraum wird durch den Wert für die Gültigkeitsdauer **(Time to Live, TTL)** angegeben, der dem DNS-Ressourcen Daten Satz zugeordnet ist. Sie können den Cache auch manuell leeren. Nachdem Sie den Cache geleert haben, muss der Computer die DNS-Server erneut für alle DNS-Ressourcen Einträge Abfragen, die zuvor vom Computer aufgelöst wurden. Führen `ipconfig /flushdns` Sie an einer Eingabeaufforderung aus, um die Einträge im DNS-Konflikt Löser-Cache zu löschen.

## <a name="next-step"></a>Nächster Schritt

Weitere Informationen finden [Sie unter Deaktivieren des Client seitigen DNS-Caches in Windows](https://support.microsoft.com/kb/318803) .
