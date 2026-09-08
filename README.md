# KanakkuKural (கணக்குக் குரல்) — Voice-First AI Cash Flow Assistant for Small Merchants

> **"Speak your entries. See your next move."**  
> 100% On-device, phone-first AI assistant for small Indian merchants converting supplier bills and spoken entries into a 7-day cash-flow plan (Pay, Collect, Wait).

---

## 🌟 Overview & Key Value Proposition

Small neighborhood shopkeepers (kirana stores, tea stalls, local trade merchants) in India struggle with cash flow visibility. Paper ledgers and manual notebooks don't calculate upcoming 7-day liquidity or prioritize which bills to pay versus which customer dues to collect.

**KanakkuKural (கணக்குக் குரல்)** solves this by acting as an offline, voice-enabled cash flow engine:
- **Voice-First Input**: Speak transactions naturally in English or Tamil.
- **On-Device OCR**: Instant camera scanning of supplier invoice paper receipts.
- **Actionable 7-Day Guidance**: Categorizes actions into **PAY**, **COLLECT**, or **WAIT** based on predicted cash flow safety.
- **100% Offline & Private**: Zero server dependency—all records and calculations remain strictly local on the merchant's phone.

---

## ⏱️ 90-Second Hackathon Demo Flow

Follow this step-by-step walkthrough for a live demonstration:

1. **Load Sample Merchant Context**
   - Open app and select **Lakshmi Stores** sample profile to populate realistic starting cash balance and customer/supplier ledger.
2. **Scan Supplier Bill (OCR)**
   - Tap **Scan Bill** button ➔ Point camera at **Amma Foods** bill ➔ Google ML Kit extracts total amount, supplier name, and due date automatically with optional manual override fallback.
3. **Voice Entry Transaction**
   - Tap the **Voice Input** FAB ➔ Speak *"Ravi paid 450 by UPI"* ➔ SpeechRecognizer & `SpeechParser` extract Customer Name (`Ravi`), Amount (`450`), Payment Mode (`UPI`), and update ledger instantly.
4. **Open Copilot Dashboard**
   - Navigate to **AI Copilot** tab ➔ View **Safe to Spend** top banner calculating real-time available buffer.
5. **Select Bill & View Recommendation**
   - Tap the scanned **Amma Foods** bill ➔ Copilot analyzes upcoming cash inflow vs outflow and recommends action (**PAY**, **COLLECT**, or **WAIT**).
6. **Draft Customer Payment Reminder**
   - Copilot identifies overdue customer dues (e.g., *Suresh*) and generates a pre-formatted WhatsApp/SMS draft reminder in Tamil or English with single-tap copy/share.

---

## 🏗️ App Architecture & Tech Stack

```
   ┌─────────────────────────────────────────────────────────┐
   │                     UI Layer                            │
   │      Jetpack Compose + Material 3 + ViewModels           │
   └──────────────────────────┬──────────────────────────────┘
                              │
   ┌──────────────────────────┴──────────────────────────────┐
   │                    Engine / Domain                      │
   │  SpeechParser (Regex NLP) │ 7-Day CashFlow Engine       │
   │  LocalAiService Interface │ OCR Receipt Extractor       │
   └──────────────────────────┬──────────────────────────────┘
                              │
   ┌──────────────────────────┴──────────────────────────────┐
   │                    Data & Infrastructure                │
   │  Room DB (SQLite) │ CameraX + ML Kit Text Recognition  │
   │  Android SpeechRecognizer (Offline/On-Device)           │
   └─────────────────────────────────────────────────────────┘
```

- **Language & UI**: Kotlin, Jetpack Compose, Material 3, MVVM Architecture
- **Local Persistence**: Room Database for 100% offline data persistence
- **On-Device OCR**: CameraX + Google ML Kit Text Recognition
- **Voice Parsing**: Android `SpeechRecognizer` + custom `SpeechParser` local regex NLP parser
- **Localization**: Dual Language Support (English & Tamil)

---

## 🎨 Color System & Key Features

### Color Palette

| Token Name | Hex Code | Visual Sample | Purpose / Usage |
| :--- | :--- | :---: | :--- |
| **Dark Navy** | `#07152E` | `████` | Primary App Background, Top Headers |
| **Secondary Navy** | `#0D2450` | `████` | Card Containers, Ledger Cards |
| **Saffron** | `#F2A93B` | `████` | Primary Accent, Highlights, Action Badges |
| **Mint** | `#60D9C6` | `████` | Safe-to-Spend Status, Cash Inflows |
| **Cream** | `#F7F3EC` | `████` | High-Contrast Typography & Surface Elements |
| **Muted Red** | `#D9534F` | `████` | Urgent Dues, Outflow Warnings |

### Key Features
- **Safe to Spend Banner**: High-visibility banner displaying usable balance after reserving funds for upcoming 7-day mandatory supplier payments.
- **7-Day Cash Flow Projection Engine**: Dynamic liquidity model that projects daily cash balances over the next week based on expected collections and supplier deadlines.
- **Bill Scanner Fallback**: Camera OCR receipt reader backed by editable input fields to handle wrinkled or partially legible bills smoothly.
- **Draft Reminders**: One-tap payment reminder templates in Tamil and English ready to share via WhatsApp/SMS to collect customer dues.

---

## 🛠️ Project Setup & Build Steps

### Prerequisites
- **Android Studio**: Android Studio Ladybug (2024.2.1) or newer
- **JDK**: Java 17
- **Minimum SDK**: API Level 26 (Android 8.0 Oreo)
- **Target SDK**: API Level 34/35

### Build Commands

```bash
# Clone repository
git clone https://github.com/your-repo/KanakkuKural.git
cd KanakkuKural

# Build Debug APK
./gradlew assembleDebug

# Run Unit Tests
./gradlew test
```

---

## 🚀 Limitations & Future Scope

- **Expanded Tamil NLP**: Extending `SpeechParser` regex and phonetic pattern matching to support regional spoken Tamil dialects and colloquial Tanglish phrases.
- **On-Device LLM Integration**: Clean architectural interface (`LocalAiService`) designed to easily integrate on-device open-source LLMs (such as Gemma or Llama via MediaPipe LLM Inference API) as hardware capabilities evolve.

---

## 🔒 Privacy Disclaimer

> **KanakkuKural tracks and plans payments. It does not access bank accounts, payment gateways, credit scoring, or initiate transactions. All records stay 100% on this device.**
