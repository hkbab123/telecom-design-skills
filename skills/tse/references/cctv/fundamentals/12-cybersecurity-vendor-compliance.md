# Cybersecurity and Vendor Compliance

**Banned-vendor-list restrictions.** A growing number of rail and government-adjacent projects (and some O&G projects working with government/critical-infrastructure clients) explicitly exclude cameras, VMS software, or components from named manufacturers on national-security grounds — this is a real, spec-level requirement in many jurisdictions now, not a hypothetical. It must be confirmed at Tender stage (rule 3) and checked against the actual OEM shortlist before any commitment — discovering a banned-vendor conflict after equipment has been selected, let alone installed, is expensive and sometimes legally serious to unwind.

**IT/OT segmentation for the VMS network.** The same principle SCADA applies for its control network applies to a VMS network: segregate it from general IT/office traffic and from any OT/process-control network, with a defined DMZ or controlled interface point for any data that needs to cross (e.g. a PSIM correlating CCTV alerts with access-control events on a different network). Camera firmware vulnerabilities are a well-documented attack surface — treating a camera as "just an IoT device with no security implication" is a mistake.

**Firmware/patch management.** IP cameras and VMS software need an ongoing patch-management process, the same as any networked device — define who owns this (client IT, the integrator under a maintenance contract, or a hybrid) at Tender stage, not as an afterthought once the system is live.

**VMS authentication and access control.** Role-based access to the VMS (who can view live, who can export/download footage, who can delete/modify retention settings) is both a cybersecurity and an evidentiary-integrity concern — an unrestricted "everyone can export and delete" configuration undermines any chain-of-custody value the recorded footage might otherwise have.

**Why this matters for design decisions:** this is the subsystem-specific rule (3) most likely to be missed by an engineer trained on CCTV as a purely technical/optical problem — flag vendor-compliance and cybersecurity requirements at the very start of Tender-stage spec development, alongside coverage-zone scoping, not after equipment selection.

**Formal reference:** no single unifying standard — national procurement/security regulations vary by jurisdiction (confirm the applicable restriction per project and client), general cybersecurity practice aligned with ISO/IEC 27001 and the same IEC 62443 IT/OT segmentation discipline used for SCADA.
