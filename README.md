# penetration-testing-report
<img width="369" height="292" alt="3" src="https://github.com/user-attachments/assets/6e4efc15-4533-4a88-ae7c-7fe68d271f4f" />

## 1. Liability Disclaimer

This report has been prepared for educational and training purposes only, as part of cybersecurity learning activities. The information it contains is based on publicly available sources and on tools used within an authorized and controlled scope. The author does not encourage, condone or accept responsibility for any unauthorized access, misuse, or illegal activity carried out using the techniques, tools or information described here.

The findings reflect the state of the identified resources at the time of the exercise and may have since changed. The author accepts no liability for any loss, damage or disruption arising from the use of, or reliance on, the contents of this report. Readers must obtain proper written authorization before performing any security testing on systems they do not own.

## 2. Introduction

Footprinting and reconnaissance are the first phases of a penetration test. They involve collecting as much information as possible about a target, its systems and its exposed services, before any active testing begins. This information helps a tester, and equally an attacker, understand what is exposed on the internet and where weaknesses are likely to be found.

The objective of this exercise was to demonstrate how publicly indexed information can be discovered using search engine queries (Google dorks) from the Google Hacking Database (GHDB), and how network scanning with Zenmap can then be used to map hosts, open ports and running services. Two sets of results were documented: Table 1, a list of internet-facing webcam interfaces, and Table 2, a list of publicly accessible open directories. Both are attached in Section 8.

## 3. Tools Used

**Google Hacking Database (GHDB).** A public, categorized collection of search queries known as Google dorks, maintained as part of Exploit-DB. Dorks use advanced search operators such as `intitle:`, `inurl:` and `allintitle:` to surface pages, devices and files that were unintentionally exposed and indexed by search engines.

**Zenmap.** The official graphical interface for Nmap, an open-source network scanner. Zenmap was used to run scans using preset profiles, and to view discovered hosts, open ports, services and network topology in an organized way.

---

## 4. Activities Performed

### 4.1 Footprinting and Reconnaissance

Passive information gathering was carried out using GHDB-style Google dorks. Two categories of queries were used:

- **Exposed webcam interfaces (Table 1):** queries such as `intitle:"webcamXP" inurl:8080` and `intitle:"NetCamSC*"` returned the web interfaces of network cameras and camera-server software. Ten results were recorded together with the dork that found each one.
- **Open directories (Table 2):** the query `intitle:index.of "parent directory" mathematics pdf` returned ten servers with directory listing enabled, exposing folders of mathematics PDF files.

For each result the link, the relevant dork and any username or password required were recorded. Only information visible through public search results was collected during this phase.

### 4.2 Network Scanning with Zenmap

Zenmap was used to perform network scanning in order to identify live hosts, open ports, service versions and operating systems. The scan profiles applied were:

- **Ping scan:** to discover which hosts are online.
- **Quick scan:** to identify the most common open ports rapidly.
- **Intense scan:** to detect service versions, operating systems and run basic scripts.

## 5. Risk Analysis / Impact

The exposures identified were assessed by likelihood and potential impact. The ratings below are qualitative and based on the type of exposure.

| Finding | Risk | Potential Impact |
|---|---|---|
| Internet-facing webcam interfaces (Table 1) | High | Unauthorized viewing of live feeds, loss of privacy, physical security exposure, and use of the device as an entry point into the internal network, especially where default or no credentials are used. |
| Open directory listings (Table 2) | Medium | Disclosure of files and folder structure not meant to be public. Directories can expose sensitive documents, backups or configuration files; in this case the content seen was mathematics PDFs, so the impact was lower. |
| Search engine indexing of sensitive pages | Medium | Makes reconnaissance fast and free for attackers, who can find vulnerable targets at scale without touching the target. |
| Exposed ports and services (Zenmap) | Varies | Open ports with outdated or misconfigured services give attackers a path to exploitation, and reveal software versions. |

## 6. Recommendations

