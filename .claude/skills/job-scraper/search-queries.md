# Search Queries for Job Scraper

Search scope: entry-level, junior, and internship software roles in South Korea. Prioritize backend development with Java and Spring Boot.

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI first. Shipped country-agnostic CLIs include `linkedin-search` and `freehire-search`; Danish demos and any skill you add with `/add-portal` are included the same way. You do **not** need a matching `site:` line below for those CLIs to run.

The `site:` query templates in this file are the **WebSearch fallback** — for portals without a CLI, company career pages, or when a CLI fails.

**Language scope:** write every query category in every language listed in your CLAUDE.md Languages table (typically 1-2, sometimes more). A posting requiring a language you have *not* declared, as a job condition, is excluded before scoring; a posting requiring a *higher level* than you declared in a language you *do* work in is flagged for your own judgment, not excluded — see `04-job-evaluation.md`'s Language Gate, the single source of truth for this rule. Translate each category's keywords rather than machine-translating word-for-word (e.g. "Frontend Developer" -> "Desarrollador Frontend", not a literal word-for-word translation) if you work in more than one language.

## Search Sites

Korean public sources (WebSearch):
- [점핏](https://jumpit.saramin.co.kr/positions?jobCategory=1&sort=popular) and [원티드](https://www.wanted.co.kr/) for developer roles.
- [사람인](https://www.saramin.co.kr/zf_user/), [잡코리아](https://www.jobkorea.co.kr/), and [인크루트](https://job.incruit.com/) for regular hiring and entry-level recruitment.
- [링커리어](https://linkareer.com/) for internships and graduate recruitment. Keep individual job postings from the results.

Additional public sources:
- LinkedIn Jobs and Freehire through their enabled portal CLIs. For LinkedIn, use South Korea as the location.
- Public employer careers pages for known target companies.
- [당근 채용](https://careers.daangn.com/jobs/) through public web search; the Career Ops scanner did not recognize this board in the comparison run.

Manual source:
- [SSAFY 채용관](https://recruiting.ssafy.com/login.php?ref_url=/) requires sign-in. Use a posting URL or text supplied by the user; leave this source out of automatic web searches.

For public web searches, open the individual posting and confirm the role, experience requirements, location, and closing date before keeping it. If the public details are unavailable, use the employer's public posting or flag the result for manual review.

## Query Categories

Queries are grouped by priority. Write **each category in every language from your Languages table** (see Language scope above). Combine each query with your location terms (e.g. your city, region, or metro area) where the site supports it.

**Organize by function, not job title.** The same underlying work carries different titles across companies and markets (a "Data Scientist" role at one employer may be posted as "Insights Analyst" or "Data Consultant" at another). Name each priority category after the function it covers, and list several plausible job titles as query variants within that category rather than betting an entire priority tier on one exact title string.

### Priority 1: Junior backend and server development

Look for backend and server development roles open to junior candidates and new graduates.

```
site:jumpit.saramin.co.kr/position/ (백엔드 OR 서버개발) (신입 OR 주니어 OR 경력무관)
site:wanted.co.kr/wd/ (백엔드 OR 서버) (신입 OR 주니어 OR "경력 1년")
site:careers.daangn.com (백엔드 OR backend) (신입 OR 인턴 OR 채용전환형)
site:linkedin.com/jobs "backend engineer" (junior OR "new grad" OR intern) ("South Korea" OR Seoul OR Busan)
```

### Priority 2: Java and Spring backend

Look for Java, Spring, and Spring Boot roles that accept early-career candidates.

```
site:saramin.co.kr/zf_user/jobs (Java OR Spring) (백엔드 OR 서버) (신입 OR 경력무관)
site:jobkorea.co.kr/Recruit/GI_Read (Java OR Spring) (백엔드 OR 서버) (신입 OR 경력무관)
site:job.incruit.com (Java OR Spring) (백엔드 OR 서버개발) (신입 OR 경력무관)
```

### Priority 3: Backend internships and graduate hiring

Look for development internships, conversion-track internships, and graduate hiring with a software or backend role.

```
site:linkareer.com/activity/ (백엔드 OR 서버개발 OR 소프트웨어) (인턴 OR 채용연계형 OR 신입)
site:jumpit.saramin.co.kr/position/ (백엔드 OR 서버) (인턴 OR 채용전환형)
site:linkedin.com/jobs "software engineer intern" (backend OR server) ("South Korea" OR Seoul OR Busan)
```

### Priority 4: Adjacent software development

Use for a broader search. Keep roles where the posting describes backend responsibilities such as API or database work.

```
site:wanted.co.kr/wd/ (웹개발 OR 풀스택) (Java OR Spring) (신입 OR 주니어)
site:jobkorea.co.kr/Recruit/GI_Read ("웹 개발" OR "소프트웨어 개발") (API OR Spring) (신입 OR 경력무관)
```

## Location Filter

Search nationwide in South Korea until the user sets a narrower area. Report the listed work location and any stated remote or hybrid arrangement. Check commute or relocation constraints against confirmed preferences before assessing location fit.

## Language Filter

Your working languages and levels are in CLAUDE.md's Languages table. When filtering scraped results, apply `04-job-evaluation.md`'s Language Gate: a posting requiring a language you haven't declared at all is excluded; a posting requiring a higher level than you declared in a language you do work in is not excluded, flag it clearly instead (see `job-scraper/SKILL.md`'s Step 3 "Quick Fit Assessment" for how the flag surfaces in `/scrape` output). Postings simply *written* in a language you don't work in, that don't require it on the job, are fine.

## Date Filter

Only include jobs posted within the last 14 days, or with an application deadline that has not yet passed. If a posting date cannot be determined, include it but flag as "date unknown".

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and also generate 2-3 custom queries for that focus. For example:
- "/scrape [focus_area]" -> relevant category queries + custom focus-specific queries
