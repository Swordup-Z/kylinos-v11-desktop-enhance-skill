# Repository Rules

## Git Commits

- Do not include AI-related author, co-author, generator, or assistant attribution in any git commit message.
- Avoid trailers and phrases such as `Co-authored-by: Claude`, `Co-authored-by: Codex`, `Generated with ...`, `AI-assisted`, or similar AI disclosure text.
- Keep commit messages focused on the actual repository change.
- Use git author `Swordup-Z <swordup.zeng@gmail.com>` when committing from this repository.
- Before committing changes to this skill repository, check whether `README.md` and `README.en.md` need updates. If the change affects installation, supported enhancement coverage, reference entry points, safety boundaries, global prompts, or public usage workflow, update the READMEs in the same commit.

## Documentation

- Experience documents use Chinese by default.
- Avoid writing user-specific absolute paths, user names, one-time logs, or local-only state. Use `$HOME`, `<user>`, `<app-id>`, `<desktop-id>`, and similar placeholders.
- This repository is for reusable KylinOS Desktop V11 feature enhancement knowledge. Do not store ordinary application code or project-specific implementation notes here.
