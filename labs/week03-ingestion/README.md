# Week 03 Lab

Build an ingestion pipeline from a public API/dataset; handle errors and retries.

Starter files for this week's lab will be added here before the lab session
(pulled into your repo via `git fetch upstream && git merge upstream/main`,
as introduced in the Week 1 lab).
1. The bad status code was easiest to trigger because setting `LATITUDE = 999` reliably produced HTTP 400. The timeout was the least predictable because it depended on network timing, although setting `timeout=0.001` made it easy to provoke. A connection error could also be triggered by changing the API hostname to one that did not resolve.

2. Exponential backoff doubled the waiting time after each failed attempt. With `BASE_DELAY = 1` and four total attempts, the code printed delays of **1, 2, and 4 seconds**, then gave up after the fourth failure without an 8-second delay. The actual time between attempts also included the time spent waiting for each request to fail.

3. We did not retry HTTP 400 because the request itself was invalid; repeating the same invalid latitude would not fix it. Timeouts and connection errors can be temporary, so another attempt may succeed. This connects to the lecture’s distinction between transient and permanent failures and the risk of retries amplifying load on an already struggling service.

4. A data contract should define the JSON structure, required fields, types, and handling of missing or null values. Its semantics should specify temperature in °C, wind speed in km/h, humidity as a percentage, city coordinates, and the timezone and meaning of timestamps. The SLA should define the expected delivery schedule, maximum acceptable delay, and how consumers are notified about missing city files or failed runs. Change management should require versioning, advance notice, and a migration period for breaking changes such as renamed fields, changed types, units, or file naming conventions.
