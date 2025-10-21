# Vendored Dependencies

This directory contains vendored copies of dependencies with patches applied.

## minify-js

Version: 0.6.0

### Patches Applied

1. **Fix for top-level if-statement minification (Issue #225)**
   - Changed `is_closure()` to `is_closure_or_global()` on lines 288 and 316
   - Replaced assertion with conditional check on line 331
   - Properly handle both returning and non-returning if-else branches

   These changes fix panics when minifying JavaScript code with if-else statements at the top level (not inside a function/closure).

### Files Modified
- `src/minify/pass1.rs`: Lines 288, 316, and 330-343
