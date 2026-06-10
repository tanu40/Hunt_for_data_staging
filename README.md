# 📁 Hunt for Data Staging - CTF Challenge

## 📋 Overview

**Hunt for Data Staging** is an interactive, browser-based Capture The Flag (CTF) challenge designed for cybersecurity training. This challenge focuses on detecting data staging activities where attackers aggregate sensitive files into a single folder before exfiltration. Participants analyze Sysmon Event 11 (File Creation) logs to identify suspicious file collection patterns.

## 🎯 Learning Objectives

By completing this CTF, participants will learn:

- **Threat Hypothesis**: Develop hunting hypotheses for data exfiltration patterns
- **Log Analysis**: Analyze Sysmon Event 11 file creation logs to detect staging behavior
- **Pattern Recognition**: Identify unusual file creation bursts in staging directories
- **Correlation Analysis**: Connect file staging with compression tool execution
- **Network Detection**: Recognize post-staging exfiltration indicators
- **Timeline Analysis**: Visualize file creation events over time

## 🛠️ Challenge Tasks (5 Total)

| Task | Description | Skill Focus |
|------|-------------|-------------|
| **Task 1** | Formulate hunting hypothesis (attacker aggregates files into staging folder) | Threat Hunting |
| **Task 2** | Identify the staging folder path (`C:\Users\Public\staging`) | Log Analysis |
| **Task 3** | Count files created in 10 minutes (>50 files) | Data Analysis |
| **Task 4** | Correlate with compression tool execution (7z.exe) | Correlation |
| **Task 5** | Detect post-staging exfiltration indicator (large outbound connection) | Network Monitoring |

## 🚀 Quick Start

### Prerequisites
- A modern web browser (Chrome, Firefox, Edge, Safari)
- No server required - runs entirely in the browser
- No installation needed

### Access the Challenge
1. Open the HTML file directly in your browser
2. Enter your name
3. Use the password: `45_2026`
4. Complete all 5 tasks to capture the flag

### Hosting on GitHub Pages
1. Fork or clone this repository
2. Go to repository Settings > Pages
3. Select the branch (usually `main`) and save
4. Access via `https://your-username.github.io/repository-name`

## 🎮 How to Play

### Login
```
Password: 45_2026
Name: Enter any name (progress is saved locally)
```

### Game Features

- **Heatmap Visualization**: Color-coded grid showing file creation intensity
- **Timeline Bar**: Interactive visualization of 62 file creation events
- **Interactive Evidence Display**: Scrollable log entries with highlighted data
- **Answer Validation**: Immediate feedback on submitted answers
- **Progress Tracking**: Local storage saves your progress across sessions
- **Toast Notifications**: Visual feedback for correct/incorrect answers

### Completing Tasks
1. Read each task description carefully
2. Analyze the provided Sysmon logs and visualizations
3. Type your answer in the input field
4. Click "Submit" to validate
5. Receive immediate feedback
6. Complete all 5 tasks to reveal the flag

## 🏆 Flag

```
FLAG{DATA_STAGING_FOUND}
```

The flag is revealed only after completing all 5 tasks successfully.

## 📊 Challenge Details

### Simulated Data Includes

**Sysmon Event 11 Logs (62 File Creation Events):**
```
Event 11: FileCreate | C:\Users\Public\staging\report_Q1.docx
Event 11: FileCreate | C:\Users\Public\staging\customers.db
Event 11: FileCreate | C:\Users\Public\staging\sourcecode.zip
Event 11: FileCreate | C:\Users\Public\staging\finances.xlsx
Event 11: FileCreate | C:\Users\Public\staging\employee_data.csv
Event 11: FileCreate | C:\Users\Public\staging\secrets.txt
Event 11: FileCreate | C:\Users\Public\staging\backup_2025.sql
Event 11: FileCreate | C:\Users\Public\staging\ssh_private.key
Event 11: FileCreate | C:\Users\Public\staging\aws_credentials.csv
... (53 more files)
```

**Compression Tool Execution:**
```
Process Create: "C:\Program Files\7-Zip\7z.exe" a -pSecret123 
C:\Users\Public\staging\archive.7z C:\Users\Public\staging\*
```

**Exfiltrated File Types:**
- Financial records (finances.xlsx, salary_2025.xlsx)
- Customer data (customers.db, employee_data.csv)
- Credentials (aws_credentials.csv, api_keys.txt)
- Source code (sourcecode.zip)
- SSH keys (ssh_private.key)
- Database dumps (db_dump.tar, backup_2025.sql)
- Legal documents (legal_contracts.pdf)
- Security tools (mimikatz.exe, procdump.exe, bloodhound.zip)

