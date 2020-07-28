---
title: Failoverclustering-System Protokollereignisse
description: Eine Liste der Failoverclustering-Ereignisse im Windows Server-System Protokoll. Diese Ereignisse können verwendet werden, um Probleme mit einem Cluster zu beheben.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
manager: lizross
ms.technology: storage-failover-clustering
ms.date: 01/14/2020
ms.openlocfilehash: 5988842ef2a88687bca95781b996babb4e4f3faa
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181706"
---
# <a name="failover-clustering-system-log-events"></a>Failoverclustering-System Protokollereignisse

> Gilt für: Windows Server 2019, Windows Server 2016

In diesem Thema werden die Failoverclustering-Ereignisse aus dem Windows Server-System Protokoll (sichtbar in Ereignisanzeige) aufgelistet. Diese Ereignisse verwenden alle die Ereignis Quelle von **Failoverclustering** und können bei der Problembehandlung eines Clusters hilfreich sein.

## <a name="critical-events"></a>Kritische Ereignisse

### <a name="event-1000-unexpected_fatal_error"></a>Ereignis 1000: UNEXPECTED_FATAL_ERROR

Unerwarteter schwerwiegender Fehler in Zeile %1 des Quell Moduls %2. Clusterdienst Fehlercode: %3.

### <a name="event-1001-assertion_failure"></a>Ereignis 1001: ASSERTION_FAILURE

Fehler bei der Gültigkeits Überprüfung in Zeile "%1" des Quell Moduls "%2" Clusterdienst. "%3"

### <a name="event-1006-nm_event_membership_halt"></a>Ereignis 1006: NM_EVENT_MEMBERSHIP_HALT

Clusterdienst wurde aufgrund unvollständiger Konnektivität mit anderen Cluster Knoten angehalten.

### <a name="event-1057-dm_database_corrupt_or_missing"></a>Ereignis 1057: DM_DATABASE_CORRUPT_OR_MISSING

Die Cluster Datenbank konnte nicht geladen werden. Die Datei ist möglicherweise nicht vorhanden oder beschädigt.
Es kann versucht werden, eine automatische Reparatur auszuführen.

### <a name="event-1070-nm_event_begin_join_failed"></a>Ereignis 1070: NM_EVENT_BEGIN_JOIN_FAILED

Fehler beim Hinzufügen des Failoverclusters "%1" durch den Knoten aufgrund des Fehlercodes "%2".

### <a name="event-1073-cs_event_inconsistency_halt"></a>Ereignis 1073: CS_EVENT_INCONSISTENCY_HALT

Der Clusterdienst wurde angehalten, um eine Inkonsistenz innerhalb des Failoverclusters zu verhindern. Fehlercode: ' %1 '.

### <a name="event-1080-cs_diskwrite_failure"></a>Ereignis 1080: CS_DISKWRITE_FAILURE

Fehler beim Aktualisieren der Cluster Datenbank durch den Clusterdienst (Fehlercode "%1").
Mögliche Ursachen sind nicht genügend Speicherplatz oder eine Beschädigung des Dateisystems.

### <a name="event-1090-cs_event_reg_operation_failed"></a>Ereignis 1090: CS_EVENT_REG_OPERATION_FAILED

Der Clusterdienst kann nicht gestartet werden. Fehler beim Lesen von Konfigurationsdaten aus der Windows-Registrierung (Fehler: "%1"). Verwenden Sie das Failoverclusterverwaltungs-Snap-in, um sicherzustellen, dass dieser Computer Mitglied eines Clusters ist.
Wenn Sie diesen Computer einem vorhandenen Cluster hinzufügen möchten, verwenden Sie den Assistenten zum Hinzufügen von Knoten. Wenn dieser Computer als Mitglied eines Clusters konfiguriert wurde, ist es auch erforderlich, die fehlenden Konfigurationsdaten wiederherzustellen, die für den Cluster Dienst erforderlich sind, um festzustellen, dass er ein Mitglied eines Clusters ist.
Führen Sie eine System Status Wiederherstellung dieses Computers aus, um die Konfigurationsdaten wiederherzustellen.

### <a name="event-1092-nm_event_mm_form_failed"></a>Ereignis 1092: NM_EVENT_MM_FORM_FAILED

Fehler beim Erstellen des Clusters "%1" mit dem Fehlercode "%2". Der Failovercluster ist nicht verfügbar.

### <a name="event-1093-nm_event_node_not_member"></a>Ereignis 1093: NM_EVENT_NODE_NOT_MEMBER

Der Clusterdienst kann den Knoten "%1" nicht als Mitglied des Failoverclusters "%2" identifizieren. Wenn der Computername für diesen Knoten vor kurzem geändert wurde, sollten Sie den vorherigen Namen wiederherstellen. Alternativ dazu können Sie den Knoten dem Failovercluster hinzufügen und ggf. Cluster Anwendungen neu installieren.

### <a name="event-1105-cs_event_rpc_init_failed"></a>Ereignis 1105: CS_EVENT_RPC_INIT_FAILED

Der Clusterdienst konnte nicht gestartet werden, da die Schnittstelle (n) beim RPC-Dienst nicht registriert werden konnte. Fehlercode: ' %1 '.

### <a name="event-1135-event_node_down"></a>Ereignis 1135: EVENT_NODE_DOWN

Der Cluster Knoten "%1" wurde aus der aktiven failoverclustermitgliedschaft entfernt. Die Clusterdienst auf diesem Knoten wurde möglicherweise beendet. Dies kann auch darauf zurückzuführen sein, dass der Knoten die Kommunikation mit anderen aktiven Knoten im Failovercluster verloren hat.
Führen Sie den Konfigurationsüberprüfungs-Assistenten aus, um die Netzwerkkonfiguration zu überprüfen. Wenn die Bedingung weiterhin besteht, prüfen Sie, ob Hardware-oder Softwarefehler im Zusammenhang mit den Netzwerkadaptern auf diesem Knoten vorliegen. Überprüfen Sie auch, ob in anderen Netzwerkkomponenten, mit denen der Knoten verbunden ist, wie z. b. Hubs, Switches oder Bridges, auf Fehler.

### <a name="event-1146-rcm_event_resmon_died"></a>Ereignis 1146: RCM_EVENT_RESMON_DIED

Der RHS-Prozess (Cluster Ressourcenhosting-Subsystem) wurde beendet und wird neu gestartet. Dies ist in der Regel mit der Cluster Integritäts Erkennung und-Wiederherstellung einer Ressource verbunden. Bestimmen Sie anhand des System Ereignis Protokolls, welche Ressource und Ressourcen-DLL das Problem verursacht.

### <a name="event-1177-mm_event_arbitration_failed"></a>Ereignis 1177: MM_EVENT_ARBITRATION_FAILED

Der Clusterdienst wird heruntergefahren, weil das Quorum verloren gegangen ist. Dies kann auf den Verlust der Netzwerk Konnektivität zwischen einigen oder allen Knoten im Cluster oder einem Failover des Zeugen Datenträgers zurückzuführen sein.

Führen Sie den Konfigurationsüberprüfungs-Assistenten aus, um die Netzwerkkonfiguration zu überprüfen. Wenn die Bedingung weiterhin besteht, prüfen Sie, ob Hardware-oder Softwarefehler im Zusammenhang mit dem Netzwerkadapter vorliegen. Überprüfen Sie auch, ob in anderen Netzwerkkomponenten, mit denen der Knoten verbunden ist, wie z. b. Hubs, Switches oder Bridges, auf Fehler.

### <a name="event-1181-netres_resource_start_error"></a>Ereignis 1181: NETRES_RESOURCE_START_ERROR

Die Cluster Ressource "%1" kann nicht online geschaltet werden, da der zugehörige Dienst nicht gestartet werden konnte. Der Dienst Rückgabecode ist "%2". Überprüfen Sie, ob dem Dienst weitere Ereignisse zugeordnet sind, und stellen Sie sicher, dass der Dienst richtig gestartet wird

### <a name="event-1247-cluster_event_invalid_service_sid_type"></a>Ereignis 1247: CLUSTER_EVENT_INVALID_SERVICE_SID_TYPE

Der Typ der Sicherheits-ID (SID) für den Cluster Dienst ist als "%1" konfiguriert, aber der erwartete SID-Typ ist "uneingeschränkt". Der Cluster Dienst ändert seine sid-typkonfiguration automatisch mit dem Dienststeuerungs-Manager (Service Control Manager, SCM) und wird neu gestartet, damit diese Änderung wirksam wird.

### <a name="event-1248-cluster_event_service_sid_missing"></a>Ereignis 1248: CLUSTER_EVENT_SERVICE_SID_MISSING

Die mit dem Cluster Dienst verknüpfte Sicherheits-ID (SID) "%1" ist im Prozess Token nicht vorhanden. Der Cluster Dienst behebt dieses Problem automatisch und führt einen Neustart durch.

### <a name="event-1282-sm_event_handshake_timeout"></a>Ereignis 1282: SM_EVENT_HANDSHAKE_TIMEOUT

Der Sicherheits Hand Shake zwischen lokalen und Remote Endpunkten "%2" wurde in "%1" Sekunden nicht beendet, der Knoten beendet die Verbindung.

### <a name="event-1542-service_prerestore_failed"></a>Ereignis 1542: SERVICE_PRERESTORE_FAILED

Die Wiederherstellungs Anforderung für die Cluster Konfigurationsdaten ist fehlgeschlagen. Diese Wiederherstellung ist während der Phase "vor der Wiederherstellung" nicht erfolgreich, was normalerweise darauf hinweist, dass einige Knoten, die den Cluster enthalten, zurzeit Stellen Sie sicher, dass der Cluster Dienst auf allen Knoten, die diesen Cluster umfassen, erfolgreich ausgeführt wird.

### <a name="event-1543-service_postrestore_failed"></a>Ereignis 1543: SERVICE_POSTRESTORE_FAILED

Fehler beim Wiederherstellungs Vorgang der Cluster Konfigurationsdaten. Bei dieser Wiederherstellung ist während der Phase "nach der Wiederherstellung" ein Fehler aufgetreten Es wird empfohlen, dass Sie die aktuelle Cluster Konfigurationsdatendatei (CLUSDB) durch "%1" ersetzen.

### <a name="event-1546-service_form_version_incompatible"></a>Ereignis 1546: SERVICE_FORM_VERSION_INCOMPATIBLE

Der Knoten "%1" konnte keinen Failovercluster bilden. Dies liegt an einem oder mehreren Knoten, die inkompatible Versionen der Cluster Dienst Software ausführen. Wenn der Knoten "%1" oder ein anderer Knoten im Cluster vor kurzem aktualisiert wurde, überprüfen Sie, ob alle Knoten kompatible Versionen der Cluster Dienst Software ausführen.

### <a name="event-1547-service_connect_version_incompatible"></a>Ereignis 1547: SERVICE_CONNECT_VERSION_INCOMPATIBLE

Der Knoten "%1" hat versucht, einem Failovercluster beizutreten, konnte aber aufgrund von Inkompatibilität zwischen den Versionen der Cluster Dienst Software nicht ausgeführt werden. Wenn der Knoten "%1" oder ein anderer Knoten im Cluster vor kurzem aktualisiert wurde, überprüfen Sie, ob die geänderte Cluster Bereitstellung mit verschiedenen Versionen der Cluster Dienst Software unterstützt wird.

### <a name="event-1553-service_no_network_connectivity"></a>Ereignis 1553: SERVICE_NO_NETWORK_CONNECTIVITY

Dieser Cluster Knoten verfügt über keine Netzwerk Konnektivität. Sie kann erst am Cluster teilnehmen, wenn die Verbindung wieder hergestellt wird. Führen Sie den Konfigurationsüberprüfungs-Assistenten aus, um die Netzwerkkonfiguration zu überprüfen. Wenn die Bedingung weiterhin besteht, prüfen Sie, ob Hardware-oder Softwarefehler im Zusammenhang mit dem Netzwerkadapter vorliegen. Überprüfen Sie auch, ob in anderen Netzwerkkomponenten, mit denen der Knoten verbunden ist, wie z. b. Hubs, Switches oder Bridges, auf Fehler.

### <a name="event-1554-service_network_connectivity_lost"></a>Ereignis 1554: SERVICE_NETWORK_CONNECTIVITY_LOST

Dieser Cluster Knoten hat alle Netzwerkverbindungen verloren. Sie kann erst am Cluster teilnehmen, wenn die Verbindung wieder hergestellt wird. Der Cluster Dienst auf diesem Knoten wird beendet.

### <a name="event-1556-service_unhandled_exception_in_worker_thread"></a>Ereignis 1556: SERVICE_UNHANDLED_EXCEPTION_IN_WORKER_THREAD

Der Cluster Dienst hat ein unerwartetes Problem feststellen und wird heruntergefahren. Fehlercode: "%2".

### <a name="event-1561-service_nonstorage_witness_better_tag"></a>Ereignis 1561: SERVICE_NONSTORAGE_WITNESS_BETTER_TAG

Clusterdienst konnte nicht gestartet werden, da dieser Knoten festgestellt hat, dass er nicht über die neueste Kopie der Cluster Konfigurationsdaten verfügt. Die Änderungen am Cluster sind aufgetreten, während sich dieser Knoten nicht in der Mitgliedschaft befand und somit keine Konfigurationsdaten Aktualisierungen empfangen konnte.

#### <a name="guidance"></a>Leitfaden

Versuchen Sie, den Cluster Dienst auf allen Knoten im Cluster zu starten, damit Knoten mit der neuesten Kopie der Cluster Konfigurationsdaten zuerst den Cluster bilden können. Dieser Knoten kann dann in den Cluster eingebunden werden und erhält automatisch die aktualisierten Cluster Konfigurationsdaten. Wenn keine Knoten mit der neuesten Kopie der Cluster Konfigurationsdaten verfügbar sind, führen Sie das Windows PowerShell-Cmdlet "Start-clusternode-f" aus. Mithilfe des ForceQuorum (FQ)-Parameters wird der Cluster Dienst gestartet, und die Kopie der Cluster Konfigurationsdaten dieses Knotens wird als autorisierend gekennzeichnet. Das Erzwingen des Quorums auf einem Knoten mit einer veralteten Kopie der Cluster Datenbank führt möglicherweise zu Änderungen an der Cluster Konfiguration, die aufgetreten sind, während der Knoten nicht an dem Cluster beteiligt war.

### <a name="event-1564-res_fsw_arbitratefailure"></a>Ereignis 1564: RES_FSW_ARBITRATEFAILURE

Die Dateifreigabe-Zeugen Ressource "%1" konnte die Dateifreigabe "%2" nicht überzeugen.
Stellen Sie sicher, dass die Dateifreigabe "%2" vorhanden ist und dass der Cluster darauf zugreifen kann.

### <a name="event-1570-service_connect_authentication_failure"></a>Ereignis 1570: SERVICE_CONNECT_AUTHENTICATION_FAILURE

Der Knoten "%1" konnte beim beitreten zum Cluster keine Kommunikationssitzung einrichten.
Dies war auf einen Authentifizierungsfehler zurückzuführen. Überprüfen Sie, ob die Knoten kompatible Versionen der Cluster Dienst Software ausführen.

### <a name="event-1571-service_connect_authorizaion_failure"></a>Ereignis 1571: SERVICE_CONNECT_AUTHORIZAION_FAILURE

Der Knoten "%1" konnte beim beitreten zum Cluster keine Kommunikationssitzung einrichten.
Dies wurde aufgrund eines Autorisierungs Fehlers verursacht. Überprüfen Sie, ob die Knoten kompatible Versionen der Cluster Dienst Software ausführen.

### <a name="event-1572-service_netft_route_initial_failure"></a>Ereignis 1572: SERVICE_NETFT_ROUTE_INITIAL_FAILURE

Der Knoten "%1" konnte dem Cluster nicht beitreten, weil er keine Netzwerk Nachrichten zur Fehlererkennung mit anderen Cluster Knoten senden und empfangen konnte. Führen Sie den Konfigurationsüberprüfungs-Assistenten aus, um die Netzwerkeinstellungen sicherzustellen. Überprüfen Sie außerdem die Regeln der Windows-Firewall "Failovercluster".

### <a name="event-1574-dm_database_unload_failed"></a>Ereignis 1574: DM_DATABASE_UNLOAD_FAILED

Die failoverclusterdatenbank konnte nicht entladen werden. Wenn das Problem durch einen Neustart des Cluster Dienstanbieter nicht behoben werden kann, starten Sie den Computer neu.

### <a name="event-1575-dm_database_corrupt_or_missing_fixquorum"></a>Ereignis 1575: DM_DATABASE_CORRUPT_OR_MISSING_FIXQUORUM

Der Versuch, den Cluster Dienst zu erzwingen, ist fehlgeschlagen, da die Cluster Konfigurationsdaten auf diesem Knoten entweder nicht vorhanden oder beschädigt sind. Starten Sie zunächst den Cluster Dienst auf einem anderen Knoten, der über eine intakte und gültige Kopie der Cluster Konfigurationsdaten verfügt. Wiederholen Sie dann den Startvorgang auf diesem Knoten (der versucht, aktualisierte gültige Konfigurationsinformationen automatisch abzurufen). Wenn kein anderer Knoten verfügbar ist, verwenden Sie "Wbadmin. msc", um eine System Status Wiederherstellung dieses Knotens durchzuführen, um die Konfigurationsdaten wiederherzustellen.

### <a name="event-1593-dm_could_not_discard_changes"></a>Ereignis 1593: DM_COULD_NOT_DISCARD_CHANGES

Die failoverclusterdatenbank konnte nicht entladen werden, und möglicherweise falsche Änderungen im Arbeitsspeicher konnten nicht verworfen werden. Der Cluster Dienst versucht, die Datenbank zu reparieren, indem er von einem anderen Cluster Knoten abgerufen wird. Wenn der Cluster Dienst nicht online geschaltet wird, starten Sie den Cluster Dienst auf diesem Knoten neu. Wenn das Problem durch einen Neustart des Cluster Dienstanbieter nicht behoben werden kann, starten Sie den Computer neu. Wenn der Cluster Dienst nach einem Neustart nicht online geschaltet werden kann, stellen Sie die Cluster Datenbank aus der letzten Sicherung wieder her. Die aktuelle Datenbank wurde nach "%1" kopiert. Wenn keine Sicherungen verfügbar sind, kopieren Sie "%1" nach "%2", und versuchen Sie, den Cluster Dienst zu starten. Wenn der Cluster Dienst dann auf diesem Knoten online geschaltet wird, gehen möglicherweise einige Änderungen an der Cluster Konfiguration verloren, und der Cluster funktioniert möglicherweise nicht ordnungsgemäß. Führen Sie den Konfigurationsüberprüfungs-Assistenten aus, um die Cluster Konfiguration zu überprüfen und sicherzustellen, dass die gehosteten Dienste und Anwendungen online und ordnungsgemäß funktionieren.

### <a name="event-1672-event_node_quarantined"></a>Ereignis 1672: EVENT_NODE_QUARANTINED

Der Cluster Knoten "%1" wurde unter Quarantäne gestellt. Im Knoten sind %2 aufeinanderfolgende Fehler innerhalb eines kurzen Zeitraums aufgetreten, der aus dem Cluster entfernt wurde, um weitere Unterbrechungen zu vermeiden. Der Knoten wird bis "%3" unter Quarantäne gestellt, und anschließend versucht der Knoten automatisch, den Cluster erneut beizutreten.

Informationen zu den Problemen auf diesem Knoten finden Sie in den System-und Anwendungs Ereignisprotokollen. Wenn das Problem behoben ist, kann die Quarantäne manuell gelöscht werden, damit der Knoten mit dem Windows PowerShell-Cmdlet "Start-clusternode – clearquarantäne" erneut verknüpft werden kann.

Knoten Name: %1

