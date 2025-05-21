# Policies in `iptables`

A **policy** in iptables determines the default action applied to packets that do not match any rules in a chain. Policies are set at the chain level and define whether to allow or block unmatched traffic.

---

### **Key Features of Policies**

1. **Default Behavior**
    
    - Policies ensure there is a default action for every packet entering a chain.
    - Typically used on built-in chains (`INPUT`, `FORWARD`, and `OUTPUT`).
2. **Common Policies**
    
    - **`ACCEPT`**: Allows unmatched packets.
    - **`DROP`**: Silently discards unmatched packets.
    - **`REJECT`**: Blocks unmatched packets and sends an error message to the sender.
3. **Immutable for Built-in Chains**
    
    - Policies can only be set for built-in chains, not user-defined ones.

---

### **Setting Policies**

The `-P` option is used to set or change the default policy for a chain.

#### **Syntax**

```bash
iptables -P [CHAIN] [POLICY]
```

---

### **Examples**

1. **Set the Default Policy to `DROP` for `INPUT` Chain**
    
    - This configuration discards all incoming packets unless explicitly allowed.
    
    ```bash
    iptables -P INPUT DROP
    ```
    
2. **Set the Default Policy to `ACCEPT` for `OUTPUT` Chain**
    
    - Allows all outgoing packets by default.
    
    ```bash
    iptables -P OUTPUT ACCEPT
    ```
    
3. **Set the Default Policy to `REJECT` for `FORWARD` Chain**
    
    - Blocks all forwarded packets and sends an error response.
    
    ```bash
    iptables -P FORWARD REJECT
    ```
    

---

### **Checking Current Policies**

Use the `iptables -L` command to view the current policies for all chains.

#### **Example**

```bash
iptables -L
```

#### Output:

```
Chain INPUT (policy DROP)
Chain FORWARD (policy REJECT)
Chain OUTPUT (policy ACCEPT)
```

This output indicates:

- The default policy for `INPUT` is `DROP`.
- The default policy for `FORWARD` is `REJECT`.
- The default policy for `OUTPUT` is `ACCEPT`.

---

### **Best Practices for Policies**

1. **Default to `DROP` for Incoming Traffic**
    
    - Enhances security by rejecting all incoming connections unless explicitly allowed.
    
    ```bash
    iptables -P INPUT DROP
    ```
    
2. **Default to `ACCEPT` for Outgoing Traffic**
    
    - Simplifies operations as outgoing packets are usually safe.
    
    ```bash
    iptables -P OUTPUT ACCEPT
    ```
    
3. **Avoid `ACCEPT` as the Policy for `INPUT` Chain**
    
    - Using `ACCEPT` as the default policy for `INPUT` can expose the system to unwanted connections.
4. **Explicitly Define Exceptions**
    
    - Ensure critical services (e.g., SSH) are explicitly allowed when using restrictive policies.

---

### **Scenario: Setting a Secure Default Policy**

1. Default all traffic to `DROP` for strict security.
    
    ```bash
    iptables -P INPUT DROP
    iptables -P FORWARD DROP
    iptables -P OUTPUT ACCEPT
    ```
    
2. Allow only specific incoming traffic (e.g., SSH, HTTP):
    
    ```bash
    iptables -A INPUT -p tcp --dport 22 -j ACCEPT  # Allow SSH
    iptables -A INPUT -p tcp --dport 80 -j ACCEPT  # Allow HTTP
    ```
    

---

### **Summary**

- **Policies** define the default action for packets unmatched by rules.
- Policies can be set to `ACCEPT`, `DROP`, or `REJECT`.
- Using secure policies (e.g., `DROP` for `INPUT`) enhances system security.
- Explicitly define rules to allow only the required traffic.