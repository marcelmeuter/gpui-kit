# Glyphs local defect patches

Upstream: https://github.com/longbridge/gpui-kit
Base revision: `77ff6f794dca3bcee2e90977cedf12a64aed17e4`

The user authorized a local GPUI/GPUI Kit fork for defect fixes on 2026-11-02.
This source snapshot preserves upstream licenses and assets. GPUI itself remains
on the upstream pinned 0.3.9 snapshot family until a demonstrated defect requires
a separate patch. No upstream contribution or publication is implied.

## Aligned Markdown selection

`crates/base/src/text/inline.rs`: retain text alignment with shaped lines and use
one aligned geometry path for selection, retained Copy, row hit bounds, caret
edges, word selection and links. Preserve multiline selection painting semantics.
Regression includes shaped left/center/right numeric text. GPUI Base library tests:
1437 passed with `--features test-support`; native highlights/copy checked in the
qualification harness. Independent recheck found no remaining material defect;
see `docs/reviews/gpui-stack-qualification-review-20261102.md` in the owning
repository. Reversed partial-drag coverage also passes. Soft-wrap regression
coverage remains a recommended follow-up. Product acceptance is separate.

## Focused buttons becoming disabled

`crates/base/src/button.rs`: retain the dispatch ancestry of an already-focused
button when it becomes disabled, without keeping it as a Tab stop or allowing
activation. Previously disabling Save removed the focused node, so parent
keyboard commands (including Escape and Tab) stopped receiving events. The
regression fails on the pinned implementation and passes with the patch, checking
parent key delivery, disabled activation and navigation to the next control.
All nine base-button tests and all 1,438 base tests pass. Independent native
Save → Tab and Escape rechecks passed in the Glyphs GPUI form; see the owning
repository's `docs/reviews/gpui-model-settings-native-review-20261103.md`.
