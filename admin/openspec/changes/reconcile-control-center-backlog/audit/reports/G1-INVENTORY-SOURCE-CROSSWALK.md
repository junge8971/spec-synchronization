# G1-INVENTORY-SOURCE-CROSSWALK — E12/E12a local accounting

**Proposed accounting receipt; independent review pending.** Every accepted direct-member and observed nested row is mapped below. This is not renewed Jira discovery, semantic acceptance or source-sufficiency approval. **E13 remains separate/open; tasks2.3/2.4/2.6 and global6/28 unchanged.**

`C` = `openspec/changes/reconcile-control-center-backlog`; `A` = `C/audit`. All abbreviated paths expand literally beneath A. Cutoff: accepted records through **D-058 / coverage-partial-r41**, plus this run's explicitly scoped local path discovery. External freshness was not checked. Accepted timestamps, hashes, acquisition safeguards and prior field inspections remain attributed to their collectors/reviewers/parent; none was independently recertified.

## 1. Evidence conventions and actual coverage

The membership authority is `inventory-acceptance.json:1–33` and complete `inventory-reconciliation.json`: **26 modules /157 direct members /16 observed nested subtasks**, membership only. All26 referenced inventory reports were read completely, not their underlying hierarchy/index bodies. Their historical collection suggestions are not adopted as new requests.

Baseline aliases:

- **H** = `sources/jira-hierarchy/r1/content.json`, retrieved2026-10-16T11:08:08.629Z. H(r,c) means `/results/r/children/c`; module row is `/results/r`.
- **I** = `sources/jira-member-index/r1/content.json`, retrieved2026-10-16T11:20:38.570Z. I(n) means `/items/n`. **B** coverage: selected key/summary/type/status/updated/subtasks; description, comments, attachment field and custom acceptance fields omitted. Actual records omit parent; H establishes membership. Missing fields are not zero.
- **S** = `sources/jira-subtasks/r1/content.json`, retrieved2026-10-16T11:23:01.951Z. S(n) means `/items/n`; selected description, parent and attachment metadata retained, comments/custom acceptance fields omitted, attachment bodies not acquired in that capture. Packet redaction limits remain.
- **F** = `sources/jira-feedback/r1/content.json`, retrieved2026-10-16T11:17:16.813Z. F(n) means `/items/n`; descriptions and selected identity/status/update/subtask fields retained; parent/comments/attachment indexes/custom acceptance fields omitted.
- **AD** = `sources/jira-api-delta-scenarios/r1/content.json`, retrieved2026-10-16T11:23:51.742Z. AD(n) means `/items/n`. This supplement already appears in accepted782/783 inventories; it is not an additional member or necessarily a later acquisition than every inventory report.

Every source alias includes its adjacent `metadata.json` as attributed provenance; metadata presence does not imply fields omitted from the content were returned. No primary source body or metadata was reopened here. `source-checkpoint-r1.json:1–110` corroborates these saved packet/index paths; r2's complete supplemental register and `collection-checkpoint.md:1–165` are historical/additive, not exhaustive present registries.

### Later accepted source coverage dictionary

**L** = complete `reports/G1-JIRA-DETAIL-DOCUMENT-EDGES.md:1–175`, especially coverage `:15–31`, attachment ledger `:72–103`; complete review `reviews/R-G1-JIRA-DETAIL-DOCUMENT-EDGES.md:1–143`; accepted **D-046**.

**P** = complete `reports/G1-JIRA-SPECIAL-DOCUMENT-EDGES.md:1–122`, especially `:11–24`; complete review `reviews/R-G1-JIRA-SPECIAL-DOCUMENT-EDGES.md:1–120`; accepted **D-047**.

`ALIAS(n)` below means exact `/items/n` in the named JSON content, with the row's coverage below; singleton Markdown or object packets use their explicit locator. All JSON descriptions are the saved descriptions, not certification of full remote exports. All custom acceptance fields and separate remote-link indexes remain outside this inspected accepted coverage. Description prose is not a collected custom field.

