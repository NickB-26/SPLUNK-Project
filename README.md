# 🛡️ Splunk SIEM Project — SOC Analyst Fundamentals

A hands-on project demonstrating the fundamentals of using Splunk as a SIEM (Security Information and Event Management) platform — covering installation, data ingestion, dashboard setup, and writing Search Processing Language (SPL) queries to analyse Windows Event Logs.

---

## 🎯 Project Overview

This project showcases practical SIEM skills by deploying Splunk Enterprise locally, ingesting Windows Event Log data, and building dashboards and queries that an entry-level SOC analyst would use daily. The goals are: to demonstrate basic understanding of Splunk and the ability to translate raw log data into actionable security insight.

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
  <img src="REPLACE_WITH_GITHUB_URL_FOR_Log_into_the_Splunk_account.png" alt="Splunk login page" width="700"><br>
  <em>Figure 1: Logging into the Splunk account</em>
</p>

<br>

**Step 2** — Download the corresponding Splunk Enterprise software for your operating system. I installed Windows 11 on a virtual machine using VMware Fusion on my Mac.

<p align="center">
  <img src="https://github.com/user-attachments/assets/c992ec67-5f96-46ad-a9e9-907e267e7070" alt="Splunk installer running on Windows 11 VM" width="700"><br>
  <em>Figure 2: Running the Splunk installer on the Windows 11 VM</em>
</p>

<br>

**Step 3** — Install Splunk and complete the first-time sign-in to access the Splunk Enterprise interface.

<p align="center">
  <img src="REPLACE_WITH_GITHUB_URL_FOR_Screenshot_2026-04-13_at_00_10_43.png" alt="Splunk Enterprise first-time sign-in screen" width="700"><br>
  <em>Figure 3: Splunk Enterprise first-time sign-in</em>
</p>

---

## 📊 Phase 2: Data Ingestion

**Step 1** — Once the installation is complete, data sources can be added so we have data to analyse. Click **Settings** in the top right corner, then **Add Data**.

<p align="center">
  <img src="https://github.com/user-attachments/assets/a545fdd9-cab1-4840-be9c-541cbec481a6" alt="Splunk Settings menu showing Add Data option" width="700"><br>
  <em>Figure 4: Navigating to Settings → Add Data</em>
</p>

<br>

**Step 2** — Splunk presents multiple onboarding categories — Cloud computing, Networking, Operating System, and Security — alongside several manual data input methods.

<p align="center">
  <img src="REPLACE_WITH_GITHUB_URL_FOR_Add_data.png" alt="Splunk Add Data page showing onboarding categories" width="700"><br>
  <em>Figure 5: Selecting a data source category in the Splunk onboarding page</em>
</p>

<br>

**Step 3** — Select a data source from the various options available (Local Event Logs, Remote Event Logs, Files and Directories, etc.). I chose a directory from my local machine and worked through the remaining steps to finish adding the data source.

<p align="center">
  <img src="https://github.com/user-attachments/assets/5a6ba2b3-d3c3-453f-8671-67bcaaa2c1bd" alt="Selecting a data source in Splunk" width="700"><br>
  <em>Figure 6: Selecting a local directory as the data source</em>
</p>

<br>

**Step 4** — Splunk identified **28,617 WinEventLog events** from the provided source (visible in the top left corner of the search interface). A wide range of filter options can be used to display only the data relevant to the current investigation.

<p align="center">
  <img src="REPLACE_WITH_GITHUB_URL_FOR_28617_events_were_found.png" alt="Splunk search interface showing 28,617 ingested WinEventLog events" width="700"><br>
  <em>Figure 7: Splunk search interface displaying 28,617 ingested events</em>
</p>

---

## 📈 Phase 3: Dashboard Setup

Splunk offers two main dashboarding options:

- **Classic Dashboards** — built using XML
- **Dashboard Studio** — a modern, customisable framework using JSON

A wide range of metrics can be visualised, categorised broadly into **infrastructure**, **application**, and **network health**. As an example, I set up a **CPU Usage** home dashboard to monitor the deployment in real time.

<p align="center">
  <img src="REPLACE_WITH_GITHUB_URL_FOR_Choose_a_home_dashboard.png" alt="Choose a home dashboard dialog with CPU Usage options" width="700"><br>
  <em>Figure 8: Selecting CPU Usage: Deployment as the home dashboard</em>
</p>

<br>

The dashboard displays multiple panels, including **Deployment-Wide Median CPU Usage** and **Median CPU Usage** over a 30-minute window, giving an immediate at-a-glance view of system health.

<p align="center">
  <img src="REPLACE_WITH_GITHUB_URL_FOR_Median_CPU_usage_for_the_last_30_minutes.png" alt="Splunk dashboard showing median CPU usage over 30 minutes" width="700"><br>
  <em>Figure 9: Deployment-Wide Median CPU Usage panel (30-minute window)</em>
</p>

<br>

The dashboard also breaks CPU usage down by process class — separating index service, search, scripted input, and the splunkd server itself — which is useful for spotting which Splunk components are consuming the most resources.

