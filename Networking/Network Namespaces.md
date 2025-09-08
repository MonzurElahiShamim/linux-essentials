# Network Namespaces

> Rizwanul Ratul: Interactive cares.

```bash
lsns
```

```bash
ip link show
```

```bash
sudo ip netns add testns
```

```bash
ip netns list
```

```bash
sudo ip link add veth0 type veth peer name veth1
```

```bash
sudo ip link set veth1 netns testns
```

```bash
ip route show
```


