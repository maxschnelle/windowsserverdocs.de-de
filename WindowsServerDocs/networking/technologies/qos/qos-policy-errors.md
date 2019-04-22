---
title: QoS-Richtlinie Fehler- und Ereignismeldungen
description: Dieses Thema enthält eine Liste der Fehler- und ereignismeldungen für Quality of Service (QoS)-Richtlinie in Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 76974e10-6a57-4533-83be-cfd5a0d364a3
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 774d9473beed1da861c6827357710133aeaca15e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824051"
---
# <a name="qos-policy-error-and-event-messages"></a>QoS-Richtlinie Fehler- und Ereignismeldungen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Es folgen die Fehler- und ereignismeldungen, die QoS-Richtlinie zugeordnet sind.  
  
## <a name="informational-messages"></a>Informationsmeldungen  

Es folgt eine Liste von informationsmeldungen von QoS-Richtlinie.

|||  
|-|-|  
|**MessageId**|16500|  
|**Schweregrad**|Informationen|  
|**SymbolicName**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_NO_CHANGE|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS-Richtlinien für Computer wurden erfolgreich aktualisiert. Änderungen wurden nicht gefunden.|  
  
|||  
|-|-|  
|**MessageId**|16501|  
|**Schweregrad**|Informationen|  
|**SymbolicName**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_WITH_CHANGE|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS-Richtlinien für Computer wurden erfolgreich aktualisiert. Richtlinienänderungen, die erkannt werden.|  
  
|||  
|-|-|  
|**MessageId**|16502|  
|**Schweregrad**|Informationen|  
|**SymbolicName**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_NO_CHANGE|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS-Richtlinien für Benutzer wurden erfolgreich aktualisiert. Änderungen wurden nicht gefunden.|  
  
|||  
|-|-|  
|**MessageId**|16503|  
|**Schweregrad**|Informationen|  
|**SymbolicName**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_WITH_CHANGE|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS-Richtlinien für Benutzer wurden erfolgreich aktualisiert. Richtlinienänderungen, die erkannt werden.|  
  
|||  
|-|-|  
|**MessageId**|16504|  
|**Schweregrad**|Informationen|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NOT_CONFIGURED|  
|**Sprache**|Englisch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für eingehenden TCP-Durchsatz wurden erfolgreich aktualisiert. Der Einstellungswert ist von QoS-Richtlinien nicht angegeben. Standardwert des lokalen Computers werden angewendet.|  
  
|||  
|-|-|  
|**MessageId**|16505|  
|**Schweregrad**|Informationen|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_OFF|  
|**Sprache**|Englisch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für eingehenden TCP-Durchsatz wurden erfolgreich aktualisiert. Der Einstellungswert ist Ebene 0 (minimaler Durchsatz).|  
  
|||  
|-|-|  
|**MessageId**|16506|  
|**Schweregrad**|Informationen|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_HIGHLY_RESTRICTED|  
|**Sprache**|Englisch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für eingehenden TCP-Durchsatz wurden erfolgreich aktualisiert. Der Einstellungswert ist auf Ebene 1.|  
  
|||  
|-|-|  
|**MessageId**|16507|  
|**Schweregrad**|Informationen|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_RESTRICTED|  
|**Sprache**|Englisch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für eingehenden TCP-Durchsatz wurden erfolgreich aktualisiert. Der Einstellungswert ist Ebene 2.|  
  
|||  
|-|-|  
|**MessageId**|16508|  
|**Schweregrad**|Informationen|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NORMAL|  
|**Sprache**|Englisch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für eingehenden TCP-Durchsatz wurden erfolgreich aktualisiert. Der Einstellungswert ist auf Ebene 3 (maximaler Durchsatz).|  
  
|||  
|-|-|  
|**MessageId**|16509|  
|**Schweregrad**|Informationen|  
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_NOT_CONFIGURED|  
|**Sprache**|Englisch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für den DSCP-Markierung überschreibt wurden erfolgreich aktualisiert. Der Einstellungswert ist nicht angegeben. Anwendungen können DSCP-Werte unabhängig von QoS-Richtlinien festlegen.|  
  
