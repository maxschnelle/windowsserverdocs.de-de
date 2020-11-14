---
title: SDN-Datenpfad-diagnoseerweiterung im Windows Admin Center
description: Verwenden Sie dieses Thema, um Paket Erfassungs basierte Paket Erfassungen mit der Sdn-Datenpfad-Diagnose Erweiterung im Windows Admin Center zu automatisieren.
ms.topic: how-to
author: khdownie
ms.author: v-kedow
ms.date: 11/12/2020
ms.openlocfilehash: 9b1a247e0d07a4e44ba7640aa2e95180956ccee8
ms.sourcegitcommit: 8808f871c8cf131f819ef5540286218bd425da96
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/14/2020
ms.locfileid: "94632519"
---
# <a name="sdn-data-path-diagnostics-extension-in-windows-admin-center"></a>SDN-Datenpfad-diagnoseerweiterung im Windows Admin Center

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows 10, Azure Stack HCI, Azure Stack Hub, Azure

Die Sdn-Daten Pfad Diagnose ist ein Tool innerhalb der Sdn-Überwachungs Erweiterung von Windows Admin Center, das Paket Erfassungs basierte Paket Erfassungen gemäß verschiedenen Sdn-Szenarios automatisiert und die Ausgabe in einer einzelnen Ansicht anzeigt, die einfach zu befolgen und zu bearbeiten ist.

## <a name="what-is-packet-monitor-pktmon"></a>Was ist Paket Monitor (pktmon)?
Der Paket Monitor (pktmon) ist ein Komponenten übergreifendes Netzwerk Diagnosetool für Windows. Sie kann zum Erfassen von Paketen, zum Löschen von Paketen, zum Filtern von Paketen und zum zählen verwendet werden. Das Tool ist besonders bei Virtualisierungsszenarien hilfreich, z. b. bei Container Netzwerken und Sdn, da es im Netzwerk Stapel sichtbar ist.

## <a name="what-is-windows-admin-center"></a>Was ist Windows Admin Center?
Windows Admin Center ist ein lokal bereitgestelltes, browserbasiertes Verwaltungs Tool, mit dem Sie Ihre Windows-Server ohne Azure-oder cloudabhängigkeit verwalten können. Windows Admin Center ermöglicht die vollständige Kontrolle über alle Aspekte der Serverinfrastruktur und ist besonders nützlich für die Verwaltung von Servern in privaten Netzwerken, die nicht mit dem Internet verbunden sind. Windows Admin Center ist die moderne Weiterentwicklung von integrierten Verwaltungstools wie Server-Manager und MMC.

## <a name="before-you-start"></a>Vor der Installation
- Um das Tool verwenden zu können, muss auf dem Zielserver Windows Server 2019 Version 1903 (19h1) und höher ausgeführt werden.
- [Installieren Sie das Windows Admin Center](/windows-server/manage/windows-admin-center/deploy/install).
- Hinzufügen eines Clusters zum Windows Admin Center:
  1. Klicken Sie unter **Alle Verbindungen** auf **+ Hinzufügen**.
  2. Wählen Sie das Hinzufügen einer Hyper-Converged Cluster Verbindung aus.
  3. Geben Sie den Namen des Clusters und, falls Sie dazu aufgefordert werden, die zu verwendenden Anmelde Informationen ein.
  4. Aktivieren Sie **Konfigurieren des Netzwerk Controllers** , um fortzufahren.
  5. Geben Sie den Netzwerk Controller-URI ein, und klicken Sie auf **Validate**
  6. Klicken Sie zum Beenden auf **Hinzufügen** .

Der Cluster wird der Verbindungsliste hinzugefügt. Klicken Sie darauf, um das Dashboard zu starten.

<center>

:::image type="content" source="media/add-sdn-enabled-hci-connection.png" alt-text="Hinzufügen einer Sdn-aktivierten HCI-Verbindung mit dem Windows Admin Center" border="true":::

</center>

## <a name="getting-started"></a>Erste Schritte

Um zum Tool zu gelangen, navigieren Sie zu dem Cluster, den Sie im vorherigen Schritt erstellt haben, und dann zur Erweiterung "Sdn-Überwachung" und dann zur Registerkarte "Daten Pfad Diagnose".