Anzahl der aufeinander folgenden Cluster Mitgliedschaften verliert: %2

Die Zeit Quarantäne wird automatisch gelöscht: %3

## <a name="error-events"></a>Fehlerereignisse

### <a name="event-1024-cp_reg_ckpt_restore_failed"></a>Ereignis 1024: CP_REG_CKPT_RESTORE_FAILED

Der Registrierungs Prüf Punkt für die Cluster Ressource "%1" konnte nicht im Registrierungsschlüssel HKEY_LOCAL_MACHINE "%2" wieder hergestellt werden \\ . Die Ressource funktioniert möglicherweise nicht ordnungsgemäß.
Stellen Sie sicher, dass keine anderen Prozesse über geöffnete Handles für Registrierungsschlüssel in dieser Registrierungs Unterstruktur verfügen.

### <a name="event-1034-res_disk_missing"></a>Ereignis 1034: RES_DISK_MISSING

Die physische Datenträger Ressource "%1" des Clusters kann nicht online geschaltet werden, da der zugehörige Datenträger nicht gefunden wurde. Die erwartete Signatur des Datenträgers war "%2".
Wenn der Datenträger ersetzt oder wieder hergestellt wurde, können Sie im Failovercluster-Manager-Snap-in die Reparatur Funktion (auf dem Blatt "Eigenschaften" für den Datenträger) verwenden, um den neuen oder wiederhergestellten Datenträger zu reparieren. Wenn der Datenträger nicht ersetzt wird, löschen Sie die zugehörige Datenträger Ressource.

### <a name="event-1035-res_disk_mount_failed"></a>Ereignis 1035: RES_DISK_MOUNT_FAILED

Beim Online schalten der Datenträger Ressource "%1" ist der Zugriff auf ein oder mehrere Volumes mit Fehler "%2" fehlgeschlagen. Führen Sie den Konfigurationsüberprüfungs-Assistenten aus, um die Speicherkonfiguration zu überprüfen. Optional können Sie CHKDSK ausführen, um die Integrität aller Volumes auf diesem Datenträger zu überprüfen.

### <a name="event-1037-res_disk_filesystem_failed"></a>Ereignis 1037: RES_DISK_FILESYSTEM_FAILED

Das Dateisystem für eine oder mehrere Partitionen auf dem Datenträger für die Ressource "%1" ist möglicherweise beschädigt. Führen Sie den Konfigurationsüberprüfungs-Assistenten aus, um die Speicherkonfiguration zu überprüfen. Optional können Sie CHKDSK ausführen, um die Integrität aller Volumes auf diesem Datenträger zu überprüfen.

### <a name="event-1038-res_disk_reservation_lost"></a>Ereignis 1038: RES_DISK_RESERVATION_LOST

Der Besitz des Cluster Datenträgers "%1" wurde von diesem Knoten unerwartet verloren. Führen Sie den Konfigurationsüberprüfungs-Assistenten aus, um die Speicherkonfiguration zu überprüfen.

### <a name="event-1039-res_genapp_create_failed"></a>Ereignis 1039: RES_GENAPP_CREATE_FAILED

Die generische Anwendung "%1" konnte bei dem Versuch, den Prozess zu erstellen, nicht online geschaltet werden (mit Fehler "%2"). Zu den möglichen Ursachen gehören: die Anwendung ist möglicherweise nicht auf diesem Knoten vorhanden, der Pfadname wurde möglicherweise falsch angegeben, der binäre Name wurde möglicherweise falsch angegeben.

### <a name="event-1040-res_gensvc_open_failed"></a>Ereignis 1040: RES_GENSVC_OPEN_FAILED

Der generische Dienst "%1" konnte beim Versuch, den Dienst zu öffnen, nicht online geschaltet werden (mit Fehler "%2"). Zu den möglichen Ursachen gehören: der Dienst ist entweder nicht installiert, oder der angegebene Dienst Name ist ungültig.

### <a name="event-1041-res_gensvc_start_failed"></a>Ereignis 1041: RES_GENSVC_START_FAILED

Der generische Dienst "%1" konnte beim Versuch, den Dienst zu starten, nicht online geschaltet werden (mit Fehler "%2"). Mögliche Ursache: die angegebenen Dienst Parameter sind möglicherweise ungültig.

### <a name="event-1042-res_gensvc_failed_after_start"></a>Ereignis 1042: RES_GENSVC_FAILED_AFTER_START

Der generische Dienst "%1" ist mit Fehler "%2" fehlgeschlagen. Überprüfen Sie das Anwendungs Ereignisprotokoll.

### <a name="event-1044-res_ipaddr_nbt_interface_create_failed"></a>Ereignis 1044: RES_IPADDR_NBT_INTERFACE_CREATE_FAILED

Fehler beim Erstellen einer neuen NetBIOS-Schnittstelle beim Online schalten der Ressource "%1" (Fehlercode "%2"). Möglicherweise wurde die maximale Anzahl von NetBIOS-Namen überschritten.

### <a name="event-1046-res_ipaddr_invalid_subnet"></a>Ereignis 1046: RES_IPADDR_INVALID_SUBNET

Die Cluster-IP-Adress Ressource "%1" kann nicht online geschaltet werden, da der Wert für die Subnetzmaske ungültig ist. Überprüfen Sie die Eigenschaften der IP-Adress Ressource.

### <a name="event-1047-res_ipaddr_invalid_address"></a>Ereignis 1047: RES_IPADDR_INVALID_ADDRESS

Die Cluster-IP-Adress Ressource "%1" kann nicht online geschaltet werden, da der Adress Wert ungültig ist. Überprüfen Sie die Eigenschaften der IP-Adress Ressource.

### <a name="event-1048-res_ipaddr_invalid_adapter"></a>Ereignis 1048: RES_IPADDR_INVALID_ADAPTER

Die Cluster-IP-Adress Ressource "%1" konnte nicht online geschaltet werden. Die Konfigurationsdaten für den Netzwerkadapter, der der Cluster Netzwerkschnittstelle "%2" entspricht, konnten nicht ermittelt werden (Fehlercode: "%3"). Überprüfen Sie, ob die IP-Adress Ressource mit den richtigen Adress-und Netzwerk Eigenschaften konfiguriert ist.

### <a name="event-1049-res_ipaddr_in_use"></a>Ereignis 1049: RES_IPADDR_IN_USE

Die Cluster-IP-Adress Ressource "%1" kann nicht online geschaltet werden, weil im Netzwerk eine doppelte IP-Adresse "%2" erkannt wurde. Stellen Sie sicher, dass alle IP-Adressen eindeutig sind.

### <a name="event-1050-res_netname_duplicate"></a>Ereignis 1050: RES_NETNAME_DUPLICATE

Die Cluster Netzwerk-namens Ressource "%1" kann nicht online geschaltet werden, weil der Name "%2" mit diesem Cluster Knoten Namen übereinstimmt. Stellen Sie sicher, dass die Netzwerknamen eindeutig sind.

### <a name="event-1051-res_netname_no_ip_address"></a>Ereignis 1051: RES_NETNAME_NO_IP_ADDRESS

Die Cluster Netzwerk-namens Ressource "%1" kann nicht online geschaltet werden. Stellen Sie sicher, dass die Netzwerkadapter für abhängige IP-Adress Ressourcen auf mindestens einen DNS-Server zugreifen können. Aktivieren Sie alternativ NetBIOS für abhängige IP-Adressen.

### <a name="event-1052-res_netname_cant_add_name_status"></a>Ereignis 1052: RES_NETNAME_CANT_ADD_NAME_STATUS

Die Cluster Netzwerk-namens Ressource "%1" kann nicht online geschaltet werden, da der Name dem System nicht hinzugefügt werden konnte. Der zugehörige Fehlercode wird im Daten Abschnitt gespeichert.

### <a name="event-1053-res_smb_cant_create_share"></a>Ereignis 1053: RES_SMB_CANT_CREATE_SHARE

Die Cluster Dateifreigabe "%1" kann nicht online geschaltet werden, da die Freigabe nicht erstellt werden konnte.

### <a name="event-1054-res_smb_share_not_found"></a>Ereignis 1054: RES_SMB_SHARE_NOT_FOUND

Fehler bei der Integritäts Überprüfung für die Dateifreigabe Ressource "%1". Fehler beim Abrufen von Informationen für Freigabe "%2" (mit Netzwerkname "%3"). Fehlercode: "%4". Stellen Sie sicher, dass die Freigabe vorhanden und zugänglich ist.

### <a name="event-1055-res_smb_share_failed"></a>Ereignis 1055: RES_SMB_SHARE_FAILED

Fehler bei der Integritäts Überprüfung für die Dateifreigabe Ressource "%1". Beim Abrufen von Informationen für die Freigabe "%2" (mit dem Netzwerknamen "%3") wurde angegeben, dass die Freigabe nicht vorhanden ist (Fehlercode "%4"). Stellen Sie sicher, dass die Freigabe vorhanden und zugänglich ist.

### <a name="event-1069-rcm_resource_failure"></a>Ereignis 1069: RCM_RESOURCE_FAILURE

Fehler bei der Cluster Ressource "%1" in der Cluster Rolle "%2".

### <a name="event-1069-rcm_resource_failure_with_typename"></a>Ereignis 1069: RCM_RESOURCE_FAILURE_WITH_TYPENAME

Fehler bei der Cluster Ressource "%1" vom Typ "%3" in der Cluster Rolle "%2".<br><br>Basierend auf den Fehler Richtlinien für die Ressource und Rolle versucht der Cluster Dienst möglicherweise, die Ressource auf diesem Knoten online zu schalten oder die Gruppe auf einen anderen Knoten des Clusters zu verschieben und dann neu zu starten. Überprüfen Sie den Ressourcen-und Gruppenstatus mithilfe Failovercluster-Manager oder des Windows PowerShell-Cmdlets Get-Clusterresource.

### <a name="event-1069-rcm_resource_failure_with_cause"></a>Ereignis 1069: RCM_RESOURCE_FAILURE_WITH_CAUSE

Fehler bei der Cluster Ressource "%1" vom Typ "%3" in der Cluster Rolle "%2". Fehlercode: "%5" ("%4").<br><br>Basierend auf den Fehler Richtlinien für die Ressource und Rolle versucht der Cluster Dienst möglicherweise, die Ressource auf diesem Knoten online zu schalten oder die Gruppe auf einen anderen Knoten des Clusters zu verschieben und dann neu zu starten. Überprüfen Sie den Ressourcen-und Gruppenstatus mithilfe Failovercluster-Manager oder des Windows PowerShell-Cmdlets Get-Clusterresource.

### <a name="event-1069-rcm_resource_failure_with_error_code"></a>Ereignis 1069: RCM_RESOURCE_FAILURE_WITH_ERROR_CODE

Fehler bei der Cluster Ressource "%1" vom Typ "%3" in der Cluster Rolle "%2". Fehlercode: "%4".<br><br>Basierend auf den Fehler Richtlinien für die Ressource und Rolle versucht der Cluster Dienst möglicherweise, die Ressource auf diesem Knoten online zu schalten oder die Gruppe auf einen anderen Knoten des Clusters zu verschieben und dann neu zu starten. Überprüfen Sie den Ressourcen-und Gruppenstatus mithilfe Failovercluster-Manager oder des Windows PowerShell-Cmdlets Get-Clusterresource.

### <a name="event-1069-rcm_resource_failure_due_to_veto"></a>Ereignis 1069: RCM_RESOURCE_FAILURE_DUE_TO_VETO

Fehler bei der Cluster Ressource "%1" vom Typ "%3" in der Cluster Rolle "%2" aufgrund eines Versuchs, eine erforderliche Zustandsänderung in dieser Cluster Ressource zu blockieren.

### <a name="event-1077-res_ipaddr_ipv4_address_interface_failed"></a>Ereignis 1077: RES_IPADDR_IPV4_ADDRESS_INTERFACE_FAILED

Fehler bei der Integritäts Überprüfung für die IP-Schnittstelle "%1" (Adresse "%2") (Status ist "%3"). Führen Sie den Konfigurationsüberprüfungs-Assistenten aus, um sicherzustellen, dass der Netzwerkadapter ordnungsgemäß funktioniert.

### <a name="event-1078-res_ipaddr_wins_address_failed"></a>Ereignis 1078: RES_IPADDR_WINS_ADDRESS_FAILED

Die Cluster-IP-Adress Ressource "%1" kann nicht online geschaltet werden, weil die WINS-Registrierung für die Schnittstelle "%2" mit Fehler "%3" fehlgeschlagen ist Stellen Sie sicher, dass ein gültiger, zugänglicher WINS-Server angegeben wurde.

### <a name="event-1121-cp_crypto_ckpt_restore_failed"></a>Ereignis 1121: CP_CRYPTO_CKPT_RESTORE_FAILED

Verschlüsselte Einstellungen für die Cluster Ressource "%1" konnten nicht erfolgreich auf den Container Namen "%2" auf diesem Knoten angewendet werden.

### <a name="event-1127-tm_event_cluster_netinterface_failed"></a>Ereignis 1127: TM_EVENT_CLUSTER_NETINTERFACE_FAILED

Fehler bei der Cluster Netzwerkschnittstelle "%1" für Cluster Knoten "%2" im Netzwerk "%3". Führen Sie den Konfigurationsüberprüfungs-Assistenten aus, um die Netzwerkkonfiguration zu überprüfen. Wenn die Bedingung weiterhin besteht, prüfen Sie, ob Hardware-oder Softwarefehler im Zusammenhang mit dem Netzwerkadapter vorliegen. Überprüfen Sie auch, ob in anderen Netzwerkkomponenten, mit denen der Knoten verbunden ist, wie z. b. Hubs, Switches oder Bridges, auf Fehler.

### <a name="event-1129-tm_event_cluster_network_partitioned"></a>Ereignis 1129: TM_EVENT_CLUSTER_NETWORK_PARTITIONED

Das Cluster Netzwerk "%1" ist partitioniert. Einige angefügte Failoverclusterknoten können nicht über das Netzwerk miteinander kommunizieren. Der Speicherort des Fehlers konnte vom Failovercluster nicht bestimmt werden. Führen Sie den Konfigurationsüberprüfungs-Assistenten aus, um die Netzwerkkonfiguration zu überprüfen. Wenn die Bedingung weiterhin besteht, prüfen Sie, ob Hardware-oder Softwarefehler im Zusammenhang mit dem Netzwerkadapter vorliegen. Überprüfen Sie auch, ob in anderen Netzwerkkomponenten, mit denen der Knoten verbunden ist, wie z. b. Hubs, Switches oder Bridges, auf Fehler.

### <a name="event-1130-tm_event_cluster_network_down"></a>Ereignis 1130: TM_EVENT_CLUSTER_NETWORK_DOWN

Das Cluster Netzwerk "%1" ist nicht herunter. Keiner der verfügbaren Knoten kann mit diesem Netzwerk kommunizieren. Führen Sie den Konfigurationsüberprüfungs-Assistenten aus, um die Netzwerkkonfiguration zu überprüfen. Wenn die Bedingung weiterhin besteht, prüfen Sie, ob Hardware-oder Softwarefehler im Zusammenhang mit dem Netzwerkadapter vorliegen. Überprüfen Sie auch, ob in anderen Netzwerkkomponenten, mit denen der Knoten verbunden ist, wie z. b. Hubs, Switches oder Bridges, auf Fehler.

### <a name="event-1137-rcm_drain_move_failed"></a>Ereignis 1137: RCM_DRAIN_MOVE_FAILED

Das Verschieben der Cluster Rolle "%1" für den Ausgleich konnte nicht abgeschlossen werden. Fehler beim Vorgang. Fehlercode: %2.

### <a name="event-1138-res_smb_cant_create_dfs_root"></a>Ereignis 1138: RES_SMB_CANT_CREATE_DFS_ROOT

Die Cluster Dateifreigabe-Ressource "%1" kann nicht online geschaltet werden. Fehler beim Erstellen des DFS-Namespace Stamms (Fehler: ' %3 '). Dies liegt möglicherweise daran, dass der DFS-Namespace-Dienst nicht gestartet oder der DFS-N-Stamm für die Freigabe "%2" nicht erstellt werden konnte.

### <a name="event-1141-res_smb_cant_init_dfs_svc"></a>Ereignis 1141: RES_SMB_CANT_INIT_DFS_SVC

Die Cluster Dateifreigabe-Ressource "%1" kann nicht online geschaltet werden. Fehler bei der erneuten Synchronisierung des DFS-Stamm Ziels "%2". Fehler: "%3".

### <a name="event-1142-res_smb_cant_online_dfs_root"></a>Ereignis 1142: RES_SMB_CANT_ONLINE_DFS_ROOT

Die Cluster Dateifreigabe-Ressource "%1" für den DFS-Namespace kann aufgrund des Fehlers "%2" nicht online geschaltet werden.

### <a name="event-1182-netres_resource_stop_error"></a>Ereignis 1182: NETRES_RESOURCE_STOP_ERROR

Die Cluster Ressource "%1" kann nicht online geschaltet werden, da der zugeordnete Dienst bei einem versuchten Neustart einen Fehler verursacht hat. Der Fehlercode lautet "%2". Der Dienst erforderte einen Neustart, um Parameter zu aktualisieren. Der Dienst konnte jedoch nicht beendet und neu gestartet werden. Überprüfen Sie, ob dem Dienst weitere Ereignisse zugeordnet sind, und stellen Sie sicher, dass der Dienst ordnungsgemäß funktioniert.

### <a name="event-1183-res_disk_invalid_mp_source_not_clustered"></a>Ereignis 1183: RES_DISK_INVALID_MP_SOURCE_NOT_CLUSTERED