|||  
|-|-|  
|**MessageId**|16510|  
|**Schweregrad**|Informationen|  
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_IGNORED|  
|**Sprache**|Englisch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für den DSCP-Markierung überschreibt wurden erfolgreich aktualisiert. Anforderungen der Anwendung DSCP-Markierung werden ignoriert. Nur die QoS-Richtlinien können DSCP-Werte festlegen.|  
  
|||  
|-|-|  
|**MessageId**|16511|  
|**Schweregrad**|Informationen|  
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_ALLOWED|  
|**Sprache**|Englisch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für den DSCP-Markierung überschreibt wurden erfolgreich aktualisiert. Anwendungen können DSCP-Werte unabhängig von QoS-Richtlinien festlegen.|  
  
|||  
|-|-|  
|**MessageId**|16512|  
|**Schweregrad**|Informationen|  
|**SymbolicName**|EVENT_EQOS_INFO_LOCAL_SETTING_DONT_USE_NLA|  
|**Sprache**|Englisch|  
|**Nachricht**|Selektive Anwendung von QoS-Richtlinien, die basierend auf Domäne Netzwerkkategorie wurde deaktiviert. QoS-Richtlinien werden für alle Netzwerkschnittstellen angewendet werden.|  
  
## <a name="warning-messages"></a>Warnmeldungen

Es folgt eine Liste von Warnmeldungen für die QoS-Richtlinie.

|||  
|-|-|  
|**MessageId**|16600|  
|**Schweregrad**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_TEST_1|  
|**Sprache**|Englisch|  
|**Nachricht**|EQOS: *** Tests\*\*\*[, mit einer Zeichenfolge] "%2".|  
  
|||  
|-|-|  
|**MessageId**|16601|  
|**Schweregrad**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_TEST_2|  
|**Sprache**|Englisch|  
|**Nachricht**|EQOS: *** Tests\*\*\*[, mit zwei Zeichenfolgen, string1 ist] "%2" [, string2 hat die] "%3".|  
  
|||  
|-|-|  
|**MessageId**|16602|  
|**Schweregrad**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_VERSION|  
|**Sprache**|Englisch|  
|**Nachricht**|Der Computer QoS-Richtlinie "%2" hat eine ungültige Versionsnummer. Diese Richtlinie wird nicht angewendet werden.|  
  
|||  
|-|-|  
|**MessageId**|16603|  
|**Schweregrad**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_VERSION|  
|**Sprache**|Englisch|  
|**Nachricht**|Der Benutzer QoS-Richtlinie "%2" hat eine ungültige Versionsnummer. Diese Richtlinie wird nicht angewendet werden.|  
  
|||  
|-|-|  
|**MessageId**|16604|  
|**Schweregrad**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_PROFILE_NOT_SPECIFIED|  
|**Sprache**|Englisch|  
|**Nachricht**|Der Computer QoS-Richtlinie "%2" gibt keine DSCP-Wert oder Drosselung Rate. Diese Richtlinie wird nicht angewendet werden.|  
  
|||  
|-|-|  
|**MessageId**|16605|  
|**Schweregrad**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_PROFILE_NOT_SPECIFIED|  
|**Sprache**|Englisch|  
|**Nachricht**|Der Benutzer QoS-Richtlinie "%2" gibt keine DSCP-Wert oder Drosselung Rate. Diese Richtlinie wird nicht angewendet werden.|  
  
|||  
|-|-|  
|**MessageId**|16606|  
|**Schweregrad**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_QUOTA_EXCEEDED|  
|**Sprache**|Englisch|  
|**Nachricht**|Die maximale Anzahl von Computer-QoS-Richtlinien überschritten. Die QoS-Richtlinie "%2" und die nachfolgenden Computer QoS-Richtlinien werden nicht angewendet werden.|  
  
