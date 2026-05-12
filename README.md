# 🛡️ Splunk SIEM Project — SOC Analyst Fundamentals

A hands-on project covering Splunk Enterprise installation, data ingestion, dashboard setup, and writing SPL queries to analyse Windows Event Logs.

---

## 🎯 Project Overview

I built this project to get hands-on experience with Splunk as a SIEM platform. The idea was simple: deploy Splunk locally, feed it real Windows Event Log data, and start writing queries that an entry-level SOC analyst would actually use. Less theory, more doing.

---

## 🖥️ Environment

- **Operating System:** Windows 11 (running on a VMware Fusion virtual machine)
- **SIEM Platform:** Splunk Enterprise
- **Data Source:** Windows Event Logs
- **Events Ingested:** 28,617 WinEventLog events

---

## 📥 Phase 1: Splunk Installation

**Step 1** — Go to [Splunk](https://www.splunk.com), create an account, and log in.

<p align="center">
  <img src="https://github.com/user-attachments/assets/5e8446cb-1dd4-4523-af3c-55f951f1fa85" alt="Log into the Splunk account" alt="Splunk login page" width="700"><br>
  <em>Figure 1: Logging into the Splunk account</em>
</p>

<br>

**Step 2** — Download the Splunk Enterprise installer for your operating system. I was running Windows 11 inside a VMware Fusion VM on my Mac.

<p align="center">
  <img src="https://github.com/user-attachments/assets/c992ec67-5f96-46ad-a9e9-907e267e7070" alt="Splunk installer running on Windows 11 VM" width="700"><br>
  <em>Figure 2: Running the Splunk installer on the Windows 11 VM</em>
</p>

<br>

**Step 3** — Install Splunk and complete the first-time sign-in to access the Splunk Enterprise interface.

<p align="center">
  <img src="https://github.com/user-attachments/assets/4cb50572-314e-4107-bd86-fd2ae917d60d" alt="Splunk Enterprise first-time sign-in screen" width="700"><br>
  <em>Figure 3: Splunk Enterprise first-time sign-in</em>
</p>

---

## 📊 Phase 2: Data Ingestion

**Step 1** — Click **Settings** in the top right corner, then **Add Data** to start bringing in a data source.

<p align="center">
  <img src="https://github.com/user-attachments/assets/44cc48d9-23e0-467d-8a3d-d3f6d8a77d42" alt="Splunk Settings menu showing Add Data option" width="700"><br>
  <em>Figure 4: Navigating to Settings → Add Data</em>
</p>

<br>

**Step 2** — Splunk gives you several onboarding categories to choose from — Cloud computing, Networking, Operating System, and Security — plus manual input options for files, directories, and event logs.

<p align="center">
  <img src="https://github.com/user-attachments/assets/016fc670-659f-49ed-9efb-3cc931c2bc10" alt="Splunk Add Data page showing onboarding categories" width="700"><br>
  <em>Figure 5: Selecting a data source category in the Splunk onboarding page</em>
</p>

<br>

**Step 3** — I picked a local directory on my machine as the data source and worked through the remaining steps to finish the setup.

<p align="center">
  <img src="https://github.com/user-attachments/assets/a545fdd9-cab1-4840-be9c-541cbec481a6" alt="Selecting a data source in Splunk" width="700"><br>
  <em>Figure 6: Selecting a local directory as the data source</em>
</p>

<br>

**Step 4** — Splunk picked up **28,617 WinEventLog events** from the source. From here you can start filtering down to whatever is relevant to the investigation.

<p align="center">
  <img src="https://github.com/user-attachments/assets/cad8b802-a2ff-44e8-82c8-2231b4230440" alt="Splunk search interface showing 28,617 ingested WinEventLog events" width="700"><br>
  <em>Figure 7: Splunk search interface displaying 28,617 ingested events</em>
</p>

---

## 📈 Phase 3: Dashboard Setup

**Step 1** — Splunk offers two dashboarding options: Classic Dashboard (XML-based) and Dashboard Studio (a more modern, customisable framework using JSON). I went with Dashboard Studio.

<p align="center">
  <img src="https://github.com/user-attachments/assets/02e889ba-c512-4964-884e-7c798e2d96df" alt="Choose a home dashboard dialog with CPU Usage options" width="700"><br>
  <em>Figure 8: Selecting CPU Usage deployment as the home dashboard</em>
</p>

<br>

**Step 2** — There are a lot of metrics to choose from across infrastructure, application, and network health. I started with the **CPU Usage** home dashboard to get a feel for how dashboards work. It shows **Deployment-Wide Median CPU Usage** and **Median CPU Usage** over a 30-minute window — a quick way to see system health at a glance.

<p align="center">
  <img src="https://github.com/user-attachments/assets/5e1c7344-0a80-482f-8526-7e5b2d862f7e" alt="Splunk dashboard showing median CPU usage over 30 minutes" width="700"><br>
  <em>Figure 9: Displaying Median CPU Usage (30-minute window)</em>
</p>

<br>

**Step 3** — Drilling down further, you can break CPU usage down by process class — separating index service, search, scripted input, and the splunkd server — which makes it easy to spot which component is eating the most resources.

<p align="center">
  <img src="https://github.com/user-attachments/assets/5214a808-cc41-48bf-a3b6-b09e70d83230" alt="Median CPU Usage by Process Class panel" width="700"><br>
  <em>Figure 10: Median CPU Usage by Process Class — splunkd server, search, scripted input</em>
</p>

<br>

Dashboards support several chart types depending on what you're trying to show:
- Column & bar charts — comparing values across categories
- Line & area charts — showing changes or trends over time
- Pie & donut charts — displaying proportional breakdowns of a whole

---

## 🔍 Phase 4: SPL — Search Processing Language

The Splunk search bar runs **Search Processing Language (SPL)** — Splunk's query language for filtering and analysing data.

**Step 1** — The search bar autocompletes as you type, suggesting matching source types and recent terms. SPL accepts several input types:

- **Search terms & keywords** — e.g. `error`, `failed`, `login`
- **Field-value pairs** — e.g. `host=webserver`, `sourcetype=access_combined`
- **Boolean operators** — `AND`, `OR`, `NOT`
- **Wildcards** — e.g. `fail*` matches *failure*, *failed*, etc.
- **Quoted phrases** — e.g. `"database error"` for exact matches

<p align="center">
  <img src="https://github.com/user-attachments/assets/6d4119bf-b7b6-4f29-8668-d2bed3cf9ad7" alt="Splunk search bar with SPL autocomplete suggestions" width="700"><br>
  <em>Figure 11: SPL autocomplete suggesting WinEventLog source types</em>
</p>

<br>

**Step 2** — Commands can be **chained using the pipe symbol (`|`)**. Each command takes the output of the previous one and processes it further — so you can progressively filter and shape the data rather than trying to do everything in one go.

### Example query — events over time, broken down by account

Filters for Windows Security events and uses `timechart` to plot event counts grouped by `Account_Name`, limited to the top 10:

```spl
source="WinEventLog:Security" | timechart count by Account_Name limit=10
```

<p align="center">
  <img src="https://github.com/user-attachments/assets/1152408e-3cb2-4257-ab2e-9e26a52c81f1" alt="SPL timechart visualisation showing event count by account name" width="700"><br>
  <em>Figure 12: timechart visualisation showing peaks in account activity over a 1-hour window</em>
</p>

<br>

### Example query — single-value visualisation

SPL also supports aggregation functions like `avg()` for single-value summaries — handy for KPI tiles on a dashboard:

```spl
source="WinEventLog:Security" date_second=55 | timechart avg(RecordNumber)
```

<p align="center">
  <img src="https://github.com/user-attachments/assets/1617b3db-65ca-4825-a2e6-4f2002e213e9" alt="Splunk single-value visualisation showing average RecordNumber" width="700"><br>
  <em>Figure 13: Single-value visualisation displaying the average RecordNumber across 294 events</em>
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/8b2a1876-32ce-49d0-91d7-50ee0015de00" alt="Timechart count by account name" width="700"><br>
  <em>Figure 14: Visualisation of events generated by the various accounts</em>
</p>

---

## 🎓 Lessons Learned

### Technical insights
- **SPL is more powerful than it looks.** I expected a basic search box. What I got was a full pipeline language — once I understood how the `|` operator works and how each command reshapes the output, writing useful queries became much faster.
- **28,000 events is a lot of noise.** Unfiltered searches were overwhelming. I quickly learned that effective analysis starts with knowing your Event IDs before you touch the search bar — otherwise you're just scrolling through data with no direction.
- **Dashboards are for answering specific questions.** The most useful ones I built weren't the most visually impressive — they were the ones built around a question I actually wanted to answer.

### SOC analyst mindset
- **I started asking "what would an attacker look like in this data?" instead of "what does this data show?"** That shift made my queries much more focused and actually useful.
- **One event means nothing. Patterns mean everything.** A single failed login is noise. Five failed logins followed by a success from the same account is something worth investigating. I kept reminding myself to look for sequences, not just individual events.

### Challenges & how I overcame them
- **I didn't know where to start with so many Event IDs.** Rather than trying to cover everything, I picked one scenario — multiple failed logins followed by a success — and built queries around that. Working from a specific threat rather than general curiosity made it much easier to make progress.

### What I would do differently next time
- **Set up alerts before building dashboards.** I got caught up making things look good before I had alerts configured. In a real SOC, alerts come first — dashboards support investigation, they don't replace it.
- **Keep a query notebook from the start.** Writing up this project took longer than it should have because I hadn't documented my SPL queries as I went. Next time I'll keep a running note of every query alongside what it showed me.

---

## 📚 References

- [Splunk Official Site](https://www.splunk.com)
- [Splunk Search Reference](https://docs.splunk.com/Documentation/Splunk/latest/SearchReference/WhatsInThisManual)
- [Splunk Search Tutorial](https://docs.splunk.com/Documentation/Splunk/latest/SearchTutorial/WelcometotheSearchTutorial)
