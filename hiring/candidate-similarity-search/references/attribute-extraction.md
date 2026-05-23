# Attribute Extraction

The taxonomy and rules for pulling search-useful attributes out of a seed
LinkedIn profile. Use `search-playbook.md` for what to do with them.

## Attribute taxonomy

Work through every category. For each attribute, cite the profile text it
came from (headline, About, a specific experience entry, Skills section,
Education). Mark categories the profile does not show as "not stated" —
never guess.

### Role
- **Current title** — exact wording from the current experience entry or
  headline.
- **Prior titles** — list in reverse-chronological order; note any title
  changes within the same company.
- **Title trajectory** — IC progression (Designer → Senior → Staff),
  movement into management, discipline shifts (e.g. PD → DE).

### Seniority
- **Years in field** — sum the relevant experience entries; ignore
  internships and unrelated work.
- **Level keywords** — Junior / Mid / Senior / Staff / Principal / Lead /
  Director / VP / Head of, as they appear in titles.
- **IC vs management** — note explicit people-management language
  ("managed a team of 6", "hired and grew the team").

### Company
- **Current employer.**
- **Prior employers** (reverse-chronological).
- **Company type** — startup (seed / Series A-C) / scale-up / enterprise /
  agency / consultancy / FAANG-ish / nonprofit / government. Infer from
  the About sections of those employers when the profile doesn't say.
- **Industry / vertical** for each employer — fintech, healthtech, dev
  tools, marketplaces, B2B SaaS, consumer social, etc.

### Skills & tools
- **Skills section** — pull verbatim.
- **Tools and frameworks** mentioned in experience bullets — design tools
  (Figma, Framer), languages (TypeScript, Swift), platforms (AWS, Vercel),
  data tools (SQL, dbt), etc.
- **Methodologies** — research methods, design systems, agile / scrum,
  experimentation, etc.

### Domain expertise
- **Industries worked in** (often a superset of company industries).
- **Problem types** — onboarding, payments, growth, internal tools,
  developer experience, B2B procurement, etc. — taken from experience
  bullets, not inferred from job title alone.

### Education
- **Degree** — level and field.
- **Schools** — undergrad, grad, bootcamps, notable certifications.
- **Graduation year** — only if it helps estimate seniority and the
  profile shows it.

### Location
- **City** and region.
- **Remote signal** — explicit "remote" in title or headline, or a
  long-distance gap between location and employer HQ.

### Tenure pattern
- **Average years per role** — short tenures (<18 months) and long
  tenures (>4 years) are both signals worth surfacing.
- **Total years of professional experience.**

### Side signals
- Open-source projects, talks, conference papers, published writing,
  community involvement, side projects linked from the profile.
- These are useful as search anchors (handle reuse, GitHub username) but
  should not dominate the similarity rating unless the user has asked
  for them.

## What to skip

Do not extract or search on:
- Name and photo (used only for disambiguation, not similarity).
- Contact info (email, phone).
- LinkedIn recommendation text.
- Mutual connections.
- Any personal information outside professional context (family,
  relationship status, religious or political activity, health).

## Weighting rubric

Not every attribute matters equally. The right weighting depends on what
the user is sourcing for.

- **Must-match candidates by default** — current title (or close synonym),
  seniority, two strongest skills, industry.
- **Nice to match** — company type / tier, location, education, tenure
  pattern.
- **Tiebreakers only** — side signals, exact tools beyond the top two
  skills.

If the user's request is ambiguous about which attributes matter, ask
before generating the playbook. If the user does not specify, use the
default weighting above and state that default in the output so they can
correct it.

## Evidence rule

Every extracted attribute in the Attribute Profile must point back to
specific text in the seed profile (headline, About, a specific experience
entry, Skills section, Education). This matches the evidence rule used by
`de-linkedin-profile-evaluation` — the user must be able to verify every
attribute against the source.