## <a name="selecting-scenarios"></a>Auswählen von Szenarien

Auf der ersten Seite werden alle Sdn-Szenarien aufgelistet, die als Arbeits Auslastungs Szenarien und Infrastruktur Szenarios klassifiziert sind, wie in der folgenden Abbildung dargestellt Wählen Sie zunächst das Sdn-Szenario aus, das diagnostiziert werden muss.

<center>

:::image type="content" source="media/sdn-data-path-diagnostics-main-page.png" alt-text="SDN-Überwachung: Seite &quot;Diagnose Szenarios&quot;" border="true":::

</center>

## <a name="scenario-parameters"></a>Szenarioparameter

Nachdem Sie das Szenario ausgewählt haben, füllen Sie eine Liste der obligatorischen und optionalen Parameter zum Starten der Erfassung aus. Diese grundlegenden Parameter zeigen das Tool auf die Verbindung, die diagnostiziert werden muss. Das Tool verwendet diese Parameter dann für Abfragen, um eine erfolgreiche Erfassung auszuführen, ohne dass ein Eingreifen des Benutzers erforderlich ist, um den erwarteten Paketfluss, die an dem Szenario beteiligten Computer, ihren Speicherort im Cluster oder die auf den einzelnen Computern anzuwendenden Erfassungs Filter zu ermitteln. Mit den obligatorischen Parametern kann die Erfassung ausgeführt werden, und die optionalen Parameter helfen dabei, ein gewisses Rauschen zu filtern.

<center>

:::image type="content" source="media/sdn-data-path-diagnostics-scenario-parameters.png" alt-text="SDN-Überwachung-Seite &quot;Erfassungs Bedingungen&quot;" border="true":::

</center>

## <a name="capture-log"></a>Aufzeichnungs Protokoll

Nach dem Start der Erfassung wird in der Erweiterung eine Liste der Computer angezeigt, auf denen die Erfassung gestartet wird. Wenn Ihre Anmelde Informationen nicht gespeichert wurden, werden Sie möglicherweise aufgefordert, sich bei diesen Computern anzumelden. Sie können den Ping oder das Problem, das Sie diagnostizieren möchten, mit der Reproduktion der relativen Pakete beginnen. Nachdem die Pakete aufgezeichnet wurden, werden in der Erweiterung Markierungen neben den Computern angezeigt, auf denen die Pakete aufgezeichnet wurden.

<center>

:::image type="content" source="media/sdn-data-path-diagnostics-loading-wheel2.png" alt-text="Starten der Paket Erfassung" border="true":::

</center>

Nachdem Sie die Erfassung beendet haben, werden die Protokolle aller Computer auf einer einzelnen Seite angezeigt, dividiert durch den Titel des Computers. Jeder Titel enthält den Computernamen, seine Rolle im Szenario und seinen Host im Fall von virtuellen Computern (Virtual Machines, VMS).

<center>

:::image type="content" source="media/sdn-data-path-diagnostics-log.png" alt-text="Datenpfad-Diagnoseprotokoll nach dem Beenden der Erfassung" border="true":::

</center>

Die Ergebnisse werden in einer Tabelle angezeigt, in der die Hauptparameter der erfassten Pakete angezeigt werden: Timestamp, Quellen-IP-Adresse, Quellport, Ziel-IP-Adresse, Zielport, etherstyp, Protokoll, TCP-Flags, ob das Paket gelöscht wurde, und Ablage Grund.

   - Der Zeitstempel für die einzelnen Pakete ist auch ein Hyperlink, mit dem Sie zu einer anderen Seite umgeleitet werden, auf der Sie weitere Informationen zum ausgewählten Paket finden können. Weitere Informationen finden Sie weiter unten im Abschnitt "Details".
   - Alle gelöschten Pakete haben einen "true"-Wert **auf der Register** Karte "verworfen", einen Ablage Grund, der in rotem Text angezeigt wird, um die Identifizierung zu vereinfachen.
   - Alle Registerkarten können aufsteigend und absteigend sortiert werden.
   - Sie können in einer beliebigen Spalte im Protokoll mithilfe der Suchleiste nach einem Wert suchen.
   - Mithilfe der Schaltfläche **neu starten** können Sie die Erfassung mit denselben ausgewählten Filtern neu starten.

