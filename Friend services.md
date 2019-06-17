# friend:u, friend:v, friend:m, friend:s, friend:a

This is "nn::friends::detail::ipc::IServiceCreator".

| Cmd | Name                                         | Notes                                                                                         |
| --- | -------------------------------------------- | --------------------------------------------------------------------------------------------- |
| 0   | CreateFriendService                          | Returns an [\#IFriendService](#IFriendService "wikilink").                                    |
| 1   | \[2.0.0+\] CreateNotificationService         | Takes an input userID and returns [\#INotificationService](#INotificationService "wikilink"). |
| 2   | \[4.0.0+\] CreateDaemonSuspendSessionService | Returns an [\#IDaemonSuspendSessionService](#IDaemonSuspendSessionService "wikilink").        |

## IFriendService

This is "nn::friends::detail::ipc::IFriendService".

| Cmd   | Name                                                     |
| ----- | -------------------------------------------------------- |
| 0     | GetCompletionEvent                                       |
| 1     | Cancel                                                   |
| 10100 | GetFriendListIds                                         |
| 10101 | GetFriendList                                            |
| 10102 | UpdateFriendInfo                                         |
| 10110 | GetFriendProfileImage                                    |
| 10200 | SendFriendRequestForApplication                          |
| 10211 | AddFacedFriendRequestForApplication                      |
| 10400 | GetBlockedUserListIds                                    |
| 10500 | GetProfileList                                           |
| 10600 | DeclareOpenOnlinePlaySession                             |
| 10601 | DeclareCloseOnlinePlaySession                            |
| 10610 | UpdateUserPresence                                       |
| 10700 | GetPlayHistoryRegistrationKey                            |
| 10701 | GetPlayHistoryRegistrationKeyWithNetworkServiceAccountId |
| 10702 | AddPlayHistory                                           |
| 11000 | GetProfileImageUrl                                       |
| 20100 | GetFriendCount                                           |
| 20101 | GetNewlyFriendCount                                      |
| 20102 | GetFriendDetailedInfo                                    |
| 20103 | SyncFriendList                                           |
| 20104 | RequestSyncFriendList                                    |
| 20110 | LoadFriendSetting                                        |
| 20200 | GetReceivedFriendRequestCount                            |
| 20201 | GetFriendRequestList                                     |
| 20300 | GetFriendCandidateList                                   |
| 20301 | \[3.0.0+\] GetNintendoNetworkIdInfo                      |
| 20302 | \[5.0.0+\] GetSnsAccountLinkage                          |
| 20303 | \[5.0.0+\] GetSnsAccountProfile                          |
| 20304 | \[5.0.0+\] GetSnsAccountFriendList                       |
| 20400 | GetBlockedUserList                                       |
| 20401 | SyncBlockedUserList                                      |
| 20500 | GetProfileExtraList                                      |
| 20501 | GetRelationship                                          |
| 20600 | GetUserPresenceView                                      |
| 20700 | GetPlayHistoryList                                       |
| 20701 | GetPlayHistoryStatistics                                 |
| 20800 | LoadUserSetting                                          |
| 20801 | SyncUserSetting                                          |
| 20900 | RequestListSummaryOverlayNotification                    |
| 21000 | GetExternalApplicationCatalog                            |
| 30100 | DropFriendNewlyFlags                                     |
| 30101 | DeleteFriend                                             |
| 30110 | DropFriendNewlyFlag                                      |
| 30120 | ChangeFriendFavoriteFlag                                 |
| 30121 | ChangeFriendOnlineNotificationFlag                       |
| 30200 | SendFriendRequest                                        |
| 30201 | SendFriendRequestWithApplicationInfo                     |
| 30202 | CancelFriendRequest                                      |
| 30203 | AcceptFriendRequest                                      |
| 30204 | RejectFriendRequest                                      |
| 30205 | ReadFriendRequest                                        |
| 30210 | GetFacedFriendRequestRegistrationKey                     |
| 30211 | AddFacedFriendRequest                                    |
| 30212 | CancelFacedFriendRequest                                 |
| 30213 | GetFacedFriendRequestProfileImage                        |
| 30214 | GetFacedFriendRequestProfileImageFromPath                |
| 30215 | SendFriendRequestWithExternalApplicationCatalogId        |
| 30216 | ResendFacedFriendRequest                                 |
| 30217 | \[3.0.0+\] SendFriendRequestWithNintendoNetworkIdInfo    |
| 30300 | \[5.0.0+\] GetSnsAccountLinkPageUrl                      |
| 30301 | \[5.0.0+\] UnlinkSnsAccount                              |
| 30400 | BlockUser                                                |
| 30401 | BlockUserWithApplicationInfo                             |
| 30402 | UnblockUser                                              |
| 30500 | GetProfileExtraFromFriendCode                            |
| 30700 | DeletePlayHistory                                        |
| 30810 | ChangePresencePermission                                 |
| 30811 | ChangeFriendRequestReception                             |
| 30812 | ChangePlayLogPermission                                  |
| 30820 | IssueFriendCode                                          |
| 30830 | ClearPlayLog                                             |
| 49900 | DeleteNetworkServiceAccountCache                         |

## INotificationService

This is "nn::friends::detail::ipc::INotificationService".

| Cmd | Name     |
| --- | -------- |
| 0   | GetEvent |
| 1   | Clear    |
| 2   | Pop      |

## IDaemonSuspendSessionService

This is "nn::friends::detail::ipc::IDaemonSuspendSessionService".

| Cmd | Name       |
| --- | ---------- |
| 0   | \[4.0.0+\] |
| 1   | \[4.0.0+\] |
| 2   | \[4.0.0+\] |
| 3   | \[4.0.0+\] |
| 4   | \[4.0.0+\] |

# nd:app

# nd:sys

[Category:Services](Category:Services "wikilink")
