---
title: dsf
deprecated: false
hidden: false
metadata:
  robots: index
---
This guide explains how exceptions to rules work, how to set and view them.

## When create exceptions to rules

[Global rules](https://documentation.bloomreach.com/discovery/docs/discovery-glossary#global-rules) can affect all queries and categories on a site, or target specific queries or categories. Sites lower in the hierarchy inherit [external rules](https://documentation.bloomreach.com/discovery/docs/discovery-glossary#external-rules) from [accounts](https://documentation.bloomreach.com/discovery/docs/discovery-glossary#account) and [site groups](https://documentation.bloomreach.com/discovery/docs/discovery-glossary#site-group) above them.

In certain cases, a rule that improves results broadly can hurt performance for specific queries or categories.

For example, a global rule boosting products based on "newness" or "margin" might be beneficial for most categories, but not for a "New in" category, which should be merchandised to feature fresh inventory.

Exceptions to rules let you ignore any rules (global or inherited) that impact specific queries or categories without removing the rule entirely or duplicating it manually on individual pages.

## How exceptions to rules work

When you set an exception on a query or category ranking rule, the ignored rule's configuration is disabled for that scope. The rule continues to apply everywhere else. Since exceptions disable the full configuration of a rule, you can’t partially disable a rule.

The following aren't supported:

- Set exceptions to inherited rules that can apply to global rules.
- Set exceptions via API.
- Set exceptions to [Recommendations rules](https://documentation.bloomreach.com/discovery/docs/merchandising-capabilities).

## Create an exception to rule

1. Go to the query or category rule to set an exception at the site level:&#x20;

- **Merchandising > Site search > Ranking rules** for search ranking rule.
- **Merchandising > Categories > Ranking rules** for category ranking rule. <br /><br />You can also set an exception while creating a [new rule](https://documentation.bloomreach.com/discovery/docs/boost-and-position-lock-your-first-product#create-a-ranking-rule-using-visual-editor).

2. Go to the **External Changes** tab. This tab shows global scope rules from this site and external rules (rules inherited from account or site group levels).&#x20;

3. Switch the toggle from **Apply** to **Ignore**.


<Image src="https://files.readme.io/378ff30a0438375cfadd708374a44628935b1946c93f25f405d6da2d7c53bb54-image1.png" alt="The External Changes tab on a query-level ranking rule, with the toggle set to Ignore for a global rule." align="center" caption="some test" border={true} />


<br />

> 📘 **Note**
>
> For [active A/B tests](https://documentation.bloomreach.com/discovery/docs/run-ab-test-or-save-draft), the **External Changes** tab lists every variant. For instance, if there are 3 global rules, each with 3 variants, a total of 9 variants appear. Apply or ignore each variant individually.

4. Click **Save**.

The rule is now ignored for that query or category. Results for all other queries and categories are unaffected.

## View exceptions

The ranking rules listing pages for both queries and categories show the **Exception** tag for rules with active exceptions.&#x20;


<Image src="https://files.readme.io/3d659c298b214de29e0df8d740b5fbc3d26a59e6997b51de88556a2aa5d0c2bc-image3.png" alt="The ranking rules listing page for search queries, showing the Exception tag on a rule with an active exception." align="center" caption="The ranking rules listing page shows the Exception tag." border={true} />


## Manage exceptions

To edit or remove the exception, go to the query or category rule with the exception. Under the **External Changes** tab, switch the toggle back from **Ignore to Apply**. Click **Save**.

## Conflict resolution

When multiple customizations are active for the same request, the system merges all their exception settings and applies the combined result.

### Example

Say you have two ranking customizations active for the query "running shoes":

- A single-query rule for "running shoes" with an exception that ignores all global category rules.
- A broad rule covering "running shoes" and "blue shoes" with an exception that ignores a specific rule by ID.

Both exceptions apply to "running shoes." The system doesn't drop the broad rule's exception just because a more specific rule is also active.

You must account for what the broader rule contributes when configuring your query-level exception. To learn more about how the system generally resolves conflicts between rules, see [Conflict resolution for ranking rules](https://documentation.bloomreach.com/discovery/docs/conflict-resolution-for-ranking-rules).