## <a name="details-page"></a>Detailseite

Die Informationen auf dieser Seite sind besonders wertvoll, wenn Sie falsche Probleme bei der Paket Weitergabe oder Fehlkonfigurationen haben, da Sie den Fluss des Pakets durch jede Komponente des Netzwerk Stapels untersuchen können. Für jeden pakethop sind Details vorhanden, die die Paket Parameter sowie die unformatierten Paket Details enthalten.

- Die Hops werden basierend auf den beteiligten Komponenten gruppiert. Jeder Adapter und die darauf darauf enden Treiber werden nach dem Namen des Adapters gruppiert. Dadurch wird das Paket auf einer hohen Ebene durch diese Gruppentitel leichter nachverfolgt.
- Alle gelöschten Pakete werden auch in rotem Text angezeigt, damit Sie leichter zu identifizieren sind.

<center>

:::image type="content" source="media/sdn-data-path-diagnostics-details-page.png" alt-text="Seite &quot;Details zur Daten Pfad Diagnose&quot;" border="true":::

</center>

Wählen Sie einen Hop aus, um weitere Details anzuzeigen. In Kapselungs-und NAT-Szenarios (Netzwerk Adressübersetzung) können Sie mit dieser Funktion sehen, wie sich das Paket ändert, wenn es den Netzwerk Stapel durchläuft, und auf fehlerhafte Konfigurationsprobleme überprüfen.

<center>

:::image type="content" source="media/sdn-data-path-diagnostics-details-page-with-pane1.png" alt-text="Anzeigen von Details zu einem bestimmten Hop" border="true":::

</center>

Scrollen Sie nach unten, um die unformatierten Paket Details

<center>

:::image type="content" source="media/sdn-data-path-diagnostics-details-page-with-pane-raw-packet1.png" alt-text="Anzeigen von rohpaket Details zu einem bestimmten Hop" border="true":::

</center>

## <a name="display-filters"></a>Anzeige Filter

Die Anzeige Filter ermöglichen es Ihnen, das Protokoll nach dem Erfassen der Pakete zu filtern. Für jeden Filter können Sie Paket Parameter wie Mac-Adressen, IP-Adressen, Ports, EtherType und Transport Protokoll angeben.

   - Anzeige Filter können zwischen Quelle und Ziel von IP-Adressen, Mac-Adressen und Ports unterscheiden.
   - Anzeige Filter können gelöscht und bearbeitet werden, nachdem Sie angewendet wurden, um die Ansicht des Protokolls zu ändern.
   - Anzeige Filter werden in den gespeicherten Protokollen umgekehrt.

<center>

:::image type="content" source="media/sdn-data-path-diagnostics-display-filters.png" alt-text="Filtern von Protokollen mit Anzeige Filtern" border="true":::

</center>

## <a name="save"></a>Speichern

Mithilfe der Schaltfläche speichern können Sie das Protokoll auf dem lokalen Computer speichern, um Sie über andere Tools zu analysieren. Anzeige Filter werden im gespeicherten Protokoll umgekehrt. Protokolle können in verschiedenen Formaten gespeichert werden:

   - ETL-Format, das mit Microsoft-Netzwerkmonitor analysiert werden kann. Hinweis: auf [dieser Seite finden Sie](pktmon-netmon-support.md) Weitere Informationen.
   - Textformat, das mit einem beliebigen Text-Editor wie TextAnalysisTool.net analysiert werden kann.
   - Pcapng Fomat, das mithilfe von Tools wie wireshark analysiert werden kann.
      - Die meisten Paket Monitor Metadaten gehen während der Konvertierung verloren. Hinweis: auf [dieser Seite finden Sie](pktmon-pcapng-support.md) Weitere Informationen.

<center>

:::image type="content" source="media/sdn-data-path-diagnostics-save.png" alt-text="Lokales Speichern von Protokollen" border="true":::

</center>