| Join | Exact packet / accepted evidence | Description; comments; attachment field/body disposition |
|---|---|---|
| **U** | Accepted inventory row + no issue-detail join in L/P or inspected later checkpoint/disposition records | B remains the positive evidence. Description/comments/attachment metadata and bodies/custom fields **unverified within inspected records** because baseline selected extraction omitted them and no accepted later join was identified. Not global missing/deleted, remote denial, irrelevance or an instruction to fetch. |
| AD(n) | `sources/jira-api-delta-scenarios/r1/content.json`; L coverage AD | Description retained; comments omitted. n0/1/2 each have one indexed plan839666/839773/839665 respectively; n3 explicitly `attachments:[]`. Bodies of those three plans index-only under L/D046; no body authority. |
| SK(n) | `sources/jira-details-MOS-774/r1/content.json:1`; L coverage SK | Descriptions retained for n0–18; comments omitted. n1 indexed817149/825983/817148; n2 indexed817153/817152/826603/817151; n3 indexed817155/817154; n0,n4–18 empty saved attachment arrays. All nine indexed bodies remain index-only per L. |
| LC | `sources/jira-lifecycle-details/r2/content.md:1–67`; L coverage LC | MOS1119 only: normalized description/tables, two selected comment excerpts1122856/1125304, not complete original wording/MR URL. Attachment833803 indexed at59–63 and body retained `sources/jira-attachment-833803/r1/content.md`, accepted D017 via L. |
| MN(n) | `sources/jira-monitoring-details/r1/content.json:1–195`; L coverage MN | Descriptions retained; singular `attachment:[]` each. `comment/comments` counts n0/1/2/3 =0/1/0/0, matching saved totals; n1 comment1126159. |
| OP(n) | `sources/jira-operations-details/r1/content.json:1–121`; L coverage OP | Descriptions retained; `attachments:[]` each. `comments/items`: n0 has2/2 comments1131251/1131293; n1–4 have0/0. |
| RP(n) | `sources/jira-reports-details/r1/content.json:1–134`; L coverage RP | Descriptions retained; `attachments:[]` each. `comments/items`: n4 has1/1 comment1120059; n0–3,n5 have0/0. |
| SB(n) | `sources/jira-sandbox-details/r1/content.json:1–70`; L coverage SB | Descriptions retained; empty attachments and comments/items0/0 each. |
| SH(n) | `sources/jira-shell-details/r1/content.json:1–240`; L coverage SH | Descriptions retained; comments/items n0–5 counts0/1/1/1/2/2, matching saved totals. n1 indexed817138/825952/817137; n2 indexed817141/826497/817140; n3 indexed817144/825968/817143; n0,n4,n5 empty arrays. Nine bodies index-only under L. |
| SW(n) | `sources/jira-skill-switch-details/r1/content.json:1–183`; L coverage SW | Descriptions retained; n0 empty singular attachment and0 comments; n1 attachment835759 and2/2 comments1125431/1127708. Body retained `sources/jira-attachment-835759/r1/content.md`, accepted D030 via L; older unread wording superseded for this exact ID only. |
| F(n)/P | Same baseline F packet; P coverage F, D047 | Later accepted coverage review, **not a new capture**: saved descriptions retained, comments/attachment indexes still omitted for all12 records. No filename/title binding to wiki prototypes. |
| J909 | `sources/jira-MOS-909/r1/content.md:1–25`; P coverage L | Normalized description; returned empty attachment/subtask arrays reported in extraction, not raw arrays. Two comments1122872 reduced MR excerpt and1122881 verbatim; omitted URLs/custom fields remain unknown. |
| J1321 | `sources/jira-MOS-1321/r1/content.json:1–31`; P coverage D | `/description`; `/attachments:[]`; comments/items1129117 omitted-MR-body placeholder +1129414 text, start0/max2/total2. |
| J1386 | `sources/jira-MOS-1386/r1/content.json:1–31`; P coverage R | Same selected schema; empty attachments; comments1131237 omitted-MR placeholder +1131540 text, start0/max2/total2. |
| J1399 | `sources/jira-MOS-1399/r1/content.json:1–31`; P coverage T | Same selected schema; empty attachments; comments1131561 omitted-MR placeholder +1131702 text, start0/max2/total2. |

These codes are explicit per-row extraction/unknown dispositions, not a claim the fourteen bundles exhaust all retained files. Saved zero counts are bounded to their captured response pages, not hidden/current Jira completeness. L's50 records and P's16 include module parents and selected revisions: **no subtraction from157** is used.

## 2. Module register and baseline locators

Each report path is `reports/JIRA-MOS-<module>.md`. The listed complete read ranges are also the exact accepted evidence locators for the member tables in §3. For non-feedback modules, H child position for §3 is the member's zero-based order within its module, as established by the accepted reports. Feedback is exempt: `reports/JIRA-MOS-1246.md:10–19` establishes hierarchy membership, but individual feedback H child positions were not independently established from the consulted accepted reports. Exact F(1–11) detail pointers remain; F(0) is its separate parent.

