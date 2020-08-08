---
title: Fehler-und Ereignismeldungen der QoS-Richtlinie
description: Dieses Thema enthält eine Liste der Fehler-und Ereignismeldungen für Quality of Service (QoS)-Richtlinie in Windows Server 2016.
ms.topic: article
ms.assetid: 76974e10-6a57-4533-83be-cfd5a0d364a3
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: dc100c7ae8ff4ab65dc8cacdde9d46ade8d2b20e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940021"
---
# <a name="qos-policy-error-and-event-messages"></a>Fehler-und Ereignismeldungen der QoS-Richtlinie

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Im folgenden finden Sie die Fehler-und Ereignismeldungen, die der QoS-Richtlinie zugeordnet sind.

## <a name="informational-messages"></a>Informationsmeldungen

Im folgenden finden Sie eine Liste von Informationsmeldungen zur QoS-Richtlinie.

|||
|-|-|
|**MessageId**|16500|
|**Schweregrad**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_NO_CHANGE|
|**Sprache**|Englisch|
|**Meldung**|Die Computer-QoS-Richtlinien wurden erfolgreich aktualisiert. Es wurden keine Änderungen erkannt.|

|||
|-|-|
|**MessageId**|16501|
|**Schweregrad**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_WITH_CHANGE|
|**Sprache**|Englisch|
|**Meldung**|Die Computer-QoS-Richtlinien wurden erfolgreich aktualisiert. Richtlinien Änderungen wurden erkannt.|

|||
|-|-|
|**MessageId**|16502|
|**Schweregrad**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_NO_CHANGE|
|**Sprache**|Englisch|
|**Meldung**|Benutzer-QoS-Richtlinien wurden erfolgreich aktualisiert. Es wurden keine Änderungen erkannt.|

|||
|-|-|
|**MessageId**|16503|
|**Schweregrad**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_WITH_CHANGE|
|**Sprache**|Englisch|
|**Meldung**|Benutzer-QoS-Richtlinien wurden erfolgreich aktualisiert. Richtlinien Änderungen wurden erkannt.|

|||
|-|-|
|**MessageId**|16504|
|**Schweregrad**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NOT_CONFIGURED|
|**Sprache**|Englisch|
|**Meldung**|Die erweiterte QoS-Einstellung für die eingehende TCP-Durchsatz Stufe wurde erfolgreich aktualisiert. Der Einstellungs Wert wird nicht durch eine QoS-Richtlinie angegeben. Der Standardwert des lokalen Computers wird angewendet.|

|||
|-|-|
|**MessageId**|16505|
|**Schweregrad**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_OFF|
|**Sprache**|Englisch|
|**Meldung**|Die erweiterte QoS-Einstellung für die eingehende TCP-Durchsatz Stufe wurde erfolgreich aktualisiert. Der Wert für die Einstellung ist Ebene 0 (minimaler Durchsatz).|

|||
|-|-|
|**MessageId**|16506|
|**Schweregrad**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_HIGHLY_RESTRICTED|
|**Sprache**|Englisch|
|**Meldung**|Die erweiterte QoS-Einstellung für die eingehende TCP-Durchsatz Stufe wurde erfolgreich aktualisiert. Der Wert für die Einstellung ist Ebene 1.|

|||
|-|-|
|**MessageId**|16507|
|**Schweregrad**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_RESTRICTED|
|**Sprache**|Englisch|
|**Meldung**|Die erweiterte QoS-Einstellung für die eingehende TCP-Durchsatz Stufe wurde erfolgreich aktualisiert. Der Wert für die Einstellung ist Ebene 2.|

|||
|-|-|
|**MessageId**|16508|
|**Schweregrad**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NORMAL|
|**Sprache**|Englisch|
|**Meldung**|Die erweiterte QoS-Einstellung für die eingehende TCP-Durchsatz Stufe wurde erfolgreich aktualisiert. Der Wert für die Einstellung ist Ebene 3 (maximaler Durchsatz).|

