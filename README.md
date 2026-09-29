<div align="center">

# 🔐 Authentication with Better Auth

**A modern, secure, and type-safe authentication system built with [Better Auth](https://www.better-auth.com).**

Sign up, sign in, manage sessions, and protect routes, all with a clean developer experience.

![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)
![Better Auth](https://img.shields.io/badge/Better_Auth-1A1A1A?style=for-the-badge&logo=auth0&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

[Features](#-features) • [Tech Stack](#-tech-stack) • [Getting Started](#-getting-started) • [Project Structure](#-project-structure) • [Roadmap](#-roadmap) • [Contributing](#-contributing)

</div>

---

## 📖 About the Project

**athentication-betterAuth** is a full-featured authentication project that demonstrates how to add secure user authentication to a modern web application using **Better Auth**, a framework-agnostic, TypeScript-first authentication library.

The goal of this project is to provide a clean, production-minded starting point for:

- Learning how modern authentication works end to end
- Bootstrapping the auth layer of a new application
- Understanding sessions, protected routes, and social login with real code

Unlike hosted providers, all user and session data lives in **your own database**, so you keep full control over your data.

---

## ✨ Features

- 📧 **Email & Password Authentication**: register and log in with secure password hashing
- 🌐 **Social Login (OAuth)**: sign in with providers like Google and GitHub
- 🍪 **Secure Session Management**: cookie-based sessions with server-side validation
- 🛡️ **Protected Routes**: restrict pages and API routes to authenticated users only
- 👤 **User Profile & Dashboard**: view the currently signed-in user's information
- 🔁 **Persistent Login**: stay signed in across page refreshes and browser restarts
- 🚪 **Sign Out**: securely end a session from any device
- ✅ **Form Validation**: client-side and server-side input validation with clear error messages
- 🎨 **Responsive UI**: works smoothly on mobile, tablet, and desktop
- 🧩 **Extensible**: easily add 2FA, magic links, roles, and more via Better Auth plugins

---

## 🛠️ Tech Stack

| Category | Technology |
| --- | --- |
| **Language** | TypeScript |
| **Framework** | Next.js (React) |
| **Authentication** | [Better Auth](https://www.better-auth.com) |
| **Database** | PostgreSQL / MongoDB / SQLite (configurable) |
| **ORM / Adapter** | Prisma or Drizzle |
| **Styling** | Tailwind CSS |
| **Validation** | Zod |
| **Package Manager** | npm / pnpm / yarn |

> 💡 The exact database and ORM depend on your `auth.ts` configuration.

---

## 🚀 Getting Started

### Prerequisites

- **Node.js** v18 or higher
- **Git**
- A running database (local or cloud)
- OAuth credentials (optional, only for social login)

### 1. Clone the repository

```bash
git clone https://github.com/abirhosen30/athentication-betterAuth.git
cd athentication-betterAuth
```

### 2. Install dependencies

```bash
npm install
# or
pnpm install
```

### 3. Configure environment variables

Create a `.env` file in the project root:

```env
# App
BETTER_AUTH_SECRET=your_super_secret_key
BETTER_AUTH_URL=http://localhost:3000

# Database
DATABASE_URL=your_database_connection_string

# Social providers (optional)
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret
GITHUB_CLIENT_ID=your_github_client_id
GITHUB_CLIENT_SECRET=your_github_client_secret
```

> 🔑 Generate a strong secret with: `openssl rand -base64 32`

### 4. Set up the database

```bash
npx @better-auth/cli generate   # generate the auth schema
npx @better-auth/cli migrate    # apply it to your database
```

### 5. Run the development server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser. 🎉

---

## 📁 Project Structure

```
athentication-betterAuth/
├── app/                    # Pages, layouts, and API routes
│   ├── api/auth/[...all]/  # Better Auth API handler
│   ├── sign-in/            # Login page
│   ├── sign-up/            # Registration page
│   └── dashboard/          # Protected page
├── components/             # Reusable UI components
├── lib/
│   ├── auth.ts             # Better Auth server configuration
│   └── auth-client.ts      # Better Auth client instance
├── .env                    # Environment variables (not committed)
├── package.json
└── README.md
```

> 📌 Your folder names may differ slightly; adjust this section to match your repo.

---

## 🔄 How Authentication Works

```
  User ──► Sign up / Sign in form
              │
              ▼
     Better Auth API route  ──►  Validates credentials
              │
              ▼
      Session created & stored in database
              │
              ▼
   Secure cookie sent to browser  ──►  Access to protected routes ✅
```

1. The user submits credentials or chooses a social provider.
2. Better Auth verifies the request and creates a session in the database.
3. A secure, HTTP-only cookie is returned to the browser.
4. Protected pages check the session on the server before rendering.

---

## 💻 Usage Example

**Server configuration (`lib/auth.ts`)**

```ts
import { betterAuth } from "better-auth";

export const auth = betterAuth({
  emailAndPassword: { enabled: true },
  socialProviders: {
    github: {
      clientId: process.env.GITHUB_CLIENT_ID as string,
      clientSecret: process.env.GITHUB_CLIENT_SECRET as string,
    },
  },
});
```

**Client usage**

```ts
import { createAuthClient } from "better-auth/react";

export const authClient = createAuthClient();

// Sign in
await authClient.signIn.email({ email, password });

// Sign out
await authClient.signOut();
```

---

## 🖼️ Screenshots

| Sign In | Sign Up | Dashboard |
| :---: | :---: | :---: |
| _add screenshot_ | _add screenshot_ | _add screenshot_ |

> Put your images in a `/screenshots` folder and link them here, e.g. `![Sign In](./screenshots/sign-in.png)`.

---

## 🗺️ Roadmap

- [x] Email & password authentication
- [x] Social login (OAuth)
- [x] Protected routes
- [ ] Email verification
- [ ] Forgot / reset password
- [ ] Two-factor authentication (2FA)
- [ ] Magic link login
- [ ] Role-based access control (admin / user)
- [ ] Rate limiting and audit logs

---

## 🔒 Security Notes

- Never commit your `.env` file. Add it to `.gitignore`.
- Use a long, random `BETTER_AUTH_SECRET` in production.
- Always serve your app over **HTTPS** in production.
- Rotate OAuth client secrets if they are ever exposed.

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

1. Fork the project
2. Create your feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m "Add amazing feature"`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

---

## 📄 License

This project is licensed under the **MIT License**. See the [LICENSE](./LICENSE) file for details.

---

## 👨‍💻 Author

**Abir Hosen**

- GitHub: [@abirhosen30](https://github.com/abirhosen30)

---

<div align="center">

⭐ If you found this project helpful, please give it a star! ⭐

Made with ❤️ using Better Auth

</div>
