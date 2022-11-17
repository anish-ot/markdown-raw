#Connectivity, Staging & Production

TerraPay system's are hosted on AWS across regions where available. A partner connecting to TerraPay system will connect to the nearest AWS region which is in close proximity to the partner network. TerraPay systems are hosted as primary (Live) site, DR site and GR site. TerraPay will connect to partner DR and GR systems as well to ensure service is not impacted when primary sites are down.

Partner systems are allowed access to the TerraPay network through a secure VPN tunnel. This is set up in both the primary and DR setups. Each of these will have two VPN tunnels, active and standby.

All the API interfaces between TerraPay and partner will be on HTTPS. TerraPay's inbound APIs are protected with a CA issued SSL certificate. Partner must also secure a CA issued SSL certificate for all APIs.

Partners integrate with TerraPay, on the EIG (External Interface Gateway) system which are hosted in a DMZ (De-Militarized Zone) of the TerraPay network. Access to all inbound and outbound APIs will be provided on the TerraPay staging system for integration testing. After API testing and validations are done then partners will be migrated to live production systems.

