#### Self-Hosted Agile Tool – Plane Deployment on AWS

**Live URL:** [https://plane.10xscale.ai/](https://plane.10xscale.ai/)  
**Date:** June 2025  
**Prepared for:** Leadership Team  
**Prepared by:** Shudipto Trafder

---

### ✅ Executive Summary

We have successfully deployed **Plane**, a self-hosted **Agile Project Management Tool**, at:

🔗 [https://plane.10xscale.ai/](https://plane.10xscale.ai/)

This deployment runs on AWS using cost-efficient and scalable services: EC2, RDS, and S3. It offers **data privacy**, **full ownership**, **zero per-user cost**, and **customizability** — making it a strong alternative to commercial SaaS products like Jira.

---

### 🔧 Deployment Architecture

#### AWS Components Used

| Component | Configuration                                      |
| --------- | -------------------------------------------------- |
| **EC2**   | `t3.medium` (2 vCPU, 4 GB RAM, 30 GB SSD)          |
| **RDS**   | PostgreSQL – Free Tier                             |
| **S3**    | Used for file attachments and static asset storage |

##### URL:
- **Live Instance:** [https://plane.10xscale.ai/](https://plane.10xscale.ai/)

---

### 💡 Why This Setup is Viable

#### 1. **Cost-Effective**
- Uses AWS Free Tier for RDS
- EC2 instance costs approx **$25/month**
- S3 storage usage currently costs **< $1/month**
- Total monthly infra cost: **~$30–40**

#### 2. **Scalable**
- Can upgrade EC2 instance to handle more traffic
- RDS and S3 scale automatically
- Easy to migrate to managed or high-availability configurations later

#### 3. **Performance**
- Plane runs stably on current EC2 instance
- Database performance is strong due to RDS management
- Fast load times and minimal latency for internal usage
- For 25 User uses around (1.5/4 GB ram)

---
### 🔐 Data Reliability & Security

| Feature                 | Details                                                                                |
| ----------------------- | -------------------------------------------------------------------------------------- |
| **Data Ownership**      | All data (tasks, comments, files) stored privately under our AWS account               |
| **Backup & Redundancy** | RDS provides automated backups and point-in-time recovery; S3 offers 11 9's durability |
| **Encryption**          | HTTPS enforced on all communication; IAM roles and security groups tightly configured  |
| **Control**             | Full ability to monitor, export, and move our data at any time                         |

---
### 📊 Cost Comparison – Jira vs Plane (Self-Hosted)

| Item            | Jira Cloud          | Plane (Self-Hosted)       |
| --------------- | ------------------- | ------------------------- |
| Cost per user   | $8/user/month       | $0                        |
| Infra cost      | N/A (included)      | ~$30/month                |
| 10 users        | $80/month           | $30                       |
| 25 users        | $200/month          | $30–40                    |
| 50 users        | $400/month          | $30–60                    |
| 100 users       | $800/month          | $60–100                   |
| Custom features | Limited             | Fully customizable        |
| Data privacy    | Stored by Atlassian | Fully private             |
| Exportability   | Vendor lock-in risk | Full access to DB & files |

---
#### 💰 Annual Savings Example (25 Users):
- **Jira Cloud:** $200 × 12 = **$2,400/year**
- **Self-Hosted Plane:** ~$35 × 12 = **$420/year**
- **Savings:** **~$2,000/year**

---

### 🚀 Business Benefits

- **Cost Savings**: No per-user fee, flat infra cost
- **Data Control**: Hosted in our own AWS infrastructure
- **Customization**: Modify or extend Plane for internal workflows
- **Agility**: No vendor lock-in, no upgrade delays
- **Integration Ready**: Can be hooked into CI/CD, custom dashboards, or internal services

---
### 📈 Scaling Plan

| Trigger            | Action                                             |
| ------------------ | -------------------------------------------------- |
| > 100 active users | Upgrade EC2 to `t3.large` or `m5.large`            |
| > 20 GB DB size    | Move to paid RDS tier with Multi-AZ replication    |
| Need HA            | Use Load Balancer + Auto Scaling group             |
| Storage scaling    | S3 scales automatically; enable lifecycle policies |

---
### 🧾 Conclusion

Hosting **Plane** as an agile project management tool at [https://plane.10xscale.ai/](https://plane.10xscale.ai/) gives us:
✅ Enterprise-grade reliability  
✅ Transparent cost structure  
✅ Full ownership and security  
✅ Long-term strategic advantage over per-user SaaS tools like Jira

This approach aligns with our company’s goals of **efficiency**, **privacy**, and **technical independence**.