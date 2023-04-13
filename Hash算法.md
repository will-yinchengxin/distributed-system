# HASH 算法

在记录的关键字与记录的存储地址之间建立的一种对应关系叫哈希函数。 哈希函数就是一种**映射**，是从关键字到存储地址的映射。 通常，包含哈希函数的算法的算法复杂度都假设为O(1)，这就是为什么在哈希表中搜索数据的时间复杂度会被认为是**平均为O(1)的复杂度**

### 负载均衡 与 hash 算法有什么联系

负载均衡和哈希算法是常用于分布式系统中的两个概念，它们之间有一定的联系。

负载均衡是指将网络流量分配到多个服务器上，以达到提高系统的性能、可用性和可扩展性的目的。**在负载均衡中，可以采用不同的算法来实现流量的分配，其中一种常见的算法就是哈希算法**。

哈希算法是将任意长度的消息压缩成固定长度的消息摘要的一种算法。在分布式系统中，可以使用哈希算法来将请求分配到不同的服务器上。具体来说，可以将请求的源地址、目的地址、协议、端口等信息作为输入，通过哈希算法计算出一个哈希值，再将哈希值与服务器列表取模，得到一个服务器的编号，从而将请求发送到该服务器上。

```
m = hash(o) mod n, 其中，o为对象名称，n为机器的数量，m为机器编号

三个机器: 1 2 3
10 个数字: 1 ~ 10
数据分布: 机器0: 3，6，9   机器1: 1，4，7，10  机器2: 2，5，8
```

因此，哈希算法可以作为负载均衡算法的一种实现方式，可以根据请求的属性将请求分配到不同的服务器上，从而实现负载均衡。

### Hash 冲突（碰撞）

对于不同的关键字ki、kj，若ki  !=  kj，但 H(ki) = H(kj) 的现象叫 **冲突** (collision) ，即不同的输入却有相同的输出。我们应该尽量避免冲突，因为冲突不仅会使我们在查找的时候效率变慢，还甚至会被攻击者利用从而大量消耗系统资源。

### 不可逆性指的是
对于任何给定的输入消息，这些加密哈希函数都能够生成唯一的输出，并且无法通过输出反推出原始输入。

### 唯一性指的是
对于不同的输入消息，这些加密哈希函数生成的输出相互独立，几乎不会出现两个不同的输入生成相同的输出。

### 常见的 hash 算法

- MD5：一种常见的 128 位哈希算法，具有高度的不可逆性和唯一性，但由于其较短的输出长度，存在碰撞的可能性。
- SHA-1：一种常见的 160 位哈希算法，具有高度的不可逆性和唯一性，但由于其输出长度较短，存在碰撞的可能性。
- SHA-256：一种常见的 256 位哈希算法，具有高度的不可逆性和唯一性, 具有更高的安全性和更低的碰撞概率，但计算速度较慢。
- MurmurHash：一种高性能的非加密哈希算法，具有一定的不可逆性和唯一性，但是相对于加密哈希函数来说，它的安全性要弱一些, 适用于分布式系统中的哈希表、缓存和消息传递等场景。
- CityHash：一种快速的哈希算法，具有一定的不可逆性和唯一性, 适用于大规模数据的哈希和字符串的哈希。适用于高性能的哈希表和消息传递场景。
- FNV Hash：一种简单的哈希算法，具有一定的不可逆性和唯一性, 适用于哈希表和消息摘要等场景。
- Jenkins Hash：一种优秀的哈希算法，具有一定的不可逆性和唯一性, 可以快速地生成哈希值，适用于哈希表和密码学等场景。适用于一般的哈希表和密码学场景
- CRC32 Hash：一种循环冗余校验算法，不具有高度的不可逆性和唯一性, 适用于数据传输错误检测和校验等场景。
- CRC64 Hash：一种循环冗余校验算法，不具有高度的不可逆性和唯一性, 可以生成 64 位哈希值，适用于数据传输和校验等场景，具有高度的错误检测能力和较快的计算速度。
- Adler32：一种快速的哈希算法，不具有高度的不可逆性和唯一性, 可以生成 32 位哈希值，适用于数据传输和校验等场景，具有较快的计算速度和较高的错误检测能力。
- MapHash：一种用于哈希表的哈希算法，具有一定的不可逆性和唯一, 适用于哈希表的哈希函数和数据结构等场景，具有较高的哈希效率和较低的冲突率。
- xxHash：一种高速的哈希算法，具有高度的不可逆性和唯一性, 可以快速地生成哈希值，适用于数据校验和哈希表等场景。
- BLAKE2：一种高速的哈希算法，具有高度的不可逆性和唯一性, 具有高度的安全性和可扩展性，适用于密码学和数字签名等领域。
- SipHash：一种安全的哈希算法，具有高度的不可逆性和唯一性, 适用于哈希表和密码学等场景，具有高度的安全性和高速的计算能力。
- Tiger：一种较为安全的哈希算法，具有高度的不可逆性和唯一性, 适用于消息摘要和数字签名等领域，具有较高的安全性和较快的计算速度。
- Whirlpool：一种比较安全的哈希算法，具有高度的不可逆性和唯一性, 适用于数字签名和消息摘要等领域，具有较高的安全性和较慢的计算速度。

