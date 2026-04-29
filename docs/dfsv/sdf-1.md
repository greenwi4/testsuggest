---
title: sdf
deprecated: false
hidden: false
metadata:
  robots: index
---
<a href="/reference/10x-api-reference"><Banner  

s, see our 10x API reference page."  



 </a>

<br />

Fabric is the extendable kernel at the core of the 10x Platform. It manages the key entities required for any financial product – Products, Parties, Subscriptions, Transactions and Balances.​ It is an immutable, secure and auditable interface that supports both synchronous and asynchronous processing.​

The key entities can be extended using attributes to hold client-defined data alongside the 10x Data Model. ​

See our [Fabric overview](doc:fabric-overview) guide for more information.

<br />

# Key parameters

The following key parameters are used through the products APIs:

| Parameter         | Description                                                                   |
| :---------------- | :---------------------------------------------------------------------------- |
| `productKey`      | The unique ID assigned to the product on the 10x Platform.                    |
| `productVersion`  | The version of the product.                                                   |
| `partyKey`        | The unique ID assigned to the customer.                                       |
| `subscriptionKey` | The unique ID assigned to the account.                                        |
| `transactionKey`  | The unique ID assigned to the transaction.                                    |
| `correlationKey`  | Used to associate transactions that are directly conditional upon each other. |

<br />

# Fabric endpoints

The 10x Platform enables you to perform a number of actions and facilitate a variety of use-cases for your customers. The links below provide information on how to work with our Fabric APIs:

## Products

<Cards columns={2}>
  <Card title="Amend the attributes of a product" href="/reference/fabricproductattributes" icon="fa-pencil" iconColor="#6902CD" target="_blank">
    POST /v1/fabric/products/attributes
  </Card>
</Cards>

## Subscriptions

<Cards columns={2}>
  <Card title="Create an account with one or more owners" href="/reference/fabricssubscribev1" icon="fa-circle-plus" iconColor="#6902CD" target="_blank">
    POST /v1/fabric/subscriptions/subscribe
  </Card>
	<Card title="Amend the attributes of a subscription" href="/reference/fabricsattributesv1" icon="fa-pencil" iconColor="#6902CD" target="_blank">
    POST /v1/fabric/subscriptions/attributes
  </Card>
	<Card title="Amend the party roles of a subscription" href="/reference/fabricspartyrolesv1" icon="fa-pencil" iconColor="#6902CD" target="_blank">
    PUT /v1/fabric/subscriptions/party-roles
  </Card>
	<Card title="Move subscriptions between products" href="/reference/movesubscriptionsfabricv1" icon="fa-arrows-left-right" iconColor="#6902CD" target="_blank">
    POST /v1/fabric/subscriptions/move
  </Card>
	<Card title="Amend the party roles of a subscription" href="/reference/fabricpostspartyrolesv1" icon="fa-pencil" iconColor="#6902CD" target="_blank">
    POST /v1/fabric/subscriptions/party-roles
  </Card>
	<Card title="Subscriptions search" href="/reference/searchsubscriptionsfabricv1" icon="fa-search" iconColor="#6902CD" target="_blank">
    POST /v1/fabric/subscriptions/search
  </Card>
	<Card title="Amend the state of a subscription" href="/reference/fabricsstatev1" icon="fa-pencil" iconColor="#6902CD" target="_blank">
    POST /v1/fabric/subscriptions/state
  </Card>
	<Card title="Update a subscription" href="/reference/upsesubscriptionfabricv1" icon="fa-arrow-rotate-right" iconColor="#6902CD" target="_blank">
    POST /v1/fabric/subscriptions/update
  </Card>
</Cards>

## Transactions

<Cards columns={2}>
  <Card title="Credit or debit transactions" href="/reference/bookfabricledgertransactions" icon="fa-hand-holding-dollar" iconColor="#6902CD" target="_blank">
    POST /v1/fabric/ledgers/book
  </Card>
</Cards>

<br />
