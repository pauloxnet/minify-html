# Changes for Issue #225 Fix

## Summary
Fixed panic in minify-js 0.6.0 when minifying JavaScript code with if-else statements at the top level (not inside a function/closure).

## Files Modified

### Core Changes
1. **Cargo.toml** - Added patch directive to use vendored minify-js
2. **vendor/minify-js/src/minify/pass1.rs** - Fixed two issues:
   - Lines 288 & 316: Changed `is_closure()` to `is_closure_or_global()`
   - Lines 330-343: Replaced assertion with conditional logic

### Supporting Changes
3. **.gitignore** - Added `.venv/` and `.venv*/` patterns
4. **minify-html-python/pyproject.toml** - Added `module-name` configuration for maturin
5. **vendor/README.md** - Documentation of vendored patches
6. **SECURITY_SUMMARY.md** - Security analysis and verification

## Vendored minify-js
The entire minify-js 0.6.0 crate has been vendored in `vendor/minify-js/` with patches applied. This approach was chosen because:
- Minimal changes to the main codebase (just Cargo.toml patch directive)
- Clear visibility of patches for review
- Easy to update or remove when upstream fixes are available

## Testing
- All existing minify-html tests pass
- Verified with original reproducible case from issue #225
- Tested with multiple edge cases (see SECURITY_SUMMARY.md)

## Minimal Change Philosophy
The fix follows minimal change principles:
- Only modified the specific code causing the panic
- No architectural changes
- No new dependencies
- Changes are localized to the problematic function
- All changes are documented and justified
