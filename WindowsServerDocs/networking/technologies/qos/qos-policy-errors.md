---
title: QoS-Richtlinie Fehler- und Ereignismeldungen
description: Dieses Thema enthält eine Liste der Fehler- und Ereignis für Quality of Service (QoS)-Richtlinie in Windows Server2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 76974e10-6a57-4533-83be-cfd5a0d364a3
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e2e890a7947d4f7de09159d7de606c0542f45045
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="qos-policy-error-and-event-messages"></a>QoS-Richtlinie Fehler- und Ereignismeldungen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Es folgen die Nachrichten von Fehlern und Ereignissen, die QoS-Richtlinie zugeordnet sind.  
  
## <a name="informational-messages"></a>Informationsmeldungen  

Es folgt eine Liste der QoS-Richtlinie informationsmeldungen angezeigt.

|||  
|-|-|  
|**Nachrichten-ID**|16500|  
|**Schweregrad**|Information|  
|**Spmevent_package_fault**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_NO_CHANGE|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS-Richtlinien für Computer wurden erfolgreich aktualisiert. Keine Änderung festgestellt.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16501|  
|**Schweregrad**|Information|  
|**Spmevent_package_fault**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_WITH_CHANGE|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS-Richtlinien für Computer wurden erfolgreich aktualisiert. Richtlinienänderungen erkannt.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16502|  
|**Schweregrad**|Information|  
|**Spmevent_package_fault**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_NO_CHANGE|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS-Richtlinien für Benutzer wurden erfolgreich aktualisiert. Keine Änderung festgestellt.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16503|  
|**Schweregrad**|Information|  
|**Spmevent_package_fault**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_WITH_CHANGE|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS-Richtlinien für Benutzer wurden erfolgreich aktualisiert. Richtlinienänderungen erkannt.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16504|  
|**Schweregrad**|Information|  
|**Spmevent_package_fault**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NOT_CONFIGURED|  
|**Sprache**|Englisch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für eingehenden TCP-Durchsatz wurde erfolgreich aktualisiert. Wert ist nicht von einer QoS-Richtlinie angegeben. Standardwert des lokalen Computers wird angewendet.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16505|  
|**Schweregrad**|Information|  
|**Spmevent_package_fault**|EVENT_EQOS_INFO_TCP_AUTOTUNING_OFF|  
|**Sprache**|Englisch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für eingehenden TCP-Durchsatz wurde erfolgreich aktualisiert. Wert ist 0 (minimaler Durchsatz).|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16506|  
|**Schweregrad**|Information|  
|**Spmevent_package_fault**|EVENT_EQOS_INFO_TCP_AUTOTUNING_HIGHLY_RESTRICTED|  
|**Sprache**|Englisch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für eingehenden TCP-Durchsatz wurde erfolgreich aktualisiert. Wert ist auf Ebene 1.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16507|  
|**Schweregrad**|Information|  
|**Spmevent_package_fault**|EVENT_EQOS_INFO_TCP_AUTOTUNING_RESTRICTED|  
|**Sprache**|Englisch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für eingehenden TCP-Durchsatz wurde erfolgreich aktualisiert. Wert ist die Stufe 2.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16508|  
|**Schweregrad**|Information|  
|**Spmevent_package_fault**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NORMAL|  
|**Sprache**|Englisch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für eingehenden TCP-Durchsatz wurde erfolgreich aktualisiert. Wert ist die Stufe 3 (maximaler Durchsatz).|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16509|  
|**Schweregrad**|Information|  
|**Spmevent_package_fault**|EVENT_EQOS_INFO_APP_MARKING_NOT_CONFIGURED|  
|**Sprache**|Englisch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für DSCP-Markierung überschreibt wurden erfolgreich aktualisiert. Wert nicht angegeben. Anwendungen können DSCP-Werten unabhängig von QoS-Richtlinien festlegen.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16510|  
|**Schweregrad**|Information|  
|**Spmevent_package_fault**|EVENT_EQOS_INFO_APP_MARKING_IGNORED|  
|**Sprache**|Englisch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für DSCP-Markierung überschreibt wurden erfolgreich aktualisiert. Anwendung DSCP-markierungsanforderungen werden ignoriert. QoS-Richtlinien können DSCP-Werte festlegen.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16511|  
|**Schweregrad**|Information|  
|**Spmevent_package_fault**|EVENT_EQOS_INFO_APP_MARKING_ALLOWED|  
|**Sprache**|Englisch|  
|**Nachricht**|Die erweiterte QoS-Einstellung für DSCP-Markierung überschreibt wurden erfolgreich aktualisiert. Anwendungen können DSCP-Werten unabhängig von QoS-Richtlinien festlegen.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16512|  
|**Schweregrad**|Information|  
|**Spmevent_package_fault**|EVENT_EQOS_INFO_LOCAL_SETTING_DONT_USE_NLA|  
|**Sprache**|Englisch|  
|**Nachricht**|Selektive Anwendung von QoS-Richtlinien auf Grundlage der Domäne Netzwerkkategorie wurde deaktiviert. QoS-Richtlinien werden auf alle Netzwerkschnittstellen angewendet werden.|  
  