| Module | H result r | Direct / nested | Accepted report completely read | Parent detail disposition in inspected accepted records |
|---|---:|---:|---|---|
| MOS-624 | 0 |29/1|`reports/JIRA-MOS-624.md:1–69`|Hierarchy initially; SH(0) later selected description/comments0/index empty.|
| MOS-651 |1|5/0|`reports/JIRA-MOS-651.md:1–45`|Hierarchy only; full parent fields unverified, selected hierarchy omitted them.|
| MOS-652 |2|4/0|`reports/JIRA-MOS-652.md:1–68`|Same hierarchy-only limit.|
| MOS-768 |3|4/0|`reports/JIRA-MOS-768.md:1–85`|Same.|
| MOS-769 |4|2/0|`reports/JIRA-MOS-769.md:1–38`|Same.|
| MOS-770 |5|0/0|`reports/JIRA-MOS-770.md:1–38`|Explicit empty observed children; parent detail unverified.|
| MOS-771 |6|1/1|`reports/JIRA-MOS-771.md:1–55`|Hierarchy only; parent detail unverified.|
| MOS-772 |7|0/0|`reports/JIRA-MOS-772.md:1–35`|Explicit empty observed children; parent detail unverified.|
| MOS-773 |8|11/5|`reports/JIRA-MOS-773.md:1–69`|Hierarchy only; parent detail unverified.|
| MOS-774 |9|18/3|`reports/JIRA-MOS-774.md:1–55`|SK(0) supplies selected description/empty attachment array; comments omitted.|
| MOS-775 |10|3/0|`reports/JIRA-MOS-775.md:1–49`|MN(0) supplies description, saved0 comments/empty attachments.|
| MOS-776 |11|1/0|`reports/JIRA-MOS-776.md:1–51`|SW(0) supplies description, saved0 comments/empty attachments.|
| MOS-777 |12|5/0|`reports/JIRA-MOS-777.md:1–46`|RP(0) supplies description, saved0 comments/empty attachments.|
| MOS-778 |13|6/0|`reports/JIRA-MOS-778.md:1–39`|Hierarchy only; parent detail unverified.|
| MOS-780 |14|1/0|`reports/JIRA-MOS-780.md:1–59`|Same.|
| MOS-781 |15|1/0|`reports/JIRA-MOS-781.md:1–36`|Same.|
| MOS-782 |16|25/0|`reports/JIRA-MOS-782.md:1–67`|Hierarchy only; LC r1 request timed out/no payload, no later parent join established.|
| MOS-783 |17|18/5|`reports/JIRA-MOS-783.md:1–72`|Hierarchy only; parent detail unverified.|
| MOS-784 |18|4/1|`reports/JIRA-MOS-784.md:1–55`|Same.|
| MOS-788 |19|0/0|`reports/JIRA-MOS-788.md:1–55`|Explicit empty observed children; parent detail unverified.|
| MOS-1246 |20|11/0|`reports/JIRA-MOS-1246.md:1–52`|F(0) baseline description; P later confirms same selected fields, not a full issue export.|
| MOS-1327 |21|2/0|`reports/JIRA-MOS-1327.md:1–44`|Hierarchy only; parent detail unverified.|
| MOS-1328 |22|2/0|`reports/JIRA-MOS-1328.md:1–57`|Same.|
| MOS-1329 |23|2/0|`reports/JIRA-MOS-1329.md:1–53`|Same.|
| MOS-1388 |24|1/0|`reports/JIRA-MOS-1388.md:1–35`|Same.|
| MOS-1403 |25|1/0|`reports/JIRA-MOS-1403.md:1–44`|Same.|

Module identity is Q key result, not a literal Epic or a full parent issue. Empty observed children/subtasks and statuses establish neither hidden-issue absence nor completion. Parent rows are separate from the157 direct-member population.

## 3. E12 — every direct member

Each I row has B baseline coverage; supplemental baseline AD coverage is stated explicitly. Last column is its exact later accepted packet/report join or U reason defined in §1, not semantic acceptance. For non-feedback modules, grouping preserves the accepted member-table order and therefore the exact H child position. Feedback rows preserve exact F detail order and accepted hierarchy membership only; no individual H child-position inference is made. No member is grouped away.

