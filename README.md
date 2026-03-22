# Grype Advanced HTML & PDF Report Template

This template upgrades your standard Grype vulnerability scans into a highly interactive, self-contained HTML report. It includes built-in risk scoring, dark mode aesthetics, and a highly polished PDF export feature.

## What it does

Instead of sifting through massive JSON files or basic text tables, this template uses Grype's native templating engine to output a dynamic web page. You can sort, filter, and group vulnerabilities directly in your browser.

It also features a custom PDF generation tool that takes your active view and formats it into a professional document, complete with a risk matrix summary and a dedicated appendix for file locations.

## Key Features

* **Interactive DataTables:** Search, filter, and sort your vulnerability data instantly.

* **Smart Grouping:** Group identical vulnerabilities by name and version to heavily reduce visual clutter.

* **Risk Matrix:** Automatically calculates an overall risk score (Low, Medium, High, Extreme) based on severity, fix availability, and CISA KEV status.

* **CISA KEV Integration:** Flags actively exploited vulnerabilities automatically using Grype's metadata.

* **Professional PDF Export:** Prompts for report details (Title, Organisation, Author) and generates a formatted landscape PDF with an appendix for file paths.

* **Dark Mode Design:** Easy on the eyes with colour-coded severity and state pills.

## Prerequisites

* [Anchore Grype](https://github.com/anchore/grype) installed and accessible in your system's PATH.

* A modern web browser to view the generated HTML file and export the PDF.

## How to use it

Save the provided template code as a file named `html.tmpl` in your working directory.

Run your scan using the following command format:

```bash
grype "TARGET" -o template -t html.tmpl > REPORTNAME.html
```

**Practical Examples:**

Scanning a local directory or repository:

```bash
grype "dir:C:\Projects\MySoftware" -o template -t html.tmpl > project_scan.html
```

Scanning a container image:

```bash
grype "ubuntu:latest" -o template -t html.tmpl > ubuntu_scan.html
```

Scanning a specific file (like an SBOM):

```bash
grype "sbom:my-sbom.json" -o template -t html.tmpl > sbom_scan.html
```

Once the command completes, simply open the resulting `.html` file in any modern web browser to view your report.

## Generating the PDF Report

1. Open the generated HTML report in your browser.

2. Filter, sort, or group the data to your liking (the PDF will respect your current view).

3. Click the **Export to PDF** button located at the top left of the vulnerability table.

4. You will be prompted to enter a **Report Title**, **Organisation Name**, **Author Name**, and **File Name**.

5. The browser will generate and download the beautifully formatted PDF automatically.

## Understanding the Risk Score

The built-in risk matrix evaluates your software security by weighting severity against fix availability.

Base scores are assigned as:

* **Critical:** 10

* **High:** 5

* **Medium:** 2

* **Low:** 1

If a fix is available, the score for that specific vulnerability is halved.

The system also includes circuit breakers:

1. **CISA KEV:** Vulnerabilities listed in the CISA KEV catalog trigger an automatic Extreme Risk rating.

2. **Thresholds:** Exceeding 3 Criticals or 8 Highs triggers an automatic High Risk rating, regardless of the overall numerical score.