## <a name="warning-messages"></a>Warnmeldungen

Es folgt eine Liste von Warnmeldungen QoS-Richtlinie.

|||  
|-|-|  
|**Nachrichten-ID**|16600|  
|**Schweregrad**|Warnung|  
|**Spmevent_package_fault**|EVENT_EQOS_WARNING_TEST_1|  
|**Sprache**|Englisch|  
|**Nachricht**|EQOS: *** Testing\ * \ * \ * [, mit einer Zeichenfolge] "%2".|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16601|  
|**Schweregrad**|Warnung|  
|**Spmevent_package_fault**|EVENT_EQOS_WARNING_TEST_2|  
|**Sprache**|Englisch|  
|**Nachricht**|EQOS: *** Testing\ * \ * \ * [, mit zwei Zeichenfolgen string1 ist] "%2" [, Zeichenfolge2 ist] "%3".|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16602|  
|**Schweregrad**|Warnung|  
|**Spmevent_package_fault**|EVENT_EQOS_WARNING_MACHINE_POLICY_Version|  
|**Sprache**|Englisch|  
|**Nachricht**|Der Computer QoS-Richtlinie "%2" hat eine ungültige Versionsnummer. Diese Richtlinie wird nicht angewendet werden.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16603|  
|**Schweregrad**|Warnung|  
|**Spmevent_package_fault**|EVENT_EQOS_WARNING_USER_POLICY_Version|  
|**Sprache**|Englisch|  
|**Nachricht**|Der Benutzer QoS-Richtlinie "%2" hat eine ungültige Versionsnummer. Diese Richtlinie wird nicht angewendet werden.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16604|  
|**Schweregrad**|Warnung|  
|**Spmevent_package_fault**|EVENT_EQOS_WARNING_MACHINE_POLICY_PROFILE_NOT_SPECIFIED|  
|**Sprache**|Englisch|  
|**Nachricht**|Der Computer QoS-Richtlinie "%2" gibt keinen DSCP-Wert oder drosseln Satz an. Diese Richtlinie wird nicht angewendet werden.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16605|  
|**Schweregrad**|Warnung|  
|**Spmevent_package_fault**|EVENT_EQOS_WARNING_USER_POLICY_PROFILE_NOT_SPECIFIED|  
|**Sprache**|Englisch|  
|**Nachricht**|Die QoS-Richtlinie "%2" keine DSCP-Wert oder drosseln Rate angegeben. Diese Richtlinie wird nicht angewendet werden.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16606|  
|**Schweregrad**|Warnung|  
|**Spmevent_package_fault**|EVENT_EQOS_WARNING_MACHINE_POLICY_QUOTA_EXCEEDED|  
|**Sprache**|Englisch|  
|**Nachricht**|Die maximale Anzahl von QoS-Richtlinien für Computer überschritten. Die QoS-Richtlinie "%2" und die nachfolgenden QoS-Richtlinien werden nicht angewendet werden.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16607|  
|**Schweregrad**|Warnung|  
|**Spmevent_package_fault**|EVENT_EQOS_WARNING_USER_POLICY_QUOTA_EXCEEDED|  
|**Sprache**|Englisch|  
|**Nachricht**|Die maximale Anzahl von QoS-Richtlinien für Benutzer überschritten. Die QoS-Richtlinie "%2" und die nachfolgende Benutzer QoS-Richtlinien werden nicht angewendet werden.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16608|  
|**Schweregrad**|Warnung|  
|**Spmevent_package_fault**|EVENT_EQOS_WARNING_MACHINE_POLICY_CONFLICT|  
|**Sprache**|Englisch|  
|**Nachricht**|Der Computer QoS-Richtlinie "%2" steht möglicherweise in Konflikt mit anderen QoS-Richtlinien. Weitere Informationen finden Sie in der Dokumentation für Regeln, die über die Richtlinie angewendet werden soll.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16609|  
|**Schweregrad**|Warnung|  
|**Spmevent_package_fault**|EVENT_EQOS_WARNING_USER_POLICY_CONFLICT|  
|**Sprache**|Englisch|  
|**Nachricht**|Der Benutzer QoS-Richtlinie "%2" steht möglicherweise in Konflikt mit anderen QoS-Richtlinien. Weitere Informationen finden Sie in der Dokumentation für Regeln, die über die Richtlinie angewendet werden soll.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16610|  
|**Schweregrad**|Warnung|  
|**Spmevent_package_fault**|EVENT_EQOS_WARNING_MACHINE_POLICY_NO_FULLPATH_APPNAME|  
|**Sprache**|Englisch|  
|**Nachricht**|Die QoS-Richtlinie "%2" für Computer wurde ignoriert, da der Pfad der Anwendung verarbeitet werden kann. Der Pfad der Anwendung möglicherweise ungültig, enthält einen ungültigen Laufwerkbuchstaben oder einem zugeordneten Netzwerklaufwerk enthalten.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16611|  
|**Schweregrad**|Warnung|  
|**Spmevent_package_fault**|EVENT_EQOS_WARNING_USER_POLICY_NO_FULLPATH_APPNAME|  
|**Sprache**|Englisch|  
|**Nachricht**|Der Benutzer QoS-Richtlinie "%2" wurde ignoriert, da der Pfad der Anwendung kann nicht verarbeitet werden. Der Pfad der Anwendung möglicherweise ungültig, enthält einen ungültigen Laufwerkbuchstaben oder einem zugeordneten Netzwerklaufwerk enthalten.|  
  
