# bsd:u, bsd:s

This is "nn::socket::sf::IClient".

All the services commands but the first two return -1 on failure and set
errno when that happens. Although Nintendo has the FreeBSD kernel's to
socket stack, **the errno macro definitions being in use actually come
from Linux (and not from FreeBSD as one would expect\!)**.

| Cmd | Name                                                         |
| --- | ------------------------------------------------------------ |
| 0   | RegisterClient (Initialize)                                  |
| 1   | StartMonitoring                                              |
| 2   | [\#Socket](#Socket "wikilink")                               |
| 3   | [\#SocketExempt](#Socket "wikilink")                         |
| 4   | [\#Open](#Open "wikilink")                                   |
| 5   | Select                                                       |
| 6   | Poll                                                         |
| 7   | [\#Sysctl](#Sysctl "wikilink")                               |
| 8   | Recv                                                         |
| 9   | RecvFrom                                                     |
| 10  | Send                                                         |
| 11  | SendTo                                                       |
| 12  | Accept                                                       |
| 13  | Bind                                                         |
| 14  | Connect                                                      |
| 15  | GetPeerName                                                  |
| 16  | GetSockName                                                  |
| 17  | GetSockOpt                                                   |
| 18  | Listen                                                       |
| 19  | [\#Ioctl](#Ioctl "wikilink")                                 |
| 20  | [\#Fcntl](#Fcntl "wikilink")                                 |
| 21  | SetSockOpt                                                   |
| 22  | Shutdown                                                     |
| 23  | ShutdownAllSockets                                           |
| 24  | Write                                                        |
| 25  | Read                                                         |
| 26  | Close                                                        |
| 27  | [\#DuplicateSocket](#DuplicateSocket "wikilink")             |
| 28  | [\#GetResourceStatistics](#GetResourceStatistics "wikilink") |
| 29  | \[3.0.0+\] [\#RecvMMsg](#RecvMMsg "wikilink")                |
| 30  | \[3.0.0+\] [\#SendMMsg](#SendMMsg "wikilink")                |
| 31  | \[7.0.0+\] EventFd                                           |
| 32  | \[7.0.0+\] RegisterResourceStatisticsName                    |

## Initalize

Takes a [\#BsdBufferConfig](#BsdBufferConfig "wikilink") (made-up name),
the PID, the size of the transfer memory and a copy-handle of the
latter.

### BsdBufferConfig

`/// Configuration structure for bsdInitalize`  
`typedef struct  {`  
`    u32 version;                ///< Observed 1 on 2.0 LibAppletWeb, 2 on 3.0.`  
  
`    u32 tcp_tx_buf_size;        ///< Size of the TCP transfer (send) buffer (initial or fixed).`  
`    u32 tcp_rx_buf_size;        ///< Size of the TCP recieve buffer (initial or fixed).`  
`    u32 tcp_tx_buf_max_size;    ///< Maximum size of the TCP transfer (send) buffer. If it is 0, the size of the buffer is fixed to its initial value.`  
`    u32 tcp_rx_buf_max_size;    ///< Maximum size of the TCP receive buffer. If it is 0, the size of the buffer is fixed to its initial value.`  
  
`    u32 udp_tx_buf_size;        ///< Size of the UDP transfer (send) buffer (typically 0x2400 bytes).`  
`    u32 udp_rx_buf_size;        ///< Size of the UDP receive buffer (typically 0xA500 bytes).`  
  
`    u32 sb_efficiency;          ///< Number of buffers for each socket (standard values range from 1 to 8).`  
`} BsdBufferConfig;`

The transfer memory must be larger than a the computed size below.
Should the transfer memory be smaller than that, the BSD sockets service
would only send ZeroWindow packets (for TCP), resulting in a transfer
rate not exceeding 1 byte/s.

`static size_t _bsdGetTransferMemSizeForBufferConfig(const BsdBufferConfig *config)`  
`{`  
`    u32 tcp_tx_buf_max_size = config->tcp_tx_buf_max_size != 0 ? config->tcp_tx_buf_max_size : config->tcp_tx_buf_size;`  
`    u32 tcp_rx_buf_max_size = config->tcp_rx_buf_max_size != 0 ? config->tcp_rx_buf_max_size : config->tcp_rx_buf_size;`  
`    u32 sum = tcp_tx_buf_max_size + tcp_rx_buf_max_size + config->udp_tx_buf_size + config->udp_rx_buf_size;`  
  
`    sum = ((sum + 0xFFF) >> 12) << 12; // page round-up`  
`    return (size_t)(config->sb_efficiency * sum);`  
`}`

## Socket

FreeBSD's `socket` command. `bsd:u` disallows the usage of the
`SOCK_SEQPACKET` and `SOCK_RAW` types, with the exception of `(AF_INET,
SOCK_RAW, IPPROTO_ICMP)` (IPv4 `ping`), `bsd:s` needs to be used for
those.

The only registered domains are `AF_INET` and `AF_ROUTE`.

SocketExempt: same as socket but the socket is immediately shutdown
(disconnected) on creation.

## Open

FreeBSD's `open` command, limited to opening `/dev/bpf`. This can be
used, for example, to enable promiscuous mode, see FreeBSD's `/dev/bpf`
for more details.

## Sysctl

FreeBSD's `sysctl` command. Privileged operations are reserved for
`bsd:s`. `CTL_NET`, `CTL_VM`, `CTL_KERN` and `CTL_DEBUG` commands are
implemented (?).

## Ioctl

FreeBSD's `ioctl` function. The following ioctls are whitelisted, refer
to FreeBSD's headers for more details: SIOCATMARK, BIOCGBLEN, BIOCSETF
BIOCIMMEDIATE, BIOCSETIF, BIOCVERSION, FIONSPACE, FIONWRITE, FIONREAD,
SIOCGETSGCNT, SIOCGIFMETRIC, SIOCSIFMETRIC, SIOCDIFADDR, SIOCGIFINDEX,
SIOCGIFADDR, SIOCGIFCONF, SIOCGIFNETMASK, SIOCAIFADDR, SIOCGIFMTU,
SIOCSIFMTU, SIOCGIFMEDIA, SIOCSIFLLADDR and SIOCGIFXMEDIA.

Nintendo use the following definition (hence changing all ioctls using
this structure):

`struct bpf_program {`  
`   u_int bf_len;`  
`   struct bpf_insn bf_insns[BPF_MAXINSNS]; // [512]. This is a pointer in the official structure`  
`};`

## Fcntl

FreeBSD's `fcntl`, limited to `F_GETFL` and `F_SETFL` with `O_NONBLOCK`.

## DuplicateSocket

Takes a socket file descriptor and an unused u64. Duplicates the socket
(FreeBSD's `dup`). Reserved to `bsd:s`.

## GetResourceStatistics

Takes a total of 8-bytes of input, a PID, a type-0x22 output buffer, and
returns a total of 8-bytes of output.

\[4.0.0+\] Now takes an additional 8-bytes of input.

\[7.0.0+\] Now takes an additional type-0x21 input buffer.

## RecvMMsg

Takes a total of 0x20-bytes of input, a type-0x22 output buffer, and
returns a total of 8-bytes of output.

\[7.0.0+\] The buffer was replaced with a type-0x6 output buffer.

## SendMMsg

Takes a total of 0xC-bytes of input, two type-0x21 input buffers, and
returns a total of 8-bytes of output.

\[7.0.0+\] The buffers were replaced with a type-0x6 output buffer.

# bsdcfg

This is "nn::bsdsocket::cfg::ServerInterface".

| Cmd | Name                                               |
| --- | -------------------------------------------------- |
| 0   | [\#SetIfUp](#SetIfUp "wikilink")                   |
| 1   | [\#SetIfUpWithEvent](#SetIfUpWithEvent "wikilink") |
| 2   | CancelIf                                           |
| 3   | SetIfDown                                          |
| 4   | GetIfState                                         |
| 5   | DhcpRenew                                          |
| 6   | AddStaticArpEntry                                  |
| 7   | RemoveArpEntry                                     |
| 8   | LookupArpEntry                                     |
| 9   | LookupArpEntry2                                    |
| 10  | ClearArpEntries                                    |
| 11  | ClearArpEntries2                                   |
| 12  | PrintArpEntries                                    |

## SetIfUp

Takes a total of 0x28-bytes of input and a type-0x5 input buffer, no
output.

\[3.0.0+\] Takes an additional 4-bytes of input.

## SetIfUpWithEvent

Takes a total of 0x28-bytes of input and a type-0x5 input buffer,
returns an output handle.

\[3.0.0+\] Takes an additional 4-bytes of input.

# ethc:c

This is "nn::eth::sf::IEthInterface".

| Cmd | Name         |
| --- | ------------ |
| 0   | Initialize   |
| 1   | Cancel       |
| 2   | GetResult    |
| 3   | GetMediaList |
| 4   | SetMediaType |
| 5   | GetMediaType |

# ethc:i

This is "nn::eth::sf::IEthInterfaceGroup".

| Cmd | Name              |
| --- | ----------------- |
| 0   | GetReadableHandle |
| 1   | Cancel            |
| 2   | GetResult         |
| 3   | GetInterfaceList  |
| 4   | GetInterfaceCount |

# sfdnsres

This is "nn::socket::resolver::IResolver".

This service uses `bionic/libc/dns` to perform its tasks.

| Cmd | Name                                                     |
| --- | -------------------------------------------------------- |
| 0   | SetDnsAddressesPrivateRequest (stubbed, returns 0x7FE03) |
| 1   | GetDnsAddressPrivateRequest (stubbed, returns 0x7FE03)   |
| 2   | GetHostByNameRequest                                     |
| 3   | GetHostByAddrRequest                                     |
| 4   | GetHostStringErrorRequest                                |
| 5   | GetGaiStringErrorRequest                                 |
| 6   | [\#GetAddrInfoRequest](#GetAddrInfoRequest "wikilink")   |
| 7   | GetNameInfoRequest                                       |
| 8   | GetCancelHandleRequest                                   |
| 9   | CancelRequest                                            |
| 10  | \[5.0.0+\] GetHostByNameRequestWithOptions               |
| 11  | \[5.0.0+\] GetHostByAddrRequestWithOptions               |
| 12  | \[5.0.0+\] GetAddrInfoRequestWithOptions                 |
| 13  | \[5.0.0+\] GetNameInfoRequestWithOptions                 |
| 14  | \[5.0.0+\] ResolverSetOptionRequest                      |
| 15  | \[5.0.0+\] ResolverGetOptionRequest                      |

## GetAddrInfoRequest

Takes three type 5 buffers (host, port, and hints), and a type 6 buffer
(the output addrinfos). Also takes a u8 (padded to 4 bytes so the next
raw parameter can align), a u32, and a u64. The u8 is a boolean for
whether to enable "nsd resolve" (1) or not (0). Not sure what the u32
is. It seems to either come from a parameter to `GetAddrInfo` or be
zero. The u64 is most likely a placeholder for the server to copy the
PID into and should be zero. Both hints and the output buffer contain
serialized addrinfo chains. The hints buffer is sized 0x400 bytes long
by default, and the output buffer 0x1000 bytes.

### Addrinfo Serialization Format

Each struct addrinfo in the linked list is serialized according to this
format and then written to the buffer. All numbers are in network byte
order.

| Size (bytes)                  | Name          | Notes                              |
| ----------------------------- | ------------- | ---------------------------------- |
| 4                             | Magic         | Needs to be 0xBEEFCAFE. Seriously. |
| 4                             | ai\_flags     |                                    |
| 4                             | ai\_family    |                                    |
| 4                             | ai\_socktype  |                                    |
| 4                             | ai\_protocol  |                                    |
| 4                             | ai\_addrlen   |                                    |
| ai\_addrlen ? ai\_addrlen : 4 | ai\_addr      |                                    |
| null-terminated string        | ai\_canonname |                                    |

If `ai_addrlen` is zero, `ai_addr` will occupy 4 bytes.

| Size (bytes) | Name     | Notes |
| ------------ | -------- | ----- |
| 4            | ai\_addr |       |

If `ai_family` is recognized as AF\_INET6 (28) or AF\_INET (2),
`ai_addr` is read as `struct sockaddr_in` or `struct sockaddr_in6`.
Otherwise, it's just read as `u8[ai_addrlen]`.

The list should be terminated with a sentinel four-byte zero value.

# nsd:u, nsd:a

This is "nn::nsd::detail::IManager".

| Cmd | Name                                                                 |
| --- | -------------------------------------------------------------------- |
| 10  | GetSettingName                                                       |
| 11  | [\#GetEnvironmentIdentifier](#GetEnvironmentIdentifier "wikilink")   |
| 12  | GetDeviceId                                                          |
| 13  | DeleteSettings                                                       |
| 14  | ImportSettings                                                       |
| 15  | \[4.0.0+\] SetChangeEnvironmentIdentifierDisabled                    |
| 20  | Resolve                                                              |
| 21  | ResolveEx                                                            |
| 30  | GetNasServiceSetting                                                 |
| 31  | GetNasServiceSettingEx                                               |
| 40  | GetNasRequestFqdn                                                    |
| 41  | GetNasRequestFqdnEx                                                  |
| 42  | GetNasApiFqdn                                                        |
| 43  | GetNasApiFqdnEx                                                      |
| 50  | GetCurrentSetting                                                    |
| 51  | \[9.0.0+\] WriteTestParameter                                        |
| 52  | \[9.0.0+\] ReadTestParameter                                         |
| 60  | [\#ReadSaveDataFromFsForTest](#ReadSaveDataFromFsForTest "wikilink") |
| 61  | [\#WriteSaveDataToFsForTest](#WriteSaveDataToFsForTest "wikilink")   |
| 62  | [\#DeleteSaveDataOfFsForTest](#DeleteSaveDataOfFsForTest "wikilink") |
| 63  | \[4.0.0+\] IsChangeEnvironmentIdentifierDisabled                     |

## GetEnvironmentIdentifier

Takes a type-0x16 buffer with size 8. Returns a string.

The output string is used by [NIM](NIM%20services.md "wikilink") for the
"eid:%s" in the User-Agent strings.

This is the "lp1" string also used in domains.

## ReadSaveDataFromFsForTest

Requires the `nsd!test_mode` setting to be equal to 1.

Mounts the system save data for bsdsockets as `nsdsave` and reads from
`nsd:/file` to the specified buffer, at the specified size and offset
with no checks whatsoever. `nsdsave` is then unmounted.

## WriteSaveDataToFsForTest

Requires the `nsd!test_mode` setting to be equal to 1.

Mounts the system save data for bsdsockets as `nsdsave` and writes to
`nsd:/file` (appending is allowed) using the specified buffer, at the
specified size and offset, with no checks whatsoever. `nsdsave` is then
commited and unmounted.

## DeleteSaveDataOfFsForTest

Requires the `nsd!test_mode` setting to be equal to 1.

Deletes the system save data for bsdsockets.

[Category:Services](Category:Services "wikilink")
