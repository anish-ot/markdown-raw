#Assumptions

* The send partner system will provide and manage the necessary interfaces required by the sender to create an international money transfer request.
2. The send partner system then integrates with TerraPay to access the services provided.
3. TerraPay will integrate directly with receiving partner systems to delivery funds to the beneficiary.
4. The sender is a registered subscriber on the sending partner system.
5. The beneficiary is a registered subscriber on the receiving partner system.
6. A partner should be able to authenticate a subscriber with valid KYC documents.
7. Connectivity between the partner network and TerraPay network can be over S2S VPN or by white listing of IPs
8. The S2S VPN tunnel provides a secure and encrypted connection between the partner's system and TerraPay's system.
9. The partner system will use HTTPS/JSON based API integration with the TerraPay system.
10. TerraPay will provide a secure SSL certificate to use for APIs connecting into the partner system.
11. The partner will provide a secure SSL certificate to use for APIs connecting into the TerraPay system.
12. In order to provide good end user experiences the response times to API requests should be as low as possible
13. All timestamps on the TerraPay system are in GMT.
