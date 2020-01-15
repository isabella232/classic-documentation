---
template: page-sidebar
title: Alias
anchor: alias
---

You can target a customer with any attribute from your [datasources](/rest/reference#dcp_tables) (also called "tables") by creating an _alias_.

Aliases are links between your customer IDs and the Optimizely user IDs. With multiple datasources linked, Optimizely is able to generate [consolidated customer profiles](/rest/reference/#consolidated-profile), which enable advanced, specific customer targeting.

Optimizely automatically generates each Optimizely user ID and stores it in the `optimizelyEndUserId` cookie.

<img src="/assets/img/dcp/alias.png" alt="ANON_ID_1 and OEU_2 are in separate columns of the same row in the 'Alias Table'. Two arrows show that ANON_ID_1 and OEU_2 are originally from separate tables." title="ANON_ID_1 and OEU_2 are in separate columns of the same row in the 'Alias Table'. Two arrows show that ANON_ID_1 and OEU_2 are originally from separate tables.">

In the above figure, the highlighted alias indicates that `ANON_ID_1` in "My Datasource" is the *same customer* as `OEU_2` in "Optimizely Datasource".

<div class="attention attention--warning push--bottom">
See the [API Reference](/rest/reference#dcp_alias) for endpoints related to aliases.
</div>
