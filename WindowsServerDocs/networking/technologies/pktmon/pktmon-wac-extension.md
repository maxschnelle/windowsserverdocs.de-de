---
title: Paket Überwachungs Erweiterung im Windows Admin Center
description: Verwenden Sie diese Seite, um den Paket Monitor (pktmon) über das Windows Admin Center zu betreiben und zu nutzen.
ms.topic: how-to
author: khdownie
ms.author: v-kedow
ms.date: 11/12/2020
ms.openlocfilehash: 85d204d1731ebcf21c55364f48ebe0e7b6dc157c
ms.sourcegitcommit: 8808f871c8cf131f819ef5540286218bd425da96
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/14/2020
ms.locfileid: "94632524"
---
# <a name="packet-monitoring-extension-in-windows-admin-center"></a>Paket Überwachungs Erweiterung im Windows Admin Center

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows 10, Azure Stack HCI, Azure Stack Hub, Azure

Die Paket Überwachungs Erweiterung ermöglicht es Ihnen, den Paket Monitor über das Windows Admin Center zu betreiben und zu nutzen. Die Erweiterung unterstützt Sie bei der Diagnose Ihres Netzwerks durch erfassen und Anzeigen von Netzwerk Datenverkehr über den Netzwerk Stapel in einem Protokoll, das leicht zu befolgen und zu bearbeiten ist.

## <a name="what-is-packet-monitor-pktmon"></a>Was ist Paket Monitor (pktmon)?
Der Paket Monitor (pktmon) ist ein Komponenten übergreifendes Netzwerk Diagnosetool für Windows. Sie kann für die Paket Erfassung, die Paket Ablage Erkennung, das Filtern und zählen von Paketen verwendet werden. Das Tool ist besonders bei Virtualisierungsszenarien hilfreich, z. b. bei Container Netzwerken und Sdn, da es im Netzwerk Stapel sichtbar ist.

## <a name="what-is-windows-admin-center"></a>Was ist Windows Admin Center?
Windows Admin Center ist ein lokal bereitgestelltes, browserbasiertes Verwaltungs Tool, mit dem Sie Ihre Windows-Server ohne Azure-oder cloudabhängigkeit verwalten können. Windows Admin Center ermöglicht die vollständige Kontrolle über alle Aspekte der Serverinfrastruktur und ist besonders nützlich für die Verwaltung von Servern in privaten Netzwerken, die nicht mit dem Internet verbunden sind. Windows Admin Center ist die moderne Weiterentwicklung von integrierten Verwaltungstools wie Server-Manager und MMC.

## <a name="before-you-start"></a>Vor der Installation
- Um das Tool verwenden zu können, muss auf dem Zielserver Windows Server 2019 Version 1903 (19h1) und höher ausgeführt werden.
- [Installieren Sie das Windows Admin Center](/windows-server/manage/windows-admin-center/deploy/install).
- Hinzufügen eines Servers zum Windows Admin Center:
  1. Klicken Sie unter **Alle Verbindungen** auf **+ Hinzufügen**.
  2. Wählen Sie die Option zum Hinzufügen einer Server Verbindung aus.
  3. Geben Sie den Namen des Servers und, wenn Sie dazu aufgefordert werden, die zu verwendenden Anmelde Informationen ein.
  4. Klicken Sie zum fertig **Stellen auf Senden** .

Der Server wird auf der **Übersichts** Seite zur Verbindungsliste hinzugefügt.

## <a name="getting-started"></a>Erste Schritte

Um zum Tool zu gelangen, navigieren Sie zu dem Server, den Sie im vorherigen Schritt erstellt haben, und klicken Sie dann auf die Erweiterung "Paket Überwachung".

## <a name="applying-filters"></a>Anwenden von Filtern

Es wird dringend empfohlen, vor dem Starten einer Paket Erfassung Filter anzuwenden, da die Problembehandlung bei der Verbindung mit einem bestimmten Ziel einfacher ist, wenn Sie sich auf einen einzelnen Stream von Paketen konzentrieren. Andererseits kann das Erfassen des gesamten Netzwerk Datenverkehrs dazu führen, dass die Ausgabe zu stark ist, um analysiert zu werden. Entsprechend führt die Erweiterung Sie vor dem Start der Erfassung durch den Filterbereich. Sie können diesen Schritt überspringen, indem Sie auf **weiter** klicken, um die Erfassung ohne Filter zu starten Der Bereich "Filter" führt Sie durch das Hinzufügen von Filtern in drei Schritten.

