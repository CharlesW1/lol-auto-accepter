# CHANGELOG


## v1.1.0 (2026-06-27)

### Bug Fixes

- Bundle the clicker package into the built executable
  ([`693073b`](https://github.com/CharlesW1/Python-Image-Clicker/commit/693073b0659b31ffd7162da8c401b8260b95675f))

PyInstaller's static analysis never discovered src/clicker because the script only adds it to
  sys.path at runtime (Image-Clicker(v1.2).py adds SRC via sys.path.insert before importing it),
  which PyInstaller's modulegraph doesn't see. Every released exe (confirmed on the published v1.0.1
  asset) crashed immediately with "ModuleNotFoundError: No module named 'clicker'". Passing --paths
  src lets PyInstaller's analyzer find and bundle the package correctly; verified via its own
  module-discovery output, which now shows zero missing clicker submodules.

### Features

- Add auto-accept-only build variant
  ([`b73ece1`](https://github.com/CharlesW1/Python-Image-Clicker/commit/b73ece18bc6b1d66e6ec978adf1b7bd24240df2c))

Adds a second release executable, Image-Clicker-auto-accept.exe, that only bundles the accept/
  template folder -- just clicking the ready-check Accept button, with none of the find-match or
  post-game buttons (find_match/play_again/continue/skip_stats). No script changes needed since
  template discovery is already dynamic (IMAGE_DIR.rglob); this just points a second PyInstaller
  build at a curated image subset. Wired up in both the CI release workflow and the local
  build_exe.bat script.


## v1.0.1 (2026-06-27)

### Bug Fixes

- Auto-clicker missing Play Again/Continue during ARAM Mayhem matches
  ([`4aacd84`](https://github.com/CharlesW1/Python-Image-Clicker/commit/4aacd84f65333ea47e95d1083aa7921973d97b70))

The default-skin play_again and continue templates didn't match the ARAM Mayhem event UI, so the
  script silently failed to click those buttons. Captured fresh templates from a live Mayhem match
  (already added in the previous commit); this documents it in ACTION_ITEMS.md and triggers a
  release build for the fix.


## v1.0.0 (2026-02-16)

### Features

- Reorganize images and set version to 1.2.0
  ([`97a23c6`](https://github.com/CharlesW1/Python-Image-Clicker/commit/97a23c6c4651ce11ba11d46ac270b652eed1d053))

- Set project version to 1.2.0 in pyproject.toml and src/clicker/__init__.py. - Reorganized images/
  directory into common, 1600, and 1900 subdirectories. - Standardized image filenames to
  snake_case. - Updated Image-Clicker(v1.2).py to recursively search for images. - Updated release
  workflow and build script to build resolution-specific executables.

Co-authored-by: CharlesW1 <8813880+CharlesW1@users.noreply.github.com>

- Reorganize images by function and set version to 1.2.0
  ([`4d0c811`](https://github.com/CharlesW1/Python-Image-Clicker/commit/4d0c811ea103ef9ed7896f31ba977f8286fb6c84))

- Set project version to 1.2.0 in pyproject.toml and src/clicker/__init__.py. - Reorganized images/
  directory by function (accept, find_match, play_again, misc) as requested in PR feedback. -
  Updated Image-Clicker(v1.2).py to recursively search for images using rglob. - Updated release
  workflow and build script to produce a single 'Image-Clicker-auto-queue' preset executable.

Co-authored-by: CharlesW1 <8813880+CharlesW1@users.noreply.github.com>


## v0.1.0 (2026-02-14)

### Chores

- Remove Windows run scripts; prefer shell launcher
  ([`9f20d31`](https://github.com/CharlesW1/Python-Image-Clicker/commit/9f20d3101145933e716c8d2c66dd93dc2e57e660))

Remove Windows-specific run scripts (run_image_clicker.bat and run_image_clicker_from_dist.bat).
  Keep un_image_clicker.sh as the canonical launcher for cross-platform contributors who prefer sh.

### Features

- Add automated versioning and releases via GitHub Actions
  ([`3f6272c`](https://github.com/CharlesW1/Python-Image-Clicker/commit/3f6272c6c0a62a15846e56acae2febb8306226e1))

- Added `pyproject.toml` with `python-semantic-release` configuration. - Initialized versioning in
  `src/clicker/__init__.py`. - Created `.github/workflows/release.yml` for automated releases and
  Windows builds. - Ensured the workflow correctly handles the original script filename. - Addressed
  PR feedback regarding documentation and permissions.

Co-authored-by: CharlesW1 <8813880+CharlesW1@users.noreply.github.com>

- Add automated versioning and releases via GitHub Actions
  ([`6945305`](https://github.com/CharlesW1/Python-Image-Clicker/commit/6945305f8c326bc04e7065e7018b6dafdf040439))

- Added `pyproject.toml` with `python-semantic-release` configuration. - Initialized versioning in
  `src/clicker/__init__.py`. - Created `.github/workflows/release.yml` for automated versioning and
  Windows builds. - Kept the original entry point filename `Image-Clicker(v1.2).py` as requested. -
  Updated build and release scripts to handle the original filename with parentheses.

Co-authored-by: CharlesW1 <8813880+CharlesW1@users.noreply.github.com>

- Add automated versioning and releases via GitHub Actions
  ([`38f2f48`](https://github.com/CharlesW1/Python-Image-Clicker/commit/38f2f4821e776d1b9a021b0891a9cf8b28429edb))

- Renamed entry point to `image_clicker.py` for a stable filename. - Initialized versioning in
  `src/clicker/__init__.py`. - Added `pyproject.toml` with `python-semantic-release` configuration.
  - Created `.github/workflows/release.yml` for automated versioning and Windows builds. - Updated
  all references in documentation and scripts.

Co-authored-by: CharlesW1 <8813880+CharlesW1@users.noreply.github.com>

### Refactoring

- Consolidate clicker modules into src/clicker and remove legacy top-level modules
  ([`29f3c95`](https://github.com/CharlesW1/Python-Image-Clicker/commit/29f3c95bb78d7784bc4917a9d851cde116afc9cc))

Move implementation into the src/clicker package; remove duplicate top-level modules
  (clicker_config.py, clicker_logging.py, clicker_killswitch.py, clicker_imaging.py,
  clicker_window.py).
