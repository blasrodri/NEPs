---
NEP: XXXX
Title: Adding extra hashing functions and trie data structure required for IBC compatibility
Author: Blas Rodriguez Irizar <rodrigblas@gmail.com>
DiscussionsTo: https://github.com/nearprotocol/neps/pull/0000
Status: Draft
Type: Runtime Spec
Category: Contract
Created: 15-Jul-2022
---

## Summary

Following NEP-364 additional elements are introduced to make NEAR IBC compatible.
In particular, this NEP introduces a set of missing hashing functions and an interface to
efficiently retrieve data from the storage.
// TODO: improve this paragraph once the proposal is fleshed out

## Motivation

Trustless bridges require a protocol to adequately sync states between different chains.
The Cosmos ecosystem has been using [IBC](https://github.com/cosmos/ibc)
(inter-blockchain communication protocol) successfully for some time. Projects aiming to
interoperate with NEAR building trustless bridges using a standard protocol
might opt for IBC.

This NEP introduces the changes that - combined with NEP-364 - are missing to provide developers
with the tools to use IBC on NEAR.

## Rationale and alternatives

There are trade-offs between running code that is compiled natively and exposed through a host function or
having the smart contract developer compile it using wasm. Host functions provide users with faster primitives,
while they introduce both breaking changes into the protocol and potential risks for vulnerabilities in the system.
Wasm-compiled code on the other hand is safer, given that's isolated into the smart contract runtime, at the cost
of throughput and or latency.

This NEP introduces very CPU-intensive operations (such as hashing) that shine when running on native code.
And introducing these functions as native functions will allow developers using IBC on NEAR to process
more packages in one transaction at a lower gas cost.

The impact of not doing this change is either making some interoperability unfeasible or unnecessarily expensive.

## Specification

Explain the proposal as if it was already implemented and you were teaching it to another developer. That generally means:

- Introducing new named concepts.
- Explaining the feature largely in terms of examples.
- If feature introduces new abstractions, explaining how users and/or developers should _think_ about it;
- If applicable, describe the differences between the existing functionality.

For user-facing NEPs this section should focus on user stories.

## Reference Implementation (Required for Contract category, optional for other categories)

This is the technical portion of the NEP. Explain the design in sufficient detail that:

- Its interaction with other features is clear.
- Where possible, include a `Minimum Viable Interface` subsection expressing the required behavior and types in a target Near Contract language. (ie. traits and structs for rust, interfaces and classes for javascript, function signatures and structs for c, etc.)
- It is reasonably clear how the feature would be implemented.
- Corner cases are dissected by example.

The section should return to the examples given in the previous section, and explain more fully how the detailed proposal makes those examples work.

## Security Implications (Optional)

If there are security concerns in relation to the NEP, those concerns should be explicitly written out to make sure reviewers of the NEP are aware of them.

## Drawbacks (Optional)

Why should we _not_ do this?

## Unresolved Issues (Optional)

- What parts of the design do you expect to resolve through the NEP process before this gets merged?
- What parts of the design do you expect to resolve through the implementation of this feature before stabilization?
- What related issues do you consider out of scope for this NEP that could be addressed in the future independently of the solution that comes out of this NEP?

## Future possibilities

Think about what the natural extension and evolution of your proposal would
be and how it would affect the project as a whole in a holistic
way. Try to use this section as a tool to more fully consider all possible
interactions with the project in your proposal.
Also consider how the this all fits into the roadmap for the project
and of the relevant sub-team.

This is also a good place to "dump ideas", if they are out of scope for the
NEP you are writing but otherwise related.

If you have tried and cannot think of any future possibilities,
you may simply state that you cannot think of anything.

Note that having something written down in the future-possibilities section
is not a reason to accept the current or a future NEP. Such notes should be
in the section on motivation or rationale in this or subsequent NEPs.
The section merely provides additional information.

## Copyright

[copyright]: #copyright

Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