|||
|-|-|
|**MessageId**|16509|
|**Schweregrad**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_NOT_CONFIGURED|
|**Sprache**|Englisch|
|**Meldung**|Die erweiterte QoS-Einstellung für die DSCP-Markierung wurde erfolgreich aktualisiert. Der Einstellungs Wert ist nicht angegeben. Anwendungen können DSCP-Werte unabhängig von QoS-Richtlinien festlegen.|

|||
|-|-|
|**MessageId**|16510|
|**Schweregrad**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_IGNORED|
|**Sprache**|Englisch|
|**Meldung**|Die erweiterte QoS-Einstellung für die DSCP-Markierung wurde erfolgreich aktualisiert. Anwendungs-DSCP-Markierungs Anforderungen werden ignoriert. Nur QoS-Richtlinien können DSCP-Werte festlegen.|

|||
|-|-|
|**MessageId**|16511|
|**Schweregrad**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_ALLOWED|
|**Sprache**|Englisch|
|**Meldung**|Die erweiterte QoS-Einstellung für die DSCP-Markierung wurde erfolgreich aktualisiert. Anwendungen können DSCP-Werte unabhängig von QoS-Richtlinien festlegen.|

|||
|-|-|
|**MessageId**|16512|
|**Schweregrad**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_LOCAL_SETTING_DONT_USE_NLA|
|**Sprache**|Englisch|
|**Meldung**|Die selektive Anwendung von QoS-Richtlinien, die auf der Domänen Netzwerk Kategorie basieren, wurde deaktiviert. QoS-Richtlinien werden auf alle Netzwerkschnittstellen angewendet.|

## <a name="warning-messages"></a>Warnmeldungen

Im folgenden finden Sie eine Liste der Warnmeldungen der QoS-Richtlinie.

|||
|-|-|
|**MessageId**|16600|
|**Schweregrad**|Warnung|
|**SymbolicName**|EVENT_EQOS_WARNING_TEST_1|
|**Sprache**|Englisch|
|**Meldung**|EQoS: * * * Testen \* \* \* [, mit einer Zeichenfolge] "%2".|

|||
|-|-|
|**MessageId**|16601|
|**Schweregrad**|Warnung|
|**SymbolicName**|EVENT_EQOS_WARNING_TEST_2|
|**Sprache**|Englisch|
|**Meldung**|EQoS: * * * Testen \* \* \* [, mit zwei Zeichen folgen, Zeichenfolge1 ist] "%2" [, Zeichenfolge2 ist] "%3".|

|||
|-|-|
|**MessageId**|16602|
|**Schweregrad**|Warnung|
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_VERSION|
|**Sprache**|Englisch|
|**Meldung**|Die Computer-QoS-Richtlinie "%2" weist eine ungültige Versionsnummer auf. Diese Richtlinie wird nicht angewendet.|

|||
|-|-|
|**MessageId**|16603|
|**Schweregrad**|Warnung|
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_VERSION|
|**Sprache**|Englisch|
|**Meldung**|Die Benutzer-QoS-Richtlinie "%2" weist eine ungültige Versionsnummer auf. Diese Richtlinie wird nicht angewendet.|

|||
|-|-|
|**MessageId**|16604|
|**Schweregrad**|Warnung|
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_PROFILE_NOT_SPECIFIED|
|**Sprache**|Englisch|
|**Meldung**|In der Computer-QoS-Richtlinie "%2" ist kein DSCP-Wert oder eine Drosselungs Rate angegeben. Diese Richtlinie wird nicht angewendet.|

|||
|-|-|
|**MessageId**|16605|
|**Schweregrad**|Warnung|
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_PROFILE_NOT_SPECIFIED|
|**Sprache**|Englisch|
|**Meldung**|In der Benutzer-QoS-Richtlinie "%2" ist kein DSCP-Wert oder eine Drosselungs Rate angegeben. Diese Richtlinie wird nicht angewendet.|

|||
|-|-|
|**MessageId**|16606|
|**Schweregrad**|Warnung|
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_QUOTA_EXCEEDED|
|**Sprache**|Englisch|
|**Meldung**|Die maximale Anzahl von QoS-Richtlinien für Computer wurde überschritten. Die QoS-Richtlinie "%2" und die nachfolgenden Computer-QoS-Richtlinien werden nicht angewendet.|

