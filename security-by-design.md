# A global multi-tenant platform

Pirum offers a SaaS platform used by financial institutions worldwide, requiring multi-tenancy and localization support. Its portfolio of products rely on multiple sources of data:

- clients, who enter into a contractual agreement with Pirum in order to use our products, trust us with their financial data.
- banks, who act on behalf of clients and by proxy provide us with a thorough description of their bank accounts and assets. Access to that data is subject to the client blessing the flow of information between Pirum and the relevant banks; something that can be revoked at any time, either temporarily or permanently.
- reference data agencies, who provide Pirum with metadata about assets exchanged around the world, which Pirum uses to enrich client-provided data. This data does *not* belong to a client, even though it is used in combination with client data in order to produce new artifacts.

## Relationships

One emergent feature of Pirum products is that some clients of the platform enter into business agreements *out* of the platform, and can use the latter as a hub to mediate transactions. For that to happen, both the scope and the duration of the agreement is materialised on the platform via so-called relationships.

The creation of a relationship is initiated by Pirum staff after asynchronous communication happens with both clients, and manifests itself into a product notification that invites each client to either agree or disagree with the creation. When both of them eventually do, data falling under the defined scope is used to enrich both clients' view of their data with their counterpart's data. This relation can of course be revoked at any moment and a process of renewal takes place near its expiration time.

## Task

As part of the work involved in building a new product, you have been tasked in creating a system that is secure by design, notably:

- at any point in time, it must be guaranteed that users (including Pirum staff) can only ever access and manipulate data up to their security clearance
- at any point in time, any software component or module is guaranteed to only access and manipulate data in a way that does not break tenant walls, except when explicitly permitted

Design a multi-tenant architecture that can serve multiple financial institutions, abides by the constraints detailed above and can be used as a template for future products.
