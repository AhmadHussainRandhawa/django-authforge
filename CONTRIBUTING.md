# Contributing to AuthForge

Thanks for considering a contribution. This project's entire value is in getting authentication details right — so contributions that improve correctness, security, or clarity are the ones that matter most here.

---

## Reporting a Security Issue

**Do not open a public issue for a real vulnerability.** Authentication and 2FA bugs can be actively exploitable the moment they're public.

Instead, email **official.ahmadrandhawa@gmail.com** with:
- A description of the issue and its impact
- Steps to reproduce
- Any suggested fix, if you have one

You'll get a response before it's discussed anywhere public. Once resolved, credit is given in the fix's commit and release notes if you'd like it.

Non-security bugs (typos, broken templates, unclear docs) can go straight to a public issue as normal.

---

## Where to Start

The [Security Hardening Checklist](README.md#security-hardening-checklist) and [Roadmap](README.md#roadmap) in the README are the current priority list — both are pre-approved in direction, so you can go straight to a PR rather than pitching the idea first. Good first contributions:

- Closing a checklist item (e.g. wiring up the disabled rate-limit decorators)
- Adding tests — there's no test suite yet, so almost any test is net-new coverage
- Finishing a partially-wired feature (SMS OTP, email OTP)

For anything not already listed there, open an issue describing the change before starting — it saves rework if the approach needs discussion first.

---

## Branching & Commits

Branch off `main`:

| Prefix | Use for |
|---|---|
| `fix/<name>` | Bug or security fixes |
| `feature/<name>` | New functionality |
| `docs/<name>` | Documentation only |
| `test/<name>` | Test additions, no behavior change |

Commits follow **[Conventional Commits](https://www.conventionalcommits.org/)**:

```
fix(auth): enable rate-limit decorators on LoginView
feat(2fa): wire up SMS delivery for phonenumber plugin
test(activation): add coverage for expired activation tokens
docs(readme): update hardening checklist status
```

One commit, one concern. No `wip`, `fix stuff`, or `update`.

---

## Code Style

- Follow PEP 8; match the existing pattern of class-based views in `core_auth/views.py`
- Keep authentication logic in `backends.py`, `views.py`, and `forms.py` — don't scatter auth decisions across templates or unrelated apps
- New views touching login, activation, or 2FA should explain *why*, not just *what*, in the commit body — the reasoning matters as much as the diff for security-sensitive code

---

## Testing

There's no test suite yet — this is the single highest-value gap in the project. Any PR that changes authentication, activation, or 2FA behavior should include a test for it, even if nothing else in that area is tested yet. Priority areas:

- Token expiry and reuse (activation and password reset)
- Rate-limit triggering and the 429 response path
- TOTP and backup-code verification, including the failure paths

Run the suite before opening a PR:

```bash
python manage.py test
```

---

## Pull Requests

1. Branch from `main`, keep the PR scoped to one concern
2. Describe **what** changed, **why**, and how you tested it
3. If it touches a hardening checklist item, note which one — it'll be checked off in the README as part of the merge
4. Expect the security-relevant parts of the diff to get the closest review, before style or naming

---

## Recognition

Every merged PR is credited in commit history; security reports handled privately are credited in the fix and release notes, with your permission.

Thanks for helping make this project trustworthy, not just functional.
