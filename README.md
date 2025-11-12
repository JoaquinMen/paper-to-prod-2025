# GSD: Paper to Prod - 2025

## 🚀 Setting Up Your Networking Environment

To ensure your hackathon project notebooks (which run as a secure, managed service) can communicate with Google services like BigQuery, you need a basic network configuration.

Run these two commands in your Cloud Shell or terminal:

### 1\. Create a Network with Default Rules

This command quickly sets up a secure network that Google Cloud services can use. The `--subnet-mode auto` ensures a usable IP address range is created in every region, and all standard security rules (like allowing internal traffic) are handled for you.

```shell
gcloud compute networks create default --subnet-mode auto
```

> 💡 **What it does:** It creates a **private, internal network** for your project, similar to having your own internal office network in the cloud.

-----

### 2\. Enable Private Access for Notebooks

This step is **critical** for running your notebooks. Notebook runtimes (VMs) are given a private IP address for security. By enabling `--enable-private-ip-google-access`, you allow the notebook's private IP to securely reach Google's APIs (like BigQuery and Vertex AI) using Google's internal network, **without ever touching the public internet.**

We are setting this up for the `us-central1` region, which is common for AI/ML services.

```shell
gcloud compute networks subnets update default --region us-central1 --enable-private-ip-google-access
```

> **Result:** Once both commands are run, your project has the necessary **secure, private connectivity** to launch and run notebooks.