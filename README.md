![Corda](https://www.corda.net/wp-content/uploads/2016/11/fg005_corda_b.png)

# Negotiation CorDapp

This CorDapp shows how multi-party negotiation is handled on the Corda ledger, in the absence of an API for user 
interaction.

A flow is provided that allows a node to propose a trade to a counterparty. The counterparty has two options:

* Accepting the proposal, converting the `ProposalState` into a `TradeState` with identical attributes
* Modifying the proposal, consuming the existing `ProposalState` and replacing it with a new `ProposalState` for a new 
  amount

Only the recipient of the proposal has the ability to accept it or modify it. If the sender of the proposal tries to 
accept or modify the proposal, this attempt will be rejected automatically at the flow level.

# Pre-requisites:
  
See https://docs.corda.net/getting-set-up.html.

# Usage

This CorDapp does not have a front-end. However, you can see it working by running the flow and contract tests.

## Running the flow tests:

Use the IntelliJ run configurations provided:

* `Run Proposal Flow Tests`
* `Run Acceptance Flow Tests`
* `Run Modification Flow Tests`

## Running the contract tests:

Use the IntelliJ run configuration provided:

* `Run Proposal Contract Tests`

## from Hung Do ###
I cloned this repo from https://github.com/corda/negotiation-cordapp  with the purpose of creating a more functional negotiation flow
Instructions to run from Windows cmd terminal

`taskkill /f /im java.exe`

`gradlew clean deployNodes
`
`cd build/nodes`

`runnodes`

`
start ProposalFlow$Initiator role: Buyer, amount: 1000, counterparty: "O=PartyB,L=New York,C=US"
`
`flow start ModificationFlow$Initiator proposalId: "ac74252f-8a55-4b4d-b461-4dd576fa27da", newAmount: 800
`
`flow start AcceptanceFlow$Initiator proposalId: "ac74252f-8a55-4b4d-b461-4dd576fa27da"`

`run vaultQuery contractStateType: com.negotiation.ProposalState`

`run vaultQuery contractStateType: com.negotiation.TradeState`