1. Filtern nach Netzwerk Stapel Komponenten

   Wenn Sie Datenverkehr erfassen möchten, der nur bestimmte Komponenten durchläuft, wird im ersten Schritt des Filter Bereichs das Netzwerk Stapel Layout angezeigt, sodass Sie die Komponenten auswählen können, nach denen gefiltert werden soll. Dies ist auch ein guter Ausgangspunkt, um das Layout des Netzwerk Stapels Ihres Computers zu analysieren und zu verstehen.

   :::image type="content" source="media/filtering-by-networking-stack-components.png" alt-text="Beispiel für das Filtern nach Netzwerk Stapel Komponenten" border="true":::

2. Filtern nach Paket Parametern

   Im zweiten Schritt ermöglicht der Bereich das Filtern von Paketen nach ihren Parametern. Damit ein Paket gemeldet wird, muss es mit allen in mindestens einem Filter angegebenen Bedingungen identisch sein. bis zu 8 Filter werden gleichzeitig unterstützt. Für jeden Filter können Sie Paket Parameter angeben, z. b. Mac-Adressen, IP-Adressen, Ports, etheryp, Transport Protokoll, VLAN-ID.

   - Wenn zwei Macs, IPS oder Ports angegeben werden, unterscheidet das Tool nicht zwischen Quelle und Ziel. Es werden Pakete erfasst, die beide Werte enthalten, ob als Ziel oder Quelle. Allerdings können Anzeige Filter diesen Unterschied ausmachen. Weitere Informationen finden Sie unten im Abschnitt [Anzeigen von Filtern](#display-filters) .
   - Zum weiteren Filtern von TCP-Paketen kann eine optionale Liste von TCP-Flags bereitgestellt werden. Unterstützte Flags sind FIN, SYN, RST, PSH, ACK, URG, ECE und CWR.
   - Wenn das Feld **Kapselung** aktiviert ist, wendet das Tool den Filter zusätzlich zum äußeren Paket auf gekapselte innere Pakete an. Unterstützte Kapselungs Methoden sind vxlan, GRE, nvgre und IP-in-IP. Der benutzerdefinierte vxlan-Port ist optional, und der Standardwert ist 4789.

   :::image type="content" source="media/filtering-by-packet-parameters.png" alt-text="Beispiel für das Filtern nach Paket Parametern" border="true":::

3. Filtern nach Paketfluss Status

   Der Paket Monitor erfasst standardmäßig eingehende und gelöschte Pakete. Um nur gelöschte Pakete zu erfassen, wählen Sie **verworfene Pakete** aus.

   :::image type="content" source="media/filtering-by-packet-flow-status.png" alt-text="Beispiel für das Filtern nach dem Paketfluss Status" border="true":::

   Anschließend wird eine Zusammenfassung aller ausgewählten Filterbedingungen für die Überprüfung angezeigt. Sie können diese Ansicht abrufen, nachdem Sie die Erfassung über die Schaltfläche **Erfassungs Bedingungen** gestartet haben.

   :::image type="content" source="media/filters-review.png" alt-text="Erfassen von nur gelöschten Paketen" border="true":::

## <a name="capture-log"></a>Aufzeichnungs Protokoll

Die Ergebnisse werden in einer Tabelle angezeigt, in der die Hauptparameter der erfassten Pakete angezeigt werden: Timestamp, Quellen-IP-Adresse, Quellport, Ziel-IP-Adresse, Zielport, etherstyp, Protokoll, TCP-Flags, ob das Paket gelöscht wurde, und Ablage Grund.

   - Der Zeitstempel für die einzelnen Pakete ist auch ein Hyperlink, mit dem Sie zu einer anderen Seite umgeleitet werden, auf der Sie weitere Informationen zum ausgewählten Paket finden können. Weitere Informationen finden Sie weiter unten im Abschnitt "Details".
   - Alle gelöschten Pakete haben einen "true"-Wert **auf der Register** Karte "verworfen", einen Ablage Grund, der in rotem Text angezeigt wird, um die Identifizierung zu vereinfachen.
   - Alle Registerkarten können aufsteigend und absteigend sortiert werden.
   - Sie können in einer beliebigen Spalte im Protokoll mithilfe der Suchleiste nach einem Wert suchen.
   - Mithilfe der Schaltfläche **neu starten** können Sie die Erfassung mit denselben ausgewählten Filtern neu starten.

   :::image type="content" source="media/capture-log-result.png" alt-text="Beispiel Tabelle für Aufzeichnungs Protokoll Ergebnisse" border="true":::

## <a name="details-page"></a>Detailseite

Diese Seite zeigt eine Momentaufnahme des Pakets an, während es von jeder Komponente des lokalen Netzwerk Stapels fließt. In dieser Ansicht wird der Paketfluss Pfad angezeigt, und Sie können untersuchen, wie sich die Pakete ändern, wenn Sie von den einzelnen Komponenten verarbeitet werden, die von Ihnen übergeben werden.

   - Die Paket Momentaufnahmen werden nach den einzelnen Adaptern/switchstapeln gruppiert. die Paket Momentaufnahmen, die von einem Adapter/Switch, den Filter Treibern und den zugehörigen Protokolltreibern aufgezeichnet werden, werden also unter dem Namen des Adapters/Schalters gruppiert. Dadurch wird es einfacher, den Paket Ablauf von einem Adapter zum anderen zu befolgen.
   - Wenn eine Momentaufnahme ausgewählt wird, werden weitere Details zu dieser bestimmten Momentaufnahme angezeigt, einschließlich der unformatierten Paket Header.
   - Alle gelöschten Pakete haben einen "true"-Wert **auf der Register** Karte "verworfen", einen Ablage Grund, der in rotem Text angezeigt wird, um die Identifizierung zu vereinfachen.

   :::image type="content" source="media/details-page.png" alt-text="Beispiel für eine Detailseite mit Paket Momentaufnahmen" border="true":::

## <a name="display-filters"></a>Anzeige Filter

Die Anzeige Filter ermöglichen es Ihnen, Ihr Protokoll nach dem Erfassen der Pakete zu filtern. Für jeden Filter können Sie Paket Parameter wie Mac-Adressen, IP-Adressen, Ports, EtherType und Transport Protokoll angeben. Im Gegensatz zu Erfassungs filtern:

   - Anzeige Filter können zwischen Quelle und Ziel von IP-Adressen, Mac-Adressen und Ports unterscheiden.
   - Anzeige Filter können gelöscht und bearbeitet werden, nachdem Sie angewendet wurden, um die Ansicht des Protokolls zu ändern.
   - Anzeige Filter werden in den gespeicherten Protokollen umgekehrt.

   :::image type="content" source="media/display-filters.png" alt-text="Anzeige Filter-Bildschirm" border="true":::

## <a name="save-feature"></a>Funktion Speichern

Mithilfe der Schaltfläche speichern können Sie das Protokoll auf dem lokalen Computer, auf dem Remote Computer oder in beiden speichern. Anzeige Filter werden im gespeicherten Protokoll umgekehrt.

   - Wenn das Protokoll auf dem lokalen Computer gespeichert wird, können Sie es in verschiedenen Formaten speichern:
      - ETL-Format, das mit Microsoft-Netzwerkmonitor analysiert werden kann. Hinweis: auf dieser Seite finden Sie weitere Informationen.
      - Textformat, das mit einem beliebigen Text-Editor wie TextAnalysisTool.net analysiert werden kann.
      - Pcapng Fomat, das mithilfe von Tools wie wireshark analysiert werden kann.
         - Die meisten Paket Monitor Metadaten gehen während der Konvertierung verloren. Auf [dieser Seite finden Sie](pktmon-pcapng-support.md) Weitere Informationen.

   :::image type="content" source="media/packet-monitoring-save-feature.png" alt-text="Speichern einer lokalen Kopie der Erfassung" border="true":::

## <a name="open-feature"></a>Feature öffnen

Mit dem Feature "Öffnen" können Sie alle fünf zuletzt gespeicherten Protokolle erneut öffnen, um Sie über das Tool zu analysieren.

   :::image type="content" source="media/open.png" alt-text="Öffnen eines aktuellen Protokolls" border="true":::