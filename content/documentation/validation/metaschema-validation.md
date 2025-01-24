---
title: Metaschema Validation
weight: 220
---
# Metaschema Validation

Maintainers of [the core OSCAL models](https://github.com/usnistgov/OSCAL/tree/main/src/metaschema) and the [FedRAMP OSCAL Constraints](https://github.com/GSA/fedramp-automation/tree/develop/src/validations/constraints) use [the Metaschema Information Modeling Framework](https://framework.metaschema.dev/). Metaschema [has several capabilities](https://framework.metaschema.dev/specification/overview/), including validating the OSCAL data models in JSON, XML, or YAML formats with a unified framework to ease maintenance for maintainers and community adopters.

## Constraints: Validation Rules for Metaschema

The use of Metaschema for OSCAL modeling allows for developers to use [Metaschema constraints](https://framework.metaschema.dev/specification/syntax/constraints/) for validation. Metaschema constraints are a robust mechanism to declaratively describe requirements for OSCAL data elements, be it in JSON, XML, or YAML, independently or in relation to one another. Developers may also use variables in constraints to cache important data for one or more constraints to facilitate [DRY constraint code and not repeat yourself](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself).

Developers can define constraints directly with Metaschema models (e.g. constraints within [each of the core OSCAL models](https://github.com/usnistgov/OSCAL/tree/main/src/metaschema)), or customize and extend the model with constraints in external files, like FedRAMP's OSCAL constraints for its specific use cases. The [oscal-cli](./oscal-cli.md), or other conforrmant software, can process both or either for target OSCAL content.

There are currently [six types of constraints](https://framework.metaschema.dev/specification/syntax/constraints/#constraint-types). 

- `allowed-values`
- `expect`
- `has-cardinality`
- `index`
- `index-has-key`
- `is-unique`
- `matches`

Each constraint type addresses a different use case and provides a common patterns to define its requirements. Each constraint type has a similar structure with [common attributes and elements](https://pages.nist.gov/metaschema/specification/syntax/constraints/#common-constraint-data).

| Data | Data Type | Use      | Default Value |
|:--- |:--- |:--- |:--- |
| [`@id`](#id) | [`token`](/specification/datatypes/#token) | optional | *(no default)* |
| [`@level`](#level) | `DEBUG`,`INFORMATIONAL`, `WARNING`, `ERROR`, or `CRITICAL` | optional | `ERROR` |
| [`@target`](#target) | special | *(varies)* | `.` |
| [`<formal-name>`](#formal-name) | [`string`](/specification/datatypes/#string) | 0 or 1 | *(no default)* |
| [`<description>`](#description) | [`markup-line`](/specification/datatypes/#markup-line) | 0 or 1 | *(no default)* |
| [`<prop>`](#prop) | special | 0 to ∞ | *(no default)* |
| [`<remarks>`](#remarks) | special | 0 or 1 | *(no default)* |

FedRAMP uses all of these attributes and elements, in an opinionated way, to follow [its own style guide for Metaschema constraint development](https://github.com/GSA/fedramp-automation/blob/develop/src/validations/styleguides/STYLE.md) and [constraints to validate the Metaschema constraints themselves](https://github.com/GSA/fedramp-automation/blob/develop/src/validations/styleguides/fedramp-constraint-style.xml).

## Metapath

Metaschema constraints have `@target` and `@test` attributes. These attributes provide a robust way for developers to use the expression language for Metaschema constraints, [Metapath](https://framework.metaschema.dev/specification/syntax/metapath/) to logically describe one data element, a sequence of similar, adjacent elements, or a conditional relationship between multiple elements in one or multiple OSCAL documents. The inventory of FedRAMP OSCAL Constraints has hundreds of examples. The [Metaschema specification](https://framework.metaschema.dev/specification/) has full detail on the full syntax and capabilities of the language.
