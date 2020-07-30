# Socket Programming

For better clarification read [Beej's guide to network programming](https://beej.us/guide/bgnet/pdf/bgnet_a4_c_1.pdf).
Topics from  socket IO multiplexing to basic sockets are discussed in detail.

## Structs

### 1. `struct addrinfo`

   Used for hostname lookups. Used in conjunction with `getaddrinfo()`.\
   Try to use `getaddrinfo()` whenever possible instead handcrafting the `struct sockadrr`

   ```c
   struct addrinfo {
    int ai_flags; // AI_PASSIVE, AI_CANONNAME, etc.
    int ai_family; // AF_INET, AF_INET6, AF_UNSPEC
    int ai_socktype; // SOCK_STREAM, SOCK_DGRAM
    int ai_protocol; // use 0 for "any"
    size_t ai_addrlen; // size of ai_addr in bytes
    struct sockaddr *ai_addr; // struct sockaddr_in or _in6
    char *ai_canonname; // full canonical hostname
    struct addrinfo *ai_next; // linked list, next node
   };
   ```

### 2. `struct sockaddr`

   Hold socket address for many types of sockets\(ip4, ip6 and other services\).

```c
struct sockaddr {
    unsigned short sa_family; // address family, AF_xxx
    char sa_data[14]; // 14 bytes of protocol address
};
```

### 3. `struct sockaddr_in`

   Holds socket address for ip4 and can be casted to `sockaddr`

```c
struct sockaddr_in {
    short int sin_family; // Address family, AF_INET
    unsigned short int sin_port; // Port number
    struct in_addr sin_addr; // Internet address
    unsigned char sin_zero[8]; // Same size as struct sockaddr
};

struct in_addr {
uint32_t s_addr; // that's a 32-bit int (4 bytes)
};
```

### 4. `struct sockaddr_in6`

   Similiar to `sockaddr_in` but for ipv6

```c
struct sockaddr_in6 {
    u_int16_t sin6_family; // address family, AF_INET6
    u_int16_t sin6_port; // port number, Network Byte Order
    u_int32_t sin6_flowinfo; // IPv6 flow information
    struct in6_addr sin6_addr; // IPv6 address
    u_int32_t sin6_scope_id; // Scope ID
};

struct in6_addr {
    unsigned char s6_addr[16]; // IPv6 address
};
```

### 4. `struct sockaddr_storage`

   Large enough to hold both ipv4 and ipv6.

   Check if ss\_family is `AF_INET` or `AF_INET6` and cast into  one of the above structs

   ```c
   struct sockaddr_storage {
    sa_family_t ss_family; // address family
    // all this is padding, implementation specific, ignore it:
    char __ss_pad1[_SS_PAD1SIZE];
    int64_t __ss_align;
    char __ss_pad2[_SS_PAD2SIZE];
   };
   ```


## System Calls
### 1. `getaddrinfo()`

Function to fill up the `sockaddr_in` and do dns lookups.

```c
int getaddrinfo(const char *node, // e.g. "www.example.com" or IP
    const char *service, // e.g. "http" or port number
    const struct addrinfo *hints,
    struct addrinfo **res);
```

Hints struct should be filled to provide some hints like protocol, or socktype.
```c
hints.ai_family = AF_UNSPEC; // don't care IPv4 or IPv6
hints.ai_socktype = SOCK_STREAM; // TCP stream sockets
hints.ai_flags = AI_PASSIVE; // fill in my IP for me
```
The returned info can be directly given to `socket()`

```c
s = socket(res->ai_family, res->ai_socktype, res->ai_protocol);
```

### 2. `socket()`
Get a socket file descriptor. Domain is `PF_INET`
or `PF_INET6`, type is `SOCK_STREAM` or `SOCK_DGRAM`, and protocol can be set to 0 to choose the proper
protocol for the given type
```c
#include <sys/types.h>
#include <sys/socket.h>
int socket(int domain, int type, int protocol);
```


