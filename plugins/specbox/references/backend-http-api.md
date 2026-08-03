# Backend HTTP API Requirements

Use these rules only for backend HTTP API requirements.

Preserve the project's established specification layout, contract source,
language, and grouping. The conventions below are defaults only when the
project has no applicable convention. Do not duplicate an OpenAPI document or
language-native models in a TypeScript block.

## Endpoint feature

When no existing layout applies, use one YAML file per HTTP method and path
template: `GET /orders/{orderId}` and `PATCH /orders/{orderId}` are separate
features. Set `feature` to that method and path. Otherwise preserve the local
feature boundary. Keep the feature `code` and file placement consistent with
the project.

## Contract model

Use the project's existing contract source and representation. When neither
exists, write the endpoint contract in Markdown `description` with a TypeScript
block containing the applicable `params`, `query`, and `body` request parts,
plus models for successful and error responses. When a block uses a model from
another feature, put an explicit `$<feature-code>` link immediately below the
block, outside the code fence.

````yaml
feature: GET /orders/{orderId}
code: get-order
description: |
  ```ts
  type GetOrderRequest = { params: { orderId: string } };
  type GetOrderResponse = { id: string; status: string };
  type ApiError = { code: string; message: string };
  ```

  Order model: $order-model.
specs-unit:
  200 OK:
    - assert: For an existing order, the API returns 200 and GetOrderResponse.
  403 Forbidden:
    - assert: Without authorization, the endpoint returns 403 and ApiError $authorization.
  404 Not Found:
    - propose: For a missing orderId, the API returns 404 and ApiError.
````

Authorization belongs to its own feature. Describe endpoint access in its
`403 Forbidden` group and link that authorization feature.

## Status scenarios

Preserve established requirement groups. When none exist, group `specs-unit`
by HTTP status, such as `200 OK` or `409 Conflict`. Put each distinct reason
for the same status in a separate `assert` or `propose`.
Each entry states the input or precondition, status, response model, and a
significant side effect or its absence when that matters. Do not repeat fields
already defined by the contract model.

`assert` describes an accepted requirement; `propose` describes a draft. During
extraction, create `assert` only from implementation evidence. During delivery,
a `propose` becomes `assert` before its RED test and implementation. Apply the
same structural rules to both; only `assert` participates in test mapping.

## Quality criteria

For every entry, verify that the input or precondition, status, and observable
result are complete, correct, feasible, necessary, unambiguous, and testable.
For a file or selected set, verify method/path uniqueness, status and contract
consistency, changeability, and traceable links. Use an existing priority
mechanism only when the project already has one. Do not add YAML fields merely
to satisfy these checks.
