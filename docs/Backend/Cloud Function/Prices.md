---
title: Pricing Overview
layout: page
---

## Google Cloud API Gateway Pricing

The Google Cloud API Gateway facilitates efficient management and routing of API calls. Pricing for the API Gateway is structured to accommodate a range of usage patterns, from small projects to large-scale enterprise applications.

### Per-call Pricing

- **0-2 million calls per month**: Free
- **2 million to 1 billion calls per month**: $3 per million calls
- **Over 1 billion calls per month**: $1.50 per million calls

This pricing model ensures that the API Gateway is accessible for projects of all sizes, scaling cost-effectively as your application grows.

## Google Cloud Function Pricing

Google Cloud Functions offer a serverless execution environment for building and connecting cloud services. The pricing for Cloud Functions is based on the number of invocations, compute time, and networking.

### Invocations

- **First 2 million invocations per month**: Free
- **Beyond 2 million invocations**: $0.40 per million invocations

### Compute Time

Compute time pricing is determined by the allocated memory and CPU resources, and is calculated per 100ms of execution time:

- **Example Pricing**:
  - 128MB memory with .083 vCPU: $0.000000231 (Tier 1) and $0.000000324 (Tier 2) per 100ms
  - The pricing increases with higher memory and vCPU allocations, maxing out at 32768MB memory with 8 vCPU: $0.000272000 (Tier 1) and $0.000380800 (Tier 2) per 100ms

### Networking

- **Outbound Data (Egress)**: $0.12 per GB, with the first 5GB per month free.
- **Inbound Data (Ingress)**: Free.
- **Outbound data to Google APIs in the same region**: Free.

This comprehensive pricing structure for Google Cloud Functions and API Gateway allows developers to estimate costs based on their project's specific needs, ensuring transparency and predictability in cloud expenses.
