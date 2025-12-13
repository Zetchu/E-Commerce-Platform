# **Project Roadmap & Architecture Evolution**

## **Phase I: Release Candidate**

The MVP demonstrated the core value (buying an item), but a release-ready product requires robustness, scalability, and integration with the real world.

### **What was added to MVP?**

To move from MVP to Phase I, the following components were added:

1.  **Payment Gateway Integration (Stripe/PayPal):**

    - **Reason:** The MVP likely mocked payments. Real transactions require secure, PCI-compliant external handling.
    - **Element:** External Payment Provider.

2.  **Search Service (Elasticsearch/Solr):**

    - **Reason:** SQL LIKE queries are too slow for product discovery. A dedicated full-text search engine is required for user experience.
    - **Element:** Search Service (New Microservice).

3.  **Content Delivery Network (CDN) & Object Storage:**

    - **Reason:** Storing product images in the database or local file system is not scalable. We need S3 (storage) and CloudFront (CDN) for fast asset loading.
    - **Element:** AWS S3 + CDN.

4.  **Caching Layer (Redis):**

    - **Reason:** Repeatedly hitting the database for "hot" products (e.g., homepage items) will crash the system under load.
    - **Element:** Redis Cache.

## **Phase II: Growth & Engagement**

Once the product is live, the focus shifts to retention, data analysis, and optimization.

### **Planned Features**

1.  **User Reviews & Ratings:**

    - Adds social proof to products. Requires a new Review Service.

2.  **Wishlists:**

    - Allows users to save items for later, reducing cart abandonment friction.

3.  **Analytics Pipeline:**

    - Instead of just operational logs, we need business intelligence (BI) to track conversion rates.

### **Implementation Order & Signals**

How do we decide what comes first?

We will use User Signals and System Metrics to prioritize:

- **Signal:** High volume of search queries with 0 results.

  - **Action:** Prioritize **Advanced Search/fuzzy matching** improvements.

- **Signal:** High cart abandonment rate on the payment page.

  - **Action:** Prioritize **Alternative Payment Methods** (Apple Pay/Google Pay).

- **Signal:** Database CPU spiking during flash sales.

  - **Action:** Prioritize **Read Replicas** or aggressive **Caching**.

## **Future Phases (Long Term)**

These features are complex and high-cost, reserved for when the user base justifies the investment.

- **ML-Based Recommendation Engine:**

  - **Why:** To increase Average Order Value (AOV).
  - **Trigger:** When we have enough user data (10k+ orders) to train a model.

- **Global Localization (i18n):**

  - **Why:** Expansion into new regions.
  - **Trigger:** Traffic spikes from specific non-native regions.

- **Chat Support Bot:**

  - **Why:** To reduce customer support costs.
  - **Trigger:** When support ticket volume exceeds manual capacity.
