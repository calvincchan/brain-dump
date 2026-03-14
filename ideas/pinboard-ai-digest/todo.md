# To-Do

Never delete completed items — mark them `[x]` and leave them in place.

### Discovery
- [ ] Review Pinboard API docs — understand auth, bookmark fetch endpoints, unread flag
- [ ] Decide on video transcript source (YouTube Data API, yt-dlp + Whisper, third-party service)
- [ ] Choose email delivery service (Resend, Postmark, SES, SMTP)
- [ ] Decide where processed-link state is stored (SQLite file, Pinboard tag, hosted DB)

### Design
- [ ] Define pipeline stages and data flow diagram
- [ ] Define what "deeper research" produces per link (schema for agent output)
- [ ] Design digest email format — what does one day's email look like?
- [ ] Decide on hosting/scheduling approach (cron job, GitHub Actions, cloud scheduler)

### Build
- [ ] Pinboard fetcher — poll for new/unread bookmarks
- [ ] Web scraper / reader — extract clean text from URLs
- [ ] Video transcript extractor
- [ ] Per-link AI research agent
- [ ] Daily digest synthesizer — roll up individual summaries
- [ ] Email renderer and sender
- [ ] Scheduler and orchestration

### Refinement
- [ ] Add Pinboard tag-based routing (e.g. `digest:skip`, `digest:deep`)
- [ ] Consider cross-referencing new links against previously saved ones
