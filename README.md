# mono-repo

A React Native monorepo containing **project1** and **project2** as independent apps under a single repository.

---

## Table of Contents

- [Prerequisites](#prerequisites)
- [Folder Structure](#folder-structure)
- [Step 1 — Create the Monorepo](#step-1--create-the-monorepo)
- [Step 2 — Create project1](#step-2--create-project1)
- [Step 3 — Create project2](#step-3--create-project2)
- [Step 4 — Configure the Monorepo](#step-4--configure-the-monorepo)
- [Step 5 — Push to GitHub](#step-5--push-to-github)
- [Running the Apps](#running-the-apps)

---

## Prerequisites

Make sure the following are installed before you begin:

- [Node.js](https://nodejs.org/) (v18 or later)
- [npm](https://www.npmjs.com/) or [Yarn](https://yarnpkg.com/)
- [React Native CLI](https://reactnative.dev/docs/environment-setup)
- [Git](https://git-scm.com/)
- Xcode (for iOS builds on macOS)
- Android Studio (for Android builds)
- CocoaPods — `sudo gem install cocoapods`

---

## Folder Structure

```
mono-repo/
├── apps/
│   ├── project1/          # React Native app 1
│   └── project2/          # React Native app 2
├── .gitignore
└── README.md
```

---

## Step 1 — Create the Monorepo

### 1.1 Create the root folder and initialize git

```bash
mkdir mono-repo
cd mono-repo
git init
```

### 1.2 Create the apps directory

```bash
mkdir apps
```

### 1.3 Create a root `.gitignore`

```bash
cat > .gitignore <<EOF
node_modules/
.DS_Store
*.log
EOF
```

---

## Step 2 — Create project1

### 2.1 Scaffold the React Native app

```bash
cd apps
npx react-native@latest init project1
```

### 2.2 Install iOS dependencies (macOS only)

```bash
cd project1/ios
pod install
cd ../..
```

---

## Step 3 — Create project2

### 3.1 Scaffold the React Native app

```bash
cd apps
npx react-native@latest init project2
```

### 3.2 Install iOS dependencies (macOS only)

```bash
cd project2/ios
pod install
cd ../..
```

---

## Step 4 — Configure the Monorepo

### 4.1 Verify the folder structure

From the root of `mono-repo`, confirm both apps exist:

```bash
ls apps/
# project1   project2
```

### 4.2 Stage all files from the root

```bash
cd ../../          # back to mono-repo root
git add apps/project1 apps/project2
git status
```

### 4.3 Create the initial commit

```bash
git commit -m "Add project1 and project2 to monorepo"
```

---

## Step 5 — Push to GitHub

### 5.1 Create a new GitHub repository

Go to [github.com/new](https://github.com/new) and create a repository named `mono-repo`. Do **not** initialize it with a README.

### 5.2 Add the remote and push

```bash
git remote add origin https://github.com/<your-username>/mono-repo.git
git branch -M main
git push -u origin main
```

---

## Running the Apps

### Run project1

```bash
cd apps/project1

# Android
npx react-native run-android

# iOS
npx react-native run-ios
```

### Run project2

```bash
cd apps/project2

# Android
npx react-native run-android

# iOS
npx react-native run-ios
```

---

## Notes

- Each app under `apps/` is a fully independent React Native project with its own `package.json`, Android, and iOS configurations.
- Run Metro bundler from within each app's directory, not from the monorepo root.
- If you see port conflicts when running both apps simultaneously, start Metro manually with a custom port:

```bash
npx react-native start --port 8082
```

Then in a separate terminal:

```bash
npx react-native run-android --port 8082
# or
npx react-native run-ios --port 8082
```