## 🔍 Investigation Walkthrough

### Task 1: Hunting Hypothesis
The correct hypothesis is **"data staging"** - attackers copy many sensitive files into a single staging folder before compression and exfiltration. This technique is used to:
- Consolidate stolen data in one location
- Prepare files for archiving
- Minimize the number of exfiltration connections

### Task 2: Identify Staging Folder
The staging folder is `C:\Users\Public\staging`. This location is suspicious because:
- `C:\Users\Public` is accessible to all users
- Creates a centralized collection point
- Less likely to be monitored than user-specific directories

### Task 3: Count File Creations
A total of **62 files** were created in the staging folder within 10 minutes. This high rate (~6.2 files/minute) indicates automated file collection rather than normal user activity.

### Task 4: Compression Correlation
**7z.exe** (7-Zip) was executed with the following suspicious indicators:
- Password protection (`-pSecret123`)
- Archiving entire staging directory
- Timestamp correlates with staging completion

### Task 5: Post-Staging Indicator
After staging and compression, look for **"large outbound connection"** - unusually large data transfers indicating exfiltration of the compressed archive.

## 🎨 Visual Features

- **Heatmap Grid**: 62 cells showing file creation intensity with color gradients
- **Timeline Bar**: Hoverable events showing individual file names
- **Color-coded Logs**: Suspicious entries highlighted with orange borders
- **Progress Indicators**: Visual completion status for each task
- **Pulsing Flag Animation**: Celebratory flag reveal with glow effect
- **Toast Notifications**: Non-intrusive success/error messages
- **Dark Theme**: Orange-accented UI for data staging theme

## 💾 Data Storage

- **Progress**: Saved in browser's `localStorage`
- **Persistence**: Progress survives page refreshes
- **Privacy**: All data stays on the user's device
- **Reset**: Clear browser data to reset progress

## 🛡️ Security Concepts Covered

1. **Sysmon Event 11** (File Creation) monitoring
2. **Data Exfiltration** detection techniques
3. **Threat Hunting** hypothesis development
4. **Log Analysis** and pattern recognition
5. **Timeline Analysis** for incident response
6. **Correlation Analysis** across log sources
7. **Network Traffic** anomaly detection
8. **Compression Tool** abuse detection

## 📁 File Structure

```
hunt-data-staging/
│
├── index.html          # Main CTF challenge file
├── README.md           # This documentation
└── (no other files required)
```

## 🔧 Technical Implementation

- **Pure Frontend**: HTML5, CSS3, JavaScript (Vanilla)
- **No Dependencies**: Zero external libraries
- **Responsive Design**: Works on desktop and mobile
- **Animations**: CSS keyframe animations for heatmap and timeline
- **Storage**: Browser localStorage API
- **Gamification**: Progress tracking, badge system, visual rewards

## 📊 Data Staging Indicators (Detection Guide)

### High-Fidelity Indicators:
- Multiple file creation events in short time window
- Files collected from diverse locations into single folder
- Use of public/shared directories for staging
- Compression tool execution after file collection
- Large outbound network connections

### Medium-Fidelity Indicators:
- Password-protected archives
- Unusual file types being collected (.key, .ovpn, .rdp)
- Security tools appearing in staging folder
- File creation during non-business hours

### Low-Fidelity Indicators:
- Single file type collections
- Small number of files
- Files in user-specific directories

## 🎓 Educational Use Cases

- **Cybersecurity Training Programs**
- **SOC Analyst Onboarding**
- **Threat Hunting Workshops**
- **Blue Team Exercises**
- **Security Awareness Training**
- **Academic Courses** (Network Security, Incident Response)
- **Self-paced Learning**
- **DFIR Training**

## 🔄 Version History

- **v1.0** - Initial release
  - 5 tasks with validation
  - Heatmap and timeline visualizations
  - 62 simulated Sysmon Event 11 logs
  - Local storage progress tracking
  - Student login system

## 👥 Target Audience

- Security Operations Center (SOC) Analysts
- Incident Response Team Members
- Threat Hunters
- Digital Forensics Analysts
- Cybersecurity Students
- IT Security Professionals
- Blue Team Practitioners


---

**Happy Data Hunting! 📊**