| Module | Member | Baseline record | Current accepted join / extraction disposition |
|---|---|---|---|
|624|MOS-668|I(0)|U|
|624|MOS-659|I(1)|U|
|624|MOS-660|I(2)|U|
|624|MOS-661|I(3)|U|
|624|MOS-664|I(4)|U|
|624|MOS-666|I(5)|U; nested1053 separately S(0)|
|624|MOS-665|I(6)|U|
|624|MOS-663|I(7)|U|
|624|MOS-646|I(8)|U|
|624|MOS-669|I(9)|U|
|624|MOS-672|I(10)|SH(1)|
|624|MOS-673|I(11)|SH(2)|
|624|MOS-674|I(12)|SH(3)|
|624|MOS-685|I(13)|U|
|624|MOS-699|I(14)|U|
|624|MOS-717|I(15)|OP(0)|
|624|MOS-754|I(16)|OP(1)|
|624|MOS-755|I(17)|U|
|624|MOS-767|I(18)|U|
|624|MOS-904|I(19)|SH(4)|
|624|MOS-905|I(20)|SH(5)|
|624|MOS-923|I(21)|OP(4)|
|624|MOS-961|I(22)|SB(1)|
|624|MOS-922|I(23)|OP(3)|
|624|MOS-962|I(24)|SB(2)|
|624|MOS-960|I(25)|SB(0)|
|624|MOS-920|I(26)|OP(2)|
|624|MOS-1049|I(27)|U|
|624|MOS-1142|I(28)|U|
|651|MOS-927|I(29)|U|
|651|MOS-1009|I(30)|U|
|651|MOS-1024|I(31)|U|
|651|MOS-1029|I(32)|U|
|651|MOS-1034|I(33)|U|
|652|MOS-756|I(34)|U|
|652|MOS-670|I(35)|U|
|652|MOS-671|I(36)|U|
|652|MOS-912|I(37)|U|
|768|MOS-836|I(38)|U|
|768|MOS-931|I(39)|U|
|768|MOS-1032|I(40)|U|
|768|MOS-1033|I(41)|U|
|769|MOS-903|I(42)|U|
|769|MOS-908|I(43)|U|
|771|MOS-816|I(44)|U; nested1150 separately S(1)|
|773|MOS-703|I(45)|U|
|773|MOS-889|I(46)|U|
|773|MOS-1037|I(47)|U; five nested rows separately S(2–6)|
|773|MOS-1038|I(48)|U|
|773|MOS-1040|I(49)|U|
|773|MOS-1041|I(50)|U|
|773|MOS-1042|I(51)|U|
|773|MOS-1043|I(52)|U|
|773|MOS-1044|I(53)|U|
|773|MOS-1045|I(54)|U|
|773|MOS-1211|I(55)|U|
|774|MOS-675|I(56)|SK(1)|
|774|MOS-676|I(57)|SK(2); nested1050/1051 separately|
|774|MOS-677|I(58)|SK(3); nested1052 separately|
|774|MOS-701|I(59)|SK(4)|
|774|MOS-944|I(60)|SK(5)|
|774|MOS-945|I(61)|SK(6)|
|774|MOS-1018|I(62)|SK(7)|
|774|MOS-1019|I(63)|SK(8)|
|774|MOS-1020|I(64)|SK(9)|
|774|MOS-1021|I(65)|SK(10)|
|774|MOS-1022|I(66)|SK(11)|
|774|MOS-1023|I(67)|SK(12)|
|774|MOS-1025|I(68)|SK(13)|
|774|MOS-1026|I(69)|SK(14)|
|774|MOS-1027|I(70)|SK(15)|
|774|MOS-1030|I(71)|SK(16)|
|774|MOS-1031|I(72)|SK(17)|
|774|MOS-1409|I(73)|SK(18)|
|775|MOS-1146|I(74)|MN(1)|
|775|MOS-1397|I(75)|MN(2)|
|775|MOS-1398|I(76)|MN(3)|
|776|MOS-1145|I(77)|SW(1); exact835759 body accepted D030|
|777|MOS-885|I(78)|RP(1)|
|777|MOS-916|I(79)|RP(2)|
|777|MOS-919|I(80)|RP(3)|
|777|MOS-1015|I(81)|RP(4)|
|777|MOS-1016|I(82)|RP(5)|
|778|MOS-734|I(83)|U|
|778|MOS-818|I(84)|U|
|778|MOS-915|I(85)|U|
|778|MOS-1011|I(86)|U|
|778|MOS-1012|I(87)|U|
|778|MOS-1013|I(88)|U|
|780|MOS-713|I(89)|U|
|781|MOS-890|I(90)|U|
|782|MOS-802|I(91)|U|
|782|MOS-803|I(92)|U|
|782|MOS-804|I(93)|U|
|782|MOS-805|I(94)|U|
|782|MOS-806|I(95)|U|
|782|MOS-811|I(96)|U|
|782|MOS-809|I(97)|U|
|782|MOS-808|I(98)|U|
|782|MOS-807|I(99)|U|
|782|MOS-810|I(100)|U|
|782|MOS-859|I(101)|U|
|782|MOS-907|I(102)|U|
|782|MOS-909|I(103)|J909; supersedes only its LC-r1 no-payload gap|
|782|MOS-935|I(104)|U|
|782|MOS-942|I(105)|U|
|782|MOS-929|I(106)|U|
|782|MOS-933|I(107)|U|
|782|MOS-1119|I(108)|LC; selected r2 + exact833803 body D017|
|782|MOS-1120|I(109)|U plus LC r1 timeout/no payload; not repaired by MOS1119/909|
|782|MOS-1141|I(110)|U|
|782|MOS-1153|I(111)|U|
|782|MOS-1157|I(112)|U|
|782|MOS-1245|I(113) + AD(0)|AD(0)/L; indexed839666, body index-only|
|782|MOS-1306|I(114) + AD(1)|AD(1)/L; indexed839773, body index-only|
|782|MOS-1381|I(115)|U|
|783|MOS-707|I(116)|U|
|783|MOS-708|I(117)|U|
|783|MOS-709|I(118)|U; five nested rows separately S(10–14)|
|783|MOS-712|I(119)|U|
|783|MOS-901|I(120)|U|
|783|MOS-910|I(121)|U|
|783|MOS-911|I(122)|U|
|783|MOS-913|I(123)|U|
|783|MOS-914|I(124)|U|
|783|MOS-958|I(125)|U|
|783|MOS-959|I(126) + AD(3)|AD(3)/L; explicit empty attachment array|
|783|MOS-976|I(127)|U|
|783|MOS-1130|I(128)|U|
|783|MOS-1178|I(129)|U|
|783|MOS-1237|I(130) + AD(2)|AD(2)/L; indexed839665, body index-only|
|783|MOS-1308|I(131)|U|
|783|MOS-1336|I(132)|U|
|783|MOS-1407|I(133)|U|
|784|MOS-704|I(134)|U|
|784|MOS-705|I(135)|U; nested1054 separately S(15)|
|784|MOS-706|I(136)|U|
|784|MOS-906|I(137)|U|
|1327|MOS-1321|I(138)|J1321|
|1327|MOS-1399|I(139)|J1399|
|1328|MOS-1322|I(140)|U|
|1328|MOS-1362|I(141)|U|
|1329|MOS-1323|I(142)|U|
|1329|MOS-1384|I(143)|U|
|1388|MOS-1387|I(144)|U|
|1403|MOS-1386|I(145)|J1386|
|1246|MOS-1231|F(1)|F(1)/P; attachment/comment fields omitted|
|1246|MOS-1249|F(2)|F(2)/P; same omission|
|1246|MOS-1250|F(3)|F(3)/P; same omission|
|1246|MOS-1251|F(4)|F(4)/P; same omission|
|1246|MOS-1254|F(5)|F(5)/P; same omission|
|1246|MOS-1255|F(6)|F(6)/P; same omission|
|1246|MOS-1256|F(7)|F(7)/P; same omission|
|1246|MOS-1257|F(8)|F(8)/P; same omission|
|1246|MOS-1258|F(9)|F(9)/P; same omission|
|1246|MOS-1259|F(10)|F(10)/P; same omission|
|1246|MOS-1260|F(11)|F(11)/P; same omission|