在工程中，哈希算法的选择取决于具体的应用场景和需求。不同的应用场景需要不同的哈希算法来保证数据的安全性、可靠性和高效性。一般来说，工程中常用的哈希算法包括：

- SHA-256：适用于密码学和数字签名等领域，具有更高的安全性和更低的碰撞概率。
- MurmurHash：适用于哈希表、缓存和消息传递等场景，具有高效的哈希能力和低碰撞率。
- CityHash：适用于大规模数据的哈希和字符串的哈希，具有快速的哈希速度和较低的碰撞率。
- FNV Hash：适用于哈希表和消息摘要等场景，具有简单的哈希算法和较低的哈希冲突率。

在分布式系统中，常用的哈希算法包括一致性哈希（Consistent Hashing）和一致性哈希加虚拟节点（Virtual Node Consistent Hashing）。这些算法可以根据服务器的数量和负载情况动态调整哈希值的分布，从而实现负载均衡和高可用性。

### Hash 算法的 golang 实现

**MD5**

```go
package main

import (
    "crypto/md5"
    "encoding/hex"
    "fmt"
)

func main() {
    data := []byte("hello world")
    hash := md5.Sum(data)
    fmt.Println(hex.EncodeToString(hash[:]))
}
```

**SHA-1**

```go
package main

import (
    "crypto/sha1"
    "encoding/hex"
    "fmt"
)

func main() {
    data := []byte("hello world")
    hash := sha1.Sum(data)
    fmt.Println(hex.EncodeToString(hash[:]))
}
```

**SHA-256**

```go
package main

import (
    "crypto/sha256"
    "encoding/hex"
    "fmt"
)

func main() {
    data := []byte("hello world")
    hash := sha256.Sum256(data)
    fmt.Println(hex.EncodeToString(hash[:]))
}
```

**MurmurHash**

```go
package main

import (
    "fmt"
    "github.com/spaolacci/murmur3"
)

func main() {
    data := []byte("hello world")
    hash := murmur3.Sum32(data)
    fmt.Println(hash)
}
```

**CityHash**

```go
package main

import (
    "fmt"
    "github.com/OneOfOne/cityhash"
)

func main() {
    data := []byte("hello world")
    hash := cityhash.CityHash64(data, uint32(len(data)))
    fmt.Println(hash)
}
```

**FNV Hash**

```go
package main

import (
    "fmt"
    "hash/fnv"
)

func main() {
    data := []byte("hello world")
    h := fnv.New32a()
    h.Write(data)
    hash := h.Sum32()
    fmt.Println(hash)
}
```

**CRC32**

```go
package main

import (
    "fmt"
    "hash/crc32"
)

func main() {
    data := []byte("hello world")
    hash := crc32.ChecksumIEEE(data)
    fmt.Println(hash)
}
```

**Adler32**

```go
package main

import (
    "fmt"
    "hash/adler32"
)

func main() {
    data := []byte("hello world")
    hash := adler32.Checksum(data)
    fmt.Println(hash)
}
```

**Jenkins Hash**

```go
package main

import (
    "fmt"
    "github.com/dgryski/go-jenkins"
)

func main() {
    data := []byte("hello world")
    hash := jenkins.Sum32(data)
    fmt.Println(hash)
}
```

**xxHash**

```go
package main

import (
    "fmt"
    "github.com/cespare/xxhash"
)

func main() {
    data := []byte("hello world")
    hash := xxhash.Sum64(data)
    fmt.Println(hash)
}
```

**BLAKE2**

```go
package main

import (
    "crypto/blake2b"
    "encoding/hex"
    "fmt"
)

func main() {
    data := []byte("hello world")
    hash := blake2b.Sum256(data)
    fmt.Println(hex.EncodeToString(hash[:]))
}
```

**SipHash**

```go
package main

import (
    "fmt"
    "github.com/dchest/siphash"
)

func main() {
    data := []byte("hello world")
    key := []byte("0123456789abcdef")
    hash := siphash.Hash(0, 0, data, key)
    fmt.Println(hash)
}
```

**Tiger**

```go
package main

import (
    "crypto/tiger"
    "encoding/hex"
    "fmt"
)

func main() {
    data := []byte("hello world")
    hash := tiger.Sum(data)
    fmt.Println(hex.EncodeToString(hash[:]))
}
```

**Whirlpool**

```go
package main

import (
    "crypto/whirlpool"
    "encoding/hex"
    "fmt"
)

func main() {
    data := []byte("hello world")
    hash := whirlpool.Sum(data)
    fmt.Println(hex.EncodeToString(hash[:]))
}
```

