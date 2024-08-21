## Initial brief

You have been assigned a task to design a system for the coordination of transactions between entities. The system itself 
is not performing the transactions, only coordinating them. In particular, it relies on the existance of external signals 
to track their progress and provides affordances for entities involved in a transaction to be notified whenever their
counterparty has made progress. As part of the requirements, we expect the system to provide a series interfaces to trigger
and/or react to state changes.

The happy path for a transactions goes through the following states:

- **initial state**: when a transaction is created, it is _pending_ to indicate the fact that it has been initiated but has
  not been settled in the marketplace yet
- once a transaction is settled, it is marked as _open_, at which point it can't be cancelled anymore
- the destinator to a transaction is notified of any open transaction and initiates their commitment by sending a
  proof that they have acted on the transaction, at which point the transaction is _accepted_
- **final state**: when the initiatior witnesses that the transaction has indeed been acted up on their end, they can make the
  transaction as _closed_ and completed

In addition to these, we need to take care of a few exceptional scenarios:

- a pending transaction can be _cancelled_, after all everyone can make mistakes or have a change of mind
- all transactions have a due date and missing it might trigger fines and other penalties in the marketplace, so it is
  vital that the system does not impede progress. Should a transaction reach its due date before it is closed, it
  transitions to the _late_ state and cannot be interacted with anymore.

The system is a hub that journals the whole history of transactions by keeping track of any discrete event that happened
throughout the lifetime of each transaction.

**We ask you to review this brief and outline what you approach would be if you were assigned this project. Please think about
everything, not just the design of the solution. In particular, we'd love to hear how you think about team dynamics, project
management, stakeholders, feature discovery, etc. Based on your answers, we will delve more deeply into some aspects.**

## Add-on #1: Dispute resolution

Any open transaction can be _contested_ and a dispute resolution protocol is put in place to resolve the issue.

When a transaction is contested, the system mediates the communication between parties in order to resolve the dispute.
This takes the form of a conversation where users from both parties can message each other to discuss the matter at 
hand. Furthermore, any update of the transaction pushed to the system is manifested by showing the before/after state
of the transaction.

A contested transaction can move on back to being open when the counterparty is happy with the resolution, which they signal 
by agreeing with the transaction.

**We ask you to bring that new feature into the design you came up with above. Again, please think holistically and not just
on the implementation.**

## Add-on #2: Progress automation

The process of accepting, contesting or resolving a transaction can be automated to some extent. To that end, the system 
allows users to define matching rules and policies as follows:

- a matching rule is a predicate that defines a subset of all possible transactions
- a policy is an execution strategy for a set of matching rules, which can be:
  - deny or allow by default
  - at least $n$ rules must match or all rules must match
  - a rule must not match
 
**Finally, we ask you to think about this feature in the same manner as the previous one, and perhaps find out opportunities
for improvements or synergies with other features.**
