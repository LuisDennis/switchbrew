# acc:su

This is
"nn::account::IAccountServiceForAdministrator".

| Cmd | Name                                                                                  | Notes                                                                                                                                                 |
| --- | ------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0   | GetUserCount                                                                          |                                                                                                                                                       |
| 1   | GetUserExistence                                                                      |                                                                                                                                                       |
| 2   | ListAllUsers                                                                          |                                                                                                                                                       |
| 3   | ListOpenUsers                                                                         |                                                                                                                                                       |
| 4   | GetLastOpenedUser                                                                     |                                                                                                                                                       |
| 5   | GetProfile                                                                            | Returns an [\#IProfile](#IProfile "wikilink").                                                                                                        |
| 6   | GetProfileDigest                                                                      |                                                                                                                                                       |
| 50  | IsUserRegistrationRequestPermitted                                                    |                                                                                                                                                       |
| 51  | TrySelectUserWithoutInteraction                                                       |                                                                                                                                                       |
| 60  | \[5.0.0-5.1.0\] ListOpenContextStoredUsers                                            |                                                                                                                                                       |
| 99  | \[6.0.0+\] DebugActivateOpenContextRetention                                          | No input, returns an [\#ISessionObject](#ISessionObject "wikilink").                                                                                  |
| 100 | GetUserRegistrationNotifier                                                           | Returns an [\#INotifier](#INotifier "wikilink").                                                                                                      |
| 101 | GetUserStateChangeNotifier                                                            | Returns an [\#INotifier](#INotifier "wikilink").                                                                                                      |
| 102 | GetBaasAccountManagerForSystemService                                                 | Returns an [\#IManagerForSystemService](#IManagerForSystemService "wikilink").                                                                        |
| 103 | GetBaasUserAvailabilityChangeNotifier                                                 | Returns an [\#INotifier](#INotifier "wikilink").                                                                                                      |
| 104 | GetProfileUpdateNotifier                                                              | Returns an [\#INotifier](#INotifier "wikilink").                                                                                                      |
| 105 | \[4.0.0+\] CheckNetworkServiceAvailabilityAsync                                       | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                                                              |
| 110 | StoreSaveDataThumbnail                                                                |                                                                                                                                                       |
| 111 | ClearSaveDataThumbnail                                                                |                                                                                                                                                       |
| 112 | LoadSaveDataThumbnail                                                                 |                                                                                                                                                       |
| 113 | GetSaveDataThumbnailExistence                                                         |                                                                                                                                                       |
| 130 | \[6.0.0+\] ActivateOpenContextRetention                                               | Takes a total of 0x8-bytes of input, returns an [\#ISessionObject](#ISessionObject "wikilink").                                                       |
| 140 | \[6.0.0+\] ListQualifiedUsers                                                         |                                                                                                                                                       |
| 190 | GetUserLastOpenedApplication                                                          |                                                                                                                                                       |
| 191 | \[7.0.0+\] UpdateNotificationReceiverInfo (\[5.0.0-5.1.0\] ActivateOpenContextHolder) |                                                                                                                                                       |
| 200 | BeginUserRegistration                                                                 |                                                                                                                                                       |
| 201 | CompleteUserRegistration                                                              |                                                                                                                                                       |
| 202 | CancelUserRegistration                                                                |                                                                                                                                                       |
| 203 | DeleteUser                                                                            |                                                                                                                                                       |
| 204 | SetUserPosition                                                                       |                                                                                                                                                       |
| 205 | GetProfileEditor                                                                      | Takes an input userID and returns an [\#IProfileEditor](#IProfileEditor "wikilink").                                                                  |
| 206 | CompleteUserRegistrationForcibly                                                      |                                                                                                                                                       |
| 210 | CreateFloatingRegistrationRequest                                                     | Returns an [\#IFloatingRegistrationRequest](#IFloatingRegistrationRequest "wikilink").                                                                |
| 211 | \[8.0.0+\]                                                                            | Takes a total of 0x4-bytes of input and a handle, returns an [\#IOAuthProcedureForUserRegistration](#IOAuthProcedureForUserRegistration "wikilink").  |
| 212 | \[8.0.0+\]                                                                            | Takes a total of 0x14-bytes of input and a handle, returns an [\#IOAuthProcedureForUserRegistration](#IOAuthProcedureForUserRegistration "wikilink"). |
| 230 | AuthenticateServiceAsync                                                              | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                                                              |
| 250 | GetBaasAccountAdministrator                                                           | Returns an [\#IAdministrator](#IAdministrator "wikilink").                                                                                            |
| 290 | ProxyProcedureForGuestLoginWithNintendoAccount                                        | Returns an [\#IOAuthProcedureForExternalNsa](#IOAuthProcedureForExternalNsa "wikilink").                                                              |
| 291 | ProxyProcedureForFloatingRegistrationWithNintendoAccount                              | Returns an [\#IOAuthProcedureForExternalNsa](#IOAuthProcedureForExternalNsa "wikilink").                                                              |
| 299 | SuspendBackgroundDaemon                                                               | Returns an [\#ISessionObject](#ISessionObject "wikilink").                                                                                            |
| 997 | DebugInvalidateTokenCacheForUser                                                      |                                                                                                                                                       |
| 998 | DebugSetUserStateClose                                                                |                                                                                                                                                       |
| 999 | DebugSetUserStateOpen                                                                 |                                                                                                                                                       |

## IManagerForSystemService

This is
"nn::account::baas::IManagerForSystemService".

| Cmd | Name                                                              | Notes                                                                        |
| --- | ----------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| 0   | CheckAvailability                                                 |                                                                              |
| 1   | GetAccountId                                                      |                                                                              |
| 2   | EnsureIdTokenCacheAsync                                           | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                     |
| 3   | LoadIdTokenCache                                                  |                                                                              |
| 100 | SetSystemProgramIdentification                                    |                                                                              |
| 101 | \[7.0.0+\] RefreshNotificationTokenAsync                          |                                                                              |
| 110 | \[4.0.0+\] GetServiceEntryRequirementCache                        |                                                                              |
| 111 | \[4.0.0+\] InvalidateServiceEntryRequirementCache                 |                                                                              |
| 112 | \[4.0.0-6.2.0\] InvalidateTokenCache                              |                                                                              |
| 113 | \[6.1.0+\] GetServiceEntryRequirementCacheForOnlinePlay           | Takes a total of 0x8-bytes of input, returns a total of 0x4-bytes of output. |
| 120 | GetNintendoAccountId                                              |                                                                              |
| 130 | GetNintendoAccountUserResourceCache                               |                                                                              |
| 131 | RefreshNintendoAccountUserResourceCacheAsync                      | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                     |
| 132 | RefreshNintendoAccountUserResourceCacheAsyncIfSecondsElapsed      | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                     |
| 140 | \[5.0.0+\] GetNetworkServiceLicenseCache                          |                                                                              |
| 141 | \[5.0.0+\] RefreshNetworkServiceLicenseCacheAsync                 | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                     |
| 142 | \[5.0.0+\] RefreshNetworkServiceLicenseCacheAsyncIfSecondsElapsed | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                     |
| 150 | CreateAuthorizationRequest                                        | Returns an [\#IAuthorizationRequest](#IAuthorizationRequest "wikilink").     |

## IFloatingRegistrationRequest

This is
"nn::account::baas::IFloatingRegistrationRequest".

| Cmd | Name                                                       | Notes                                                                           |
| --- | ---------------------------------------------------------- | ------------------------------------------------------------------------------- |
| 0   | GetSessionId                                               |                                                                                 |
| 12  | GetAccountId                                               |                                                                                 |
| 13  | GetLinkedNintendoAccountId                                 |                                                                                 |
| 14  | GetNickname                                                |                                                                                 |
| 15  | GetProfileImage                                            |                                                                                 |
| 21  | LoadIdTokenCache                                           |                                                                                 |
| 100 | RegisterUser (\[1.0.0-3.0.2\] RegisterAsync)               | \[1.0.0-3.0.2\] Used to return an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 101 | RegisterUserWithUid (\[1.0.0-3.0.2\] RegisterWithUidAsync) | \[1.0.0-3.0.2\] Used to return an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 102 | \[4.0.0+\] RegisterNetworkServiceAccountAsync              | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                        |
| 103 | \[4.0.0+\] RegisterNetworkServiceAccountWithUidAsync       | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                        |
| 110 | SetSystemProgramIdentification                             |                                                                                 |
| 111 | EnsureIdTokenCacheAsync                                    | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                        |

## IAdministrator

This is
"nn::account::baas::IAdministrator".

| Cmd                 | Name                                                                  | Notes                                                                                                          |
| ------------------- | --------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| 0                   | CheckAvailability                                                     |                                                                                                                |
| 1                   | GetAccountId                                                          |                                                                                                                |
| 2                   | EnsureIdTokenCacheAsync                                               | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                       |
| 3                   | LoadIdTokenCache                                                      |                                                                                                                |
| 100                 | SetSystemProgramIdentification                                        |                                                                                                                |
| 101                 | \[7.0.0+\] RefreshNotificationTokenAsync                              |                                                                                                                |
| 110                 | \[4.0.0+\] GetServiceEntryRequirementCache                            |                                                                                                                |
| 111                 | \[4.0.0+\] InvalidateServiceEntryRequirementCache                     |                                                                                                                |
| \[4.0.0-6.2.0\] 112 | InvalidateTokenCache                                                  |                                                                                                                |
| 113                 | \[6.1.0+\] GetServiceEntryRequirementCacheForOnlinePlay               | Takes a total of 0x8-bytes of input, returns a total of 0x4-bytes of output.                                   |
| 120                 | GetNintendoAccountId                                                  |                                                                                                                |
| 130                 | GetNintendoAccountUserResourceCache                                   |                                                                                                                |
| 131                 | RefreshNintendoAccountUserResourceCacheAsync                          | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                       |
| 132                 | RefreshNintendoAccountUserResourceCacheAsyncIfSecondsElapsed          | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                       |
| 140                 | \[5.0.0+\] GetNetworkServiceLicenseCache                              |                                                                                                                |
| 141                 | \[5.0.0+\] RefreshNetworkServiceLicenseCacheAsync                     |                                                                                                                |
| 142                 | \[5.0.0+\] RefreshNetworkServiceLicenseCacheAsyncIfSecondsElapsed     |                                                                                                                |
| 150                 | CreateAuthorizationRequest                                            | Returns an [\#IAuthorizationRequest](#IAuthorizationRequest "wikilink").                                       |
| 200                 | IsRegistered                                                          |                                                                                                                |
| 201                 | RegisterAsync                                                         | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                       |
| 202                 | UnregisterAsync                                                       | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                       |
| 203                 | DeleteRegistrationInfoLocally                                         |                                                                                                                |
| 220                 | SynchronizeProfileAsync                                               | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                       |
| 221                 | UploadProfileAsync                                                    | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                       |
| 222                 | SynchronizeProfileAsyncIfSecondsElapsed                               | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                       |
| 250                 | IsLinkedWithNintendoAccount                                           |                                                                                                                |
| 251                 | CreateProcedureToLinkWithNintendoAccount                              | Returns an [\#IOAuthProcedureForNintendoAccountLinkage](#IOAuthProcedureForNintendoAccountLinkage "wikilink"). |
| 252                 | ResumeProcedureToLinkWithNintendoAccount                              | Returns an [\#IOAuthProcedureForNintendoAccountLinkage](#IOAuthProcedureForNintendoAccountLinkage "wikilink"). |
| 255                 | CreateProcedureToUpdateLinkageStateOfNintendoAccount                  | Returns an [\#IOAuthProcedure](#IOAuthProcedure "wikilink").                                                   |
| 256                 | ResumeProcedureToUpdateLinkageStateOfNintendoAccount                  | Returns an [\#IOAuthProcedure](#IOAuthProcedure "wikilink").                                                   |
| 260                 | CreateProcedureToLinkNnidWithNintendoAccount                          | Returns an [\#IOAuthProcedure](#IOAuthProcedure "wikilink").                                                   |
| 261                 | ResumeProcedureToLinkNnidWithNintendoAccount                          | Returns an [\#IOAuthProcedure](#IOAuthProcedure "wikilink").                                                   |
| 280                 | ProxyProcedureToAcquireApplicationAuthorizationForNintendoAccount     | Returns an [\#IOAuthProcedure](#IOAuthProcedure "wikilink").                                                   |
| 290                 | \[8.0.0+\]                                                            |                                                                                                                |
| 300                 | \[6.0.0+\] TryRecoverNintendoAccountUserStateAsync                    | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                       |
| 400                 | \[6.1.0+\] IsServiceEntryRequirementCacheRefreshRequiredForOnlinePlay | Takes a total of 0x8-bytes of input, returns an output u8.                                                     |
| 401                 | \[6.1.0+\] RefreshServiceEntryRequirementCacheForOnlinePlayAsync      | Takes a total of 0x8-bytes of input, returns an [\#IAsyncContext](#IAsyncContext "wikilink").                  |
| 997                 | DebugUnlinkNintendoAccountAsync                                       | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                       |
| 998                 | DebugSetAvailabilityErrorDetail                                       |                                                                                                                |

## IAuthorizationRequest

This is
"nn::account::nas::IAuthorizationRequest".

| Cmd | Name                          | Notes                                                    |
| --- | ----------------------------- | -------------------------------------------------------- |
| 0   | GetSessionId                  |                                                          |
| 10  | InvokeWithoutInteractionAsync | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 19  | IsAuthorized                  |                                                          |
| 20  | GetAuthorizationCode          |                                                          |
| 21  | GetIdToken                    |                                                          |
| 22  | GetState                      |                                                          |

## IOAuthProcedure

This is
"nn::account::[http::IOAuthProcedure](Http::IOAuthProcedure.md)".

| Cmd | Name               | Notes                                                    |
| --- | ------------------ | -------------------------------------------------------- |
| 0   | PrepareAsync       | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 1   | GetRequest         |                                                          |
| 2   | ApplyResponse      |                                                          |
| 3   | ApplyResponseAsync | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 10  | Suspend            |                                                          |

## IOAuthProcedureForExternalNsa

This is
"nn::account::nas::IOAuthProcedureForExternalNsa".

| Cmd | Name                       | Notes                                                    |
| --- | -------------------------- | -------------------------------------------------------- |
| 0   | PrepareAsync               | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 1   | GetRequest                 |                                                          |
| 2   | ApplyResponse              |                                                          |
| 3   | ApplyResponseAsync         | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 10  | Suspend                    |                                                          |
| 100 | GetAccountId               |                                                          |
| 101 | GetLinkedNintendoAccountId |                                                          |
| 102 | GetNickname                |                                                          |
| 103 | GetProfileImage            |                                                          |

## IOAuthProcedureForNintendoAccountLinkage

This is
"nn::account::nas::IOAuthProcedureForNintendoAccountLinkage".

| Cmd             | Name                                   | Notes                                                    |
| --------------- | -------------------------------------- | -------------------------------------------------------- |
| 0               | PrepareAsync                           | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 1               | GetRequest                             |                                                          |
| 2               | ApplyResponse                          |                                                          |
| 3               | ApplyResponseAsync                     | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 10              | Suspend                                |                                                          |
| 100             | GetRequestWithTheme                    |                                                          |
| 101             | IsNetworkServiceAccountReplaced        |                                                          |
| \[?-5.1.0\] 199 | GetUrlForIntroductionOfExtraMembership |                                                          |

## INotifier

This is "nn::account::detail::INotifier".

| Cmd | Name           |
| --- | -------------- |
| 0   | GetSystemEvent |

## IProfile

This is "nn::account::profile::IProfile".

| Cmd | Name                                       |
| --- | ------------------------------------------ |
| 0   | [\#Get](#Get "wikilink")                   |
| 1   | [\#GetBase](#GetBase "wikilink")           |
| 10  | [\#GetImageSize](#GetImageSize "wikilink") |
| 11  | [\#LoadImage](#LoadImage "wikilink")       |

### Get

Takes an output type-0x1A buffer for [\#UserData](#UserData "wikilink"),
returns an output [\#ProfileBase](#ProfileBase "wikilink").

### GetBase

No input, returns an output [\#ProfileBase](#ProfileBase "wikilink").

### GetImageSize

No input, returns an output u32 for the size of the image buffer.

### LoadImage

Takes an output type-0x6 buffer, returns the same output u32 as
[\#GetImageSize](#GetImageSize "wikilink").

The output buffer contains the JPEG profile image icon. This is valid
for both Miis and character icons.

## IProfileEditor

This is "nn::account::profile::IProfileEditor".

| Cmd | Name                                           |
| --- | ---------------------------------------------- |
| 0   | [\#Get](#Get "wikilink")                       |
| 1   | [\#GetBase](#GetBase "wikilink")               |
| 10  | [\#GetImageSize](#GetImageSize "wikilink")     |
| 11  | [\#LoadImage](#LoadImage "wikilink")           |
| 100 | [\#Store](#Store "wikilink")                   |
| 101 | [\#StoreWithImage](#StoreWithImage "wikilink") |

### Store

Takes a [\#ProfileBase](#ProfileBase "wikilink") and an input type-0x19
buffer for [\#UserData](#UserData "wikilink").

### StoreWithImage

Takes a [\#ProfileBase](#ProfileBase "wikilink"), an input type-0x19
buffer for [\#UserData](#UserData "wikilink"), and an input type-0x5
buffer.

## IAsyncContext

This is "nn::account::detail::IAsyncContext".

| Cmd | Name           |
| --- | -------------- |
| 0   | GetSystemEvent |
| 1   | Cancel         |
| 2   | HasDone        |
| 3   | GetResult      |

## ISessionObject

This is "nn::account::detail::ISessionObject".

| Cmd | Name  |
| --- | ----- |
| 999 | Dummy |

# acc:u0

This is
"nn::account::IAccountServiceForApplication".

| Cmd | Name                                            | Notes                                                                      |
| --- | ----------------------------------------------- | -------------------------------------------------------------------------- |
| 0   | GetUserCount                                    |                                                                            |
| 1   | GetUserExistence                                |                                                                            |
| 2   | ListAllUsers                                    |                                                                            |
| 3   | ListOpenUsers                                   |                                                                            |
| 4   | GetLastOpenedUser                               |                                                                            |
| 5   | GetProfile                                      | Takes an input userID, returns an [\#IProfile](#IProfile "wikilink").      |
| 6   | GetProfileDigest                                |                                                                            |
| 50  | IsUserRegistrationRequestPermitted              |                                                                            |
| 51  | TrySelectUserWithoutInteraction                 |                                                                            |
| 60  | \[5.0.0-5.1.0\] ListOpenContextStoredUsers      |                                                                            |
| 99  | \[6.0.0+\] DebugActivateOpenContextRetention    | No input, returns an [\#ISessionObject](#ISessionObject "wikilink").       |
| 100 | InitializeApplicationInfo                       |                                                                            |
| 101 | GetBaasAccountManagerForApplication             | Returns an [\#IManagerForApplication](#IManagerForApplication "wikilink"). |
| 102 | AuthenticateApplicationAsync                    | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                   |
| 103 | \[4.0.0+\] CheckNetworkServiceAvailabilityAsync | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                   |
| 110 | StoreSaveDataThumbnail                          |                                                                            |
| 111 | ClearSaveDataThumbnail                          |                                                                            |
| 120 | CreateGuestLoginRequest                         | Returns an [\#IGuestLoginRequest](#IGuestLoginRequest "wikilink").         |
| 130 | \[5.0.0+\] LoadOpenContext                      |                                                                            |
| 131 | \[6.0.0+\] ListOpenContextStoredUsers           |                                                                            |
| 140 | \[6.0.0+\] InitializeApplicationInfo            |                                                                            |
| 141 | \[6.0.0+\] ListQualifiedUsers                   |                                                                            |
| 150 | \[6.0.0+\] IsUserAccountSwitchLocked            |                                                                            |

## IGuestLoginRequest

This is "nn::account::baas::IGuestLoginRequest".

| Cmd | Name                       |
| --- | -------------------------- |
| 0   | GetSessionId               |
| 12  | GetAccountId               |
| 13  | GetLinkedNintendoAccountId |
| 14  | GetNickname                |
| 15  | GetProfileImage            |
| 21  | LoadIdTokenCache           |

## IManagerForApplication

This is
"nn::account::baas::IManagerForApplication".

| Cmd | Name                                              | Notes                                                                                                                |
| --- | ------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| 0   | CheckAvailability                                 |                                                                                                                      |
| 1   | GetAccountId                                      |                                                                                                                      |
| 2   | EnsureIdTokenCacheAsync                           | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                             |
| 3   | LoadIdTokenCache                                  |                                                                                                                      |
| 130 | GetNintendoAccountUserResourceCacheForApplication |                                                                                                                      |
| 150 | CreateAuthorizationRequest                        | Returns an [\#IAuthorizationRequest](#IAuthorizationRequest "wikilink").                                             |
| 160 | \[5.0.0+\] StoreOpenContext                       |                                                                                                                      |
| 170 | \[6.0.0+\] LoadNetworkServiceLicenseKindAsync     | No input, returns an [\#IAsyncNetworkServiceLicenseKindContext](#IAsyncNetworkServiceLicenseKindContext "wikilink"). |

## IAsyncNetworkServiceLicenseKindContext

This is "nn::account::detail::IAsyncNetworkServiceLicenseKindContext".

This was added with \[6.0.0+\].

| Cmd | Name                         | Notes |
| --- | ---------------------------- | ----- |
| 0   | GetSystemEvent               |       |
| 1   | Cancel                       |       |
| 2   | HasDone                      |       |
| 3   | GetResult                    |       |
| 100 | GetNetworkServiceLicenseKind |       |

# acc:u1

This is
"nn::account::IAccountServiceForSystemService".

| Cmd | Name                                                                                  | Notes                                                                                           |
| --- | ------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| 0   | GetUserCount                                                                          |                                                                                                 |
| 1   | GetUserExistence                                                                      |                                                                                                 |
| 2   | ListAllUsers                                                                          |                                                                                                 |
| 3   | ListOpenUsers                                                                         |                                                                                                 |
| 4   | GetLastOpenedUser                                                                     |                                                                                                 |
| 5   | GetProfile                                                                            | Returns an [\#IProfile](#IProfile "wikilink").                                                  |
| 6   | GetProfileDigest                                                                      |                                                                                                 |
| 50  | IsUserRegistrationRequestPermitted                                                    |                                                                                                 |
| 51  | TrySelectUserWithoutInteraction                                                       |                                                                                                 |
| 60  | \[5.0.0-5.1.0\] ListOpenContextStoredUsers                                            |                                                                                                 |
| 99  | \[6.0.0+\] DebugActivateOpenContextRetention                                          | No input, returns an [\#ISessionObject](#ISessionObject "wikilink").                            |
| 100 | GetUserRegistrationNotifier                                                           | Returns an [\#INotifier](#INotifier "wikilink").                                                |
| 101 | GetUserStateChangeNotifier                                                            | Returns an [\#INotifier](#INotifier "wikilink").                                                |
| 102 | GetBaasAccountManagerForSystemService                                                 | Returns an [\#IManagerForSystemService](#IManagerForSystemService "wikilink").                  |
| 103 | GetBaasUserAvailabilityChangeNotifier                                                 | Returns an [\#INotifier](#INotifier "wikilink").                                                |
| 104 | GetProfileUpdateNotifier                                                              | Returns an [\#INotifier](#INotifier "wikilink").                                                |
| 105 | \[4.0.0+\] CheckNetworkServiceAvailabilityAsync                                       | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                        |
| 110 | StoreSaveDataThumbnail                                                                |                                                                                                 |
| 111 | ClearSaveDataThumbnail                                                                |                                                                                                 |
| 112 | LoadSaveDataThumbnail                                                                 |                                                                                                 |
| 113 | \[5.0.0+\] GetSaveDataThumbnailExistence                                              |                                                                                                 |
| 130 | \[6.0.0+\] ActivateOpenContextRetention                                               | Takes a total of 0x8-bytes of input, returns an [\#ISessionObject](#ISessionObject "wikilink"). |
| 140 | \[6.0.0+\] ListQualifiedUsers                                                         |                                                                                                 |
| 190 | GetUserLastOpenedApplication                                                          |                                                                                                 |
| 191 | \[7.0.0+\] UpdateNotificationReceiverInfo (\[5.0.0-5.1.0\] ActivateOpenContextHolder) |                                                                                                 |
| 997 | DebugInvalidateTokenCacheForUser                                                      |                                                                                                 |
| 998 | DebugSetUserStateClose                                                                |                                                                                                 |
| 999 | DebugSetUserStateOpen                                                                 |                                                                                                 |

## IOAuthProcedureForUserRegistration

This is "nn::account::nas::IOAuthProcedureForUserRegistration".

This was added with
\[8.0.0+\].

| Cmd | Name | Notes                                                                                   |
| --- | ---- | --------------------------------------------------------------------------------------- |
| 0   |      | No input, returns an [\#IAsyncContext](#IAsyncContext "wikilink").                      |
| 1   |      |                                                                                         |
| 2   |      |                                                                                         |
| 3   |      | Takes a type-0x9 input buffer, returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 10  |      |                                                                                         |
| 100 |      |                                                                                         |
| 101 |      |                                                                                         |
| 102 |      |                                                                                         |
| 103 |      |                                                                                         |
| 110 |      | No input, returns an [\#IAsyncContext](#IAsyncContext "wikilink").                      |
| 111 |      |                                                                                         |

# acc:aa

This is
"nn::account::IBaasAccessTokenAccessor".

| Cmd                | Name                             | Notes                                                    |
| ------------------ | -------------------------------- | -------------------------------------------------------- |
| 0                  | EnsureCacheAsync                 | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 1                  | LoadCache                        |                                                          |
| 2                  | GetDeviceAccountId               |                                                          |
| \[1.0.0-6.2.0\] 50 | RegisterNotificationTokenAsync   | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| \[1.0.0-6.2.0\] 51 | UnregisterNotificationTokenAsync | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |

# dauth:0

This is "nn::dauth::detail::IService".

| Cmd | Name                  |
| --- | --------------------- |
| 0   | ? (\[5.0.0-5.1.0\] ?) |
| 1   | \[6.0.0+\]            |
| 2   | \[6.0.0+\]            |
| 10  | \[6.0.0+\]            |
| 11  | \[6.0.0+\]            |
| 12  | \[6.0.0+\]            |

## IAsyncResult

This is "nn::dauth::detail::IAsyncResult".

This was added with \[6.0.0+\].

| Cmd | Name |
| --- | ---- |
| 0   |      |
| 1   |      |
| 2   |      |
| 3   |      |

# UserData

| Offset | Size | Description                                                          |
| ------ | ---- | -------------------------------------------------------------------- |
| 0x0    | 0x4? | ?                                                                    |
| 0x4    | 0x4? | Icon ID. 0 = Mii, the rest are character icon IDs.                   |
| 0x8    | 0x1? | Profile icon background color ID                                     |
| 0x9    | 0x7  | ?                                                                    |
| 0x10   | 0x10 | Some ID related to the Mii? All zeros when a character icon is used. |
| 0x20   | 0x60 | Usually zeros?                                                       |

This is a 0x80-byte struct.

# ProfileBase

| Offset | Size | Description                                 |
| ------ | ---- | ------------------------------------------- |
| 0x0    | 0x10 | userID                                      |
| 0x10   | 0x8  | POSIX UTC timestamp, for last account edit. |
| 0x18   | 0x20 | UTF-8 Username                              |
|        |      |                                             |

This is a 0x38-byte struct.

[Category:Services](Category:Services "wikilink")
