# Packagist setup

The package is not listed on public Packagist. If you use [Packagist](https://packagist.org) or a private Composer registry:

1. Submit `https://github.com/curbngo/jwt-auth` as the package source (or update the existing entry).
2. Enable the GitHub webhook so new tags are indexed automatically.
3. Confirm both release lines are available after the next sync:
   - `0.5.22` on branch `0.5.x` (legacy, Laravel 6–8)
   - `2.0.0` on branch `master` / `2.x` (Laravel 9–13)
4. Keep default branch as `master` for new installs using `^2.0`.

For VCS repositories in `composer.json`, no Packagist change is required — pin legacy apps to `"0.5.22"` and new apps to `"^2.0"`.
