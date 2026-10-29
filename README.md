# Amazon Reviews Scraping Benchmark

AIMultiple benchmark of five web scraping providers (Bright Data, Oxylabs, Decodo, Nimble and Zyte) on the same 500 Amazon product review URLs. The study measures validation success rate and end-to-end completion time.

> [Read the benchmark on AIMultiple](https://aimultiple.com/amazon-reviews-scraping)

## Workload

The URLs come from Amazon product pages with varying review counts and product categories. Each provider received every URL once, for 2,500 requests in total. Requests ran one at a time with a 2-second delay, up to 3 retries on HTTP 429 and a 600-second execution timeout.

Bright Data, Oxylabs and Decodo used dedicated Amazon APIs with structured JSON output. Nimble and Zyte returned rendered HTML, parsed with CSS selectors for five standard review fields.

- Success: HTTP status 200-399 or 404, a completed job for async providers, and at least one review with a valid review_text or rating (or a matching CSS selector). 404 pages and pages without reviews counted as valid. An empty result on a URL where another provider extracted reviews counted as a failure.
- Completion time: from the first API request to the final response, including polling for async providers.

## Benchmark results

Validation success rate and completion time per request:

| Provider | Success rate (%) | Completion time (s) |
| --- | ---: | ---: |
| Bright Data | 96 | 74 |
| Oxylabs | 92 | 4 |
| Nimble | 92 | 13 |
| Zyte | 75 | 13 |
| Decodo | 11 | 10 |

Bright Data led on success and returned 29 JSON fields per review against 10 for Oxylabs, but had the longest completion time. Decodo's Amazon parser returned empty results for most URLs, and its successes came mainly from correct 404 detection.

## Scope

Results come from one sequential pass per provider, with each provider's own API configuration. Amazon pages and anti-bot defenses change, so later runs can differ.

## Ownership

The benchmark implementation was developed for AIMultiple and belongs to AIMultiple. This repository contains a documentation summary. Source code and benchmark datasets are not distributed here.
