# AutoSOC: Autonomous Cyber Threat Detection, Investigation and Response Framework

## Project Overview

এই project-এর লক্ষ্য হলো একটি AutoSOC prototype তৈরি করা, যেখানে cyber
attack শুধু detect করা নয়, বরং related attack events analyse করে একটি
complete incident হিসেবে বোঝানো হবে।

## Sir-এর Requirement

স্যার চেয়েছেন:

1.  Cybersecurity dataset ব্যবহার করতে হবে।
2.  Attack detect করতে হবে।
3.  Multiple attack event correlate করতে হবে।
4.  Related attack-কে একটি campaign হিসেবে identify করতে হবে।
5.  Risk analysis করতে হবে।
6.  Incident summary এবং response recommendation দিতে হবে।

## Overall Flow

    TON_IoT Dataset
            |
            ↓
    Threat Detection (ML)
            |
            ↓
    Ground Truth Verification
            |
            ↓
    Attack Correlation
            |
            ↓
    Multi-stage Attack Campaign Detection
            |
            ↓
    Risk Scoring
            |
            ↓
    MITRE ATT&CK Mapping
            |
            ↓
    Incident Investigation
            |
            ↓
    Response Recommendation

## Dataset Used

### train_test_network.csv

ব্যবহার: Machine Learning threat detection।

Model: Random Forest

Detect করেছে:

-   Normal
-   Scanning
-   DDoS
-   DoS
-   Password
-   XSS
-   Backdoor
-   Ransomware
-   MITM
-   Injection

Result:

    Accuracy = 98.86%

------------------------------------------------------------------------

### GroundTruth Network Dataset

Used files:

-   GroundTruth_Network_1.csv
-   GroundTruth_Network_9.csv
-   GroundTruth_Network_16.csv
-   GroundTruth_Network_18.csv

Purpose:

Attack event verify এবং correlation।

Used information:

-   Timestamp
-   Source IP
-   Destination IP
-   Port
-   Protocol
-   Attack type

------------------------------------------------------------------------

# Implementation Details

## 1. Threat Detection

Problem:

Network traffic attack কিনা এবং কোন ধরনের attack তা detect করা।

Solution:

Random Forest model ব্যবহার করা হয়েছে।

Input:

Network features:

-   Ports
-   Duration
-   Bytes
-   Packets

Output:

Attack class prediction।

------------------------------------------------------------------------

## 2. Ground Truth Verification

Predicted attack event এবং ground truth event match করা হয়েছে:

-   Timestamp
-   Source IP
-   Destination IP
-   Port
-   Protocol

এর মাধ্যমে।

------------------------------------------------------------------------

## 3. Attack Correlation

একই attacker-এর related alert একসাথে করা হয়েছে।

Example:

Before:

    Alert 1: Password attack
    Alert 2: XSS attack

After:

    Password
        ↓
    XSS

    One Attack Campaign

Criteria:

-   Same source IP
-   Similar time period

------------------------------------------------------------------------

## 4. Multi-stage Attack Detection

System different attack stage identify করেছে।

Example:

    Source IP: 192.168.1.32

    Password
        ↓
    XSS

    Attack stages: 2

আরেকটি:

    Ransomware
        ↓
    Backdoor

------------------------------------------------------------------------

## 5. Risk Scoring

Risk calculate করা হয়েছে:

-   Attack severity
-   Total events
-   Target count
-   Number of attack stages

Example:

    Risk Score: 92.39
    Risk Level: CRITICAL

------------------------------------------------------------------------

## 6. Threat Intelligence

MITRE ATT&CK mapping:

Example:

    Password Attack
    ↓
    T1110 - Brute Force

    DDoS
    ↓
    T1498 - Network Denial of Service

    Ransomware
    ↓
    T1486 - Data Encrypted for Impact

------------------------------------------------------------------------

## 7. Incident Investigation

Automatic summary তৈরি হয়েছে।

Example:

    Source IP performed password → XSS attack chain.

    Risk:
    Critical

------------------------------------------------------------------------

## 8. Response Recommendation

Example:

Critical incident হলে:

    - Investigate source IP
    - Isolate affected systems
    - Preserve logs
    - Block malicious activity

------------------------------------------------------------------------

# Final Output

Report contains:

  Field              Meaning
  ------------------ -----------------------
  Source IP          Attacker source
  Attack Sequence    Attack chain
  Attack Stages      Number of stages
  Risk Score         Severity
  MITRE Technique    Threat intelligence
  Incident Summary   Human readable report
  Response           Recommended action

------------------------------------------------------------------------

# Final Achievement

Implemented:

✅ ML based threat detection\
✅ Multi-class attack classification\
✅ Ground truth verification\
✅ Attack correlation\
✅ Multi-stage attack detection\
✅ Risk scoring\
✅ MITRE mapping\
✅ Incident summary\
✅ Response recommendation

------------------------------------------------------------------------

## Supervisor Explanation

"আমি TON_IoT dataset ব্যবহার করে AutoSOC prototype তৈরি করেছি। প্রথমে
Random Forest দিয়ে network traffic থেকে attack type detect করেছি। এরপর
GroundTruth ব্যবহার করে attack verify করেছি। একই attacker-এর related
events IP এবং time অনুযায়ী correlate করে attack campaign তৈরি করেছি। শেষে
risk score, MITRE mapping, incident summary এবং response recommendation
generate করেছি।"
