# Selection, Search, and Filtering Requirements

Use this checklist when a feature lets users search, filter, sort, paginate, or
select displayed data.

## Establish

Determine the searchable data and matching rules, filter criteria and their
combinations, sortable values and directions, page boundaries, and reset
behavior. For selection, determine single or multiple selection, the eligible
items, whether selection persists across refreshes or pages, and what context
the selection makes available.

Ask only for unresolved decisions. Offer the existing convention first; where
there is no convention, offer relevant choices such as exact or partial search,
one or many selected items, and retained or cleared selection after refresh.
Describe actions that use a selection with `frontend-actions.md`, not here.

## Quality criteria

Every configured condition states its input, scope, and observable result.
Combined conditions and reset behavior are unambiguous when they exist.
Selection requirements state the allowed cardinality, the selection result, and
any persistence rule. A no-match, loading, or failed-result state stays with
this feature.

## Standard groups

- `Search` for query input and matching behavior.
- `Filtering` for criteria and combinations.
- `Sorting` for sortable values and order.
- `Pagination` for page movement and boundaries.
- `Selection` for selecting and retaining items.
- `Reset conditions` for clearing search, filters, sorting, or selection.
- `States` for applicable result states.
- `Error handling` for failed retrieval or processing and recovery.