<p align="center">
  <img src="REPLACE_WITH_GITHUB_URL_FOR_Median_CPU_usage_by_Process_class.png" alt="Median CPU Usage by Process Class panel" width="700"><br>
  <em>Figure 10: Median CPU Usage by Process Class — splunkd server, search, scripted input</em>
</p>

<br>

Dashboards support multiple chart types, each suited to different analytical purposes:

- **Column & bar charts** — comparing values across categories
- **Line & area charts** — showing changes or trends over time
- **Pie & donut charts** — displaying proportional breakdowns of a whole

Different fields can be selected from the left pane to tailor the view to specific analytical needs.

---

## 🔍 Phase 4: SPL — Search Processing Language

The Splunk search bar accepts **Search Processing Language (SPL)** — Splunk's proprietary query language for filtering and analysing data. The search bar offers autocomplete suggestions as you type, surfacing matching source types and recent terms.

<p align="center">
  <img src="REPLACE_WITH_GITHUB_URL_FOR_Search_bar.png" alt="Splunk search bar with SPL autocomplete suggestions" width="700"><br>
  <em>Figure 11: SPL autocomplete suggesting WinEventLog source types</em>
</p>

<br>

SPL accepts several input types:

- **Search terms & keywords** — e.g. `error`, `failed`, `login`
- **Field-value pairs** — e.g. `host=webserver`, `sourcetype=access_combined`
- **Boolean operators** — `AND`, `OR`, `NOT`
- **Wildcards** — e.g. `fail*` matches *failure*, *failed*, etc.
- **Quoted phrases** — e.g. `"database error"` for exact matches

Multiple commands can be **chained using the pipe symbol (`|`)**. This means commands following the pipe take the output from the previous command and process it further, allowing the analyst to fine-tune results by progressively filtering and transforming the data.

### Example query — events over time, broken down by account

The query below filters for Windows Security events and uses `timechart` to plot event counts grouped by `Account_Name`, limited to the top 10:

```spl
source="WinEventLog:Security" | timechart count by Account_Name limit=10
```

<p align="center">
  <img src="REPLACE_WITH_GITHUB_URL_FOR_Search_Timechart_count_by_account_name.png" alt="SPL timechart visualisation showing event count by account name" width="700"><br>
  <em>Figure 12: timechart visualisation showing peaks in account activity over a 1-hour window</em>
</p>

<br>

### Example query — single-value visualisation

SPL also supports aggregation functions like `avg()` for single-value summaries — useful for KPIs or dashboard tiles:

```spl
source="WinEventLog:Security" date_second=55 | timechart avg(RecordNumber)
```

<p align="center">
  <img src="REPLACE_WITH_GITHUB_URL_FOR_Search_by_time_chart_average_record_number.png" alt="Splunk single-value visualisation showing average RecordNumber" width="700"><br>
  <em>Figure 13: Single-value visualisation displaying the average RecordNumber across 294 events</em>
</p>

---

## 🎓 Lessons Learned

### Technical insights
- **SPL is more powerful than expected.** What initially looked like a simple search bar is actually a full pipeline language. Understanding the `|` operator and how each command transforms the previous output was a turning point in writing effective queries.
- **Data volume changes everything.** With over 28,000 Windows events ingested, I quickly realised that unfiltered searches return overwhelming noise. Effective analysis depends on knowing *what* to filter for — which means understanding the relevant Windows Event IDs before you even start typing.
- **Dashboards are storytelling tools.** A well-designed dashboard isn't just a collection of charts — it should answer the specific questions an analyst would ask during triage.

### SOC analyst mindset
- **Detection requires hypothesis-driven thinking.** Rather than asking "what does this data show?", I learned to ask "what would an attacker look like in this data?" — which led to far more meaningful searches.
- **Context matters more than alerts.** A single failed login is meaningless on its own; five failed logins followed by a success from the same source is a potential incident. Building queries that capture *patterns*, not just events, is the core skill.

### Challenges & how I overcame them
- **Choosing what to monitor was overwhelming.** With dozens of possible Event IDs, I focused on detections relevant to early-stage attacker behaviour and worked backwards from there.

### What I would do differently next time
- **Set up alerts earlier in the process.** I built dashboards before configuring alerts — but in a real SOC, automated alerting is the foundation, and dashboards support investigation rather than replacing it.
- **Document queries as I go.** Retracing my steps to write this README highlighted the value of keeping a running notebook of every SPL query alongside what it taught me.

---

## 📚 References

- [Splunk Official Site](https://www.splunk.com)
- [Splunk Search Reference](https://docs.splunk.com/Documentation/Splunk/latest/SearchReference/WhatsInThisManual)
- [Splunk Search Tutorial](https://docs.splunk.com/Documentation/Splunk/latest/SearchTutorial/WelcometotheSearchTutorial)<img width="1440" height="900" alt="Log into the Splunk account" src="https://github.com/user-attachments/assets/0e801c2b-dec6-4292-96fc-7dd6377a752b" />