**Manual row reconciliation:** I(0–145) each appears once, plus F(1–11) each once =157 direct rows, matching the accepted report partition; no new graph check. Three explicit empty modules have no direct rows to invent. U does not erase H/I identity evidence or imply no related wiki/API/business reports exist: such reports cannot fill omitted issue fields merely by discussing the same scenario.

### Named documentary supersession, not blanket enrichment

Issue-detail joins above are distinct from later retention of their linked wiki documents. Incorporate L's exact carrier/target pointers `:45–70`, P's sole MOS909→241097511 row `:35–55`, `reports/G1-JIRA-CONTRACT-COLLECTION-DELTA.md:25–47`, and D048–056 in `decisions.md:1–110`:

- 241082009: AD(3), SK(17), SB(0), SH(5); retained r2.
- 241097511: SK(5–17), SB(0), SH(5), J909:13–14; retained r2. Earlier404 remains unexplained.
- 241085439: SK(16), RP(4); 241085838: RP(1–5); 241088180: OP(0) comment1131251; 241092242: SK(15), OP(3–4); each retained r1 under D045/L.
- 241080659: SK(5,17), SH(5), now `sources/wiki-241080659/r1/content.json`, D048.
- 241095761: SK(13,16), now `sources/wiki-241095761/r1/content.json`, D049 (metrics original REVISE retained after parent locator corrections).
- 241077434: SK(17), now `sources/wiki-241077434/r1/content.json`, D050 **accepted without report edit**, original REVISE retained.
- 223087110/222659162: SH(0), now respective `sources/wiki-ID/r1/content.json`, D052/053; retained for relevance/context, not adopted shell requirements.
- 238347672: SK(5); 241079770: SH(4), now respective `sources/wiki-ID/r1/content.json`, D055/056; original user/session REVISE and two parent corrections retained.

