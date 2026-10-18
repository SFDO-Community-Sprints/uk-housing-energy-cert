# What is this?
A LWC to graphically display the energy rating (EPC / SAP) for a property

# What gets deployed
| Metadata | Name | Purpose |
|---|---|---|
| Lightning Web Component | `energyCert` (label: Energy Certificate) | The EPC rating graph |
| Custom Field | `Asset.Current_SAP_Score__c` | Current SAP score |
| Custom Field | `Asset.Target_SAP__c` | Potential / target SAP score |
| Custom Field | `Asset.Target_EPC_Band__c` | Target EPC band |
| Permission Set | `Energy_Cert_Fields` | Read/Edit on the three fields above |

# Configuration
Objects supported: Asset (record page)

Fields used:

| Label | API name | Type | Drives |
|---|---|---|---|
| Current SAP Score | `Current_SAP_Score__c` | Number (3, 0) | **Current** arrow, placed in the band containing the score |
| Target SAP | `Target_SAP__c` | Number (3, 0) | **Potential** arrow, placed the same way |
| Target EPC Band | `Target_EPC_Band__c` | Picklist (A–G) | **Target** marker on that band |

SAP bands: A 92+, B 81–91, C 69–80, D 55–68, E 39–54, F 21–38, G 0–20. Decimal scores are rounded before banding; a blank field simply hides its arrow/marker.

# Installation
```bash
sf project deploy start --source-dir force-app --target-org <alias>
sf org assign permset --name Energy_Cert_Fields --target-org <alias>
```
Assign `Energy_Cert_Fields` to every user who needs to see or edit the fields — without it the fields are invisible and the component shows no arrows.

Then:
1. Open an Asset record → **Edit Page** → drag **Energy Certificate** onto the page → Save / Activate.
2. Add the three fields to the Asset page layout (Setup → Object Manager → Asset → Page Layouts) or, with Dynamic Forms, from the **Fields** tab in Lightning App Builder.
3. Populate the SAP fields on an Asset to see the graph.

# Creator : Alastair Dutton at Salesforce

# Owner: Alastair Dutton

# Update History
Etienne-SFDO: Will now correctly handle & display out of bound field values

Etienne-SFDO: Required Asset fields and `Energy_Cert_Fields` permission set are now deployed with the component
