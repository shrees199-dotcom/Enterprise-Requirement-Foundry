```yaml
---
header_verification:
  reading_from: "Node 1 Digest"
  timestamp: "2026-08-18 15:58:08 IST"
  dsm_tier: "Medium"
  harm_risk_tier: "Medium"
  active_threat_level: "Medium"
  confirmation_required: "Please confirm this is the current, unmodified version before I proceed."
node_2_payload:
  persona_and_nhi_lock_verification: "PASS"
  behavioral_flows:
    mermaid_sequence: |
      sequenceDiagram
        actor B as Buyer / Visitor
        participant F as Ecommerce Frontend
        participant SSO as Facebook/Google SSO
        participant P as Stripe Gateway
        actor A as Admin / Owner
        participant AP as Admin Panel

        %% Buyer Flow
        B->>F: Browse / Search Products
        F-->>B: Display Product Listing / Details
        B->>F: Select Login
        F->>SSO: Authenticate User
        SSO-->>F: Authentication Token
        F-->>B: Authenticated State
        B->>F: Add to Cart & Proceed to Checkout
        F->>P: Initiate Payment Transaction
        P-->>F: Payment Response Status
        F-->>B: Order Confirmation & History Update

        %% Admin Flow
        A->>AP: Access Admin Portal
        AP-->>A: Display Dashboard (Stats/Reports)
        A->>AP: Create/Edit Product or Manage Categories
        AP-->>A: Acknowledge Updates
        A->>AP: Manage Orders / Customers
        AP-->>A: Confirm Status Changes
  workflow_reconciliation_divergence_report: []
  text_wireframes:
    screens: |
      Screen 1: Global Storefront & Discovery
      - Roles: Visitors, Buyers
      - Components: Dynamic Search Bar, Category Navigation, Product Grid, Login/Register modal (Google/Facebook SSO triggers).
      - Uncertainty Fallback: Zero search results state with suggested popular products.

      Screen 2: Buyer Checkout Interface
      - Roles: Buyers
      - Components: Cart summary, Shipping address management, Stripe payment widget.
      - HITL Approval Gate: Final "Confirm Order & Pay" button ensuring explicit human consent before financial transaction.
      - Uncertainty Fallback: Card declined/Gateway timeout error handling with retry prompt.

      Screen 3: Admin Operations Dashboard
      - Roles: Admin/Owner
      - Components: Key metrics summary (sales, active orders), Navigation drawer for CMS/Catalog/Users.
      
      Screen 4: Admin Product & Catalog Management
      - Roles: Admin/Owner
      - Components: Data entry form for new products, Inventory toggle, Price settings.
      - HITL Approval Gate: Explicit modal confirmation required before permanent deletion of a product or category.
node_2_status: "BLOCKED_AWAITING_CONFIRMATION"
handoff_protocol: "HARD STOP. COPY THIS OUTPUT INTO THE NEXT NODE."
---

```