Thus the accepted finite13-target/41-occurrence ledger has exact retained packets; this does not add descriptions/comments to U rows or repair feedback's absent attachment fields. Linked-source indexes remain their separate populations. No all-source union, precedence, requirements ownership or runtime conclusion follows.

## 4. E12 — every observed nested row

Each row below has **S coverage** from §1 and its exact accepted report in §2. Later L/P tables do not include jira-subtasks. No later accepted replacement detail/body join for these exact nested keys was identified in the consulted records. **Current disposition N for every row:** retain the saved selected description/parent/index; comments/custom fields remain omitted by that extraction and later enrichment unverified. No assertion of full original description, hidden-subtask completeness or missing remote content. Parent direct-member detail is not supplied by its nested bug description.

| Module | Nested key | Exact referring I stub → S detail | Saved parent | Later accepted join / disposition |
|---|---|---|---|---|
|624|MOS-1053|I(5)/subtasks/0 → S(0)|MOS-666|None identified; N|
|771|MOS-1150|I(44)/subtasks/0 → S(1)|MOS-816|None identified; N; saved description redaction retained|
|773|MOS-1411|I(47)/subtasks/0 → S(2)|MOS-1037|None identified; N|
|773|MOS-1412|I(47)/subtasks/1 → S(3)|MOS-1037|None identified; N|
|773|MOS-1414|I(47)/subtasks/2 → S(4)|MOS-1037|None identified; N|
|773|MOS-1419|I(47)/subtasks/3 → S(5)|MOS-1037|None identified; N|
|773|MOS-1422|I(47)/subtasks/4 → S(6)|MOS-1037|None identified; N|
|774|MOS-1050|I(57)/subtasks/0 → S(7)|MOS-676|None identified; N|
|774|MOS-1051|I(57)/subtasks/1 → S(8)|MOS-676|None identified; N|
|774|MOS-1052|I(58)/subtasks/0 → S(9)|MOS-677|None identified; N; explicit empty attachment array|
|783|MOS-1110|I(118)/subtasks/0 → S(10)|MOS-709|None identified; N|
|783|MOS-1164|I(118)/subtasks/1 → S(11)|MOS-709|None identified; N|
|783|MOS-1165|I(118)/subtasks/2 → S(12)|MOS-709|None identified; N|
|783|MOS-1166|I(118)/subtasks/3 → S(13)|MOS-709|None identified; N|
|783|MOS-1167|I(118)/subtasks/4 → S(14)|MOS-709|None identified; N|
|784|MOS-1054|I(135)/subtasks/0 → S(15)|MOS-705|None identified; N|

All S(0–15) map once. The accepted reports establish matching parent links and explicit empty further-subtask arrays. This run reuses that acceptance, not a fresh graph census.

## 5. E12a — every exact nested attachment index row

**Historical status:** metadata/index only, bodies not downloaded in S. **Current accepted later body/disposition join:** none identified for any ID below in L/P, later consulted checkpoints or D058 receipt. **Current local path status Q:** scoped `find` under A/sources returned no matching `jira-attachment-ID/**` entries and no names containing these exact IDs. Positive control `jira-attachment-833803/**` returned its r1 directory/content.md/metadata.json. No body was opened.

For each row Q checks the literal canonical namespace `A/sources/jira-attachment-<ID>/**` (all revisions, not just r1). Search respects tool visibility/.gitignore; this is **canonical-path non-discovery**, not proof no unbound copy exists anywhere, remote404, deletion, body identity or global filesystem absence. The current body-content disposition is **historically index-only / currently unverified beyond that scoped path result**.

**No-body reason NB, applied individually below:** original selected capture enumerated metadata only; attachment-byte acquisition was not authorized/performed there and this local assignment supplies no download authority. No later accepted exact-ID body join was found. Documentary necessity/semantics remain unknown, not blanket irrelevant. These rows are not added to root39, finite Jira23 or off-root session4.