|||  
|-|-|  
|**MessageId**|16607|  
|**Schweregrad**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_QUOTA_EXCEEDED|  
|**Sprache**|Englisch|  
|**Nachricht**|Die maximale Anzahl von Benutzer-QoS-Richtlinien überschritten. Die QoS-Richtlinie "%2" und nachfolgende Benutzer QoS-Richtlinien werden nicht angewendet werden.|  
  
|||  
|-|-|  
|**MessageId**|16608|  
|**Schweregrad**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_CONFLICT|  
|**Sprache**|Englisch|  
|**Nachricht**|Der Computer QoS-Richtlinie "%2" steht möglicherweise mit anderen QoS-Richtlinien in Konflikt. Finden Sie Dokumentation für Regeln, die über die Richtlinie angewendet werden soll.|  
  
|||  
|-|-|  
|**MessageId**|16609|  
|**Schweregrad**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_CONFLICT|  
|**Sprache**|Englisch|  
|**Nachricht**|Der Benutzer QoS-Richtlinie "%2" steht möglicherweise mit anderen QoS-Richtlinien in Konflikt. Finden Sie Dokumentation für Regeln, die über die Richtlinie angewendet werden soll.|  
  
|||  
|-|-|  
|**MessageId**|16610|  
|**Schweregrad**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_NO_FULLPATH_APPNAME|  
|**Sprache**|Englisch|  
|**Nachricht**|Des Computers QoS-Richtlinie "%2" wurde ignoriert, da der Pfad der Anwendung kann nicht verarbeitet werden. Der Pfad der Anwendung möglicherweise ungültig, enthalten einen ungültiger Laufwerkbuchstabe wurde, oder einem zugeordneten Netzlaufwerk enthalten.|  
  
|||  
|-|-|  
|**MessageId**|16611|  
|**Schweregrad**|Warnung|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_NO_FULLPATH_APPNAME|  
|**Sprache**|Englisch|  
|**Nachricht**|Der Benutzer QoS-Richtlinie "%2" wurde ignoriert, da es sich bei der Pfad der Anwendung kann nicht verarbeitet werden. Der Pfad der Anwendung möglicherweise ungültig, enthalten einen ungültiger Laufwerkbuchstabe wurde, oder einem zugeordneten Netzlaufwerk enthalten.|  
  
## <a name="error-messages"></a>Fehlermeldungen  

Es folgt eine Liste von Fehlermeldungen der QoS-Richtlinie.

|||  
|-|-|  
|**MessageId**|16700|  
|**Schweregrad**|Fehler|  
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_REFERESH|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS-Richtlinien für Computer konnte nicht aktualisiert werden. Fehlercode: "%2".|  
  
|||  
|-|-|  
|**MessageId**|16701|  
|**Schweregrad**|Fehler|  
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_REFERESH|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS-Richtlinien für Benutzer konnte nicht aktualisiert werden. Fehlercode: "%2".|  
  
|||  
|-|-|  
|**MessageId**|16702|  
|**Schweregrad**|Fehler|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_ROOT_KEY|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS konnte den Stammschlüssel auf Computerebene für QoS-Richtlinien zu öffnen. Fehlercode: "%2".|  
  
|||  
|-|-|  
|**MessageId**|16703|  
|**Schweregrad**|Fehler|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_ROOT_KEY|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS konnte den Stammschlüssel auf Benutzerebene für QoS-Richtlinien zu öffnen. Fehlercode: "%2".|  
  
|||  
|-|-|  
|**MessageId**|16704|  
|**Schweregrad**|Fehler|  
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_TOO_LONG|  
|**Sprache**|Englisch|  
|**Nachricht**|Eine QoS-Richtlinie für Computer überschreitet die maximal zulässige Länge. Diese Richtlinie wird unter dem Computerebene QoS-Richtlinie Hauptschlüssel mit dem Index "%2" aufgeführt.|  
  
