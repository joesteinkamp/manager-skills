# Discovery Playbook

Search-query patterns and the confidence model for `designer-link-discovery`.
Use the catalog (`platform-catalog.md`) for *what* to look for; use this file
for *how* to find it and *how confident* to be.

## Search-query patterns

Replace `Full Name` with the candidate's name in quotes, and add a
disambiguating term (employer or city) whenever the name is common.

**Name-based discovery**
- `"Full Name" designer portfolio`
- `"Full Name" UX designer` / `"Full Name" product designer` (match discipline)
- `"Full Name" + current employer`
- `"Full Name" + city`
- `"Full Name" dribbble` / `"Full Name" behance` / `"Full Name" medium`

**Site-scoped discovery** — narrows to one platform:
- `site:medium.com "Full Name"`
- `site:dribbble.com "Full Name"`
- `site:behance.net "Full Name"`
- `site:github.com "Full Name"`
- `site:read.cv "Full Name"` / `site:posts.cv "Full Name"`

**Handle-reuse discovery** — the strongest technique. Once any handle is known:
- Try that exact handle on every platform in the catalog
  (`dribbble.com/handle`, `x.com/handle`, `github.com/handle`,
  `medium.com/@handle`, `behance.net/handle`).
- Search `"@handle" designer` to find where else the handle appears.

**Portfolio-domain guessing** — try direct URLs before searching:
- `firstnamelastname.com`, `firstlastname.com`, `firstname.design`,
  `firstnamelast.co`, `firstname.studio`, `firstnamexyz.com`.

**Link-graph crawling** — once a profile is open, read its bio, About page,
and footer for outbound links, and follow them. Repeat until no new links
appear.

## Confidence model

Rate every link with one of three levels. Always name the signal behind the
rating.

### Confirmed

The link is the candidate's, with near-certainty. Any one of:
- The link is published on the candidate's own LinkedIn profile (Contact Info,
  Featured, About, or an experience entry).
- The page explicitly cross-links back to the candidate's LinkedIn or to another
  already-Confirmed link.
- The page names the same current employer **and** role (or the same distinctive
  combination of employer, city, and discipline) as LinkedIn.
- A reused handle ties it to an already-Confirmed profile and the bio/photo are
  consistent.

### Probable

Strong but not conclusive. The name and design discipline match, **and** at
least one supporting signal is present:
- same city or region,
- the same employer mentioned somewhere on the page,
- the same profile photo as a Confirmed profile,
- a reused handle, but without an explicit cross-link.
No signal contradicts the match.

### Unverified

A plausible match that could not be tied to this person:
- The name matches but discipline, employer, and location cannot be confirmed.
- The name is common and multiple plausible candidates exist.
- The only signal is a name match on a noisy platform (a bare social handle).
Put every Unverified link in the `Needs Verification` section, never in the main
inventory, and state exactly what a human should check to resolve it.

## Disambiguation for common names

When the candidate has a common name, assume multiple distinct people exist
until the signals separate them.
- Anchor every match to a distinctive detail from LinkedIn: a specific employer,
  an unusual city, a niche discipline, or the vanity-URL slug.
- Compare profile photos across platforms — a reused photo is a strong tie.
- If two candidate profiles for "the same" platform conflict (different cities,
  different employers), they are probably two people — do not merge them.
- Never present a guessed link as the candidate's. Downgrade to Unverified and
  explain the ambiguity.

## Ethics & privacy

- Stay within professional, public links: portfolio, design communities,
  writing, code, professional social accounts, speaking and community work.
- Do not search for or report private personal information: home address,
  personal phone, personal email, family members, dating profiles, or anything
  unrelated to professional work. If such a result appears, drop it.
- Report what is publicly visible; do not attempt to bypass logins, paywalls, or
  privacy settings.
- The goal is to assemble a candidate's body of professional work for a fair
  hiring review — not to build a personal dossier.