| Owner | Exact S attachment pointer | Exact ID | Historical identity/type available from accepted report | Current path / later join / reason |
|---|---|---|---|---|
|MOS-1053|`/items/0/attachments/0`|826713|404.png; image/png|Q / none identified / NB|
|MOS-1150|`/items/1/attachments/0`|831194|response_1790844958023 (1).json; application/json|Q / none identified / NB; **not screenshot-only**|
|MOS-1150|`/items/1/attachments/1`|831195|Screenshot_4.png; image/png|Q / none identified / NB|
|MOS-1411|`/items/2/attachments/0`|839653|Exact metadata ID; type not reproduced in accepted773 report|Q / none identified / NB; no type inferred|
|MOS-1412|`/items/3/attachments/0`|839662|Same report-level type limit|Q / none identified / NB|
|MOS-1414|`/items/4/attachments/0`|839675|Same report-level type limit|Q / none identified / NB|
|MOS-1419|`/items/5/attachments/0`|839862|Same report-level type limit|Q / none identified / NB|
|MOS-1422|`/items/6/attachments/0`|839906|Same report-level type limit|Q / none identified / NB|
|MOS-1422|`/items/6/attachments/1`|839905|Same report-level type limit|Q / none identified / NB|
|MOS-1050|`/items/7/attachments/0`|826531|Exact metadata ID; type not reproduced in accepted774 report|Q / none identified / NB|
|MOS-1050|`/items/7/attachments/1`|826530|Same report-level type limit|Q / none identified / NB|
|MOS-1051|`/items/8/attachments/0`|826544|Same report-level type limit|Q / none identified / NB|
|MOS-1110|`/items/10/attachments/0`|829292|2909.png; filename only here, no body inference|Q / none identified / NB|
|MOS-1164|`/items/11/attachments/0`|832277|1.png; filename only|Q / none identified / NB|
|MOS-1165|`/items/12/attachments/0`|832288|2.png; filename only|Q / none identified / NB|
|MOS-1166|`/items/13/attachments/0`|832305|3.png; filename only|Q / none identified / NB|
|MOS-1167|`/items/14/attachments/0`|832324|4.png; filename only|Q / none identified / NB|
|MOS-1167|`/items/14/attachments/1`|832323|5.png; filename only|Q / none identified / NB|
|MOS-1054|`/items/15/attachments/0`|835960|EditTools_TrimVideo1791551349542.MOV; video/quicktime|Q / none identified / NB; index-only, no playback|
|MOS-1054|`/items/15/attachments/1`|835961|XRecorder_20261009_01.mp4; video/mp4|Q / none identified / NB; index-only, no playback|

**MOS-1052:** S `/items/9/attachments` is explicitly `[]` at capture, not an omitted field and not an attachment ID. No body row or canonical filename is manufactured. Its other omitted fields remain N.

Accepted index-row evidence: `reports/JIRA-MOS-624.md:48–59`, `JIRA-MOS-771.md:15–34`, `JIRA-MOS-773.md:31–42`, `JIRA-MOS-774.md:40–49`, `JIRA-MOS-783.md:49–63`, `JIRA-MOS-784.md:28–35`; exact IDs also independently compared in `reviews/R-G1-DISPOSITION-RECEIPT.md:37–55`. Filename/size similarities never supply identity or replacement. No metadata MIME was guessed where the accepted report only listed an ID/filename.

## 6. Recommendation, exact unknowns and remaining boundary

**E12: ready for independent acceptance as bounded accounting with explicit limits.** All157 direct rows now have exact baseline packet pointers plus named accepted later coverage or the explicit U selected-extraction/no-join reason. All16 nested rows have exact stub/detail/parent mapping plus N omissions. All26 module identities, including three observed empty modules and parent-detail limitations, are represented. No known accepted row is left without a mapping/disposition in this report.

**E12a: ready for independent acceptance as index/no-body accounting with explicit limits.** Every indexed nested attachment ID has an exact S pointer, historical status, separate current scoped-path result, no later accepted join identified and NB reason. MOS1052's empty array is preserved separately. No mandatory acquisition is demonstrated by index presence.

**What remains unknown is explicit, not an unassigned remainder:** every U row's full issue fields/later enrichment outside consulted records; all N comments/custom fields; AD/SK comments; all F comments/attachment fields; LC original wording and selected MR omissions; J909/J1321/J1386/J1399 omitted MR wording; every NB body/necessity outside exact-path non-discovery. These can be accepted as accounting limitations without supplying semantics or certifying exhaustive fields. No additional generic crosswalk receipt is prescribed.

Potential concrete explanatory question supported by these records: if a pending explanation specifically depends on MOS1150's reported registry response, does the retained redacted description answer it, or is exact JSON831194 material? This is conditional necessity judgment, **not** proof the body is needed or permission to obtain it. Analogously, no video content claim is available for MOS1054; index filenames alone create no documentary requirement. Existing locator-less section7.2/MOS1249 dated-contract concerns remain in the accepted disposition receipt, not newly inferred source identities.

**E13 is not addressed/closed:** `source-checkpoint-r1.json:364–366` excludes saved-body links from its root-only enumeration. This crosswalk does not inventory root-body edges, hidden Jira material or descendants. Parent alone decides G1/source sufficiency and checkbox acceptance after independent review. Qualified API-r2 acquisition acceptance does not repair original-r1 provenance or close task2.4. Downstream owner/product/auth/runtime gates, original REVISE lineage and historical formatting issue remain unchanged.

