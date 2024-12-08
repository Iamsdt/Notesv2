---
Created by: Shudipto Trafder
Created time: 2024-12-06T11:33:00
tags:
  - server
  - gcp
---
In this guide, we'll demonstrate how to connect to a Neo4j database and Typesense hosted on one Virtual Machine (VM) from another VM using an internal IP address in Google Cloud Platform (GCP). We'll cover creating a firewall rule to allow internal traffic and verifying the connection.

---

#### **Understanding the Architecture**

- **VM1:** Hosts Neo4j and Typesense services.
- **VM2:** Needs to connect to VM1 using VM1's internal IP address.

Since the connection uses internal IPs, we need to configure GCP's firewall rules to allow traffic on the required ports within the internal network.

---

### Step 1: **Creating a Firewall Rule**

In GCP, firewall rules control traffic to and from your VMs. To allow traffic on the necessary ports for Neo4j and Typesense within your internal network, use the following `gcloud` command:

```bash
gcloud compute firewall-rules create allow-neo4j-internal \
    --network=default \
    --direction=INGRESS \
    --priority=1000 \
    --source-ranges=10.128.0.0/9 \
    --allow=tcp:7474,tcp:7687 \
    --description="Allow Neo4j ports internally"
```

#### **Breaking Down the Command**

1. **`gcloud compute firewall-rules create`:** Creates a new firewall rule.
2. **`allow-neo4j-internal`:** The name of the firewall rule. You can customize it to suit your naming conventions.
3. **`--network=default`:** Specifies the VPC network where the rule will be applied. Replace `default` with your custom network name if needed.
4. **`--direction=INGRESS`:** Indicates that the rule applies to incoming traffic to your VM.
5. **`--priority=1000`:** Priority determines the order in which firewall rules are applied (lower numbers are higher priority). 1000 is a common default.
6. **`--source-ranges=10.128.0.0/9`:** Defines the IP range allowed to access your VM. More on this below.
7. **`--allow=tcp:7474,tcp:7687`:** Specifies the allowed protocols and ports:
    - `tcp:7474`: Neo4j HTTP API
    - `tcp:7687`: Neo4j Bolt Protocol
8. **`--description`:** A descriptive note for the firewall rule.

---

#### **Understanding `10.128.0.0/9`**

The IP range `10.128.0.0/9` is a CIDR (Classless Inter-Domain Routing) notation representing all IPs in the range from `10.128.0.0` to `10.255.255.255`. This range includes:

- **Network address:** `10.128.0.0`
- **Broadcast address:** `10.255.255.255`
- **Subnet mask:** `/9`, equivalent to `255.128.0.0`

This IP range is commonly used in GCP's default network for internal traffic between VMs.

If you're using a custom network or subnet, replace this with your specific CIDR block.

---

### Step 2: **Verify the Firewall Rule**

Once the firewall rule is created, you can verify its configuration using:

```bash
gcloud compute firewall-rules list --filter="name=allow-neo4j-internal"
```

Check the output to ensure the rule exists and the ports and source range are correctly configured.

---

### Step 3: **Testing the Connection**

To ensure that VM2 can connect to the Neo4j services running on VM1, use the `nc` (Netcat) command:

```bash
nc -zv 10.128.0.5 7474
nc -zv 10.128.0.5 7687
```

#### **Breaking Down the Command**

1. **`nc`:** A utility to test network connections.
2. **`-z`:** Scans the specified ports without sending data.
3. **`-v`:** Provides verbose output for better troubleshooting.
4. **`10.128.0.5`:** The internal IP address of VM1.
5. **`7474` and `7687`:** Ports to check for Neo4j's HTTP and Bolt services.

---

### Common Errors and Troubleshooting

1. **Timeout or Connection Refused:**
    
    - Check that the Neo4j service is running on VM1.
    - Verify the internal IP of VM1 using:
        
        ```bash
        gcloud compute instances describe <VM1-name> --format="get(networkInterfaces[0].networkIP)"
        ```
        
    - Confirm the firewall rule is applied to the correct network.
2. **Incorrect Source Range:**
    
    - Ensure `10.128.0.0/9` covers VM2's internal IP. If VM2 is in a different subnet, modify the `--source-ranges` parameter to include its range.

---

### Step 4: **Extending to Typesense**

For Typesense or any other service hosted on VM1, add the required ports to the firewall rule. For example, if Typesense listens on port `8108`, modify the command:

```bash
gcloud compute firewall-rules update allow-neo4j-internal \
    --allow=tcp:7474,tcp:7687,tcp:8108
```

Then test the connection:

```bash
nc -zv 10.128.0.5 8108
```

---

### Conclusion

This guide demonstrated how to connect from one VM to another in GCP using internal IPs by creating and testing a firewall rule. Adjust the IP ranges and ports as necessary for your network and services. Understanding the principles of GCP networking ensures secure and efficient communication between your VMs.