|||
|-|-|
|**MessageId**|16607|
|**Schweregrad**|Warnung|
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_QUOTA_EXCEEDED|
|**Sprache**|Englisch|
|**Meldung**|Die maximale Anzahl von Benutzer-QoS-Richtlinien wurde überschritten. Die QoS-Richtlinie "%2" und die nachfolgenden Benutzer-QoS-Richtlinien werden nicht angewendet.|

|||
|-|-|
|**MessageId**|16608|
|**Schweregrad**|Warnung|
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_CONFLICT|
|**Sprache**|Englisch|
|**Meldung**|Die Computer-QoS-Richtlinie "%2" steht potenziell in Konflikt mit anderen QoS-Richtlinien. Regeln zur Anwendung der Richtlinie finden Sie in der Dokumentation.|

|||
|-|-|
|**MessageId**|16609|
|**Schweregrad**|Warnung|
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_CONFLICT|
|**Sprache**|Englisch|
|**Meldung**|Die Benutzer-QoS-Richtlinie "%2" steht potenziell in Konflikt mit anderen QoS-Richtlinien. Regeln zur Anwendung der Richtlinie finden Sie in der Dokumentation.|

|||
|-|-|
|**MessageId**|16610|
|**Schweregrad**|Warnung|
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_NO_FULLPATH_APPNAME|
|**Sprache**|Englisch|
|**Meldung**|Die Computer-QoS-Richtlinie "%2" wurde ignoriert, da der Anwendungspfad nicht verarbeitet werden kann. Der Anwendungspfad ist möglicherweise ungültig, enthält einen ungültigen Laufwerk Buchstaben oder enthält ein zugeordnetes Netzwerklaufwerk.|

|||
|-|-|
|**MessageId**|16611|
|**Schweregrad**|Warnung|
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_NO_FULLPATH_APPNAME|
|**Sprache**|Englisch|
|**Meldung**|Die Benutzer-QoS-Richtlinie "%2" wurde ignoriert, da der Anwendungspfad nicht verarbeitet werden kann. Der Anwendungspfad ist möglicherweise ungültig, enthält einen ungültigen Laufwerk Buchstaben oder enthält ein zugeordnetes Netzwerklaufwerk.|

## <a name="error-messages"></a>Fehlermeldungen

Im folgenden finden Sie eine Liste der QoS-Richtlinien-Fehlermeldungen.

|||
|-|-|
|**MessageId**|16700|
|**Schweregrad**|Fehler|
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_REFERESH|
|**Sprache**|Englisch|
|**Meldung**|Fehler beim Aktualisieren der QoS-Richtlinien des Computers. Fehlercode: "%2".|

|||
|-|-|
|**MessageId**|16701|
|**Schweregrad**|Fehler|
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_REFERESH|
|**Sprache**|Englisch|
|**Meldung**|Fehler beim Aktualisieren der Benutzer-QoS-Richtlinien. Fehlercode: "%2".|

|||
|-|-|
|**MessageId**|16702|
|**Schweregrad**|Fehler|
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_ROOT_KEY|
|**Sprache**|Englisch|
|**Meldung**|QoS konnte den Stamm Schlüssel auf Computer Ebene für QoS-Richtlinien nicht öffnen. Fehlercode: "%2".|

|||
|-|-|
|**MessageId**|16703|
|**Schweregrad**|Fehler|
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_ROOT_KEY|
|**Sprache**|Englisch|
|**Meldung**|QoS konnte den Stamm Schlüssel auf Benutzerebene für QoS-Richtlinien nicht öffnen. Fehlercode: "%2".|

|||
|-|-|
|**MessageId**|16704|
|**Schweregrad**|Fehler|
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_TOO_LONG|
|**Sprache**|Englisch|
|**Meldung**|Eine Computer-QoS-Richtlinie überschreitet die maximal zulässige namens Länge. Die Richtlinie für die Beschädigung wird unter dem Schlüssel der QoS-Richtlinie auf Computer Ebene mit dem Index "%2" aufgeführt.|

