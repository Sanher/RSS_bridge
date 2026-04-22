# Changelog

## 0.1.3

- Clarify the add-on context so ingress remains the preferred human access path
  while local direct HTTP access can also serve backend integrations such as
  Feedreader.

## 0.1.2

- Resolve the official RSS-Bridge entrypoint from `/app/docker-entrypoint.sh` before the fallback paths.
- Keep the wrapper compatible with the previous fallback lookup through `PATH` and `/docker-entrypoint.sh`.

## 0.1.1

- Escape `auth_token` before writing the managed `config.ini.php`.
- Keep token-based authentication compatible with quotes, backslashes, spaces,
  and line breaks in the configured value.

## 0.1.0

- Add the initial RSS Bridge Home Assistant add-on scaffold.
- Use the wrapper pattern with a canonical parent add-on and a coordinating
  child repository.
- Wrap the official RSS-Bridge image with ingress-first access and persistent
  storage under `/data/rss-bridge`.