|||  
|-|-|  
|**MessageId**|16705|  
|**Schweregrad**|Fehler|  
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_TOO_LONG|  
|**Sprache**|Englisch|  
|**Nachricht**|Eine QoS-Richtlinie für Benutzer überschreitet die maximal zulässige Länge. Diese Richtlinie wird unter dem auf Benutzerebene QoS-Richtlinie Hauptschlüssel mit dem Index "%2" aufgeführt.|  
  
|||  
|-|-|  
|**MessageId**|16706|  
|**Schweregrad**|Fehler|  
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_SIZE_ZERO|  
|**Sprache**|Englisch|  
|**Nachricht**|Eine QoS-Richtlinie für Computer hat einen Namen mit der Länge Null. Diese Richtlinie wird unter dem Computerebene QoS-Richtlinie Hauptschlüssel mit dem Index "%2" aufgeführt.|  
  
|||  
|-|-|  
|**MessageId**|16707|  
|**Schweregrad**|Fehler|  
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_SIZE_ZERO|  
|**Sprache**|Englisch|  
|**Nachricht**|Eine QoS-Richtlinie für Benutzer hat es sich um einen Namen mit der Länge 0 (null). Diese Richtlinie wird unter dem auf Benutzerebene QoS-Richtlinie Hauptschlüssel mit dem Index "%2" aufgeführt.|  
  
|||  
|-|-|  
|**MessageId**|16708|  
|**Schweregrad**|Fehler|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_SUBKEY|  
|**Sprache**|Englisch|  
|**Nachricht**|Öffnen Sie den Registrierungsunterschlüssel für einen Computer QoS-Richtlinie konnte QoS. Die Richtlinie wird unter dem Computerebene QoS-Richtlinie Hauptschlüssel mit dem Index "%2" aufgeführt.|  
  
|||  
|-|-|  
|**MessageId**|16709|  
|**Schweregrad**|Fehler|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_SUBKEY|  
|**Sprache**|Englisch|  
|**Nachricht**|Öffnen Sie den Registrierungsunterschlüssel für eine QoS-Richtlinie für Benutzer konnte QoS. Die Richtlinie wird unter dem auf Benutzerebene QoS-Richtlinie Hauptschlüssel mit dem Index "%2" aufgeführt.|  
  
|||  
|-|-|  
|**MessageId**|16710|  
|**Schweregrad**|Fehler|  
|**SymbolicName**|EVENT_EQOS_ERROR_PROCESSING_MACHINE_POLICY_FIELD|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS konnte nicht gelesen oder überprüft das Feld "%2" für den Computer QoS-Richtlinie "%3".|  
  
|||  
|-|-|  
|**MessageId**|16711|  
|**Schweregrad**|Fehler|  
|**SymbolicName**|EVENT_EQOS_ERROR_PROCESSING_USER_POLICY_FIELD|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS konnte nicht gelesen oder überprüft das Feld "%2" für den Benutzer QoS-Richtlinie "%3".|  
  
|||  
|-|-|  
|**MessageId**|16712|  
|**Schweregrad**|Fehler|  
|**SymbolicName**|EVENT_EQOS_ERROR_SETTING_TCP_AUTOTUNING|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS konnte nicht zum Lesen oder Festlegen von eingehenden TCP-Durchsatz, Fehlercode: "%2".|  
  
|||  
|-|-|  
|**MessageId**|16713|  
|**Schweregrad**|Fehler|  
|**SymbolicName**|EVENT_EQOS_ERROR_SETTING_APP_MARKING|  
|**Sprache**|Englisch|  
|**Nachricht**|Fehler beim Lesen oder Festlegen der DSCP-Markierung QoS außer Kraft setzen, festlegen, Fehlercode: "%2".|  

Im nächsten Thema in diesem Handbuch finden Sie unter [häufig gestellte Fragen zu QoS-Richtlinie](qos-policy-faq.md).

Das erste Thema in diesem Handbuch finden Sie unter [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).