- Change all default credentials on cameras and network devices, and enforce strong, unique passwords.
- Do not expose camera interfaces directly to the internet. Place them behind a firewall or VPN, and block unneeded ports such as 8080.
- Keep firmware and software (for example webcam server applications) updated, and retire unsupported devices.
- Disable directory listing on web servers (for example `Options -Indexes` in Apache) and add index pages.
- Use robots.txt, noindex tags and authentication to keep private pages out of search results, and request removal of already indexed content.
- Segment the network so that cameras and IoT devices are isolated from critical systems.
- Regularly run GHDB dorks and Nmap/Zenmap scans against your own assets, with authorization, to find exposures before attackers do.
- Monitor logs and alerts for unusual access to exposed services, and train staff on secure device deployment.

## 7. Conclusion

This exercise showed how much information can be gathered about a target using only publicly available tools. Google dorks from the GHDB quickly revealed exposed webcam interfaces and open directories, and Zenmap provides the means to map hosts and services in the next step. None of this requires advanced skill, which is why such exposures are a real risk.

The main lesson is that organizations should know what they expose to the internet. Strong credentials, restricted access, disabled directory listing, timely updates and regular self-assessment greatly reduce the chance of these weaknesses being found and abused. Footprinting and reconnaissance are therefore valuable for defenders as well as attackers.

---

## 8. Attachment

### Table 1: Exposed webcam interfaces and relevant dorks

| No. | Link | Relevant Dork | Username / Password (if any) |
|:---:|---|---|:---:|
| 1 | http://109.233.191.130 | `intitle:"webcamXP" inurl:8080` | --- |
| 2 | http://75.147.91.5 | `intitle:"NetCamSC*"` | --- |
| 3 | http://99.114.240.169 | `intitle:"Webcam" inurl:WebCam.htm` | --- |
| 4 | http://72.199.200 | `intitle:"webcamXP" inurl:8080` | --- |
| 5 | http://109.233.191.130 | Multi view - webcamXP 5 | --- |
| 6 | http://139.64.168.120 | webcamXP 5 | --- |
| 7 | http://75.149.26.30 | webcamXP 5 | --- |
| 8 | http://85.93.53.1 | webcams and ip cameras server for windows - web | --- |
| 9 | http://80.152.138.183 | `allintitle: "Network Camera NetworkCamera" Netw` | --- |
| 10 | http://75.147.91. | `intitle:"NetCamSC*"` | --- |

### Table 2: Open directories and relevant dorks

| No. | Link | Relevant Dork | Username / Password (if any) |
|:---:|---|---|:---:|
| 1 | http://www.wvfa.org › pdf › projectLearningTree | `intitle:index.of "parent directory" mathematics pdf` | --- |
| 2 | https://case.edu › artsci › math › singer › publish | `intitle:index.of "parent directory" mathematics pdf` | |
| 3 | https://www.ellerman.org › Davids-Stuff › Maths | `intitle:index.of "parent directory" mathematics pdf` | |
| 4 | https://netlib.org › math › docpdf | `intitle:index.of "parent directory" mathematics pdf` | |
| 5 | https://ochicken.net › library › Mathematics | `intitle:index.of "parent directory" mathematics pdf` | |
| 6 | http://erewhon.superkuh.com › library › Math | `intitle:index.of "parent directory" mathematics pdf` | |
| 7 | http://www.unm.edu › ~megrad › Math | `intitle:index.of "parent directory" mathematics pdf` | |
| 8 | https://education.giakonda.org.uk › Maths | `intitle:index.of "parent directory" mathematics pdf` | |
| 9 | https://www.math.dartmouth.edu › ~carlp › PDF | `intitle:index.of "parent directory" mathematics pdf` | |
| 10 | http://pcwww.liv.ac.uk › maths | `intitle:index.of "parent directory" mathematics pdf` | |

### Figure 1: Zenmap Topology

<img width="465" height="320" alt="99" src="https://github.com/user-attachments/assets/80733bab-b367-4dbb-b6ab-dff2e635741d" />


*Figure 1: Zenmap topology view of the scanned network, with the host IP addresses covered. The scanning host (localhost) connects to four discovered hosts.*

---


 
�� Author

David Idiong

Cybersecurity Professional B082

LinkedIn: https://www.linkedin.com/in/david-idiong-71476a326/



�� Project Information

Program Name: Cybersecurity program at Networkwalks | Week: 02 | Repository: GitHub
