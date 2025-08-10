No, Hire10x does not use removable media for any business operations involving our production systems or sensitive company data. We have implemented technical and administrative controls to prevent its use.

### **Controls to Prevent Use**

Our prevention strategy is multi-layered, addressing both our cloud production environment and our corporate endpoints.

**1. In Our Cloud Production Environment (AWS & GCP)**

The concept of physical removable media is fundamentally negated by our cloud-native architecture.

*   **No Physical Access:** Hire10x personnel have no physical access to the data centers that host our services. It is impossible for an employee to attach a physical device to a production server.
*   **Strict IAM Controls:** As you noted, we use stringent **Cloud IAM (Identity and Access Management)** policies to enforce this at a logical level.
    *   Our IAM policies follow the principle of least privilege.
    *   Personnel do not have the permissions to provision or attach new virtual storage volumes (like AWS EBS or GCP Persistent Disks) to production instances outside of our formal, audited change management process. This prevents the logical equivalent of "plugging in a drive."

**2. On Our Corporate Endpoints (Employee Laptops)**

To prevent data exfiltration or malware introduction via removable media on company-issued devices, we implement the following:

*   **Endpoint Security Software:** Our laptops are managed by an endpoint security solution (Mobile Device Management or Endpoint Detection and Response). This software is configured to **block the use of unauthorized external storage devices**, such as USB drives.
*   **Acceptable Use Policy:** Our Information Security Policy explicitly prohibits the use of unauthorized removable media on company equipment. Employees acknowledge this policy upon hire and during annual training.