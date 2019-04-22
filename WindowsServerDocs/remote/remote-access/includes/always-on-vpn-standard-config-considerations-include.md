## <a name="standard-configuration-considerations"></a>Überlegungen zur Standard-Konfiguration

Always On-VPN-verfügt über viele Konfigurationsoptionen. Aber Sie Ihr VPN-Konfiguration auswählen, sind jedoch die folgende Informationen an:

-   **Verbindungstyp.** Verbindung Protokollauswahl ist wichtig und letztendlich geht hand in hand mit dem Typ der Authentifizierung, die Sie verwenden möchten. Weitere Informationen über die Tunneling-Protokolle verfügbar sind, finden Sie unter [VPN-Verbindungstypen](https://docs.microsoft.com/windows/access-protection/vpn/vpn-connection-type).

-   **Routing.** In diesem Kontext bestimmen Routingregeln an, ob der Benutzer andere Netzwerkrouten während der Verbindung mit dem VPN verwenden können.

    -   _Getrenntes Tunneln_ der gleichzeitige Zugriff auf andere Netzwerke wie das Internet ermöglicht.

    -   _Erzwingen von Tunneln_ muss der gesamte Datenverkehr an das VPN ausschließlich durchlaufen und lässt keine gleichzeitigen Zugriff auf andere Netzwerke.

-   **Auslösen.** _Auslösen von_ bestimmt, wie und wann eine VPN-Verbindung initiiert wird (z. B. wenn eine app öffnet, wenn das Gerät manuell, durch den Benutzer aktiviert ist). Zum Auslösen von Optionen, finden Sie unter den [VPN-Konnektivität](#vpn-connectivity).

-   **Gerät oder die Benutzerauthentifizierung.** Always On-VPN-verwendet Zertifikate für Geräte und vom Gerät initiiert Verbindung über ein Feature namens [Gerät Tunnel](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/vpn-device-tunnel-config). Diese Verbindung kann automatisch initiiert werden und ist persistent, ähnlich wie eine tunnelverbindung des DirectAccess-Infrastruktur.

>[!TIP]
>Beim Migrieren von DirectAccess zu Always On-VPN-sollten Sie die verschiedenen Konfigurationsoptionen, die vergleichbar sind, was Sie haben, und erweitern Sie dann von dort ab.

Mithilfe von Benutzerzertifikaten, der Always On-VPN-Client verbindet sich automatisch, aber dies erfolgt auf Benutzerebene (nach der Benutzeranmeldung) anstatt auf Geräteebene (vor der Benutzeranmeldung). Die benutzererfahrung ist weiterhin für den Benutzer nahtlos, aber sie unterstützt erweiterte Authentifizierungsmechanismen, z.B. Windows Hello for Business.