Die Cluster Datenträger Ressource "%1" enthält einen ungültigen Einfügepunkt. Sowohl der Quell-als auch der Ziel Datenträger, die dem Bereitstellungs Punkt zugeordnet sind, müssen gruppierte Datenträger sein und müssen Mitglieder derselben Gruppe sein. <br>Der Einstellungspunkt "%2" für Volume "%3" verweist auf einen ungültigen Quell Datenträger. Stellen Sie sicher, dass es sich beim Quell Datenträger ebenfalls um einen gruppierten Datenträger und in derselben Gruppe wie der Ziel Datenträger handelt (der den Bereitstellungs Punkt

### <a name="event-1191-res_netname_delete_computer_account_failed_status"></a>Ereignis 1191: RES_NETNAME_DELETE_COMPUTER_ACCOUNT_FAILED_STATUS

Die Cluster Netzwerk-namens Ressource "%1" konnte das zugehörige Computer Objekt in der Domäne "%2" nicht löschen. Fehlercode: ' %3 '. <br>Bitte lassen Sie einen Domänen Administrator das Computer Objekt manuell aus der Active Directory Domäne löschen.

### <a name="event-1192-res_netname_delete_computer_account_failed"></a>Ereignis 1192: RES_NETNAME_DELETE_COMPUTER_ACCOUNT_FAILED

Die Cluster Netzwerk-namens Ressource "%1" konnte das zugehörige Computer Objekt in der Domäne "%2" aus folgendem Grund nicht löschen:<br>%3. <br><br>Bitte lassen Sie einen Domänen Administrator das Computer Objekt manuell aus der Active Directory Domäne löschen.

### <a name="event-1193-res_netname_add_computer_account_failed_status"></a>Ereignis 1193: RES_NETNAME_ADD_COMPUTER_ACCOUNT_FAILED_STATUS

Fehler beim Erstellen des zugeordneten Computer Objekts in der Domäne "%2" in der Cluster Netzwerknamen Ressource "%1" aus folgendem Grund: %3.<br><br>Der zugehörige Fehlercode lautet: %5<br><br>
Wenden Sie sich an Ihren Domänen Administrator, um Folgendes sicherzustellen:

- Computer Objekte können von der Cluster Identität "%4" erstellt werden. Standardmäßig werden alle Computer Objekte im Container "Computer" erstellt. Wenn dieser Speicherort geändert wurde, wenden Sie sich an den Domänen Administrator.
- Das Kontingent für Computer Objekte wurde nicht erreicht.
- Wenn ein Computer Objekt vorhanden ist, vergewissern Sie sich, dass die Cluster Identität "%4" für dieses Computer Objekt mit dem Tool Active Directory Benutzer und Computer über die Berechtigung "Vollzugriff" verfügt.

### <a name="event-1194-res_netname_add_computer_account_failed"></a>Ereignis 1194: RES_NETNAME_ADD_COMPUTER_ACCOUNT_FAILED

Fehler beim Erstellen des zugeordneten Computer Objekts in der Domäne "%2" in der Cluster Netzwerknamen Ressource "%1" während: %3.<br><br>Der Text für den zugeordneten Fehlercode lautet: %4

Wenden Sie sich an Ihren Domänen Administrator, um Folgendes sicherzustellen:

- Die Cluster Identität "%5" verfügt über Berechtigungen zum Erstellen von Computer Objekten. Standardmäßig werden alle Computer Objekte im gleichen Container wie die Cluster Identität "%5" erstellt.
- Das Kontingent für Computer Objekte wurde nicht erreicht.
- Wenn ein Computer Objekt vorhanden ist, überprüfen Sie, ob die Cluster Identität "%5" über die Berechtigung "Vollzugriff" für dieses Computer Objekt verfügt, indem Sie das Tool Active Directory Benutzer und Computer verwenden.

### <a name="event-1195-res_netname_dns_registration_failed_status"></a>Ereignis 1195: RES_NETNAME_DNS_REGISTRATION_FAILED_STATUS

Fehler bei der Registrierung mindestens eines zugeordneten DNS-Namens für die Cluster Netzwerk-namens Ressource "%1". Fehlercode: "%2". Stellen Sie sicher, dass die Netzwerkadapter, die abhängigen IP-Adress Ressourcen zugeordnet sind, mit Zugriff auf mindestens einen DNS-Server konfiguriert sind.

### <a name="event-1196-res_netname_dns_registration_failed"></a>Ereignis 1196: RES_NETNAME_DNS_REGISTRATION_FAILED

Fehler bei der Registrierung mindestens eines zugeordneten DNS-Namens für die Cluster Netzwerk-namens Ressource "%1" aus folgendem Grund:<br>%2.<br><br>Stellen Sie sicher, dass die Netzwerkadapter, die abhängigen IP-Adress Ressourcen zugeordnet sind, mit mindestens einem zugänglichen DNS-Server konfiguriert sind.

### <a name="event-1205-rcm_event_group_failed_online_offline"></a>Ereignis 1205: RCM_EVENT_GROUP_FAILED_ONLINE_OFFLINE

Die Cluster Rolle "%1" konnte vom Clusterdienst nicht vollständig online oder offline geschaltet werden. Mindestens eine Ressource weist einen fehlerhaften Status auf. Dies hat möglicherweise Auswirkungen auf die Verfügbarkeit der Cluster Rolle.

### <a name="event-1206-res_netname_update_computer_account_failed_status"></a>Ereignis 1206: RES_NETNAME_UPDATE_COMPUTER_ACCOUNT_FAILED_STATUS

Das Computer Objekt, das der Cluster Netzwerk-namens Ressource "%1" zugeordnet ist, konnte in der Domäne "%2" nicht aktualisiert werden. Fehlercode: ' %3 '. Der Cluster Identität "%4" fehlen möglicherweise die erforderlichen Berechtigungen zum Aktualisieren des Objekts. Wenden Sie sich an Ihren Domänen Administrator, um sicherzustellen, dass die Cluster Identität Computer Objekte in der Domäne aktualisieren kann.

### <a name="event-1207-res_netname_update_computer_account_failed"></a>Ereignis 1207: RES_NETNAME_UPDATE_COMPUTER_ACCOUNT_FAILED

Das Computer Objekt, das der Cluster Netzwerk-namens Ressource "%1" zugeordnet ist, konnte in der Domäne "%2" nicht aktualisiert werden. <br>Vorgang "%3".<br><br>Der Text für den zugeordneten Fehlercode lautet: %4<br> <br>Der Cluster Identität "%5" fehlen möglicherweise die erforderlichen Berechtigungen zum Aktualisieren des Objekts. Wenden Sie sich an Ihren Domänen Administrator, um sicherzustellen, dass die Cluster Identität Computer Objekte in der Domäne aktualisieren kann.

### <a name="event-1208-res_disk_invalid_mp_target_not_clustered"></a>Ereignis 1208: RES_DISK_INVALID_MP_TARGET_NOT_CLUSTERED

Die Cluster Datenträger Ressource "%1" enthält einen ungültigen Einfügepunkt. Sowohl der Quell-als auch der Ziel Datenträger, die dem Bereitstellungs Punkt zugeordnet sind, müssen gruppierte Datenträger sein und müssen Mitglieder derselben Gruppe sein. <br>Der Bereitstellungs Punkt "%2" für Volume "%3" verweist auf einen ungültigen Ziel Datenträger. Stellen Sie sicher, dass es sich bei dem Ziel Datenträger ebenfalls um einen gruppierten Datenträger und in derselben Gruppe wie der Quell Datenträger handelt

### <a name="event-1211-res_netname_no_writeable_dc_status"></a>Ereignis 1211: RES_NETNAME_NO_WRITEABLE_DC_STATUS

Die Cluster Netzwerk-namens Ressource "%1" kann nicht online geschaltet werden. Es wurde versucht, einen beschreibbaren Domänen Controller (in Domäne %2) zu suchen, um ein Computer Objekt zu erstellen oder zu aktualisieren, das der Ressource zugeordnet ist. Fehlercode: ' %3 '.
Stellen Sie sicher, dass für diesen Knoten innerhalb der konfigurierten Domäne ein Beschreib barer Domänen Controller verfügbar ist. Stellen Sie außerdem sicher, dass der DNS-Server ausgeführt wird, um den Namen des Domänen Controllers aufzulösen.

### <a name="event-1212-res_netname_no_writeable_dc"></a>Ereignis 1212: RES_NETNAME_NO_WRITEABLE_DC

Die Cluster Netzwerk-namens Ressource "%1" kann nicht online geschaltet werden. Der Versuch, einen beschreibbaren Domänen Controller (in Domäne %2) zu suchen, um ein Computer Objekt zu erstellen oder zu aktualisieren, das der Ressource zugeordnet ist, konnte aus folgendem Grund nicht ausgeführt werden:<br>%3.<br><br> Fehlercode: "%4". Stellen Sie sicher, dass für diesen Knoten innerhalb der konfigurierten Domäne ein Beschreib barer Domänen Controller verfügbar ist. Stellen Sie außerdem sicher, dass der DNS-Server ausgeführt wird, um den Namen des Domänen Controllers aufzulösen.

### <a name="event-1213-res_netname_rename_restore_failed"></a>Ereignis 1213: RES_NETNAME_RENAME_RESTORE_FAILED

Die Cluster Netzwerk-namens Ressource "%1" konnte das zugeordnete Computer Objekt auf dem Domänen Controller "%2" nicht vollständig umbenennen. Fehler beim Versuch, das Computer Objekt mit dem neuen Namen "%3" wieder in den ursprünglichen Namen "%4" umzubenennen. Fehlercode: ' %5 '. Dies wirkt sich möglicherweise auf die Client Konnektivität aus, bis der Netzwerkname und der zugehörige Computer Objektname konsistent sind. Bitten Sie den Domänen Administrator, das Computer Objekt manuell umzubenennen.

### <a name="event-1214-res_netname_cant_add_name2"></a>Ereignis 1214: RES_NETNAME_CANT_ADD_NAME2

Die Cluster-Netzwerknamen Ressource kann nicht bei NetBIOS registriert werden. <br><br>Netzwerk Name: "%3" <br>Fehlerursache: %2 <br>Ressourcen Name: "%1" <br><br> Führen Sie nbtstat für den Netzwerknamen aus, um sicherzustellen, dass der Name nicht bereits bei NetBIOS registriert ist.

### <a name="event-1215-res_netname_not_registered_with_rdr"></a>Ereignis 1215: RES_NETNAME_NOT_REGISTERED_WITH_RDR

Fehler bei der Integritäts Überprüfung für die Cluster Netzwerk-namens Ressource "%1". Der Netzwerkname "%2" ist nicht mehr auf diesem Knoten registriert. Fehlercode: ' %3 '. Überprüfen Sie Hardware-oder Softwarefehler im Zusammenhang mit dem Netzwerkadapter. Sie können auch den Konfigurationsüberprüfungs-Assistenten ausführen, um die Netzwerkkonfiguration zu überprüfen.

### <a name="event-1218-res_netname_online_rename_recovery_missing_account"></a>Ereignis 1218: RES_NETNAME_ONLINE_RENAME_RECOVERY_MISSING_ACCOUNT

Die Cluster Netzwerk-namens Ressource "%1" konnte keinen namens Änderungs Vorgang ausführen (es wurde versucht, den ursprünglichen Namen "%3" in den Namen "%4" zu ändern). Das Computer Objekt konnte auf dem Domänen Controller "%2" nicht gefunden werden (auf dem er erstellt wurde). Es wird versucht, das Computer Objekt neu zu erstellen, wenn die Ressource das nächste Mal online geschaltet wird. Wenden Sie sich außerdem an Ihren Domänen Administrator, um sicherzustellen, dass das Computer Objekt in der Domäne vorhanden ist.

### <a name="event-1219-res_netname_online_rename_dc_not_found"></a>Ereignis 1219: RES_NETNAME_ONLINE_RENAME_DC_NOT_FOUND

Die Cluster Netzwerk-namens Ressource "%1" konnte keinen namens Änderungs Vorgang ausführen.
Der Domänen Controller "%2", auf dem das Computer Objekt "%3" umbenannt wurde, konnte nicht kontaktiert werden. Fehlercode: "%4". Stellen Sie sicher, dass auf einen beschreibbaren Domänen Controller zugegriffen werden kann, und prüfen Sie, ob Verbindungsprobleme

### <a name="event-1220-res_netname_online_rename_recovery_failed"></a>Ereignis 1220: RES_NETNAME_ONLINE_RENAME_RECOVERY_FAILED

Fehler beim Umbenennen des Computer Kontos für die Ressource "%1" von "%2" in "%3" mithilfe des Domänen Controllers "%4". Der zugehörige Fehlercode wird im Daten Abschnitt gespeichert.<br>
<br>Das Computer Konto für diese Ressource wurde gerade umbenannt und wurde nicht fertiggestellt. Dies wurde während des Online Vorgangs für diese Ressource erkannt.
Um die Wiederherstellung durchzusetzen, muss das Computer Konto in den aktuellen Wert der Name-Eigenschaft umbenannt werden, d. h., der im Netzwerk angegebene Name.<br> <br>Möglicherweise ist der Domänen Controller, auf dem der umbenannt wurde, nicht verfügbar. Wenn dies der Fall ist, warten Sie, bis der Domänen Controller wieder verfügbar ist. Dem Domänen Controller kann der Zugriff auf das Konto verweigert werden. versuchen Sie nach dem Auflösen des Zugriffs, den Namen erneut online zu schalten.<br> <br>Wenn dies nicht möglich ist, deaktivieren Sie die Kerberos-Authentifizierung, und aktivieren Sie Sie erneut, und es wird versucht, das Computer Konto auf einem anderen Domänen Controller zu finden. Sie müssen die Name-Eigenschaft in "%2" ändern, damit das vorhandene Computer Konto verwendet werden soll.

### <a name="event-1223-res_ipaddr_invalid_network_role"></a>Ereignis 1223: RES_IPADDR_INVALID_NETWORK_ROLE

Die Cluster-IP-Adress Ressource "%1" kann nicht online geschaltet werden, weil das Cluster Netzwerk "%2" nicht für den Client Zugriff konfiguriert ist. Verwenden Sie die Failovercluster-Manager-Snap-in, um die konfigurierten Eigenschaften des Cluster Netzwerks zu überprüfen.

### <a name="event-1226-res_netname_tcb_not_held"></a>Ereignis 1226: RES_NETNAME_TCB_NOT_HELD

Für die Netzwerknamen Ressource "%1" (mit dem zugeordneten Netzwerknamen "%2") ist die Kerberos-Authentifizierungs Unterstützung aktiviert. Fehler beim Hinzufügen der erforderlichen Anmelde Informationen zum LSA. der zugeordnete Fehlercode "%3" weist auf die für diesen Vorgang normalerweise erforderlichen Berechtigungen hin. Die erforderliche Berechtigung ist "Trusted Computing Base" und muss lokal auf jedem Knoten aktiviert sein, der den Cluster umfasst.

### <a name="event-1227-res_netname_lsa_error"></a>Ereignis 1227: RES_NETNAME_LSA_ERROR

Für die Netzwerknamen Ressource "%1" (mit dem zugeordneten Netzwerknamen "%2") ist die Kerberos-Authentifizierungs Unterstützung aktiviert. Fehler beim Hinzufügen der erforderlichen Anmelde Informationen zum LSA. der zugehörige Fehlercode ist "%3".

### <a name="event-1228-res_netname_clone_failure"></a>Ereignis 1228: RES_NETNAME_CLONE_FAILURE

Fehler bei der Cluster Netzwerknamen Ressource "%1" beim Aktivieren des Netzwerk namens auf diesem Knoten. Ursache für den Fehler: <br> "%2".<br><br> Fehlercode: ' %3 '. <br><br> Sie können die Netzwerknamen Ressource zum erneuten Versuch erneut offline und online schalten.

### <a name="event-1229-res_netname_no_ips_for_dns"></a>Ereignis 1229: RES_NETNAME_NO_IPS_FOR_DNS

Von der Cluster Netzwerk-namens Ressource "%1" konnten keine IP-Adressen identifiziert werden, die bei einem DNS-Server registriert werden. Stellen Sie sicher, dass mindestens ein Netzwerk für die Cluster Verwendung mit der Einstellung "Clients das Herstellen einer Verbindung über dieses Netzwerk gestatten" vorhanden ist und dass jeder Knoten über eine gültige IP-Adresse verfügt, die für die Netzwerke konfiguriert ist.

### <a name="event-1230-rcm_deadlock_or_crash_detected"></a>Ereignis 1230: RCM_DEADLOCK_OR_CRASH_DETECTED

Eine Komponente auf dem Server hat nicht rechtzeitig reagiert. Dies hat bewirkt, dass die Cluster Ressource "%1" (Ressourcentyp "%2", dll "%3") den Timeout Schwellenwert überschreitet. Im Rahmen der Cluster Integritäts Erkennung werden Wiederherstellungs Aktionen ausgeführt.
Der Cluster versucht automatisch, eine automatische Wiederherstellung durch das Beenden und Neustarten des Ressourcenhosting-Subsystem (RHS)-Prozesses auszuführen, der diese Ressource ausgeführt hat. Überprüfen Sie, ob die zugrunde liegende Infrastruktur (z. b. Speicher, Netzwerk oder Dienste), die der Ressource zugeordnet ist, ordnungsgemäß funktioniert.

### <a name="event-1230-rcm_resource_control_deadlock_detected"></a>Ereignis 1230: RCM_RESOURCE_CONTROL_DEADLOCK_DETECTED

Eine Komponente auf dem Server hat nicht rechtzeitig reagiert. Dies hat bewirkt, dass die Cluster Ressource "%1" (Ressourcentyp "%2", dll "%3") bei der Verarbeitung des Steuerungs Codes "%4;" den Timeout Schwellenwert überschreitet. Im Rahmen der Cluster Integritäts Erkennung werden Wiederherstellungs Aktionen ausgeführt. Der Cluster versucht automatisch, eine automatische Wiederherstellung durch das Beenden und Neustarten des Ressourcenhosting-Subsystem (RHS)-Prozesses auszuführen, der diese Ressource ausgeführt hat. Überprüfen Sie, ob die zugrunde liegende Infrastruktur (z. b. Speicher, Netzwerk oder Dienste), die der Ressource zugeordnet ist, ordnungsgemäß funktioniert.

### <a name="event-1231-res_netname_logon_failure"></a>Ereignis 1231: RES_NETNAME_LOGON_FAILURE

Bei der Cluster Netzwerknamen Ressource "%1" ist ein Fehler bei der Anmeldung bei der Domäne aufgetreten. Ursache für den Fehler: <br> "%2".<br><br> Fehlercode: ' %3 '.
<br><br> Stellen Sie sicher, dass für diesen Knoten innerhalb der konfigurierten Domäne ein Domänen Controller verfügbar ist.

### <a name="event-1232-res_genscript_timeout"></a>Ereignis 1232: RES_GENSCRIPT_TIMEOUT

Der Einstiegspunkt "%2" in der generischen Skript Ressource "%1" hat die Ausführung nicht rechtzeitig beendet. Dies kann auf eine Endlosschleife oder andere Probleme zurückzuführen sein, die möglicherweise zu einem unendlichen warte Vorgang führen. Alternativ kann der angegebene ausstehende Timeout Wert für diese Ressource zu kurz sein. Überprüfen Sie den Skript Einstiegspunkt "%2", um sicherzustellen, dass alle möglichen unendlichen warte Vorgänge im Skriptcode korrigiert wurden. Dann sollten Sie ggf. den ausstehenden Timeout Wert erhöhen.

### <a name="event-1233-res_genscript_hangmode"></a>Ereignis 1233: RES_GENSCRIPT_HANGMODE

Generische Cluster Skript Ressource "%1": die Anforderung zum Ausführen des Vorgangs "%2" wird nicht verarbeitet. Dies liegt an einem zuvor fehlgeschlagenen Versuch, den Einstiegspunkt "%3" rechtzeitig auszuführen. Überprüfen Sie den Skriptcode für diesen Einstiegspunkt, um sicherzustellen, dass keine Endlosschleife oder andere Probleme vorhanden sind, die möglicherweise zu einem unendlichen warte Vorgang führen. Erhöhen Sie dann ggf. den Wert ausstehender Timeout Wert für Ressourcen.

### <a name="event-1234-cluster_event_account_missing_privs"></a>Ereignis 1234: CLUSTER_EVENT_ACCOUNT_MISSING_PRIVS

Die Clusterdienst hat festgestellt, dass für das Dienst Konto mindestens eine der erforderlichen Berechtigungen fehlt. Die Liste der fehlenden Berechtigungen lautet: "%1" und wird dem Dienst Konto derzeit nicht gewährt. Verwenden Sie die sc.exe qprivs ClusSvc, um die Berechtigungen des Clusterdienst (ClusSvc) zu überprüfen. Überprüfen Sie außerdem, ob in Active Directory Domain Services Sicherheitsrichtlinien oder Gruppenrichtlinien vorhanden sind, die möglicherweise die Standard Berechtigungen geändert haben. Geben Sie den folgenden Befehl ein, um dem Clusterdienst die erforderlichen Berechtigungen für die ordnungsgemäße Funktion zu erteilen:

```
sc.exe privs
clussvc
SeBackupPrivilege/SeRestorePrivilege/SeIncreaseQuotaPrivilege/SeIncreaseBasePriorityPrivilege/SeTcbPrivilege/SeDebugPrivilege/SeSecurityPrivilege/SeAuditPrivilege/SeImpersonatePrivilege/SeChangeNotifyPrivilege/SeIncreaseWorkingSetPrivilege/SeManageVolumePrivilege/SeCreateSymbolicLinkPrivilege/SeLoadDriverPrivilege
```

### <a name="event-1242-res_ipaddr_lease_expired"></a>Ereignis 1242: RES_IPADDR_LEASE_EXPIRED

Die Lease der IP-Adresse "%2", die der Cluster-IP-Adress Ressource "%1" zugeordnet ist, ist abgelaufen oder läuft demnächst ab und kann zurzeit nicht erneuert werden. Stellen Sie sicher, dass der zugeordnete DHCP-Server zugänglich und ordnungsgemäß konfiguriert ist, um die Lease für diese IP-Adresse zu erneuern

### <a name="event-1245-res_ipaddr_lease_renewal_failed"></a>Ereignis 1245: RES_IPADDR_LEASE_RENEWAL_FAILED

Die Cluster-IP-Adress Ressource "%1" konnte die Lease für die IP-Adresse "%2" nicht erneuern.
Stellen Sie sicher, dass der DHCP-Server zugänglich und ordnungsgemäß konfiguriert ist, um die Lease für diese IP-Adresse zu erneuern.

### <a name="event-1250-rcm_resource_embedded_failure"></a>Ereignis 1250: RCM_RESOURCE_EMBEDDED_FAILURE

Die Cluster Ressource "%1" in der Cluster Rolle "%2" hat eine Benachrichtigung über den kritischen Status erhalten. Für eine virtuelle Maschine gibt dies an, dass sich eine Anwendung oder ein Dienst innerhalb des virtuellen Computers in einem fehlerhaften Zustand befindet. Überprüfen Sie die Funktionalität des Dienstes oder der Anwendung, die auf dem virtuellen Computer überwacht wird.

### <a name="event-1254-rcm_group_terminal_failure"></a>Ereignis 1254: RCM_GROUP_TERMINAL_FAILURE

Die Cluster Rolle "%1" hat den failoverschwellen Wert überschritten. Die konfigurierte Anzahl von failoverversuchen innerhalb des Failoverzeitraums, der ihm zugewiesen wurde, ist erschöpft und wird in einem fehlerhaften Zustand verbleiben. Es werden keine weiteren Versuche unternommen, die Rolle Online zu schalten oder ein Failover auf einen anderen Knoten im Cluster durchzuführen.
Überprüfen Sie die Ereignisse, die dem Fehler zugeordnet sind. Nachdem die Probleme behoben wurden, die den Fehler verursacht haben, kann die Rolle manuell online geschaltet werden, oder der Cluster versucht, Sie nach dem Neustart Verzögerungs Zeitraum erneut online zu schalten.

### <a name="event-1255-rcm_resource_network_failure"></a>Ereignis 1255: RCM_RESOURCE_NETWORK_FAILURE

Die Cluster Ressource "%1" in der Cluster Rolle "%2" hat eine Benachrichtigung über den kritischen Status erhalten. Für eine virtuelle Maschine bedeutet dies, dass sich ein kritisches Netzwerk der virtuellen Maschine in einem fehlerhaften Zustand befindet. Überprüfen Sie die Netzwerk Konnektivität des virtuellen Computers und der virtuellen Netzwerke, für die der virtuelle Computer konfiguriert ist.

### <a name="event-1256-res_netname_dns_registration_failed_dynamic_dns_zone"></a>Ereignis 1256: RES_NETNAME_DNS_REGISTRATION_FAILED_DYNAMIC_DNS_ZONE

Fehler bei der Registrierung von mindestens einem zugeordneten DNS-Namen durch die Cluster-Netzwerknamen Ressource, weil die entsprechende DNS-Zone keine dynamischen Updates akzeptiert.<br><br>Cluster Netzwerkname: "%1"<br>DNS-Zone: "%2"

#### <a name="guidance"></a>Leitfaden

Stellen Sie sicher, dass das DNS als dynamische DNS-Zone konfiguriert ist. Wenn der DNS-Server keine dynamischen Updates akzeptiert, deaktivieren Sie in den Eigenschaften des Netzwerkadapters die Adressen dieser Verbindung in DNS registrieren.

### <a name="event-1257-res_netname_dns_registration_failed_secure_dns_zone"></a>Ereignis 1257: RES_NETNAME_DNS_REGISTRATION_FAILED_SECURE_DNS_ZONE

Fehler bei der Registrierung von mindestens einem zugeordneten DNS-Namen durch die Cluster-Netzwerknamen Ressource, weil der Zugriff zum Aktualisieren der sicheren DNS-Zone verweigert wurde.<br><br>Cluster Netzwerkname: "%1"<br>DNS-Zone: "%2"<br><br>Stellen Sie sicher, dass dem Cluster Namen Objekt (CNO) Berechtigungen für die sichere DNS-Zone erteilt werden.

### <a name="event-1258-res_netname_dns_registration_failed_timeout"></a>Ereignis 1258: RES_NETNAME_DNS_REGISTRATION_FAILED_TIMEOUT

Fehler bei der Registrierung eines oder mehrerer zugeordneter DNS-Namen durch die Cluster-Netzwerknamen Ressource, weil der DNS-Server nicht erreicht werden konnte.<br><br>Cluster Netzwerkname: "%1"<br>DNS-Zone: "%2"<br>DNS-Server: "%3"<br><br>Stellen Sie sicher, dass die Netzwerkadapter, die abhängigen IP-Adress Ressourcen zugeordnet sind, mit mindestens einem zugänglichen DNS-Server konfiguriert sind.

### <a name="event-1259-res_netname_dns_registration_failed_cleanup"></a>Ereignis 1259: RES_NETNAME_DNS_REGISTRATION_FAILED_CLEANUP

Fehler bei der Registrierung eines oder mehrerer zugeordneter DNS-Namen durch den Cluster-Netzwerknamen. der Cluster Dienst konnte die vorhandenen Datensätze, die dem Netzwerknamen entsprechen, nicht bereinigen.<br><br>Cluster Netzwerkname: "%1"<br>DNS-Zone: "%2"<br><br>Stellen Sie sicher, dass dem Cluster Namen Objekt (CNO) Berechtigungen für die sichere DNS-Zone erteilt werden.

### <a name="event-1260-res_netname_dns_registration_modify_failed"></a>Ereignis 1260: RES_NETNAME_DNS_REGISTRATION_MODIFY_FAILED

Die DNS-Registrierung konnte von der Cluster Netzwerk-namens Ressource nicht geändert werden.<br><br>Cluster Netzwerkname: "%1"<br>Fehlercode: "%2"

#### <a name="guidance"></a>Leitfaden

Stellen Sie sicher, dass die Netzwerkadapter, die abhängigen IP-Adress Ressourcen zugeordnet sind, mit Zugriff auf mindestens einen DNS-Server konfiguriert sind.

### <a name="event-1261-res_netname_dns_registration_modify_failed_status"></a>Ereignis 1261: RES_NETNAME_DNS_REGISTRATION_MODIFY_FAILED_STATUS

Die DNS-Registrierung konnte von der Cluster Netzwerk-namens Ressource nicht geändert werden.<br><br>Cluster Netzwerkname: "%1"<br>Ursache: "%2"

#### <a name="guidance"></a>Leitfaden

Stellen Sie sicher, dass die Netzwerkadapter, die abhängigen IP-Adress Ressourcen zugeordnet sind, mit Zugriff auf mindestens einen DNS-Server konfiguriert sind.

### <a name="event-1262-res_netname_dns_registration_publish_ptr_failed"></a>Ereignis 1262: RES_NETNAME_DNS_REGISTRATION_PUBLISH_PTR_FAILED

Die Cluster-Netzwerknamen Ressource konnte den PTR-Datensatz in der DNS-Reverse-Lookupzone nicht veröffentlichen.<br><br>Cluster Netzwerkname: "%1"<br>Fehler Code: "%2"

#### <a name="guidance"></a>Leitfaden

Stellen Sie sicher, dass die Netzwerkadapter, die abhängigen IP-Adress Ressourcen zugeordnet sind, mit Zugriff auf mindestens einen DNS-Server konfiguriert sind und dass die DNS-Reverse-Lookupzone vorhanden ist.

### <a name="event-1264-res_netname_dns_registration_publish_ptr_failed_status"></a>Ereignis 1264: RES_NETNAME_DNS_REGISTRATION_PUBLISH_PTR_FAILED_STATUS

Die Cluster-Netzwerknamen Ressource konnte den PTR-Datensatz in der DNS-Reverse-Lookupzone nicht veröffentlichen.<br><br>Cluster Netzwerkname: "%1"<br>Ursache: "%2"

#### <a name="guidance"></a>Leitfaden

Stellen Sie sicher, dass die Netzwerkadapter, die abhängigen IP-Adress Ressourcen zugeordnet sind, mit Zugriff auf mindestens einen DNS-Server konfiguriert sind und dass die DNS-Reverse-Lookupzone vorhanden ist.

### <a name="event-1265-res_type_control_timed_out"></a>Ereignis 1265: RES_TYPE_CONTROL_TIMED_OUT

Timeout beim Cluster Ressourcentyp "%1" während der Verarbeitung des Steuerungs Codes "%2". Der Cluster versucht, automatisch eine Wiederherstellung durchführen, indem er den Ressourcenhosting-Subsystem (RHS)-Prozess beendet und neu startet, der den-Befehl verarbeitet hat.

### <a name="event-1289-netft_adapter_not_found"></a>Ereignis 1289: NETFT_ADAPTER_NOT_FOUND

Der Cluster Dienst konnte nicht auf den Netzwerkadapter ' %1 ' zugreifen. Stellen Sie sicher, dass andere Netzwerkadapter ordnungsgemäß funktionieren, und überprüfen Sie den Geräte-Manager auf Fehler im Zusammenhang mit Adapter "%1". Wenn die Konfiguration für den Adapter "%1" geändert wurde, ist es möglicherweise erforderlich, das Feature "Failoverclustering" auf diesem Computer erneut zu installieren.

### <a name="event-1360-res_ipaddr_invalid_network"></a>Ereignis 1360: RES_IPADDR_INVALID_NETWORK

Die Cluster-IP-Adress Ressource "%1" konnte nicht online geschaltet werden. Stellen Sie sicher, dass die Netzwerk Eigenschaft ' %2 ' mit dem Cluster Netzwerknamen übereinstimmt oder die Address-Eigenschaft ' %3 ' mit einem der Subnetze in einem Cluster Netzwerk übereinstimmt. Wenn es sich um einen IPv6-Adresstyp handelt, stellen Sie sicher, dass das Cluster Netzwerk, das mit dieser Ressource übereinstimmt, mindestens ein IPv6-Präfix enthält, das kein Link-Local oder Tunnel

### <a name="event-1361-res_ipaddr_missing_dependant"></a>Ereignis 1361: RES_IPADDR_MISSING_DEPENDANT

Die IPv6-Tunnel Adress Ressource "%1" konnte nicht online geschaltet werden, da Sie nicht von einer IP-Adress Ressource (IPv4) abhängt. Es ist eine Abhängigkeit von mindestens einer IP-Adress Ressource (IPv4) erforderlich.

### <a name="event-1362-res_ipaddr_missing_data"></a>Ereignis 1362: RES_IPADDR_MISSING_DATA

Die Cluster-IP-Adress Ressource "%1" konnte nicht online geschaltet werden, weil die Eigenschaft "%2" nicht gelesen werden konnte. Stellen Sie sicher, dass die Ressource ordnungsgemäß konfiguriert ist.

### <a name="event-1363-res_ipaddr_no_isatap_support"></a>Ereignis 1363: RES_IPADDR_NO_ISATAP_SUPPORT

Die IPv6-Tunnel Adress Ressource "%1" konnte nicht online geschaltet werden. Das mit der abhängigen IP-Adresse (IPv4)-Ressource "%3" verknüpfte Cluster Netzwerk "%2" unterstützt keine ISATAP-Tunnelung. Stellen Sie sicher, dass das Cluster Netzwerk ISATAP-Tunnelung unterstützt.

### <a name="event-1540-service_backup_noquorum"></a>Ereignis 1540: SERVICE_BACKUP_NOQUORUM

Der Sicherungs Vorgang für die Cluster Konfigurationsdaten wurde abgebrochen, da das Quorum für den Cluster noch nicht erreicht wurde. Wiederholen Sie den Sicherungs Vorgang, nachdem der Cluster das Quorum erreicht hat.

### <a name="event-1554-service_restore_invaliduser"></a>Ereignis 1554: SERVICE_RESTORE_INVALIDUSER

Der Wiederherstellungs Vorgang für die Cluster Konfigurationsdaten ist fehlgeschlagen. Dies war auf unzureichende Berechtigungen zurückzuführen, die dem Benutzerkonto zugeordnet sind, das die Wiederherstellung durchführt. Stellen Sie sicher, dass das Benutzerkonto über lokale Administratorrechte verfügt.

### <a name="event-1557-service_witness_attach_failed"></a>Ereignis 1557: SERVICE_WITNESS_ATTACH_FAILED

Fehler beim Aktualisieren der Cluster Konfigurationsdaten für die Zeugen Ressource Clusterdienst. Stellen Sie sicher, dass die Zeugen Ressource online und zugänglich ist.

### <a name="event-1559-res_witness_new_node_conflict"></a>Ereignis 1559: RES_WITNESS_NEW_NODE_CONFLICT

Die der Dateifreigabe Zeugen-Ressource zugeordnete Dateifreigabe "%1" wird zurzeit von Server "%2" gehostet. Der Server "%2" wurde soeben als neuer Knoten innerhalb des Failoverclusters hinzugefügt. Das Hosting des Dateifreigabe Zeugen durch einen beliebigen Knoten, der denselben Cluster umfasst, wird nicht empfohlen. Wählen Sie einen Dateifreigabe Zeugen aus, der nicht von einem beliebigen Knoten im gleichen Cluster gehostet wird, und ändern Sie die Einstellungen der Dateifreigabe Zeugen-Ressource entsprechend.

### <a name="event-1560-res_smb_share_conflict"></a>Ereignis 1560: RES_SMB_SHARE_CONFLICT

Die Cluster Dateifreigabe-Ressource "%1" hat Konflikte im freigegebenen Ordner erkannt. Folglich sind einige dieser freigegebenen Ordner möglicherweise nicht zugänglich. Um diese Situation zu beheben, stellen Sie sicher, dass mehrere freigegebene Ordner nicht denselben Freigabe Namen aufweisen.

### <a name="event-1563-res_fsw_onlinefailure"></a>Ereignis 1563: RES_FSW_ONLINEFAILURE

Die Dateifreigabe-Zeugen Ressource "%1" konnte nicht online geschaltet werden. Stellen Sie sicher, dass die Dateifreigabe "%2" vorhanden ist und dass der Cluster darauf zugreifen kann.

### <a name="event-1566-res_netname_timedout"></a>Ereignis 1566: RES_NETNAME_TIMEDOUT

Die Cluster Netzwerk-namens Ressource "%1" kann nicht online geschaltet werden. Die Netzwerknamen Ressource wurde vom Ressourcen Host Subsystem beendet, weil ein Vorgang nicht in einem akzeptablen Zeitraum abgeschlossen wurde. Timeout des Vorgangs beim Ausführen von:<br> "%2"

### <a name="event-1567-service_failed_to_change_log_size"></a>Ereignis 1567: SERVICE_FAILED_TO_CHANGE_LOG_SIZE

Clusterdienst konnte die Größe des Ablauf Verfolgungs Protokolls nicht ändern. Überprüfen Sie die ClusterLogSize-Einstellung mit dem \| PowerShell-Cmdlet "Get-Cluster Format-List \* ". Überprüfen Sie außerdem mit dem Leistungs Monitor-Snap-in die Sitzungs Einstellungen der Ereignis Ablauf Verfolgung für Failoverclustering.

### <a name="event-1567-res_vipaddr_address_interface_failed"></a>Ereignis 1567: RES_VIPADDR_ADDRESS_INTERFACE_FAILED

Fehler bei der Integritäts Überprüfung für die IP-Schnittstelle "%1" (Adresse "%2") (Status ist "%3"). Überprüfen Sie Hardware-oder Softwarefehler im Zusammenhang mit den physischen oder virtuellen Netzwerkadaptern.

### <a name="event-1568-res_cloud_witness_cant_communicate_to_azure"></a>Ereignis 1568: RES_CLOUD_WITNESS_CANT_COMMUNICATE_TO_AZURE

Die cloudzeugen Ressource konnte Microsoft Azure Speicherdienste nicht erreichen.<br><br>Cluster Ressource: %1 <br>Cluster Knoten: %2

#### <a name="guidance"></a>Leitfaden

Dies kann auf die Netzwerkkommunikation zwischen dem Cluster Knoten und dem Microsoft Azure zu blockierenden Dienst zurückzuführen sein. Überprüfen Sie die Internet Konnektivität des Knotens mit Microsoft Azure. Stellen Sie eine Verbindung mit dem Microsoft Azure-Portal her, und überprüfen Sie, ob das Speicherkonto

### <a name="event-1569-service_using_restricted_network"></a>Ereignis 1569: SERVICE_USING_RESTRICTED_NETWORK

Das Netzwerk "%1", das für die Verwendung des Failoverclusters deaktiviert wurde, war das einzige derzeit mögliche Netzwerk, das von Knoten "%2" für die Kommunikation mit anderen Knoten im Cluster verwendet werden kann. Dies kann Auswirkungen auf die Fähigkeit der Knoten haben, am Cluster teilzunehmen. Überprüfen Sie die Netzwerk Konnektivität von Knoten "%2", und aktivieren Sie mindestens ein Netzwerk für die Cluster Kommunikation. Führen Sie den Konfigurationsüberprüfungs-Assistenten aus, um die Netzwerkkonfiguration zu überprüfen.

### <a name="event-1569-res_cloud_witness_token_expired"></a>Ereignis 1569: RES_CLOUD_WITNESS_TOKEN_EXPIRED

Die Cloud-Zeugen Ressource konnte sich nicht bei Microsoft Azure Speicherdiensten authentifizieren. Beim Kontaktieren des Microsoft Azure Speicher Kontos wurde ein Fehler vom Typ "Zugriff verweigert" zurückgegeben. <br><br>Cluster Ressource: %1

#### <a name="guidance"></a>Leitfaden

Der Zugriffsschlüssel des Speicher Kontos ist möglicherweise nicht mehr gültig. Verwenden Sie den Assistenten zum Konfigurieren des Cluster Quorums in den Failovercluster-Manager oder dem Windows PowerShell-Cmdlet Set-Clusterquorum, um die Cloud-Zeugen Ressource mit dem aktualisierten Zugriffsschlüssel für das Speicherkonto zu konfigurieren.

### <a name="event-1573-service_form_witness_failed"></a>Ereignis 1573: SERVICE_FORM_WITNESS_FAILED

Knoten "%1" konnte keinen Cluster bilden. Der Grund war, dass auf den Zeugen nicht zugegriffen werden konnte. Stellen Sie sicher, dass die Zeugen Ressource online und verfügbar ist.

### <a name="event-1580-res_netname_dns_registration_secure_zone_failed"></a>Ereignis 1580: RES_NETNAME_DNS_REGISTRATION_SECURE_ZONE_FAILED

Die Cluster Netzwerk-namens Ressource "%1" konnte den Namen "%2" für den Adapter "%4" in einer sicheren DNS-Zone nicht registrieren. Dies war auf einen vorhandenen Datensatz mit diesem Namen zurückzuführen, und die Cluster Identität verfügt nicht über ausreichende Berechtigungen zum Aktualisieren dieses Datensatzes. Fehlercode: ' %3 '. Wenden Sie sich an den DNS-Server Administrator, um zu überprüfen, ob die Cluster Identität über Berechtigungen für den DNS-Datensatz "%2

### <a name="event-1580-res_netname_dns_registration_secure_zone_failed"></a>Ereignis 1580: RES_NETNAME_DNS_REGISTRATION_SECURE_ZONE_FAILED

Die Cluster Netzwerk-namens Ressource "%1" konnte den Namen "%2" für den Adapter "%4" in einer sicheren DNS-Zone nicht registrieren. Dies war auf einen vorhandenen Datensatz mit diesem Namen zurückzuführen, und die Cluster Identität verfügt nicht über ausreichende Berechtigungen zum Aktualisieren dieses Datensatzes. Fehlercode: ' %3 '. Wenden Sie sich an den DNS-Server Administrator, um zu überprüfen, ob die Cluster Identität über Berechtigungen für den DNS-Datensatz "%2

### <a name="event-1585-res_fileserver_fscheck_srvsvc_stopped"></a>Ereignis 1585: RES_FILESERVER_FSCHECK_SRVSVC_STOPPED

Fehler bei der Integritäts Überprüfung für die Cluster Dateiserver-Ressource "%1". Dies war darauf zurückzuführen, dass der Server Dienst nicht gestartet wurde. Verwenden Sie Server-Manager, um den Status des Server Dienstanbieter auf diesem Cluster Knoten zu bestätigen.

### <a name="event-1586-res_fileserver_fscheck_scoped_name_not_registered"></a>Ereignis 1586: RES_FILESERVER_FSCHECK_SCOPED_NAME_NOT_REGISTERED

Fehler bei der Integritäts Überprüfung für die Cluster Dateiserver-Ressource "%1". Dies war darauf zurückzuführen, dass auf einige freigegebene Ordner zugegriffen werden konnte. Stellen Sie sicher, dass Clients auf die Ordner zugreifen können. Überprüfen Sie außerdem den Status des Server Dienstanbieter auf diesem Cluster Knoten mithilfe von Server-Manager, und suchen Sie nach anderen Ereignissen im Zusammenhang mit dem Server Dienst auf diesem Cluster Knoten. Möglicherweise muss die Netzwerknamen Ressource "%2" in dieser Cluster Rolle neu gestartet werden.

### <a name="event-1587-res_fileserver_fscheck_failed"></a>Ereignis 1587: RES_FILESERVER_FSCHECK_FAILED

Fehler bei der Integritäts Überprüfung für die Cluster Dateiserver-Ressource "%1". Dies war darauf zurückzuführen, dass auf einige freigegebene Ordner zugegriffen werden konnte. Stellen Sie sicher, dass Clients auf die Ordner zugreifen können. Überprüfen Sie außerdem den Status des Server Dienstanbieter auf diesem Cluster Knoten mithilfe von Server-Manager, und suchen Sie nach anderen Ereignissen im Zusammenhang mit dem Server Dienst auf diesem Cluster Knoten.

### <a name="event-1588-res_fileserver_share_cant_add"></a>Ereignis 1588: RES_FILESERVER_SHARE_CANT_ADD

Die Cluster Dateiserver-Ressource "%1" kann nicht online geschaltet werden. Fehler beim Erstellen der dem Netzwerknamen "%3" zugeordneten Dateifreigabe "%2" durch die Ressource. Fehlercode: "%4". Überprüfen Sie, ob die Ordner vorhanden und zugänglich sind. Überprüfen Sie außerdem den Status des Server Dienstanbieter auf diesem Cluster Knoten mithilfe von Server-Manager, und suchen Sie nach anderen verwandten Ereignissen auf diesem Cluster Knoten. Möglicherweise muss die Netzwerknamen Ressource "%3" in dieser Cluster Rolle neu gestartet werden.

### <a name="event-1600-clusapi_create_cannot_set_ad_dacl"></a>Ereignis 1600: CLUSAPI_CREATE_CANNOT_SET_AD_DACL

Fehler beim Festlegen der Berechtigungen für das Cluster Computer Objekt "%1" Clusterdienst. Wenden Sie sich an den Netzwerkadministrator, um die Cluster Sicherheits Beschreibung des Computer Objekts in Active Directory zu überprüfen, sicherzustellen, dass die DACL nicht zu groß ist, und entfernen Sie ggf. unnötige zusätzliche ACE (s) für das Objekt.

### <a name="event-1603-res_fileserver_clone_failed"></a>Ereignis 1603: RES_FILESERVER_CLONE_FAILED

Der Datei Server konnte nicht gestartet werden, da die erwartete Abhängigkeit von der Ressource ' Network Name ' nicht gefunden wurde oder nicht ordnungsgemäß konfiguriert wurde. Fehler = 0x %2.

### <a name="event-1606-res_disk_cno_check_failed"></a>Ereignis 1606: RES_DISK_CNO_CHECK_FAILED

Die Cluster Datenträger Ressource "%1" enthält ein durch BitLocker geschütztes Volume "%2". für dieses Volume ist das Active Directory Cluster Namen Konto (auch als Cluster Namen Objekt oder CNO bezeichnet) keine BitLocker-Schutzvorrichtung für das Volume. Dies ist für mit BitLocker geschützte Volumes erforderlich. Um dies zu beheben, entfernen Sie zunächst den Datenträger aus dem Cluster. Fügen Sie als nächstes mit dem Befehlszeilen Tool "Manage-bde.exe" den Cluster Namen als adaccountorgroup-Schutz hinzu, und verwenden Sie dabei das Format Domäne \\ Cluster Name \$ für den Cluster Namen. Fügen Sie dann den Datenträger wieder zum Cluster hinzu. Weitere Informationen finden Sie in der Dokumentation zu Manage-bde.exe

### <a name="event-1607-res_disk_cno_unlock_failed"></a>Ereignis 1607: RES_DISK_CNO_UNLOCK_FAILED

Die Cluster Datenträger Ressource "%1" konnte das durch BitLocker geschützte Volume "%2" nicht entsperren. Das Cluster Namen Objekt (CNO) ist nicht als gültige BitLocker-Schutzvorrichtung für dieses Volume festgelegt. Um dies zu beheben, entfernen Sie den Datenträger aus dem Cluster. Fügen Sie dann mit dem Befehlszeilen Tool Manage-bde.exe den Cluster Namen als adaccountorgroup-Schutzvorrichtung unter Verwendung des Formats Domain \\ Cluster Name hinzu \$ , und fügen Sie den Datenträger wieder zum Cluster hinzu. Weitere Informationen finden Sie in der Dokumentation zu Manage-bde.exe.

### <a name="event-1608-res_fileserver_leader_failed"></a>Ereignis 1608: RES_FILESERVER_LEADER_FAILED

Der Datei Server konnte nicht gestartet werden, da die erwartete Abhängigkeit von der Ressource ' Network Name ' nicht gefunden wurde oder nicht ordnungsgemäß konfiguriert wurde. Fehler = 0x %2.

### <a name="event-1609-res_soda_fileserver_leader_failed"></a>Ereignis 1609: RES_SODA_FILESERVER_LEADER_FAILED

Scale Out Datei Server konnte nicht gestartet werden, da die erwartete Abhängigkeit von der Ressource ' verteilter Netzwerk Name ' nicht gefunden wurde oder nicht ordnungsgemäß konfiguriert wurde. Fehler = 0x %2.

### <a name="event-1632-clusapi_create_mismatched_ou"></a>Ereignis 1632: CLUSAPI_CREATE_MISMATCHED_OU

Fehler beim Erstellen des Clusters. Das Cluster Namen Objekt "%1" in der Active Directory-Organisationseinheit "%2" kann nicht erstellt werden. Das Objekt ist bereits in der Organisationseinheit "%3" vorhanden. Überprüfen Sie, ob der angegebene Distinguished Name-Pfad und das Cluster Namen Objekt korrekt sind. Wenn der Distinguished Name-Pfad nicht angegeben wird, wird das vorhandene Computer Objekt "%1" verwendet.

### <a name="event-1652-service_tcp_connection_failure"></a>Ereignis 1652: SERVICE_TCP_CONNECTION_FAILURE

Cluster Knoten "%1" konnte dem Cluster nicht beitreten. Es konnte keine TCP-Verbindung mit den Knoten "%2" hergestellt werden. Überprüfen Sie die Netzwerk Konnektivität und die Konfiguration von Netzwerk Firewalls.

### <a name="event-1652-service_udp_connection_failure"></a>Ereignis 1652: SERVICE_UDP_CONNECTION_FAILURE

Cluster Knoten "%1" konnte dem Cluster nicht beitreten. Es konnte keine UDP-Verbindung mit den Knoten "%2" hergestellt werden. Überprüfen Sie die Netzwerk Konnektivität und die Konfiguration von Netzwerk Firewalls.

### <a name="event-1652-service_virtual_tcp_connection_failure"></a>Ereignis 1652: SERVICE_VIRTUAL_TCP_CONNECTION_FAILURE

Cluster Knoten "%1" konnte dem Cluster nicht beitreten. Eine TCP-Verbindung, die den Microsoft-Failovercluster-Adapter verwendet, konnte nicht für Knoten "%2" eingerichtet werden. Überprüfen Sie die Netzwerk Konnektivität und die Konfiguration von Netzwerk Firewalls.

### <a name="event-1653-service_no_connectivity"></a>Ereignis 1653: SERVICE_NO_CONNECTIVITY

Der Cluster Knoten "%1" konnte dem Cluster nicht beitreten, weil er nicht über das Netzwerk mit einem anderen Knoten im Cluster kommunizieren konnte. Überprüfen Sie die Netzwerk Konnektivität und die Konfiguration von Netzwerk Firewalls.

### <a name="event-1654-res_vipaddr_invalid_adaptername"></a>Ereignis 1654: RES_VIPADDR_INVALID_ADAPTERNAME

Fehler beim Online schalten der Cluster-IP-Adress Ressource "%1". Die Konfigurationsdaten für den Netzwerkadapter "%2" konnten nicht ermittelt werden (Fehlercode: "%3"). Überprüfen Sie, ob die IP-Adress Ressource mit den richtigen Adress-und Netzwerk Eigenschaften konfiguriert ist.

### <a name="event-1655-res_vipaddr_invalid_vsid"></a>Ereignis 1655: RES_VIPADDR_INVALID_VSID

Fehler beim Online schalten der Cluster-IP-Adress Ressource "%1". Die Konfigurationsdaten für den Netzwerkadapter, die der virtuellen Subnetz-ID "%2" und der Routing Domänen-ID "%3" entsprechen, konnten nicht ermittelt werden (Fehlercode: "%4"). Überprüfen Sie, ob die IP-Adress Ressource mit den richtigen Adress-und Netzwerk Eigenschaften konfiguriert ist.

### <a name="event-1656-res_vipaddr_address_create_failed"></a>Ereignis 1656: RES_VIPADDR_ADDRESS_CREATE_FAILED

Fehler beim Hinzufügen der IP-Adresse "%2" für die nicht zusammenhängende IP-Adress Ressource "%1" (Fehlercode: "%3"). Überprüfen Sie Hardware-oder Softwarefehler im Zusammenhang mit den physischen oder virtuellen Netzwerkadaptern.

### <a name="event-1664-cluster_upgrade_incomplete"></a>Ereignis 1664: CLUSTER_UPGRADE_INCOMPLETE

Fehler beim Upgrade der Funktionsebene des Clusters. Überprüfen Sie, ob alle Knoten des Clusters aktuell ausgeführt werden und die gleiche Version von Windows Server sind, und führen Sie dann das Windows PowerShell-Cmdlet Update-clusterfunctionallevel erneut aus.

### <a name="event-1676-event_local_node_quarantined"></a>Ereignis 1676: EVENT_LOCAL_NODE_QUARANTINED

Der lokale Cluster Knoten wurde von "%1" unter Quarantäne gestellt. Der Knoten wird bis "%2" unter Quarantäne gestellt, und anschließend versucht der Knoten automatisch, den Cluster erneut beizutreten.
<br><br>Informationen zu den Problemen auf diesem Knoten finden Sie in den System-und Anwendungs Ereignisprotokollen. Wenn das Problem behoben ist, kann die Quarantäne manuell gelöscht werden, damit der Knoten mit dem Windows PowerShell-Cmdlet "Start-clusternode – clearquarantäne" erneut verknüpft werden kann.<br><br>Quarantinetype: von %1 unter Quarantäne gestellt<br>Die Zeit Quarantäne wird automatisch gelöscht: %2

### <a name="event-1677-event_node_drain_failed"></a>Ereignis 1677: EVENT_NODE_DRAIN_FAILED

Fehler bei Knoten Ableitung auf Cluster Knoten %1. <br><br>Verweisen Sie auf die System-und Anwendungs Ereignisprotokolle und Cluster Protokolle des Knotens, um die Ursache für den Fehler bei der Ableitung zu ermitteln. Wenn das Problem behoben ist, können Sie den Ausgleichs Vorgang wiederholen.

### <a name="event-1683-res_netname_computer_account_no_dc"></a>Ereignis 1683: RES_NETNAME_COMPUTER_ACCOUNT_NO_DC

Der Cluster Dienst konnte keinen verfügbaren Domänen Controller in der Domäne erreichen. Dies kann Auswirkungen auf die Funktionalität haben, die von der Authentifizierung des Cluster Netzwerk namens abhängig ist.<br><br>DC-Server: %1

#### <a name="guidance"></a>Leitfaden

Vergewissern Sie sich, dass auf die Domänen Controller im Netzwerk auf die Cluster Knoten zugegriffen werden kann.

### <a name="event-1684-res_netname_computer_object_vco_not_found"></a>Ereignis 1684: RES_NETNAME_COMPUTER_OBJECT_VCO_NOT_FOUND

Die Cluster-Netzwerknamen Ressource konnte das zugehörige Computer Objekt in Active Directory nicht finden. Dies kann Auswirkungen auf die Funktionalität haben, die von der Authentifizierung des Cluster Netzwerk namens abhängig ist.<br><br>Netzwerk Name: %1<br>Organisationseinheit: %2

#### <a name="guidance"></a>Leitfaden

Stellen Sie das Computer Objekt für den Netzwerknamen aus dem Active Directory Papierkorb wieder her. Alternativ dazu können Sie die Cluster-Netzwerknamen Ressource offline schalten und die Reparaturaktion ausführen, um das Computer Objekt in Active Directory neu zu erstellen.

### <a name="event-1685-res_netname_computer_object_cno_not_found"></a>Ereignis 1685: RES_NETNAME_COMPUTER_OBJECT_CNO_NOT_FOUND

Die Cluster-Netzwerknamen Ressource konnte das zugehörige Computer Objekt in Active Directory nicht finden. Dies kann Auswirkungen auf die Funktionalität haben, die von der Authentifizierung des Cluster Netzwerk namens abhängig ist.<br><br>Netzwerk Name: %1<br>Organisationseinheit: %2
#### <a name="guidance"></a>Leitfaden

Stellen Sie das Computer Objekt für den Netzwerknamen aus dem Active Directory Papierkorb wieder her.

### <a name="event-1686-res_netname_computer_object_vco_disabled"></a>Ereignis 1686: RES_NETNAME_COMPUTER_OBJECT_VCO_DISABLED

Ressource des Cluster Netzwerk namens gefunden, dass das zugehörige Computer Objekt in Active Directory deaktiviert werden soll. Dies kann Auswirkungen auf die Funktionalität haben, die von der Authentifizierung des Cluster Netzwerk namens abhängig ist.<br><br>Netzwerk Name: %1<br>Organisationseinheit: %2

#### <a name="guidance"></a>Leitfaden

Aktivieren Sie das Computer Objekt für den Netzwerknamen in Active Directory.

### <a name="event-1687-res_netname_computer_object_cno_disabled"></a>Ereignis 1687: RES_NETNAME_COMPUTER_OBJECT_CNO_DISABLED

Ressource des Cluster Netzwerk namens gefunden, dass das zugehörige Computer Objekt in Active Directory deaktiviert werden soll. Dies kann Auswirkungen auf die Funktionalität haben, die von der Authentifizierung des Cluster Netzwerk namens abhängig ist.<br><br>Netzwerk Name: %1<br>Organisationseinheit: %2

#### <a name="guidance"></a>Leitfaden

Aktivieren Sie das Computer Objekt für den Netzwerknamen in Active Directory. Alternativ dazu können Sie die Cluster-Netzwerknamen Ressource offline schalten und die Reparaturaktion ausführen, um das Computer Objekt in Active Directory zu aktivieren.

### <a name="event-1688-res_netname_computer_object_failed"></a>Ereignis 1688: RES_NETNAME_COMPUTER_OBJECT_FAILED

Die Ressource "Cluster Netzwerkname" hat festgestellt, dass das zugeordnete Computer Objekt in Active Directory deaktiviert wurde und versucht, es zu aktivieren. Dies kann Auswirkungen auf die Funktionalität haben, die von der Authentifizierung des Cluster Netzwerk namens abhängig ist.<br><br>Netzwerk Name: %1<br>Organisationseinheit: %2

#### <a name="guidance"></a>Leitfaden

Aktivieren Sie das Computer Objekt für den Netzwerknamen in Active Directory.

### <a name="event-4608-nodecleanup_get_clustered_disks_failed"></a>Ereignis 4608: NODECLEANUP_GET_CLUSTERED_DISKS_FAILED

Clusterdienst konnte die Liste der gruppierten Datenträger nicht abrufen, während der Cluster zerstört wird. Fehlercode: ' %1 '. Wenn Sie auf diese Datenträger nicht zugreifen können, führen Sie das PowerShell-Cmdlet "Clear-clusterdiskreservation" aus.

### <a name="event-4611-nodecleanup_release_clustered_disks_from_partmgr_failed"></a>Ereignis 4611: NODECLEANUP_RELEASE_CLUSTERED_DISKS_FROM_PARTMGR_FAILED

Der gruppierte Datenträger mit der ID "%2" wurde vom Partitions-Manager nicht freigegeben, während der Cluster zerstört wurde. Fehlercode: ' %1 '. Durch Neustarten des Computers wird sichergestellt, dass der Datenträger vom Partitions-Manager freigegeben wird.

### <a name="event-4613-nodecleanup_clear_clusdisk_database_failed"></a>Ereignis 4613: NODECLEANUP_CLEAR_CLUSDISK_DATABASE_FAILED

Der Cluster Dienst konnte einen gruppierten Datenträger mit der ID "%2" nicht ordnungsgemäß bereinigen, während der Cluster zerstört wurde. Fehlercode: ' %1 '. Möglicherweise ist der Zugriff auf diesen Datenträger erst möglich, wenn der Bereinigung erfolgreich abgeschlossen wurde. Löschen Sie für manuelles Cleanup den Wert ' attacheddisks ' des Schlüssels ' HKEY_LOCAL_MACHINE \\ System \\ CurrentControlSet \\ Services \\ Clusdisk \\ Parameters ' in der Windows-Registrierung.

### <a name="event-4615-nodecleanup_disable_cluster_service_failed"></a>Ereignis 4615: NODECLEANUP_DISABLE_CLUSTER_SERVICE_FAILED

Der Cluster Dienst wurde beendet und als Teil der Cluster Knoten Bereinigung als deaktiviert festgelegt.

### <a name="event-4616-nodecleanup_disable_cluster_service_timeout"></a>Ereignis 4616: NODECLEANUP_DISABLE_CLUSTER_SERVICE_TIMEOUT

Das Beenden des Cluster Dienstanbieter während der Bereinigung des Cluster Knotens wurde nicht innerhalb des erwarteten Zeitraums abgeschlossen. Starten Sie den Computer neu, um sicherzustellen, dass der Cluster Dienst nicht mehr ausgeführt wird.

### <a name="event-4618-nodecleanup_reset_cluster_registry_entries_failed"></a>Ereignis 4618: NODECLEANUP_RESET_CLUSTER_REGISTRY_ENTRIES_FAILED

Fehler beim Zurücksetzen der Cluster Dienst-Registrierungseinträge während der Bereinigung des Cluster Knotens.
Fehlercode: ' %1 '. Möglicherweise ist es nicht möglich, einen Cluster mit diesem Computer zu erstellen oder zu verknüpfen, bis die Bereinigung erfolgreich abgeschlossen wurde. Führen Sie für die manuelle Bereinigung das PowerShell-Cmdlet "Clear-clusternode" auf diesem Computer aus.

### <a name="event-4620-nodecleanup_unload_cluster_hive_failed"></a>Ereignis 4620: NODECLEANUP_UNLOAD_CLUSTER_HIVE_FAILED

Fehler beim Entladen der Cluster Dienst-Registrierungs Struktur während der Bereinigung des Cluster Knotens.
Fehlercode: ' %1 '. Möglicherweise ist es nicht möglich, einen Cluster mit diesem Computer zu erstellen oder zu verknüpfen, bis die Bereinigung erfolgreich abgeschlossen wurde. Führen Sie für die manuelle Bereinigung das PowerShell-Cmdlet "Clear-clusternode" auf diesem Computer aus.

### <a name="event-4622-nodecleanup_errors"></a>Ereignis 4622: NODECLEANUP_ERRORS

Bei der Clusterdienst ist während des Knoten Bereinigungs Fehlers ein Fehler aufgetreten. Möglicherweise ist es nicht möglich, einen Cluster mit diesem Computer zu erstellen oder zu verknüpfen, bis die Bereinigung erfolgreich abgeschlossen wurde. Verwenden Sie für diesen Knoten das PowerShell-Cmdlet "Clear-clusternode".

### <a name="event-4624-nodecleanup_reset_nlbsflags_failed"></a>Ereignis 4624: NODECLEANUP_RESET_NLBSFLAGS_FAILED

Fehler beim Zurücksetzen des Registrierungs Werts für den IPSec-Sicherheits Zuordnungs Timeout während der Cluster Knoten Bereinigung. Fehlercode: ' %1 '. Führen Sie für die manuelle Bereinigung das PowerShell-Cmdlet "Clear-clusternode" auf diesem Computer aus. Alternativ können Sie das IPSec-Sicherheits Zuordnungs Timeout zurücksetzen, indem Sie den Wert "%2" und den Wert "%3" aus HKEY_LOCAL_MACHINE in der Windows-Registrierung löschen.

### <a name="event-4627-nodecleanup_delete_cluster_tasks_failed"></a>Ereignis 4627: NODECLEANUP_DELETE_CLUSTER_TASKS_FAILED

Fehler beim Löschen von gruppierten Tasks während der Knoten Bereinigung. Fehlercode: ' %1 '.
Verwenden Sie Windows Taskplaner, um alle verbleibenden gruppierten Aufgaben zu löschen.

### <a name="event-4629-nodecleanup_delete_local_account_failed"></a>Ereignis 4629: NODECLEANUP_DELETE_LOCAL_ACCOUNT_FAILED

Während der Knoten Bereinigung wurde das lokale Benutzerkonto, das vom Cluster verwaltet wird, nicht gelöscht. Fehlercode: ' %1 '. Öffnen Sie lokale Benutzer und Gruppen (lusrmgr. msc), um das Konto zu löschen.

### <a name="event-4864-res_vsstask_open_failed"></a>Ereignis 4864: RES_VSSTASK_OPEN_FAILED

Fehler beim Erstellen des Volumeschattenkopie-Dienst Tasks "%1". Fehlercode: "%2".

### <a name="event-4865-res_vsstask_terminate_task_failed"></a>Ereignis 4865: RES_VSSTASK_TERMINATE_TASK_FAILED

Fehler beim Task "%1" des Volumeschattenkopie-Diensts. Fehlercode: "%2".
Dies liegt daran, dass die zugeordnete Aufgabe nicht im Rahmen eines Offline Vorgangs beendet werden konnte. Sie müssen ihn ggf. manuell mit dem Taskplaner-Snap-in beendet.

### <a name="event-4866-res_vsstask_delete_task_failed"></a>Ereignis 4866: RES_VSSTASK_DELETE_TASK_FAILED

Fehler beim Task "%1" des Volumeschattenkopie-Diensts. Fehlercode: "%2".
Dies liegt daran, dass die zugehörige Aufgabe nicht im Rahmen eines Offline Vorgangs gelöscht werden konnte. Sie müssen es unter Umständen manuell mithilfe des Taskplaner-Snap-Ins löschen.

### <a name="event-4867-res_vsstask_online_failed"></a>Ereignis 4867: RES_VSSTASK_ONLINE_FAILED

Fehler beim Task "%1" des Volumeschattenkopie-Diensts. Fehlercode: "%2".
Dies liegt daran, dass die zugehörige Aufgabe nicht als Teil eines Online Vorgangs hinzugefügt werden konnte. Verwenden Sie das Taskplaner-Snap-in, um sicherzustellen, dass ihre Aufgaben ordnungsgemäß konfiguriert sind

### <a name="event-4868-unable_to_start_autologger"></a>Ereignis 4868: UNABLE_TO_START_AUTOLOGGER

Clusterdienst Fehler beim Starten der Ablauf Verfolgungs Sitzung für das Cluster Protokoll. Fehlercode: "%2". Der Cluster funktioniert ordnungsgemäß, aber zusätzliche Protokollierungs Informationen fehlen. Verwenden Sie das Snap-in "System Monitor", um die Ereignis Kanaleinstellungen für "%1" zu überprüfen.

### <a name="event-4869-netft_watchdog_process_hung"></a>Ereignis 4869: NETFT_WATCHDOG_PROCESS_HUNG

Die Integritäts Überwachung im Benutzermodus hat festgestellt, dass das System nicht reagiert. Der virtuelle Adapter des Failoverclusters hat die Verbindung mit dem Prozess "%1" mit der Prozess-ID "%2" für "%3" Sekunden verloren. Verwenden Sie den System Monitor, um die Integrität des Systems zu evaluieren und zu bestimmen, welcher Prozess sich negativ auf das System auswirkt.

### <a name="event-4870-netft_watchdog_process_terminated"></a>Ereignis 4870: NETFT_WATCHDOG_PROCESS_TERMINATED

Die Integritäts Überwachung im Benutzermodus hat festgestellt, dass das System nicht reagiert. Der virtuelle Adapter des Failoverclusters hat die Verbindung mit dem Prozess "%1" mit der Prozess-ID "%2" für "%3" Sekunden verloren. Wiederherstellungs Aktion wird durchgeführt.

### <a name="event-4871-netft_miniport_initialization_failure"></a>Ereignis 4871: NETFT_MINIPORT_INITIALIZATION_FAILURE

Der Cluster Dienst konnte nicht gestartet werden. Dies war darauf zurückzuführen, dass der virtuelle Adapter des Failoverclusters den Mini Port-Adapter nicht initialisieren konnte. Fehlercode: ' %1 '. Vergewissern Sie sich, dass andere Netzwerkadapter ordnungsgemäß funktionieren, und überprüfen Sie den Geräte-Manager auf Fehler. Wenn die Konfiguration geändert wurde, muss ggf. die Failoverclustering-Funktion auf diesem Computer neu installiert werden.

### <a name="event-4872-netft_missing_datalink_address"></a>Ereignis 4872: NETFT_MISSING_DATALINK_ADDRESS

Der virtuelle Adapter des Failoverclusters konnte keine eindeutige MAC-Adresse generieren.
Entweder konnte kein physischer Ethernet-Adapter gefunden werden, von dem eine eindeutige Adresse generiert werden soll, oder die generierte Adresse steht in Konflikt mit einem anderen Adapter auf diesem Computer. Führen Sie den Konfigurationsüberprüfungs-Assistenten aus, um die Netzwerkkonfiguration zu überprüfen.

### <a name="event-5122-dcm_event_root_creation_failed"></a>Ereignis 5122: DCM_EVENT_ROOT_CREATION_FAILED

Fehler beim Erstellen des Stamm Verzeichnisses "%2" für freigegebene Clustervolumes Clusterdienst.
Fehlermeldung: ' %1 '.

### <a name="event-5142-dcm_volume_no_access"></a>Ereignis 5142: DCM_VOLUME_NO_ACCESS

Auf Freigegebenes Clustervolume ' %1 ' (' %2 ') kann aufgrund des Fehlers ' %3 ' von diesem Cluster Knoten aus nicht mehr zugegriffen werden. Beheben Sie die Probleme dieser Knoten mit dem Speichergerät und der Netzwerk Konnektivität.

### <a name="event-5143-dcm_veto_resource_move_due_to_cc"></a>Ereignis 5143: DCM_VETO_RESOURCE_MOVE_DUE_TO_CC

Das Verschieben des Datenträgers ("%2") wird basierend auf dem aktuellen Status des Cache-Managers auf dem Knoten "%1" geprüft, um einen potenziellen Deadlock zu verhindern. "Cache Manager Dirty Pages theshold" ist "%3", und "Cache Manager Dirty Pages" ist "%4". Der Verschiebe Vorgang ist zulässig, wenn "geänderte Seiten des Cache-Managers" kleiner als 70% der "Cache-Manager-Änderungs Seiten theshold" ist oder wenn "Cache-Manager-Änderungs Seiten theshold" abzüglich "Cache-Manager-geänderte Seiten" größer als 128000 Seiten ist (etwa 500 MB, wenn eine Seitengröße 4096 Bytes beträgt).
Der Cluster hat eine Ressourcen Verschiebung durchführen, um einen potenziellen Deadlock aufgrund von Cache-Manager-Drosselung gepufferten Schreibvorgängen zu verhindern, während freigegebene Clustervolumes auf diesem Datenträger angehalten werden

### <a name="event-5144-dcm_snapshot_diff_area_failure"></a>Ereignis 5144: DCM_SNAPSHOT_DIFF_AREA_FAILURE

Beim Hinzufügen des Datenträgers ("%1") zu freigegebenen Clustervolumes ist das Festlegen der expliziten momentaufnahmenvergleichs-Bereichs Zuordnung für Volume ("%2") mit Fehler "%3" fehlgeschlagen. Die einzige unterstützte Software Momentaufnahme-diff-Bereichs Zuordnung für freigegebene Clustervolumes ist selbst.

### <a name="event-5145-dcm_snapshot_diff_area_delete_failure"></a>Ereignis 5145: DCM_SNAPSHOT_DIFF_AREA_DELETE_FAILURE

Von der Cluster Datenträger Ressource "%1" konnte eine Software Momentaufnahme nicht gelöscht werden. Der diff-Bereich auf Volume "%3" konnte nicht von Volume "%2" getrennt werden. Dies kann auf aktive Momentaufnahmen zurückzuführen sein. Für freigegebene Clustervolumes muss sich die Software Momentaufnahme auf demselben Datenträger befinden.

### <a name="event-5146-dcm_veto_resource_move_due_to_dismount"></a>Ereignis 5146: DCM_VETO_RESOURCE_MOVE_DUE_TO_DISMOUNT

Das Verschieben der freigegebenes Clustervolume Ressource "%1" wurde aufgehoben, da eines der Volumes, die zur Ressource gehören, nicht bereitgestellt wurde. Wiederholen Sie die Aktion, nachdem der Vorgang zum Aufheben der Bereitstellung abgeschlossen ist.

### <a name="event-5147-dcm_veto_resource_move_due_to_snapshot"></a>Ereignis 5147: DCM_VETO_RESOURCE_MOVE_DUE_TO_SNAPSHOT

Das Verschieben der freigegebenes Clustervolume Ressource "%1" wurde aufgehoben, da eines der Volumes, die zur Ressource gehören, nicht bereitgestellt wurde. Wiederholen Sie die Aktion, nachdem der Vorgang zum Aufheben der Bereitstellung abgeschlossen ist.

### <a name="event-5148-dcm_veto_resource_move_due_to_io_mode_change"></a>Ereignis 5148: DCM_VETO_RESOURCE_MOVE_DUE_TO_IO_MODE_CHANGE

Der Verschiebe Vorgang der freigegebenes Clustervolume Ressource "%1" wurde aufgehoben, da ein Änderungs Vorgang für den IO-Modus (direkte e/a-Vorgänge an umgeleitete e/a oder umgekehrt) auf einem der Volumes, die zur Ressource gehören, ausgeführt wird. Wiederholen Sie die Aktion, nachdem der Vorgang abgeschlossen wurde.

### <a name="event-5150-dcm_set_resource_in_failed_state"></a>Ereignis 5150: DCM_SET_RESOURCE_IN_FAILED_STATE

Fehler bei der physischen Datenträger Ressource "%1" für den Cluster. Der freigegebenes Clustervolume wurde mit folgendem Fehler in den Status "Fehler" versetzt: "%2"

### <a name="event-5200-cam_cannot_create_cno_token"></a>Ereignis 5200: CAM_CANNOT_CREATE_CNO_TOKEN

Clusterdienst konnte kein Cluster Identitäts Token für freigegebene Clustervolumes erstellen. Fehlercode: ' %1 '. Stellen Sie sicher, dass auf den Domänen Controller zugegriffen werden kann, und überprüfen Sie Bis die Verbindung zum Domänen Controller wieder hergestellt ist, können einige Vorgänge auf diesem Knoten mit den freigegebenen Clustervolumes fehlschlagen.

### <a name="event-5216-csv_sw_snapshot_failed"></a>Ereignis 5216: CSV_SW_SNAPSHOT_FAILED

Fehler bei der Erstellung von Software Momentaufnahmen auf Freigegebenes Clustervolume "%1" ("%2") mit Fehler "%3". Die Ressource muss online sein, um die Momentaufnahme Erstellung zu unterstützen. Überprüfen Sie den Zustand der Ressource.

### <a name="event-5217-csv_sw_snapshot_set_failed"></a>Ereignis 5217: CSV_SW_SNAPSHOT_SET_FAILED

Fehler beim Erstellen von Software Momentaufnahmen auf den freigegebenes Clustervolume ("%1") mit der Momentaufnahme Satz-ID "%2". Fehler: "%3". Überprüfen Sie den Status der CSV-Ressourcen und der Systemereignisse der Ressourcen Besitzer Knoten.

### <a name="event-5219-csv_register_snapshot_prov_with_vss_failed"></a>Ereignis 5219: CSV_REGISTER_SNAPSHOT_PROV_WITH_VSS_FAILED

Clusterdienst konnte den Momentaufnahme Anbieter für freigegebene Clustervolumes nicht mit dem volumeschattendienst (VSS) registrieren. Dies kann darauf zurückzuführen sein, dass der VSS-Dienst heruntergefahren wird oder dass ein Problem mit dem VSS-Dienst vorliegt, bei dem es nicht möglich ist, eingehende Anforderungen zu akzeptieren. <br>Fehler: %1

### <a name="event-5377-operation_exceeded_timeout"></a>Ereignis 5377: OPERATION_EXCEEDED_TIMEOUT

Ein interner Clusterdienst Vorgang hat den definierten Schwellenwert von "%2" Sekunden überschritten. Die Clusterdienst wurde beendet, um wieder hergestellt zu werden. Der Dienststeuerungs-Manager startet den Clusterdienst neu, und der Knoten wird dem Cluster erneut hinzugefügt.

### <a name="event-5396-two_partitions_have_quorum"></a>Ereignis 5396: TWO_PARTITIONS_HAVE_QUORUM

Die Clusterdienst auf diesem Knoten wird heruntergefahren, da erkannt wurde, dass andere Cluster Knoten vorhanden sind, die über ein Quorum verfügen. Dies tritt auf, wenn der Clusterdienst einen anderen Knoten erkennt, der mit dem Force-Quorum-Schalter (/FQ) gestartet wurde. Der Knoten, der mit dem Schalter Erzwingen des Quorums gestartet wurde, wird weiterhin ausgeführt. Überprüfen Sie mit Failovercluster-Manager, ob dieser Knoten beim Neustart des Cluster Dienstanbieter automatisch dem Cluster hinzugefügt wurde.

### <a name="event-5397-rlua_account_failed"></a>Ereignis 5397: RLUA_ACCOUNT_FAILED

Von der Cluster Ressource "%1" konnte das replizierte lokale Benutzerkonto "%2" auf diesem Knoten nicht erstellt oder geändert werden. Weitere Informationen finden Sie in den Cluster Protokollen.

### <a name="event-5398-nm_event_cluster_failed_to_form"></a>Ereignis 5398: NM_EVENT_CLUSTER_FAILED_TO_FORM

Der Cluster konnte nicht gestartet werden. Die neueste Kopie der Cluster Konfigurationsdaten war innerhalb der Gruppe von Knoten, die versuchen, den Cluster zu starten, nicht verfügbar. Änderungen am Cluster sind aufgetreten, während die Gruppe der Knoten nicht Mitglied der Mitgliedschaft war und daher nicht in der Lage war, Konfigurationsdaten Aktualisierungen zu empfangen. .<br><br>Zum Starten des Clusters erforderliche Stimmen: %1<br>Verfügbare Stimmen: %2<br>Knoten mit Stimmen: %3

#### <a name="guidance"></a>Leitfaden

Versuchen Sie, den Cluster Dienst auf allen Knoten im Cluster zu starten, damit Knoten mit der neuesten Kopie der Cluster Konfigurationsdaten zuerst den Cluster bilden können. Der Cluster kann gestartet werden, und die Knoten erhalten automatisch die aktualisierten Cluster Konfigurationsdaten. Wenn keine Knoten mit der neuesten Kopie der Cluster Konfigurationsdaten verfügbar sind, führen Sie das Windows PowerShell-Cmdlet "Start-clusternode-f" aus. Mithilfe des ForceQuorum (FQ)-Parameters wird der Cluster Dienst gestartet, und die Kopie der Cluster Konfigurationsdaten dieses Knotens wird als autorisierend gekennzeichnet. Das Erzwingen des Quorums auf einem Knoten mit einer veralteten Kopie der Cluster Datenbank führt möglicherweise zu Änderungen an der Cluster Konfiguration, die aufgetreten sind, während der Knoten nicht an dem Cluster beteiligt war.

## <a name="warning-events"></a>Warnungs Ereignisse

### <a name="event-1011-nm_node_evicted"></a>Ereignis 1011: NM_NODE_EVICTED

Der Cluster Knoten "%1" wurde aus dem Failovercluster entfernt.

### <a name="event-1045-res_ipaddr_ipv4_address_create_failed"></a>Ereignis 1045: RES_IPADDR_IPV4_ADDRESS_CREATE_FAILED

Es wurde keine übereinstimmende Netzwerkschnittstelle für die IP-Adresse "%2" der Ressource "%1" gefunden (Rückgabecode war "%3"). Wenn sich Ihre Cluster Knoten in verschiedenen Subnetzen befinden, kann dies normal sein.

### <a name="event-1066-res_disk_corrupt_disk"></a>Ereignis 1066: RES_DISK_CORRUPT_DISK

Die Cluster Datenträger Ressource "%1" weist auf eine Beschädigung für Volume "%2" hin. Chkdsk wird ausgeführt, um Probleme zu beheben. Der Datenträger ist erst dann verfügbar, wenn Chkdsk abgeschlossen ist.
Die CHKDSK-Ausgabe wird in der Datei "%3" protokolliert.<br> CHKDSK kann auch Informationen in das Anwendungs Ereignisprotokoll schreiben.

### <a name="event-1068-res_smb_share_cant_add"></a>Ereignis 1068: RES_SMB_SHARE_CANT_ADD

Die Cluster Dateifreigabe-Ressource "%1" kann nicht online geschaltet werden. Fehler beim Erstellen der Dateifreigabe "%2" (für den Netzwerknamen "%3" festgelegt) aufgrund des Fehlers "%4". Dieser Vorgang wird automatisch wiederholt.

### <a name="event-1071-rcm_resource_online_blocked_by_locked_mode"></a>Ereignis 1071: RCM_RESOURCE_ONLINE_BLOCKED_BY_LOCKED_MODE

Der Vorgang für die Cluster Ressource "%1" vom Typ "%3" in der Cluster Rolle "%2" konnte nicht abgeschlossen werden, da die Ressource oder einer ihrer Anbieter den gesperrten Status aufweist.

### <a name="event-1071-rcm_resource_offline_blocked_by_locked_mode"></a>Ereignis 1071: RCM_RESOURCE_OFFLINE_BLOCKED_BY_LOCKED_MODE

Der Vorgang für die Cluster Ressource "%1" vom Typ "%3" in der Cluster Rolle "%2" konnte nicht abgeschlossen werden, da die Ressource oder eine ihrer abhängigen Elemente den Status "gesperrt" aufweist.

### <a name="event-1094-sm_invalid_security_level"></a>Ereignis 1094: SM_INVALID_SECURITY_LEVEL

Die "SecurityLevel"-Eigenschaft des Clusters kann in diesem Cluster nicht geändert werden. Die Sicherheitsstufe des Clusters kann nicht geändert werden, da der Cluster derzeit für keinen Authentifizierungsmodus konfiguriert ist.

### <a name="event-1119-res_netname_dns_registration_missing"></a>Ereignis 1119: RES_NETNAME_DNS_REGISTRATION_MISSING

Die Cluster Netzwerk-namens Ressource "%1" konnte den DNS-Namen "%2" für den Adapter "%4" aus folgendem Grund nicht registrieren: <br><br>"%3"

### <a name="event-1125-tm_event_cluster_netinterface_unreachable"></a>Ereignis 1125: TM_EVENT_CLUSTER_NETINTERFACE_UNREACHABLE

Die Cluster Netzwerkschnittstelle "%1" für Cluster Knoten "%2" im Netzwerk "%3" kann nicht von mindestens einem anderen Cluster Knoten, der mit dem Netzwerk verbunden ist, erreicht werden. Der Speicherort des Fehlers konnte vom Failovercluster nicht bestimmt werden. Führen Sie den Konfigurationsüberprüfungs-Assistenten aus, um die Netzwerkkonfiguration zu überprüfen. Wenn die Bedingung weiterhin besteht, prüfen Sie, ob Hardware-oder Softwarefehler im Zusammenhang mit dem Netzwerkadapter vorliegen. Überprüfen Sie auch, ob in anderen Netzwerkkomponenten, mit denen der Knoten verbunden ist, wie z. b. Hubs, Switches oder Bridges, auf Fehler.

### <a name="event-1149-res_netname_cant_delete_dns_records"></a>Ereignis 1149: RES_NETNAME_CANT_DELETE_DNS_RECORDS

Die der Cluster Ressource "%1" zugeordneten DNS-Host Einträge (A) und Zeiger (PTR)-Einträge wurden nicht aus dem zugeordneten DNS-Server der Ressource entfernt. Gegebenenfalls können Sie manuell gelöscht werden. Wenden Sie sich an Ihren DNS-Administrator, um Unterstützung bei diesem Aufwand

### <a name="event-1150-res_netname_dns_ptr_record_delete_failed"></a>Ereignis 1150: RES_NETNAME_DNS_PTR_RECORD_DELETE_FAILED

Fehler beim Entfernen des DNS-Zeiger (PTR)-Datensatzes "%2" für den Host "%3", der der Cluster-Netzwerknamen Ressource "%1" zugeordnet ist. Fehler: "%4".
Der Datensatz kann ggf. manuell gelöscht werden. Bitten Sie den DNS-Administrator um Unterstützung.

### <a name="event-1151-res_netname_dns_a_record_delete_failed"></a>Ereignis 1151: RES_NETNAME_DNS_A_RECORD_DELETE_FAILED

Fehler beim Entfernen des DNS-Host (A)-Datensatzes "%2", der der Cluster-Netzwerknamen Ressource "%1" zugeordnet ist. Fehler: "%3". Der Datensatz kann ggf. manuell gelöscht werden. Bitten Sie den DNS-Administrator um Unterstützung.

### <a name="event-1155-rcm_event_exited_queuing"></a>Ereignis 1155: RCM_EVENT_EXITED_QUEUING

Die ausstehende Verschiebung für die Rolle "%1" wurde nicht abgeschlossen.

### <a name="event-1197-res_netname_delete_disable_failed"></a>Ereignis 1197: RES_NETNAME_DELETE_DISABLE_FAILED

Die Cluster Netzwerk-namens Ressource "%1" konnte das zugehörige Computer Objekt "%2" beim Löschen von Ressourcen nicht löschen oder deaktivieren. Fehlercode: ' %3 '. <br>Überprüfen Sie, ob der Standort schreibgeschützt ist. Stellen Sie sicher, dass das Cluster Namen Objekt über die entsprechenden Berechtigungen für das Objekt "%2" in Active Directory verfügt.

### <a name="event-1198-res_netname_delete_vco_guid_failed"></a>Ereignis 1198: RES_NETNAME_DELETE_VCO_GUID_FAILED

Die Cluster Netzwerk-namens Ressource "%1" konnte das Computer Objekt mit der GUID "%2" nicht löschen. Fehlercode: ' %3 '. <br>Überprüfen Sie, ob der Standort schreibgeschützt ist. Stellen Sie sicher, dass das Cluster Namen Objekt über die entsprechenden Berechtigungen für das Objekt "%2" in Active Directory verfügt.

### <a name="event-1216-service_netname_change_warning"></a>Ereignis 1216: SERVICE_NETNAME_CHANGE_WARNING

Fehler bei einem namens Änderungs Vorgang für die Cluster Core NetName-Ressource.
Bei dem Versuch, den namens Änderungs Vorgang auf den ursprünglichen Namen zurückzusetzen, ist ebenfalls ein Fehler aufgetreten. Fehlercode: ' %1 '. Sie sind möglicherweise nicht in der Lage, den Cluster mithilfe des Cluster namens Remote zu verwalten, bis diese Situation manuell korrigiert wurde.

### <a name="event-1221-res_netname_rename_out_of_synch_with_compobj"></a>Ereignis 1221: RES_NETNAME_RENAME_OUT_OF_SYNCH_WITH_COMPOBJ

Die Cluster Netzwerk-namens Ressource "%1" weist den Namen "%2" auf, der nicht mit dem entsprechenden Computer Objektnamen "%3" übereinstimmt. Es ist wahrscheinlich, dass eine vorherige Namensänderung des Computer Objekts nicht auf allen Domänen Controllern in der Domäne repliziert wurde. Sie können die Netzwerknamen Ressource erst umbenennen, wenn die Namen konsistent werden. Wenn das Computer Objekt nicht vor kurzem geändert wurde, wenden Sie sich an Ihren Domänen Administrator, um das Computer Objekt umzubenennen und damit konsistent zu machen. Stellen Sie außerdem sicher, dass die Replikation über Domänen Controller hinweg erfolgreich abgeschlossen wurde.

### <a name="event-1222-res_netname_set_permissions_failed"></a>Ereignis 1222: RES_NETNAME_SET_PERMISSIONS_FAILED

Das der Cluster Netzwerk-namens Ressource "%1" zugeordnete Computer Objekt konnte nicht aktualisiert werden.<br><br>Der Text für den zugeordneten Fehlercode lautet: %2<br> <br>Der Cluster Identität "%3" fehlen möglicherweise die erforderlichen Berechtigungen zum Aktualisieren des Objekts. Wenden Sie sich an Ihren Domänen Administrator, um sicherzustellen, dass die Cluster Identität Computer Objekte in der Domäne aktualisieren kann.

### <a name="event-1240-res_ipaddr_obtain_lease_failed"></a>Ereignis 1240: RES_IPADDR_OBTAIN_LEASE_FAILED

Die Cluster-IP-Adress Ressource "%1" konnte keine geleast-IP-Adresse abrufen.

### <a name="event-1243-res_ipaddr_release_lease_failed"></a>Ereignis 1243: RES_IPADDR_RELEASE_LEASE_FAILED

Die Cluster-IP-Adress Ressource "%1" konnte die Lease für die IP-Adresse "%2" nicht freigeben.

### <a name="event-1251-rcm_group_preempted"></a>Ereignis 1251: RCM_GROUP_PREEMPTED

Die Cluster Rolle "%2" wurde offline geschaltet. Diese Rolle wurde von der gruppierten Rolle "%1" mit höherer Priorität vorzeitig entfernt. Der Cluster Dienst versucht, die Cluster Rolle "%2" zu einem späteren Zeitpunkt online zu schalten, wenn Systemressourcen verfügbar sind.

### <a name="event-1544-service_vss_onabort"></a>Ereignis 1544: SERVICE_VSS_ONABORT

Der Sicherungs Vorgang für die Cluster Konfigurationsdaten wurde abgebrochen. Der VSS-Writer (Cluster Volumeschattenkopie-Dienst) hat eine Abbruch Anforderung empfangen.

### <a name="event-1548-service_connect_version_compatible"></a>Ereignis 1548: SERVICE_CONNECT_VERSION_COMPATIBLE

Knoten "%1" hat die Kommunikation mit dem Knoten "%2" hergestellt und erkannt, dass eine andere, aber kompatible Version des Betriebssystems ausgeführt wird. Es wird empfohlen, dass alle Knoten die gleiche Version des Betriebssystems ausführen. Nachdem alle Knoten aktualisiert wurden, führen Sie das Windows PowerShell-Cmdlet Update-clusterfunctionallevel aus, um das Upgrade des Clusters abzuschließen.

### <a name="event-1550-service_connect_novercheck"></a>Ereignis 1550: SERVICE_CONNECT_NOVERCHECK

Knoten "%1" hat eine Kommunikationssitzung mit dem Knoten "%2" erstellt, ohne dass eine Versions Kompatibilitätsprüfung durchgeführt wurde, da die Versions Kompatibilitäts Überprüfung deaktiviert ist. Die Deaktivierung der Versions Kompatibilitäts Überprüfung wird nicht unterstützt.

### <a name="event-1551-service_form_novercheck"></a>Ereignis 1551: SERVICE_FORM_NOVERCHECK

Knoten "%1" hat einen Failovercluster ohne Versions Kompatibilitätsprüfung erstellt, da die Überprüfung der Versions Kompatibilität deaktiviert ist. Die Deaktivierung der Versions Kompatibilitäts Überprüfung wird nicht unterstützt.

### <a name="event-1555-service_netft_disable_autoconfig_failed"></a>Ereignis 1555: SERVICE_NETFT_DISABLE_AUTOCONFIG_FAILED

Fehler beim Versuch, IPv4 für den Netzwerkadapter "%1" zu verwenden. Dies war darauf zurückzuführen, dass die automatische IPv4-Konfiguration und DHCP nicht deaktiviert wurden. Dies wird möglicherweise erwartet, wenn der DHCP-Client Dienst bereits deaktiviert ist. Wenn diese Option aktiviert ist, wird IPv6 verwendet. andernfalls ist dieser Knoten möglicherweise nicht in der Lage, an einem Failovercluster teilzunehmen.

### <a name="event-1558-service_witness_failover_attempt"></a>Ereignis 1558: SERVICE_WITNESS_FAILOVER_ATTEMPT

Der Cluster Dienst hat ein Problem mit der Zeugen Ressource festgestellt. Für die Zeugen Ressource wird ein Failover zu einem anderen Knoten im Cluster durchgeführt, wenn versucht wird, den Zugriff auf die Cluster Konfigurationsdaten wiederherzustellen.

### <a name="event-1562-res_fsw_alivefailure"></a>Ereignis 1562: RES_FSW_ALIVEFAILURE

Die Dateifreigabe-Zeugen Ressource "%1" hat eine regelmäßige Integritäts Überprüfung für die Dateifreigabe "%2" nicht bestanden. Stellen Sie sicher, dass die Dateifreigabe "%2" vorhanden ist und dass der Cluster darauf zugreifen kann.

### <a name="event-1576-res_netname_dns_registration_secure_zone_refused"></a>Ereignis 1576: RES_NETNAME_DNS_REGISTRATION_SECURE_ZONE_REFUSED

Die Cluster Netzwerk-namens Ressource "%1" konnte den Namen "%2" für den Adapter "%4" in einer sicheren DNS-Zone nicht registrieren. Dies war auf einen vorhandenen Datensatz mit diesem Namen zurückzuführen, und die Cluster Identität verfügt nicht über ausreichende Berechtigungen zum Aktualisieren dieses Datensatzes. Fehlercode: ' %3 '. Wenden Sie sich an den DNS-Server Administrator, um zu überprüfen, ob die Cluster Identität über Berechtigungen für den DNS-Datensatz "%2

### <a name="event-1576-res_netname_dns_registration_secure_zone_refused"></a>Ereignis 1576: RES_NETNAME_DNS_REGISTRATION_SECURE_ZONE_REFUSED

Die Cluster Netzwerk-namens Ressource "%1" konnte den Namen "%2" für den Adapter "%4" in einer sicheren DNS-Zone nicht registrieren. Dies war auf einen vorhandenen Datensatz mit diesem Namen zurückzuführen, und die Cluster Identität verfügt nicht über ausreichende Berechtigungen zum Aktualisieren dieses Datensatzes. Fehlercode: ' %3 '. Wenden Sie sich an den DNS-Server Administrator, um zu überprüfen, ob die Cluster Identität über Berechtigungen für den DNS-Datensatz "%2

### <a name="event-1577-res_netname_dns_server_could_not_be_contacted"></a>Ereignis 1577: RES_NETNAME_DNS_SERVER_COULD_NOT_BE_CONTACTED

Fehler beim Registrieren des Namens "%2" für den Adapter "%4" durch die Cluster Netzwerk-namens Ressource "%1". Der DNS-Server konnte nicht kontaktiert werden. Fehlercode: "%3". Stellen Sie sicher, dass über diesen Cluster Knoten auf einen DNS-Server zugegriffen werden kann. Die DNS-Registrierung wird später erneut versucht.

### <a name="event-1577-res_netname_dns_server_could_not_be_contacted"></a>Ereignis 1577: RES_NETNAME_DNS_SERVER_COULD_NOT_BE_CONTACTED

Fehler beim Registrieren des Namens "%2" für den Adapter "%4" durch die Cluster Netzwerk-namens Ressource "%1". Der DNS-Server konnte nicht kontaktiert werden. Fehlercode: "%3". Stellen Sie sicher, dass über diesen Cluster Knoten auf einen DNS-Server zugegriffen werden kann. Die DNS-Registrierung wird später erneut versucht.

### <a name="event-1578-res_netname_dns_test_for_dynamic_update_failed"></a>Ereignis 1578: RES_NETNAME_DNS_TEST_FOR_DYNAMIC_UPDATE_FAILED

Die Cluster Netzwerk-namens Ressource "%1" konnte die dynamischen Updates für den Namen "%2" über den Adapter "%4" nicht registrieren. Der DNS-Server ist möglicherweise nicht für das akzeptieren dynamischer Updates konfiguriert. Fehlercode: ' %3 '. Wenden Sie sich an den DNS-Server Administrator, um zu überprüfen, ob der DNS-Server verfügbar und für dynamische Updates konfiguriert ist.<br><br>Alternativ können Sie dynamische DNS-Updates deaktivieren, indem Sie die Einstellung "Adressen dieser Verbindung in DNS registrieren" in den erweiterten TCP/IP-Einstellungen für den Adapter "%4" auf der Registerkarte "DNS" deaktivieren.

### <a name="event-1578-res_netname_dns_test_for_dynamic_update_failed"></a>Ereignis 1578: RES_NETNAME_DNS_TEST_FOR_DYNAMIC_UPDATE_FAILED

Die Cluster Netzwerk-namens Ressource "%1" konnte die dynamischen Updates für den Namen "%2" über den Adapter "%4" nicht registrieren. Der DNS-Server ist möglicherweise nicht für das akzeptieren dynamischer Updates konfiguriert. Fehlercode: ' %3 '. Wenden Sie sich an den DNS-Server Administrator, um zu überprüfen, ob der DNS-Server verfügbar und für dynamische Updates konfiguriert ist.<br><br>Alternativ können Sie dynamische DNS-Updates deaktivieren, indem Sie die Einstellung "Adressen dieser Verbindung in DNS registrieren" in den erweiterten TCP/IP-Einstellungen für den Adapter "%4" auf der Registerkarte "DNS" deaktivieren.

### <a name="event-1579-res_netname_dns_record_update_failed"></a>Ereignis 1579: RES_NETNAME_DNS_RECORD_UPDATE_FAILED

Die Cluster Netzwerk-namens Ressource "%1" konnte den DNS-Datensatz für den Namen "%2" über den Adapter "%4" nicht aktualisieren. Fehlercode: ' %3 '. Stellen Sie sicher, dass auf einen DNS-Server von diesem Cluster Knoten aus zugegriffen werden kann, und wenden Sie sich an den DNS-Server Administrator, um zu überprüfen, ob die Cluster Identität den DNS-Datensatz

### <a name="event-1579-res_netname_dns_record_update_failed"></a>Ereignis 1579: RES_NETNAME_DNS_RECORD_UPDATE_FAILED

Die Cluster Netzwerk-namens Ressource "%1" konnte den DNS-Datensatz für den Namen "%2" über den Adapter "%4" nicht aktualisieren. Fehlercode: ' %3 '. Stellen Sie sicher, dass auf einen DNS-Server von diesem Cluster Knoten aus zugegriffen werden kann, und wenden Sie sich an den DNS-Server Administrator, um zu überprüfen, ob die Cluster Identität den DNS-Datensatz

### <a name="event-1581-clussvc_unable_to_move_hive_to_safe_file"></a>Ereignis 1581: CLUSSVC_UNABLE_TO_MOVE_HIVE_TO_SAFE_FILE

Die Wiederherstellungs Anforderung für die Cluster Konfigurationsdaten konnte keine Kopie der vorhandenen Cluster Konfigurationsdatendatei (CLUSDB) erstellen. Beim Versuch, die vorhandene Konfiguration beizubehalten, konnte der Wiederherstellungs Vorgang eine Kopie am Speicherort "%1" nicht erstellen. Dies wird möglicherweise erwartet, wenn die vorhandene Konfigurations Datendatei beschädigt ist. Der Wiederherstellungs Vorgang wurde fortgesetzt. es ist jedoch möglich, dass versucht wird, die vorhandene Cluster Konfiguration wiederherzustellen.

### <a name="event-1582-clussvc_unable_to_move_restored_hive_to_current"></a>Ereignis 1582: CLUSSVC_UNABLE_TO_MOVE_RESTORED_HIVE_TO_CURRENT

Der Cluster Dienst konnte die wiederhergestellte Cluster Struktur bei "%1" nicht nach "%2" verschieben. Dadurch wird möglicherweise verhindert, dass der Wiederherstellungs Vorgang erfolgreich ausgeführt wird. Wenn die Cluster Konfiguration nicht ordnungsgemäß wieder hergestellt wurde, wiederholen Sie den Wiederherstellungs Vorgang.

### <a name="event-1583-clussvc_netft_disable_connectionsecurity_failed"></a>Ereignis 1583: CLUSSVC_NETFT_DISABLE_CONNECTIONSECURITY_FAILED

Clusterdienst konnte die Internet Protokoll Sicherheit (IPSec) auf dem virtuellen failoverclusteradapter "%1" nicht deaktivieren. Dies kann sich negativ auf die Leistung der Cluster Kommunikation auswirken. Wenn dieses Problem weiterhin besteht, überprüfen Sie die Sicherheitsrichtlinien für lokale und Domänen Verbindungen, die auf IPSec und die Windows-Firewall angewendet werden. Überprüfen Sie außerdem, ob Ereignisse im Zusammenhang mit dem Basis Filtermodul-Dienst angezeigt werden.

### <a name="event-1584-shared_volume_not_ready_for_snapshot"></a>Ereignis 1584: SHARED_VOLUME_NOT_READY_FOR_SNAPSHOT

Eine Sicherungs Anwendung hat eine VSS-Momentaufnahme auf Freigegebenes Clustervolume "%1" ("%3") initiiert, ohne dass das Volume für die Momentaufnahme ordnungsgemäß vorbereitet wurde. Diese Momentaufnahme ist möglicherweise ungültig, und die Sicherung kann möglicherweise nicht für Wiederherstellungs Vorgänge verwendet werden. Wenden Sie sich an Ihren Anbieter für die Sicherungs Anwendung, um die Kompatibilität mit freigegebenen Clustervolumes

### <a name="event-1589-res_netname_dns_returning_ip_that_is_not_provider"></a>Ereignis 1589: RES_NETNAME_DNS_RETURNING_IP_THAT_IS_NOT_PROVIDER

Die Cluster Netzwerk-namens Ressource "%1" hat mindestens eine IP-Adresse gefunden, die dem DNS-Namen "%2" zugeordnet ist, die keine abhängigen IP-Adress Ressourcen sind. Die gefundenen zusätzlichen Adressen waren "%3". Dies wirkt sich möglicherweise auf die Client Konnektivität aus, bis der Netzwerkname und die zugehörigen DNS-Einträge konsistent sind. Wenden Sie sich an den DNS-Server Administrator, um die dem Namen "%2" zugeordneten Datensätze zu überprüfen

### <a name="event-1604-res_disk_chkdsk_spotfix_needed"></a>Ereignis 1604: RES_DISK_CHKDSK_SPOTFIX_NEEDED

Die Cluster Datenträger Ressource "%1" hat eine Beschädigung für Volume "%2" erkannt. Zum Beheben von Problemen ist "spotfix Chkdsk" erforderlich.

### <a name="event-1605-res_disk_spotfix_performed"></a>Ereignis 1605: RES_DISK_SPOTFIX_PERFORMED

Die Cluster Datenträger Ressource "%1" wurde mit dem Ausführen ChkDsk.exe/spotfix auf Volume "%2" abgeschlossen.
Der Rückgabecode war "%4". Die Ausgabe von CHKDSK wurde in der Datei "%3" protokolliert.<br>
Überprüfen Sie das Anwendungs Ereignisprotokoll auf zusätzliche Informationen von Chkdsk.

### <a name="event-1671-res_disk_online_set_attributes_completed_failure"></a>Ereignis 1671: RES_DISK_ONLINE_SET_ATTRIBUTES_COMPLETED_FAILURE

Die physische Datenträger Ressource des Clusters kann nicht online geschaltet werden.<br><br>Name der physischen Datenträger Ressource: %1<br>Fehler Code: %2<br>Verstrichene Zeit (Sekunden): %3

#### <a name="guidance"></a>Leitfaden

Führen Sie den Konfigurationsüberprüfungs-Assistenten aus, um die Speicherkonfiguration zu überprüfen. Wenn der Fehlercode ERROR_CLUSTER_SHUTDOWN wurde, wurde der ausstehende Online Status von einem Administrator abgebrochen. Wenn es sich um ein repliziertes Volume handelt, könnte dies das Ergebnis eines Fehlers beim Festlegen der Datenträger Attribute sein. Überprüfen Sie die Speicher Replikations Ereignisse auf Weitere Informationen.

### <a name="event-1673-cluster_node_entered_isolated_state"></a>Ereignis 1673: CLUSTER_NODE_ENTERED_ISOLATED_STATE

Der Cluster Knoten "%1" wurde in den isolierten Zustand versetzt.

### <a name="event-1675-event_joining_node_quarantined"></a>Ereignis 1675: EVENT_JOINING_NODE_QUARANTINED

Der Cluster Knoten "%1" wurde von "%2" unter Quarantäne gestellt und kann nicht dem Cluster beitreten. Der Knoten wird bis "%3" unter Quarantäne gestellt, und anschließend versucht der Knoten automatisch, den Cluster erneut beizutreten. <br><br>Informationen zu den Problemen auf diesem Knoten finden Sie in den System-und Anwendungs Ereignisprotokollen. Wenn das Problem behoben ist, kann die Quarantäne manuell gelöscht werden, damit der Knoten mit dem Windows PowerShell-Cmdlet "Start-clusternode – clearquarantäne" erneut verknüpft werden kann.<br><br>Knoten Name: %1<br>Quarantinetype: Quarantäne durch %2<br>Die Zeit Quarantäne wird automatisch gelöscht: %3

### <a name="event-1681-cluster_groups_unmonitored_on_node"></a>Ereignis 1681: CLUSTER_GROUPS_UNMONITORED_ON_NODE

Die virtuellen Maschinen auf dem Knoten "%1" haben einen nicht überwachten Zustand. Die Integrität der virtuellen Computer wird erneut überwacht, sobald der Knoten von einem isolierten Status zurückkehrt oder ein Failover durchführt, wenn der Knoten nicht zurückkehrt. Der virtuelle Computer wird nicht mehr überwacht: %2.

### <a name="event-1689-event_disable_and_stop_other_service"></a>Ereignis 1689: EVENT_DISABLE_AND_STOP_OTHER_SERVICE

Der Cluster Dienst hat einen Dienst erkannt, der mit dem Failoverclustering nicht kompatibel ist. Der Dienst wurde deaktiviert, um mögliche Probleme mit dem Failovercluster zu vermeiden.<br><br>Dienst Name: "%1"

### <a name="event-4625-nodecleanup_reset_nlbsflags_preserved"></a>Ereignis 4625: NODECLEANUP_RESET_NLBSFLAGS_PRESERVED

Fehler beim Zurücksetzen des Registrierungs Werts für den IPSec-Sicherheits Zuordnungs Timeout während der Cluster Knoten Bereinigung. Dies liegt daran, dass das IPSec-Sicherheits Zuordnungs Timeout geändert wurde, nachdem dieser Computer als Mitglied eines Clusters konfiguriert wurde. Führen Sie für die manuelle Bereinigung das PowerShell-Cmdlet "Clear-clusternode" auf diesem Computer aus. Alternativ können Sie das IPSec-Sicherheits Zuordnungs Timeout zurücksetzen, indem Sie den Wert "%1" und den Wert "%2" aus HKEY_LOCAL_MACHINE in der Windows-Registrierung löschen.

### <a name="event-4873-netft_clussvc_terminate_because_of_watchdog"></a>Ereignis 4873: NETFT_CLUSSVC_TERMINATE_BECAUSE_OF_WATCHDOG

Der Cluster Dienst hat festgestellt, dass der virtuelle Adapter des Failoverclusters angehalten wurde. Dies wird erwartet, wenn die CPU-Auslastung auf diesem Knoten durchgeführt wird.
Clusterdienst wird beendet und sollte nach Abschluss des Vorgangs automatisch neu gestartet werden. Überprüfen Sie, ob dem Dienst weitere Ereignisse zugeordnet sind, und stellen Sie sicher, dass der Cluster Dienst auf diesem Knoten neu gestartet wurde.

### <a name="event-5120-dcm_volume_auto_pause_after_failure"></a>Ereignis 5120: DCM_VOLUME_AUTO_PAUSE_AFTER_FAILURE

Der freigegebenes Clustervolume "%1" ("%2") hat sich aufgrund von "%3" in einen angehaltenen Zustand versetzt.
Alle e/a-Vorgänge werden vorübergehend in die Warteschlange eingereiht, bis ein Pfad zum Volume wieder hergestellt wird.

### <a name="event-5123-dcm_event_root_rename_success"></a>Ereignis 5123: DCM_EVENT_ROOT_RENAME_SUCCESS

Das Stammverzeichnis "%1" für freigegebene Clustervolumes ist bereits vorhanden. Das Verzeichnis "%1" wurde in "%2" umbenannt. Vergewissern Sie sich, dass Anwendungen, die auf Daten an diesem Speicherort zugreifen, bei Bedarf aktualisiert wurden.

### <a name="event-5124-dcm_unsafe_filters_found"></a>Ereignis 5124: DCM_UNSAFE_FILTERS_FOUND

Freigegebenes Clustervolume "%1" ("%3") hat mindestens einen aktiven Filtertreiber auf diesem Geräte Stapel identifiziert, der die CSV-Vorgänge beeinträchtigen könnte. Der e/a-Zugriff wird über das Netzwerk über einen anderen Cluster Knoten an das Speichergerät umgeleitet. Dies kann zu einer Beeinträchtigung der Leistung führen. Wenden Sie sich an den Hersteller des Filter Treibers, um die Interoperabilität mit freigegebenen Clustervolumes <br><br>Aktive Filtertreiber gefunden:<br>%2

### <a name="event-5125-dcm_unsafe_volfilter_found"></a>Ereignis 5125: DCM_UNSAFE_VOLFILTER_FOUND

Freigegebenes Clustervolume "%1" ("%3") hat mindestens einen aktiven Volumetreiber in diesem Geräte Stapel identifiziert, der die CSV-Vorgänge beeinträchtigen könnte. Der e/a-Zugriff wird über das Netzwerk über einen anderen Cluster Knoten an das Speichergerät umgeleitet. Dies kann zu einer Beeinträchtigung der Leistung führen. Bitten Sie den volumetreiberhersteller, die Interoperabilität mit freigegebenen Clustervolumes zu überprüfen <br><br>Aktive Volumetreiber gefunden:<br>%2

### <a name="event-5126-dcm_event_cannot_disable_short_names"></a>Ereignis 5126: DCM_EVENT_CANNOT_DISABLE_SHORT_NAMES

Die physische Datenträger Ressource "%1" lässt keine Deaktivierung der Kurznamen Generierung zu. Dies kann zu Anwendungs Kompatibilitätsproblemen führen. Verwenden Sie "fsutil 8dot3name Set 2", um die Deaktivierung der Kurznamen Generierung zuzulassen und die Ressource dann offline/online zu schalten.

### <a name="event-5128-dcm_event_cannot_disable_short_names"></a>Ereignis 5128: DCM_EVENT_CANNOT_DISABLE_SHORT_NAMES

Die physische Datenträger Ressource "%1" lässt keine Deaktivierung der Kurznamen Generierung zu. Dies kann zu Anwendungs Kompatibilitätsproblemen führen. Verwenden Sie "fsutil 8dot3name Set 2", um die Deaktivierung der Kurznamen Generierung zuzulassen und die Ressource dann offline/online zu schalten.

### <a name="event-5133-dcm_cannot_restore_drive_letters"></a>Ereignis 5133: DCM_CANNOT_RESTORE_DRIVE_LETTERS

Der Cluster Datenträger "%1" wurde entfernt und in der Clustergruppe "verfügbarer Speicher" wieder abgelegt. Während dieses Vorgangs wurde der Versuch, den ursprünglichen Laufwerk Buchstaben wiederherzustellen, länger als erwartet benötigt, möglicherweise aufgrund der bereits verwendeten Laufwerksbuchstaben.

### <a name="event-5134-dcm_cannot_set_acl_on_root"></a>Ereignis 5134: DCM_CANNOT_SET_ACL_ON_ROOT

Clusterdienst Fehler beim Festlegen der Berechtigungen (ACL) für das Stammverzeichnis "%1" für freigegebene Clustervolumes. Fehler: "%2".

### <a name="event-5135-dcm_cannot_set_acl_on_volume_folder"></a>Ereignis 5135: DCM_CANNOT_SET_ACL_ON_VOLUME_FOLDER

Clusterdienst konnte die Berechtigungen für das freigegebenes Clustervolume Verzeichnis "%1" ("%2") nicht festlegen. Der Fehler lautet "%3".

### <a name="event-5136-dcm_csv_into_redirected_mode"></a>Ereignis 5136: DCM_CSV_INTO_REDIRECTED_MODE

Der umgeleitete Zugriff freigegebenes Clustervolume "%1" ("%2") wurde aktiviert. Der Zugriff auf das Speichergerät wird über das Netzwerk von allen Cluster Knoten umgeleitet, die auf dieses Volume zugreifen. Dies kann zu einer Beeinträchtigung der Leistung führen. Deaktivieren Sie den umgeleiteten Zugriff für dieses Volume, um den normalen Betrieb wieder aufzunehmen.

### <a name="event-5149-dcm_csv_block_cache_resized"></a>Ereignis 5149: DCM_CSV_BLOCK_CACHE_RESIZED

Die Größe der Cache Größe wurde auf Grundlage des gefüllten Speichers in "%1" geändert. der Benutzer "setSize" ist zu hoch.

### <a name="event-5156-dcm_volume_auto_pause_after_snapshot_failure"></a>Ereignis 5156: DCM_VOLUME_AUTO_PAUSE_AFTER_SNAPSHOT_FAILURE

Der freigegebenes Clustervolume "%1" ("%2") hat sich aufgrund von "%3" in einen angehaltenen Zustand versetzt.
Dieser Fehler wird angezeigt, wenn die Volsnap-Momentaufnahmen, die dem CSV-Volume zugrunde liegen, außerhalb einer Benutzer Anforderung gelöscht werden. Mögliche Ursachen dafür, dass die Momentaufnahmen gelöscht werden, sind nicht genügend Speicherplatz auf dem Volume, um die Momentaufnahmen zu vergrößern, oder e/a-Fehler beim Aktualisieren der Momentaufnahme Daten. Alle e/a-Vorgänge werden vorübergehend in die Warteschlange eingereiht, bis der Momentaufnahme Status mit Volsnap synchronisiert wird.

### <a name="event-5157-dcm_volume_auto_pause_after_failure_expected"></a>Ereignis 5157: DCM_VOLUME_AUTO_PAUSE_AFTER_FAILURE_EXPECTED

Der freigegebenes Clustervolume "%1" ("%2") hat sich aufgrund von "%3" in einen angehaltenen Zustand versetzt.
Alle e/a-Vorgänge werden vorübergehend in die Warteschlange eingereiht, bis ein Pfad zum Volume wieder hergestellt wird.
Dieser Fehler wird normalerweise durch einen Infrastruktur Fehler verursacht. Beispielsweise können Sie die Konnektivität mit dem Speicher oder dem Knoten verlieren, der das freigegebenes Clustervolume aus der aktiven Cluster Mitgliedschaft entfernt hat.

### <a name="event-5394-pool_online_warnings"></a>Ereignis 5394: POOL_ONLINE_WARNINGS

Beim Versuch, den Speicherpool online zu schalten, sind bei der Clusterdienst Speicherfehler aufgetreten. Führen Sie die Cluster Speicher Überprüfung aus, um das Problem zu beheben.

### <a name="event-5395-rcm_group_auto_move_storage_pool"></a>Ereignis 5395: RCM_GROUP_AUTO_MOVE_STORAGE_POOL

Die Gruppe wird vom Cluster für den Speicherpool "%1" verschoben, da der aktuelle Knoten "%3" nicht über eine optimale Konnektivität mit den physischen Datenträgern des Speicherpools verfügt.

## <a name="informational-events"></a>Informations Ereignisse

### <a name="event-1592-clussvc_tcp_reconnect_connection_reestablished"></a>Ereignis 1592: CLUSSVC_TCP_RECONNECT_CONNECTION_REESTABLISHED

Der Cluster Knoten "%1" hat die Kommunikation mit dem Cluster Knoten "%2" verloren. Die Netzwerkkommunikation wurde wieder hergestellt. Dies kann darauf zurückzuführen sein, dass die Kommunikation vorübergehend durch eine Firewall oder ein Update der Verbindungs Sicherheitsrichtlinie blockiert wird. Wenn das Problem weiterhin besteht und die Netzwerkkommunikation nicht wieder hergestellt wird, wird der Cluster Dienst auf einem oder mehreren Knoten angehalten. Führen Sie in diesem Fall den Konfigurationsüberprüfungs-Assistenten aus, um die Netzwerkkonfiguration zu überprüfen. Überprüfen Sie außerdem auf Hardware-oder Softwarefehler im Zusammenhang mit den Netzwerkadaptern auf diesem Knoten, und überprüfen Sie, ob in allen anderen Netzwerkkomponenten, mit denen der Knoten verbunden ist, wie z. b. Hubs, Switches oder Bridges, auf Fehler

### <a name="event-1594-cluster_functional_level_upgrade_complete"></a>Ereignis 1594: CLUSTER_FUNCTIONAL_LEVEL_UPGRADE_COMPLETE

Clusterdienst erfolgreich ein Upgrade der Cluster Funktionsebene durchgeführt. <br><br>
Funktionsebene: %1 <br> Upgradeversion: %2

### <a name="event-1635-rcm_resource_failure_info_with_typename"></a>Ereignis 1635: RCM_RESOURCE_FAILURE_INFO_WITH_TYPENAME

Fehler bei der Cluster Ressource "%1" vom Typ "%3" in der Cluster Rolle "%2".

### <a name="event-1636-clussvc_password_changed"></a>Ereignis 1636: CLUSSVC_PASSWORD_CHANGED

Der Clusterdienst hat das Kennwort des Kontos "%1" auf dem Knoten "%2" geändert.

### <a name="event-1680-cluster_node_exited_isolated_state"></a>Ereignis 1680: CLUSTER_NODE_EXITED_ISOLATED_STATE

Der Cluster Knoten ' %1 ' hat den isolierten Status beendet.

### <a name="event-1682-cluster_group_moved_no_longer_unmonitored"></a>Ereignis 1682: CLUSTER_GROUP_MOVED_NO_LONGER_UNMONITORED

Für den virtuellen Computer "%2", der auf dem isolierten Knoten "%1" nicht überwacht wurde, wurde ein Failover auf einen anderen Knoten durchgeführt. Die Integrität des virtuellen Computers wird erneut überwacht.

### <a name="event-1682-cluster_multiple_groups_no_longer_unmonitored"></a>Ereignis 1682: CLUSTER_MULTIPLE_GROUPS_NO_LONGER_UNMONITORED

Knoten "%1" wurde dem Cluster erneut hinzugefügt, und auf den folgenden virtuellen Computern, die auf diesem Knoten ausgeführt werden, wird erneut der Integritäts Status überwacht: %2.

### <a name="event-4621-nodecleanup_success"></a>Ereignis 4621: NODECLEANUP_SUCCESS

Dieser Knoten wurde erfolgreich aus dem Cluster entfernt.

### <a name="event-5121-dcm_volume_no_direct_io_due_to_failure"></a>Ereignis 5121: DCM_VOLUME_NO_DIRECT_IO_DUE_TO_FAILURE

Auf Freigegebenes Clustervolume ' %1 ' (' %2 ') kann von diesem Cluster Knoten aus nicht mehr direkt zugegriffen werden. Der e/a-Zugriff wird über das Netzwerk an den Knoten umgeleitet, der das Volume besitzt. Wenn dies zu einer Beeinträchtigung der Leistung führt, führen Sie eine Problembehandlung für die Verbindung dieses Knotens mit dem Speichergerät und e/a-Vorgänge in einen fehlerfreien Status aus, sobald die Verbindung mit dem Speichergerät wieder hergestellt wird.

### <a name="event-5218-csv_old_sw_snapshot_deleted"></a>Ereignis 5218: CSV_OLD_SW_SNAPSHOT_DELETED

Die physische Datenträger Ressource "%1" des Clusters löschte eine Software Momentaufnahme. Die Software Momentaufnahme auf Freigegebenes Clustervolume ' %2 ' wurde gelöscht, weil Sie älter als ' %3 ' Tag (e) war. Die Momentaufnahme-ID lautete "%4" und wurde aus dem Knoten "%5" auf "%6" erstellt.
Es wird erwartet, dass Momentaufnahmen von einer Sicherungs Anwendung gelöscht werden, nachdem ein Sicherungsauftrag abgeschlossen wurde. Diese Momentaufnahme hat die Zeit überschritten, die für das vorhanden sein einer Momentaufnahme erwartet wird. Überprüfen Sie mit der Sicherungs Anwendung, ob Sicherungsaufträge erfolgreich abgeschlossen werden.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Ausführliche Ereignis Informationen für Failoverclustering-Komponenten in Windows Server 2008](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753362(v%3dws.10))
