---
title: DNS-Client seitiges Zwischenspeichern auf DNS-Clients deaktivieren
description: In diesem Artikel wird beschrieben, wie Sie das Client seitige DNS-Zwischenspeichern auf DNS-Clients deaktivieren.
manager: dcscontentpm
ms.technology: networking-dns
ms.topic: article
ms.author: delhan
ms.date: 8/8/2019
author: Deland-Han
ms.openlocfilehash: 09af41a544cacb0fd0977847b7bc2e6b0d8a59f7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860073"
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

Mit diesem Befehl wird der Inhalt des DNS-resolvercaches angezeigt, einschließlich der DNS-Ressourcen Einträge, die aus der Hostdatei vorab geladen werden, und aller vor kurzem abgefragten Namen, die vom System aufgelöst wurden. Nach einiger Zeit verwirft der Konflikt Löser den Datensatz aus dem Cache. Der Zeitraum wird durch den Wert für die Gültigkeitsdauer **(Time to Live, TTL)** angegeben, der dem DNS-Ressourcen Daten Satz zugeordnet ist. Sie können den Cache auch manuell leeren. Nachdem Sie den Cache geleert haben, muss der Computer die DNS-Server erneut für alle DNS-Ressourcen Einträge Abfragen, die zuvor vom Computer aufgelöst wurden. Führen Sie `ipconfig /flushdns` an einer Eingabeaufforderung aus, um die Einträge im DNS-Konflikt Löser-Cache zu löschen.

## <a name="using-the-registry-to-control-the-caching-time"></a>Steuern der zwischen Speicherungs Zeit mithilfe der Registrierung

> [!IMPORTANT]  
> Folgen Sie den Schritten in diesem Abschnitt sorgfältig. Wenn Ihnen beim Bearbeiten der Registrierung ein Fehler unterläuft, kann dies zu schwerwiegenden Problemen führen. Bevor Sie sie ändern, [sichern Sie die Registrierung zwecks Wiederherstellung](https://support.microsoft.com/help/322756) für den Fall, dass Probleme auftreten.

Die Zeitspanne, für die eine positive oder negative Antwort zwischengespeichert wird, hängt von den Werten der Einträge im folgenden Registrierungsschlüssel ab:

**HKEY_LOCAL_MACHINE \system\currentcontrolset\services\dnscache\parameters**

Die Gültigkeitsdauer für positive Antworten ist der kleinere der folgenden Werte: 

- Die Anzahl der Sekunden, die in der vom Konflikt Löser empfangenen Abfrage Antwort angegeben wurden.

- Der Wert der **maxcachettl** -Registrierungs Einstellung.

>[!Note]
>- Die Standard Gültigkeitsdauer für positive Antworten beträgt 86.400 Sekunden (1 Tag).
>- Die Gültigkeitsdauer für negative Antworten ist die Anzahl der Sekunden, die in der Registrierungs Einstellung maxnegativecachettl angegeben ist.
>- Die Standard Gültigkeitsdauer für negative Antworten beträgt 900 Sekunden (15 Minuten).
Wenn Sie nicht möchten, dass negative Antworten zwischengespeichert werden, legen Sie die maxnegativecachettl-Registrierungs Einstellung auf "0" fest.

So legen Sie die zwischen Speicherungs Zeit auf einem Client Computer fest:

1. Starten Sie den Registrierungs-Editor (regedit. exe).

2. Suchen Sie den folgenden Schlüssel in der Registrierung, und klicken Sie darauf:

   **HKEY_LOCAL_MACHINE \system\currentcontrolset\services\dnscache\parameters**

3. Zeigen Sie im Menü Bearbeiten auf neu, klicken Sie auf DWORD-Wert, und fügen Sie dann die folgenden Registrierungs Werte hinzu:

   - Wertname: maxcachettl

     Datentyp: REG_DWORD

     Wertdaten: Standardwert 86400 Sekunden. 
     
     Wenn Sie den maximalen TTL-Wert im DNS-Cache des Clients auf 1 Sekunde verringern, gibt dies die Darstellung an, dass der Client seitige DNS-Cache deaktiviert wurde.    

   - Wertname: maxnegativecachettl

     Datentyp: REG_DWORD

     Wertdaten: Standardwert 900 Sekunden. 
     
     Legen Sie den Wert auf 0 fest, wenn keine negativen Antworten zwischengespeichert werden sollen.

4. Geben Sie den Wert ein, den Sie verwenden möchten, und klicken Sie dann auf OK.

5. Beenden Sie den Registrierungs-Editor.