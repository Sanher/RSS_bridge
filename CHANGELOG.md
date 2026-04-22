# Changelog

## 0.1.1

- Escape `auth_token` before writing the managed `config.ini.php`.
- Keep the child `run.sh` and parent scaffold `run.sh` aligned for the auth token fix.
- Preserve token values with quotes, backslashes, and line breaks without breaking the generated config.

## 0.1.0

- Scaffold the RSS Bridge child repository as a wrapper-source project.
- Document the wrapper-pattern contract used with the canonical parent
  repository.
- Add the required workflow that notifies the canonical parent add-on repository when a version tag
  is published.
- Record the recommended upstream RSS-Bridge image and release context for the
  parent add-on.