## Code Context

### Files Retrieved

- Complete assigned `work-items/G1-INVENTORY-SOURCE-CROSSWALK.md`; complete `reports/G1-DISPOSITION-RECEIPT.md:1–151` and `reviews/R-G1-DISPOSITION-RECEIPT.md:1–127`; complete inventory acceptance/reconciliation. These supply D058 scope and accepted population.
- **All26 complete inventory reports**, exact paths/ranges enumerated in §2. No unread report tail or underlying primary graph recensus.
- Complete `C/design.md:1–133`, `C/tasks.md:1–45`, `C/specs/control-center-backlog-reconciliation/spec.md:1–108`: bounded discovery, explicit incomplete enumeration and criterion authority.
- Complete L/P reports and their complete reviews, exact paths/ranges §1. Initial report reads ended at160/110; remaining161–175/111–122 were subsequently read. Their coverage tables are the join authority, not assumed universal source inventories.
- `reports/G1-JIRA-CONTRACT-COLLECTION-DELTA.md:1–85` only; later tail not needed. Named later supersession checked against `decisions.md:1–110` (D043–058), complete `coverage-partial-r41.json`, complete `collection-checkpoint.md:1–165`, complete `source-checkpoint-r2.json:1–167`.
- `source-checkpoint-r1.json:1–110,350–366` only. Root-link middle population deliberately not read/recounted for this assignment.
- Scoped exact attachment-ID `find` results and833803 positive control; `wc -l` only to verify report/governing-file read-range citations. No attachment body or application code retrieved.

### Key Evidence

`accepted module row → H/I/F identity pointer → later accepted issue packet coverage or explicit U/N → exact attachment index pointer + separate path/disposition → independent review → parent sufficiency judgment`.

### Architecture

Membership, selected description, comment body/excerpt, attachment field, attachment metadata, bytes, documentary semantics and runtime are separate evidence layers. An issue carrying a linked contract is not a new owner assignment. Accepted later packets supersede only named historical gaps; newer collection does not overwrite baseline timestamps or raw history.

### Start Here

Read §1's coverage dictionary alongside §3's individual rows, then §5's exact-ID table. These are the actionable crosswalk, not another collection plan. Review can compare each row directly with its accepted report in §2 without opening primary Jira graph bodies.

### Validation and attribution

Manual documentary row comparison only; I(0–145)+F(1–11) and S(0–15) cover the accepted partitions. Scoped path discovery is disclosed separately from accepted historical index evidence. No hashes, original JSON parsing, byte identity, historical tool logs, remote freshness or staging state independently verified. No browser/network/credentials/downloads/rendering/playback/source execution/code/tests/build/E2E or nested delegation; no other file intentionally written. Sole report read back for review; independent review remains pending.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Explicit157 direct-member rows and16 nested rows map accepted baseline pointers to named accepted coverage or extraction/unknown reasons; every nested attachment ID separately maps its exact index pointer to historical/current scoped status and no-body reason."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/G1-INVENTORY-SOURCE-CROSSWALK.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local read and manual accepted-report crosswalk","result":"passed","summary":"All26 inventory reports and accepted later coverage tables read completely; direct and nested rows enumerated without primary graph recensus."},
    {"command":"Scoped find for exact nested attachment IDs and833803 positive control","result":"passed","summary":"No matching nested-ID canonical entries/names returned; positive control returned retained r1 content/metadata. Not global absence."},
    {"command":"wc -l on inventory reports and governing documents","result":"passed","summary":"Read-range citation lengths checked; no source execution."},
    {"command":"Network/browser/downloads/code/tests/build/E2E/hash/staging checks","result":"not-run","summary":"Outside this local documentary-only assignment; no staging attestation."}
  ],
  "validationOutput": ["157 direct rows:146 indexed plus11 feedback;16 exact nested rows;26 module rows including explicit empty modules.","E12/E12a proposed ready-with-limits for independent accounting acceptance;E13 separate/open;global6/28 unchanged."],
  "residualRisks": ["U/N and omitted-field states are bounded to inspected accepted records, not global absence or full remote coverage.","Nested attachment semantics/necessity remain unverified; scoped path non-discovery cannot exclude unbound copies or tool-hidden files.","Source sufficiency and E13 remain parent obligations after independent review; no gate closed."],
  "diffSummary":"Sole assigned crosswalk report; no historical source, registry, decision, task or code changes.",
  "reviewFindings": ["No accepted inventory row left without an explicit mapping or limitation; independent verification pending."],
  "manualNotes":"No staging-state assertion. Counts and historical integrity/acquisition claims retain accepted-register attribution. No automatic collection queue or semantic rerun."
}
```
