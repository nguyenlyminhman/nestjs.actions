# 🚀 NestJS Actions – CI/CD with GitHub Actions

A simple yet practical boilerplate demonstrating how to integrate **NestJS** with **GitHub Actions** to build, test, and deploy applications automatically.

---

## 📌 Overview

This project showcases how to implement a complete **CI/CD pipeline** for a NestJS application using GitHub Actions.

With every push or pull request, the system can:

- 📦 Install dependencies
- 🏗️ Build the application
- 🧪 Run tests (unit / e2e)
- 🎨 Lint & format code
- 🚀 Deploy (optional)

---

## 🧱 Tech Stack

- **Backend**: NestJS (TypeScript)
- **CI/CD**: GitHub Actions
- **Runtime**: Node.js
- **Testing**: Jest (default của NestJS)

---

## 📂 Project Structure

```
nestjs.actions/
├── .github/
│   └── workflows/
│       └── ci.yml        # GitHub Actions workflow
├── src/
│   ├── app.controller.ts
│   ├── app.service.ts
│   └── main.ts
├── test/                 # e2e tests
├── package.json
├── tsconfig.json
└── README.md
```

---

## ⚙️ CI/CD Workflow

File chính:

```
.github/workflows/ci.yml
```

### 🔄 Flow hoạt động

```
Push / Pull Request
        ↓
   Checkout code
        ↓
   Setup Node.js
        ↓
Install dependencies
        ↓
       Lint
        ↓
       Test
        ↓
      Build
        ↓
 Deploy (optional)
```

### 📌 Example workflow

```yaml
name: Deploy NestJS - Enterprise Standard

on:
  push:
    branches: [ "main" ]
  pull_request:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 18

      - name: Install dependencies
        run: npm install

      - name: Lint
        run: npm run lint

      - name: Run tests
        run: npm run test

      - name: Build
        run: npm run build
```

---

## 🧪 Running Locally

```bash
# install dependencies
npm install

# run app
npm run start:dev

# run test
npm run test

# build
npm run build
```

---

## 🚀 Deployment (Optional)

You can extend the workflow to deploy using:

- 🐳 Docker → push to registry
- ☁️ Cloud (AWS, GCP, etc.)
- 🔁 SSH deploy

Example SSH deployment:

```yaml
- name: Deploy
  uses: appleboy/ssh-action@master
  with:
    host: ${{ secrets.HOST }}
    username: ${{ secrets.USER }}
    key: ${{ secrets.SSH_KEY }}
    script: |
      cd /app
      git pull
      npm install
      pm2 restart app
```

---

## 🔐 Secrets Management

Use GitHub Secrets:

- HOST
- USER
- SSH_KEY

⚠️ Do not hardcode credentials in your repository.

---

## 💡 Best Practices

- ✅ Protect branch `main` (require PR + CI pass)
- ✅ Run test on every PR
- ✅ Keep workflow fast (use cache if needed)
- ✅ Separate jobs: build, test, deploy
- ✅ Use matrix build for multiple Node versions

---

## 📈 Why this project?

- 📚 Learn CI/CD with NestJS
- 🧩 Easy to integrate into microservices
- 🧪 Standardize testing & build process
- 🚀 Ready for production scaling

---

## 📌 Future Improvements

- [ ] Add Docker build & push
- [ ] Add staging & production environments
- [ ] Add Slack/Discord notifications
- [ ] Add code coverage report
- [ ] Add caching for faster CI

---

## 🤝 Contributing

Pull requests are welcome!  
Feel free to open issues or suggest improvements.

---

## 📄 License

MIT
