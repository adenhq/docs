# Aden Documentation

Documentation for the Aden platform and Hive framework.

## Scope

This `docs/` workspace covers:

- Hive framework concepts and build guides (goal-driven, adaptive agent development)

## Canonical Product References

Keep these in sync with Hive project docs:

- `hive/README.md` for positioning, setup flow, and top-level feature language
- `hive/docs/credential-store-usage.md` for credential store architecture and usage patterns
- `hive/docs/aden-credential-sync.md` for Aden credential sync API contracts and integration patterns

## Quick Start (Hive)

```bash
git clone https://github.com/adenhq/hive.git
cd hive
./quickstart.sh
```

Then build and run an exported agent:

```bash
PYTHONPATH=exports uv run python -m your_agent_name run --input '{...}'
```

## Local Docs Development

Install Mintlify CLI:

```bash
npm i -g mint
```

Run from `docs/` (where `docs.json` is located):

```bash
mint dev
```

Preview: `http://localhost:3000`

## Assets

Brand assets used by docs:

- `logo/light.svg`
- `logo/dark.svg`
- `favicon.svg`

## Resources

- [Aden Website](https://adenhq.com)
- [Hive GitHub](https://github.com/adenhq/hive)
- [Mintlify Documentation](https://mintlify.com/docs)