|||
|-|-|
|**MessageId**|16705|
|**Schweregrad**|Fehler|
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_TOO_LONG|
|**Sprache**|Englisch|
|**Meldung**|Eine Benutzer-QoS-Richtlinie überschreitet die maximal zulässige namens Länge. Die Richtlinie für die Beschädigung wird unter dem Schlüssel der QoS-Richtlinie auf Benutzerebene mit dem Index "%2" aufgeführt.|

|||
|-|-|
|**MessageId**|16706|
|**Schweregrad**|Fehler|
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_SIZE_ZERO|
|**Sprache**|Englisch|
|**Meldung**|Eine Computer-QoS-Richtlinie hat einen Namen mit der Länge Null. Die Richtlinie für die Beschädigung wird unter dem Schlüssel der QoS-Richtlinie auf Computer Ebene mit dem Index "%2" aufgeführt.|

|||
|-|-|
|**MessageId**|16707|
|**Schweregrad**|Fehler|
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_SIZE_ZERO|
|**Sprache**|Englisch|
|**Meldung**|Eine Benutzer-QoS-Richtlinie hat einen Namen mit der Länge Null. Die Richtlinie für die Beschädigung wird unter dem Schlüssel der QoS-Richtlinie auf Benutzerebene mit dem Index "%2" aufgeführt.|

|||
|-|-|
|**MessageId**|16708|
|**Schweregrad**|Fehler|
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_SUBKEY|
|**Sprache**|Englisch|
|**Meldung**|QoS konnte den Registrierungs Unterschlüssel für eine Computer-QoS-Richtlinie nicht öffnen. Die Richtlinie wird unter dem Schlüssel der QoS-Richtlinie auf Computer Ebene mit dem Index "%2" aufgeführt.|

|||
|-|-|
|**MessageId**|16709|
|**Schweregrad**|Fehler|
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_SUBKEY|
|**Sprache**|Englisch|
|**Meldung**|QoS konnte den Registrierungs Unterschlüssel für eine Benutzer-QoS-Richtlinie nicht öffnen. Die Richtlinie wird unter dem Schlüssel der QoS-Richtlinie auf Benutzerebene mit dem Index "%2" aufgeführt.|

|||
|-|-|
|**MessageId**|16710|
|**Schweregrad**|Fehler|
|**SymbolicName**|EVENT_EQOS_ERROR_PROCESSING_MACHINE_POLICY_FIELD|
|**Sprache**|Englisch|
|**Meldung**|QoS konnte das Feld "%2" für die Computer-QoS-Richtlinie "%3" nicht lesen oder überprüfen.|

|||
|-|-|
|**MessageId**|16711|
|**Schweregrad**|Fehler|
|**SymbolicName**|EVENT_EQOS_ERROR_PROCESSING_USER_POLICY_FIELD|
|**Sprache**|Englisch|
|**Meldung**|QoS konnte das Feld "%2" für die Benutzer-QoS-Richtlinie "%3" nicht lesen oder überprüfen.|

|||
|-|-|
|**MessageId**|16712|
|**Schweregrad**|Fehler|
|**SymbolicName**|EVENT_EQOS_ERROR_SETTING_TCP_AUTOTUNING|
|**Sprache**|Englisch|
|**Meldung**|QoS konnte die eingehende TCP-Durchsatz Ebene nicht lesen oder festlegen. Fehlercode: "%2".|

|||
|-|-|
|**MessageId**|16713|
|**Schweregrad**|Fehler|
|**SymbolicName**|EVENT_EQOS_ERROR_SETTING_APP_MARKING|
|**Sprache**|Englisch|
|**Meldung**|QoS konnte die Außerkraftsetzungs Einstellung der DSCP-Markierung nicht lesen oder festlegen. Fehlercode: "%2".|

Das nächste Thema dieses Handbuchs finden Sie unter [häufig gestellte Fragen zur QoS-Richtlinie](qos-policy-faq.md).

Das erste Thema in dieser Anleitung finden Sie unter [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).
