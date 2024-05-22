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
- at any point in time, any software component or module is guaranteed to only access and manipulate data in a way that does not break tenant walls, except when explicitly permitted via relationships

Design a multi-tenant architecture that can serve multiple financial institutions, abides by the constraints detailed above and can be used as a template for future products.

## Requirements

The system you come up with must respect the following requirements:

### The 3 Ws

The output of a security check is binary: either access is granted or denied. The check itself is parameterised by three properties:

- who: the _principal_ trying to perform the action
- what: the _action_ that is being performed
- where: the _resource_ that is being manipulated


### Low latency

As a user request makes its way through our systems, it will cross multiple boundaries and generate many security checks. Therefore, it is vital that the impact of those is virtually zero and does not ruin the user's experience.

Similarly, backend tasks processing client data have a high throughput expectations and increased latency of security checks would have a negative impact on the former.

### Correctness

It can be tricky sometimes to understand why access was granted or denied. The system must be able to explain a decision.

### Management

Our Client Services team is responsible for managing client/user access, they should be able to change the rules of the system without having to learn to read, write and build programs. Although it would be acceptable for them to have to learn a DSL such as JSON or something specific to security.
