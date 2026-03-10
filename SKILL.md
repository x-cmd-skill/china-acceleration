---
name: x-cmd-china-acceleration
description: |
  China region network acceleration for x-cmd.
  
  Configures x-cmd to use China-hosted CDN and sets up package manager mirrors
  for users in China region.
  
  Requires x-cmd to be installed first.
  
  **Security Warning**: This skill modifies system package manager configurations
  (apt, dnf, npm, pip, etc.). Review changes before applying in production.

license: Apache-2.0
compatibility: POSIX Shell

metadata:
  author: Li Junhao
  version: "0.0.1"
  category: x-cmd-extension
  tags: [x-cmd, china, network, mirror, cdn]
  parent: x-cmd
  repository: https://github.com/x-cmd-skill/china-acceleration
---

# x-cmd China Region Network Acceleration

> Network acceleration configuration for x-cmd users in China region.

⚠️ **Security Notice**: This skill modifies system package manager configurations.
Review all changes before applying, especially in production environments.

---

## Quick Start

```bash
# 1. Detect if in China region
x websrc testcn

# 2. Set x-cmd China channel (recommended)
x websrc set cn

# 3. Configure package manager mirrors
x apt mirror set tuna      # Debian/Ubuntu
x dnf mirror set tuna      # Fedora/RHEL
x npm mirror set ali       # Node.js/NPM
```

---

## Detect Current Network Region

```bash
x websrc testcn
```

- Returns `0` (true): Located in China region
- Returns `1` (false): Located overseas

## Switch Channels

| Command | Description |
|---------|-------------|
| `x websrc set cn` | Switch to China channel, use domestic CDN |
| `x websrc set inet` | Switch to international channel |
| `x websrc get` | View current configuration |

Once configured, x-cmd will use **China region hosted network** for accelerated distribution.

---

## System Package Manager Mirrors

### APT (Debian/Ubuntu)

```bash
x apt mirror set tuna
```

Available mirrors: `ali`, `tuna`, `bfsu`, `ustc`, `tencent`

### DNF (Fedora/RHEL)

```bash
x dnf mirror set tuna
```

Available mirrors: `ali`, `huawei`, `tuna`, `ustc`, `bfsu`

### YUM (CentOS/RHEL)

```bash
x yum mirror set tuna
```

Available mirrors: `ali`, `tuna`, `ustc`

### APK (Alpine)

```bash
x apk mirror set ali
```

Available mirrors: `ali`, `huawei`, `tuna`, `ustc`, `sjtu`, `official`

### Pacman (Arch Linux)

```bash
x pacman mirror set tuna
```

Available mirrors: `ali`, `tuna`, `ustc`, `bfsu`, `sjtu`

### Homebrew (macOS/Linux)

```bash
x brew mirror set tuna
```

Available mirrors: `ali`, `tuna`, `ustc`, `bfsu`, `sjtu`, `official`

---

## Language Package Manager Mirrors

### NPM (Node.js)

```bash
x npm mirror set ali
```

Available mirrors: `npmmirror` (default), `tencent`, `huawei`, `official`

### Pip (Python)

```bash
x pip mirror set ali
```

Available mirrors: `ali` (default), `tuna`, `ustc`, `bfsu`, `sjtu`, `hust`, `huawei`, `wangyi`

### Go

```bash
x go mirror set ali
```

Available mirrors: `ali` (default), `tencent`, `huawei`, `goproxy.cn`, `goproxy.io`, `official`

### Cargo (Rust)

```bash
x cargo mirror set tuna
```

Available mirrors: `ali` (default), `tuna`, `ustc`, `bfsu`, `sjtu`, `hust`

---

## Complete Configuration Example

```bash
# Detect and configure China acceleration
if x websrc testcn; then
    x websrc set cn
    
    # System package managers
    x apt mirror set tuna 2>/dev/null || true      # Debian/Ubuntu
    x dnf mirror set tuna 2>/dev/null || true      # Fedora/RHEL
    x yum mirror set tuna 2>/dev/null || true      # CentOS/RHEL
    x apk mirror set ali 2>/dev/null || true       # Alpine
    x pacman mirror set tuna 2>/dev/null || true   # Arch Linux
    x brew mirror set tuna 2>/dev/null || true     # macOS/Linux
    
    # Language package managers
    x npm mirror set ali 2>/dev/null || true       # Node.js
    x pip mirror set ali 2>/dev/null || true       # Python
    x go mirror set ali 2>/dev/null || true        # Go
    x cargo mirror set tuna 2>/dev/null || true    # Rust
    
    echo "China region acceleration configured"
fi
```

---

## ⚠️ Security Considerations

| Aspect | Note |
|--------|------|
| **System Changes** | Mirror commands modify system package manager configs |
| **Root Required** | Most mirror commands require sudo/root privileges |
| **Production** | Review all changes before applying in production |
| **Verification** | Verify mirror URLs are trusted before use |

---

## Related Links

- [x-cmd Main Skill](https://github.com/x-cmd-skill/x-cmd)
- [x-cmd Official Website](https://www.x-cmd.com)
