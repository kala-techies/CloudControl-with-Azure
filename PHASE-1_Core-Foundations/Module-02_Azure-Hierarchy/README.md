
##  Module 2: Azure Hierarchy

### 🛠️ Skills: Azure structure & management layers

* 4. **Cloud Physical Architecture**
* 5. **Subscriptions, Management Groups & Resource Groups**

---

### 🌐 Cloud Physical Architecture

Typically, cloud architecture is organized in this hierarchy:
`Regions → Availability Zones → Data Centers → Racks → Servers → Special OS → Operating Systems (VMs)`

* A **Region** is a geographic area — not necessarily a country, but a specific physical location like *East US*.
* Within a region, there are **Availability Zones (AZs)**. Think of AZs as isolated locations within the region to ensure high availability.
* Each AZ contains **data centers**, but as cloud consumers, we only get visibility up to AZ level — the details of data centers are abstracted.
* A **Data Center** contains:

  * **Racks**, which hold
  * **Servers (Bare Metal Machines)**, which run
  * A **Hypervisor / Special OS**, which hosts
  * **Virtual Machines (VMs)** that we use.

#### 👪 Real-life Analogy: Family System

Think of the actual **bare metal server** as the **father**, the **special OS/hypervisor** as the **mother**, and the **VMs** as the **children**.

* As users (children), when we want to spin up a VM (ask for something), we go to the special OS (mother).
* The special OS (mother) checks the resources and talks to the physical server (father), who provides the actual compute power.
* This hierarchy ensures that we (users) never directly interact with the physical server, just like how children often don't directly manage the finances but go through their mother who knows what’s possible.

This system abstracts complexity and ensures optimal use of resources while keeping things isolated and secure.

---

### 📦 Subscriptions, Management Groups & Resource Groups

Azure uses a **logical hierarchy** to help manage, secure, and bill resources across an organization:

#### 1️⃣ **Management Groups**

* **Top-most container** in the Azure hierarchy.
* Used for **governance** across multiple subscriptions.
* Can apply:

  * **Policies**
  * **Role-based Access Control (RBAC)**
  * **Budgets & Quotas**
* Useful when you have many subscriptions and want **centralized control**.

#### 2️⃣ **Subscriptions**

* Logical containers for resources.
* Separate billing units — each subscription has:

  * Its **own resource limits/quotas**
  * Its **own access control**
  * Its **own billing account**
* Commonly used to:

  * Separate **environments** (Dev, QA, Prod)
  * Manage **departments** or **projects** independently

> ⛔ You can apply RBAC, policies, and budgets at the subscription level, **but** management groups allow you to apply them across **multiple subscriptions**, making them powerful for large organizations.

#### 3️⃣ **Resource Groups**

* Logical containers for Azure resources.
* All resources in a group share:

  * **Same lifecycle** (create/update/delete together)
  * Easier **access and policy management**
* Example: A web app, database, and storage account for one solution can go in the same resource group.

---

### ✅ Summary: When to Use What?

| Layer            | Purpose                                | Scope                        |
| ---------------- | -------------------------------------- | ---------------------------- |
| Management Group | Apply governance across subscriptions  | Entire organization          |
| Subscription     | Isolate billing, access, and quotas    | Department / Environment     |
| Resource Group   | Group resources with similar lifecycle | Specific application/project |
