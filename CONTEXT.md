# 📖 CONTEXT.md — Nakorg AI Specification

## 🎯 Project Overview
**Nakorg AI** is an AI-powered chat application built using **Java (Spring Boot)** for backend and **MySQL** for persistent storage.  
The application provides access to **6 AI models** through OpenRouter API integration and is designed with a **light pastel theme** and **smooth rounded UI elements**.

---

## 💳 Plans & Credits

- **Free Plan**
  - 10 daily credits
  - 1 chat = 1 credit
  - Locked with a prompt once credits are exhausted  

- **Pro Plan**
  - ₹199 lifetime
  - Unlimited credits  

---

## 🎨 UI/Interface (Light Mode Pastel Theme)

- **Navbar**
  - Pastel background
  - Logo left
  - Login/Logout top right  

- **Hero Section**
  - Title: *“nakorg AI - Unlock 6 AI Models Today”*
  - Buttons: Rounded pastel buttons — *Start Chatting* / *Upgrade to Pro*  

- **Chat Page**
  - **Sidebar**
    - Rounded cards for AI models (6 total)
    - “New Chat” button at top
    - History section below
  - **Main Chat**
    - Responses stacked vertically in **soft pastel cards with shadows**
    - Input box at bottom with pastel accents
  - **Demo Video Placeholder**
    - Pastel bordered container  

- **Upgrade Page**
  - Rounded pastel card
  - Button: *“Upgrade Now”*  

---

## 🔌 API Integration
- **Provider:** [OpenRouter API](https://openrouter.ai/)  
- **Usage:** Proxy user queries → AI Model → Return response in stacked chat UI  
- **Implementation:** REST client inside Spring Boot service layer  

---

## 🗄 Database Schema (MySQL)

```sql
-- Users Table
CREATE TABLE users (
  id BIGINT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100),
  email VARCHAR(150) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  plan ENUM('FREE', 'PRO') DEFAULT 'FREE',
  daily_credits INT DEFAULT 10,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Chats Table
CREATE TABLE chats (
  id BIGINT AUTO_INCREMENT PRIMARY KEY,
  user_id BIGINT NOT NULL,
  model VARCHAR(100) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);

-- Messages Table
CREATE TABLE messages (
  id BIGINT AUTO_INCREMENT PRIMARY KEY,
  chat_id BIGINT NOT NULL,
  sender ENUM('USER', 'AI') NOT NULL,
  content TEXT NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (chat_id) REFERENCES chats(id) ON DELETE CASCADE
);

-- Transactions Table (for Pro plan purchase)
CREATE TABLE transactions (
  id BIGINT AUTO_INCREMENT PRIMARY KEY,
  user_id BIGINT NOT NULL,
  amount DECIMAL(10,2) NOT NULL,
  currency VARCHAR(10) DEFAULT 'INR',
  status ENUM('SUCCESS', 'FAILED') DEFAULT 'SUCCESS',
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

---

## 📂 Optimal Folder Structure (Java + Spring Boot + MySQL)

```
nakorg-ai/
│── backend/
│   ├── src/main/java/com/nakorgai/
│   │   ├── controller/      # REST controllers
│   │   ├── service/         # Business logic
│   │   ├── model/           # JPA entities
│   │   ├── repository/      # Spring Data JPA repositories
│   │   ├── config/          # Security, API, DB config
│   │   └── NakorgAiApp.java # Main Spring Boot app
│   ├── src/main/resources/
│   │   ├── application.properties  # DB + API configs
│   │   └── static/ & templates/    # (if Thymeleaf used)
│   └── pom.xml              # Maven dependencies
│
│── frontend/ (optional React/Vanilla if separate UI)
│   ├── public/
│   ├── src/
│   │   ├── components/      # Navbar, Hero, ChatUI, UpgradeCard
│   │   ├── pages/           # ChatPage, UpgradePage, LoginPage
│   │   └── App.jsx
│   └── package.json
│
│── docs/
│   └── CONTEXT.md
│
└── README.md
```

---

## ✅ Key Features
- Free vs Pro Plan with credit tracking  
- Secure authentication (Spring Security + JWT)  
- AI chat integration with OpenRouter  
- MySQL persistence for users, chats, and messages  
- Smooth pastel UI (frontend optional with React/Vanilla JS)  
