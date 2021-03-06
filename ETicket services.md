# es

This is "nn::es::IETicketService".

| Cmd  | Name                                                                                    |
| ---- | --------------------------------------------------------------------------------------- |
| 1    | ImportTicket                                                                            |
| 2    | ImportTicketCertificateSet                                                              |
| 3    | DeleteTicket                                                                            |
| 4    | DeletePersonalizedTicket                                                                |
| 5    | DeleteAllCommonTicket                                                                   |
| 6    | DeleteAllPersonalizedTicket                                                             |
| 7    | DeleteAllPersonalizedTicketEx                                                           |
| 8    | \[2.0.0-5.1.0\] GetTitleKey                                                             |
| 9    | CountCommonTicket                                                                       |
| 10   | CountPersonalizedTicket                                                                 |
| 11   | \[6.0.0+\] ListCommonTicketRightsIds (\[2.0.0-5.1.0\] ListCommonTicket)                 |
| 12   | \[6.0.0+\] ListPersonalizedTicketRightsIds (\[2.0.0-5.1.0\] ListPersonalizedTicket)     |
| 13   | ListMissingPersonalizedTicket                                                           |
| 14   | GetCommonTicketSize                                                                     |
| 15   | \[2.0.0-4.1.0\] GetPersonalizedTicketSize                                               |
| 16   | GetCommonTicketData                                                                     |
| 17   | \[2.0.0-4.1.0\] GetPersonalizedTicketData                                               |
| 18   | OwnTicket                                                                               |
| 19   | GetTicketInfo                                                                           |
| 20   | ListLightTicketInfo                                                                     |
| 21   | \[2.0.0-6.2.0\] SignData                                                                |
| 22   | \[4.0.0+\] GetCommonTicketAndCertificateSize                                            |
| 23   | \[4.0.0+\] GetCommonTicketAndCertificateData                                            |
| 24   | \[4.0.0+\] ImportPrepurchaseRecord                                                      |
| 25   | \[4.0.0+\] DeletePrepurchaseRecord                                                      |
| 26   | \[4.0.0+\] DeleteAllPrepurchaseRecord                                                   |
| 27   | \[4.0.0+\] CountPrepurchaseRecord                                                       |
| 28   | \[6.0.0+\] ListPrepurchaseRecordRightsIds (\[4.0.0-5.1.0\] ListPrepurchaseRecord)       |
| 29   | \[4.0.0+\] [\#ListPrepurchaseRecordInfo](#ListPrepurchaseRecordInfo "wikilink")         |
| 30   | \[5.0.0+\] CountTicket                                                                  |
| 31   | \[5.0.0+\] ListTicketRightsIds                                                          |
| 32   | \[5.0.0+\] CountPrepurchaseRecordEx                                                     |
| 33   | \[5.0.0-6.2.0\] ListPrepurchaseRecordRightsIdsEx                                        |
| 34   | \[5.0.0+\] GetEncryptedTicketSize                                                       |
| 35   | \[5.0.0+\] [\#GetEncryptedTicketData](#GetEncryptedTicketData "wikilink")               |
| 36   | \[6.0.0+\] DeleteAllInactiveELicenseRequiredPersonalizedTicket                          |
| 37   | \[9.0.0+\] OwnTicket2                                                                   |
| 38   | \[9.0.0+\] OwnTicket3                                                                   |
| 501  | \[6.0.0+\]                                                                              |
| 502  | \[6.0.0+\]                                                                              |
| 503  | \[6.0.0+\] [\#GetTitleKey](#GetTitleKey "wikilink")                                     |
| 504  | \[6.0.0+\]                                                                              |
| 508  | \[6.0.0+\]                                                                              |
| 509  | \[6.0.0+\]                                                                              |
| 510  | \[6.0.0+\]                                                                              |
| 511  | \[9.0.0+\]                                                                              |
| 1001 | \[6.0.0+\]                                                                              |
| 1002 | \[6.0.0+\]                                                                              |
| 1003 | \[6.0.0+\] Returns an [\#EsAsyncValue](#EsAsyncValue "wikilink").                       |
| 1004 | \[6.0.0+\]                                                                              |
| 1005 | \[6.0.0+\]                                                                              |
| 1006 | \[6.0.0+\]                                                                              |
| 1007 | \[6.0.0+\]                                                                              |
| 1009 | \[6.0.0+\]                                                                              |
| 1010 | \[6.0.0+\]                                                                              |
| 1011 | \[6.0.0+\]                                                                              |
| 1012 | \[6.0.0+\]                                                                              |
| 1013 | \[6.0.0+\]                                                                              |
| 1014 | \[6.0.0+\]                                                                              |
| 1015 | \[6.0.0+\]                                                                              |
| 1016 | \[6.0.0+\]                                                                              |
| 1017 | \[9.0.0+\]                                                                              |
| 1018 | \[9.0.0+\]                                                                              |
| 1019 | \[9.0.0+\]                                                                              |
| 1020 | \[9.0.0+\]                                                                              |
| 1021 | \[9.0.0+\]                                                                              |
| 1501 | \[6.0.0+\]                                                                              |
| 1502 | \[6.0.0+\]                                                                              |
| 1503 | \[6.0.0+\]                                                                              |
| 1504 | \[6.0.0+\]                                                                              |
| 1505 | \[6.0.0+\]                                                                              |
| 2000 | \[6.0.0+\] No input, returns an [\#EsSubinterface2000](#EsSubinterface2000 "wikilink"). |
| 2001 | \[9.0.0+\] No input, returns an [\#EsSubinterface2000](#EsSubinterface2000 "wikilink"). |
| 2100 | \[7.0.0+\]                                                                              |
| 2501 | \[6.0.0+\]                                                                              |
| 2502 | \[6.0.0+\]                                                                              |
| 3001 | \[7.0.0+\]                                                                              |
| 3002 | \[7.0.0+\]                                                                              |

## ListPrepurchaseRecordInfo

\[7.0.0+\] 0x8-bytes of input for ListPrepurchaseRecordInfo was removed.

## GetEncryptedTicketData

\[6.0.0+\] Now returns an additional 8-bytes.

## GetTitleKey

\[3.0.0+\] GetTitleKey now takes an additional 4-bytes of input.

## EsAsyncValue

This was added with \[6.0.0+\].

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |

## EsSubinterface2000

This was added with \[6.0.0+\].

| Cmd  | Name       |
| ---- | ---------- |
| 1    |            |
| 2    |            |
| 3    |            |
| 4    |            |
| 5    |            |
| 6    |            |
| 7    |            |
| 8    |            |
| 9    |            |
| 10   |            |
| 11   | \[8.0.0+\] |
| 100  |            |
| 101  |            |
| 102  |            |
| 200  |            |
| 201  |            |
| 202  |            |
| 203  |            |
| 210  |            |
| 211  |            |
| 900  |            |
| 901  |            |
| 1000 |            |
| 1001 | \[7.0.0+\] |
|      |            |

\[8.0.0+\] Cmd201 now returns an additional 0x8-bytes of output.
