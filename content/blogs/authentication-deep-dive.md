---
title: "Authentication and Authorization in JavaScript"
date: "2025-04-15"
description: "A deep dive into the core concepts of authentication and authorization, with hands-on examples."
tags: ["JavaScript", "Authentication", "Security"]
slug: "authentication-deep-dive"
---

### Introduction

In this series, we’re going to dive deep into Authentication and Authorization in JavaScript, not just the theory, but hands-on implementation as well. Before jumping into code, we’ll go over the core concepts and prerequisites that’ll make your journey smoother.

### What is Authentication?

Think of Authentication as a process that verifies who you are—whether you’re a user or a device—before giving access to protected resources. In simple terms, authentication asks: **Who are you?**

It’s important to note that Authentication is a visible process. This means the client is aware that they’re being authenticated (e.g., through login forms, tokens, or OTPs). Authorization, on the other hand, is handled more silently behind the scenes.

### Authentication Types

1.  **Single-Factor Authentication (SFA)**
    Requires only one credential to verify identity. The most common example is a password-based login. It's simple, but if your password is compromised, you're exposed.

2.  **Two-Factor Authentication (2FA)**
    Requires two layers of verification, usually something you know (a password) and something you have (an OTP sent to your phone or email).

3.  **Multi-Factor Authentication (MFA)**
    Requires two or more verification factors from different categories:
    * **Something you know:** Password, PIN
    * **Something you have:** Smartphone, Authenticator app, Security token
    * **Something you are:** Fingerprint, Face recognition

4.  **Biometric Authentication**
    Uses biological characteristics for identity verification, such as fingerprint scanning, facial recognition, or an iris scan.

### Why is Authentication Needed?

Authentication ensures that only authorized users can access sensitive data or features. If you're not authenticated, your access will be restricted to public areas of the application, which helps prevent security vulnerabilities.

### How is it Implemented?

Before we jump into implementing authentication, it’s important to understand a key building block of most backend frameworks: **middleware**.

#### Middleware

You can think of middleware as a gatekeeper—it intercepts requests, runs logic like validation, and then either blocks or allows the request to continue. While you could do manual checks in your API endpoint routes, middleware provides a cleaner and more modular way to handle these concerns.

Here’s a basic example in Express:

```javascript
const express = require("express");
const app = express();

// Built-in middleware to parse JSON
app.use(express.json());

// Custom middleware
const sampleMiddleware1 = (req, res, next) => {
  req.number = 5;
  next(); // Pass control to the next middleware or route
};

app.get("/", sampleMiddleware1, (req, res) => {
  res.send(`Hello from root\nFinal Request Number is: ${req.number}`);
});

app.listen(8001, () => {
  console.log(`Server running on port 8001`);
});
