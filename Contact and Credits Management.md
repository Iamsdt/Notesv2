
### **Credits Management:**
1. **Credit Request:**
   - Users can request credits, which must be approved by their manager.
   - Once approved, the credits are added to the user’s account, and an equivalent amount of points is deducted from the company’s account.

2. **Credit Purchase:**
   - If the company’s account lacks sufficient credits, the company can purchase additional credits.
### **Contact Management:**
1. **LinkedIn Contact Request:**
   - When a user requests a LinkedIn contact, the system first checks if the contact is already available in the cache.
   - **Cache Lookup:**
     - If the contact is found in the cache and was saved by the same company, no points are deducted.
     - If the contact belongs to another company, deduct two points:
       - 1 point for a phone number, if found.
       - 1 point for an email address, if found.
   - **Third-Party Services:**
     - If the contact is not found in the cache, the system queries third-party services:
       1. SignalHire
       2. ContactOut
       3. SalesQL
     - Once the contact information is retrieved, it is saved to the cache for future use.

2. **Integration with Candidate Service:**
   - When a profile with a valid LinkedIn contact and associated valid contact details (phone number/email) is saved by the candidate service, it should be cached in the contact management system.
   - This can be done either via event publication or API calls.

#### **Third-Party Services Integration:**
- **SignalHire Key Management:**
    - SignalHire provides multiple API keys for accessing its services.
    - **Key Rotation:**
        - When making a request, the system checks which key's credits are still available.
        - If a key’s credits are exhausted, the system automatically switches to the next available key.
    - **Monthly Credit Reset:**
        - Every month, SignalHire credits are reset.
        - A cron job will run to check the status of each key.
        - The job will mark keys as unused and available again if their credits have been restored.