---
title: Use Flows in Studio applications
description: How to use Flows in Studio applications.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

## Synopsis

Flows is a low-code data orchestrator which can perform extract, transform, and load operations on data and shape it to be more useful for Studio applications, amongst other things. For some implementations you may want to use this output of a Flow for a Studio application. For more on Flows, see [Flows Overview](../../using-flows/using-flows-overview.md). For the purposes of this demonstration we will work with an already complete Flow.  

## Prerequisite knowledge

- [x] An understanding of how to [create Studio applications](../creating-studio-applications.md).
- [x] Access to a SPREAD Studio environment.
- [x] An understanding of how to [create Flows](../../using-flows/using-flows-overview.md).
- [x] An already deployed Flow ready to integrate into a Studio application.

## Instructions

### 1. Get the Flow ID

From the SPREAD Platform launcher select **Flow Manager**, which opens a list of Flows. Find the Flow you would like to incorporate into a Studio applications and save the Flow's ID.

<figure markdown="span">
	![The list of Flows in various states](../src/spread-flow-manager-list.png)
	<figcaption>The list of Flows in various states</figcaption>
</figure>

### 2. Execute the Flow

Go to the Studio application and open the application you would like to use. To integrate Flows we will a GraphQL mutation, with the ID of the Flow hardcoded in. In the Studio canvas select **+ New query/JS** or **+ Add query/JS** > **New blank GraphQL API**.

In the URL field for GraphQL enter: `https://dev.stage.spread.ai/ein` to point the API call to the GraphQL sandbox. Then use the following mutation to execute the flow:

``` graphQL title='Execute a Flow'
mutation executeFlow($executeFlowId: ID!) {
	executeFlow(id: $executeFlowId) {
		id
	}
}
```

``` json title='Object to provide as a variable for the mutation'
{
  "executeFlowId": "the-flow-id-from-step-1"
}
```

<figure markdown="span">
	![The graphQL call to run the Flow](../src/flow-execution-in-studio.png)
	<figcaption>The graphQL call to run the Flow</figcaption>
</figure>

You use this call in a widget if you would like to trigger the execution of the Flow in a widget.

### Get the result of the Flow execution

To get the result of the Flow execution,  add a new GraphQL call by selecting **+ Add query/JS**.