## <a name="error-messages"></a>Fehlermeldungen  

Es folgt eine Liste der QoS-Richtlinie Fehlermeldungen angezeigt.

|||  
|-|-|  
|**Nachrichten-ID**|16700|  
|**Schweregrad**|Fehler|  
|**Spmevent_package_fault**|EVENT_EQOS_ERROR_MACHINE_POLICY_REFERESH|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS-Richtlinien für Computer konnte nicht aktualisiert werden. Fehlercode: "%2".|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16701|  
|**Schweregrad**|Fehler|  
|**Spmevent_package_fault**|EVENT_EQOS_ERROR_USER_POLICY_REFERESH|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS-Richtlinien für Benutzer konnte nicht aktualisiert werden. Fehlercode: "%2".|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16702|  
|**Schweregrad**|Fehler|  
|**Spmevent_package_fault**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_ROOT_KEY|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS konnte den Stammschlüssel auf Computerebene für QoS-Richtlinien zu öffnen. Fehlercode: "%2".|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16703|  
|**Schweregrad**|Fehler|  
|**Spmevent_package_fault**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_ROOT_KEY|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS konnte den Stammschlüssel auf Benutzerebene für QoS-Richtlinien zu öffnen. Fehlercode: "%2".|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16704|  
|**Schweregrad**|Fehler|  
|**Spmevent_package_fault**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_TOO_LONG|  
|**Sprache**|Englisch|  
|**Nachricht**|Eine QoS-Richtlinie für Computer überschreitet die maximal zulässige Länge. Diese Richtlinie ist unter dem Computerebene QoS-Richtlinie Stammschlüssel mit dem Index "%2" aufgeführt.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16705|  
|**Schweregrad**|Fehler|  
|**Spmevent_package_fault**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_TOO_LONG|  
|**Sprache**|Englisch|  
|**Nachricht**|Eine QoS-Richtlinie für Benutzer überschreitet die maximal zulässige Länge. Diese Richtlinie ist unter der Stammschlüssel der QoS-Richtlinie für Benutzer mit dem Index "%2" aufgeführt.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16706|  
|**Schweregrad**|Fehler|  
|**Spmevent_package_fault**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_SIZE_ZERO|  
|**Sprache**|Englisch|  
|**Nachricht**|Eine QoS-Richtlinie für Computer hat einen Namen mit der Länge Null. Diese Richtlinie ist unter dem Computerebene QoS-Richtlinie Stammschlüssel mit dem Index "%2" aufgeführt.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16707|  
|**Schweregrad**|Fehler|  
|**Spmevent_package_fault**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_SIZE_ZERO|  
|**Sprache**|Englisch|  
|**Nachricht**|Eine QoS-Richtlinie für Benutzer hat einen Namen mit der Länge Null. Diese Richtlinie ist unter der Stammschlüssel der QoS-Richtlinie für Benutzer mit dem Index "%2" aufgeführt.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16708|  
|**Schweregrad**|Fehler|  
|**Spmevent_package_fault**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_SUBKEY|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS konnte den Registrierungsunterschlüssel für eine QoS-Richtlinie für Computer zu öffnen. Die Richtlinie wird unter dem Computerebene QoS-Richtlinie Stammschlüssel mit dem Index "%2" aufgeführt.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16709|  
|**Schweregrad**|Fehler|  
|**Spmevent_package_fault**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_SUBKEY|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS konnte den Registrierungsunterschlüssel für eine QoS-Richtlinie für Benutzer zu öffnen. Die Richtlinie wird unter der Stammschlüssel der QoS-Richtlinie für Benutzer mit dem Index "%2" aufgeführt.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16710|  
|**Schweregrad**|Fehler|  
|**Spmevent_package_fault**|EVENT_EQOS_ERROR_PROCESSING_MACHINE_POLICY_FIELD|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS konnte nicht gelesen oder das Feld "%2" für den Computer "%3" QoS-Richtlinie zu überprüfen.|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16711|  
|**Schweregrad**|Fehler|  
|**Spmevent_package_fault**|EVENT_EQOS_ERROR_PROCESSING_USER_POLICY_FIELD|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS konnte nicht lesen oder überprüfen das Feld "%2" für den Benutzer QoS-Richtlinie "%3".|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16712|  
|**Schweregrad**|Fehler|  
|**Spmevent_package_fault**|EVENT_EQOS_ERROR_SETTING_TCP_AUTOTUNING|  
|**Sprache**|Englisch|  
|**Nachricht**|QoS konnte nicht gelesen oder eingehenden TCP-Durchsatz, Fehlercode festgelegt: "%2".|  
  
|||  
|-|-|  
|**Nachrichten-ID**|16713|  
|**Schweregrad**|Fehler|  
|**Spmevent_package_fault**|EVENT_EQOS_ERROR_SETTING_APP_MARKING|  
|**Sprache**|Englisch|  
|**Nachricht**|Fehler beim Lesen oder Festlegen der DSCP-Markierung QoS überschreiben Einstellung Fehlercode: "%2".|  

Im nächsten Thema in diesem Handbuch, finden Sie unter [häufig gestellte Fragen zu QoS-Richtlinie](qos-policy-faq.md).

Das erste Thema in diesem Handbuch finden Sie unter [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).
