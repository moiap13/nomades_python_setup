# 🐳 Course Dev Environment

Welcome to your course development environment!  
This container gives you a ready-to-use Python workspace identical for macOS, Linux and Windows.

---

## 🚀 Setup Steps

### 1️⃣ Create a GitHub PAT (Personal Access Token)

1. Go to [GitHub → Settings → Developer settings → Tokens (classic)](https://github.com/settings/tokens).
2. Click **Generate new token (classic)** → name it `course-setup`.
3. Check scopes:
   - ✅ `repo`
   - ✅ `admin:public_key`
4. Copy the token — you’ll use it once.

---

### 2️⃣ Download the repository

1. got to [Course GitHub](https://github.com/moiap13/nomades_python_setup).
2. On the right, click the **Code** button.
3. Click **Download ZIP**.
4. Unzip the downloaded archive.

---

### 3️⃣ Prepare .env file

1. Open a terminal in the `nomades_python_setup` directory.
2. Run the following command:
   ```bash
   cp .env.example .env
   ```
3. Edit .env with:
   1. GITHUB_USER → student GitHub username
   2. GITHUB_PAT → personal access token
   3. REPO_NAME → Nomades course version name
   4. Adjust WORKSPACE_PATH and SSH_KEYS_PATH if needed (Windows users).

---

### 4️⃣ Launch the container

1. Open a terminal in the `nomades_python_setup` directory.
2. Run the following command:
   ```bash
   docker compose up -d
   ```
   This will:
    - Generate an SSH key
    - Create the student’s private GitHub repo
    - Upload the SSH key to GitHub
    - Clone the repo into the mounted workspace
    - Mark setup as done (.setup_done in the workspace)

### 5️⃣ Install x11 server for graphics

#### OSX

1. Install brew (if not already installed):
   1. Run the following command in a terminal:
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```
2. Install XQuartz:
   1. Run the following command in a terminal:
   ```bash
   brew install --cask xquartz
   ```
   2. log out and log back in (or reboot once) so XQuartz starts properly.
3. Allow docker access to XQuartz:
   1. Run the following command in a terminal:
   ```bash
   xhost +127.0.0.1
   ```

#### Windows

1. Install [VcXsrv](https://vcxsrv.com/):
   1. Download the installer from the link above, clicking on `Free Download`.
   2. Run the installer and follow the prompts to complete the installation.

2. Start VcXsrv:
   1. Open the Start Menu and search for "VcXsrv".
      > **Know Issue:** If you encounter issues with VcXsrv (screen doesn't start)
      > - Launch `XLaunch` from the Start Menu instead.
      > - Select `multiple windows` and set the `dsiplay number` to `0`.
      > - On extra settings window, check ✅ `Disable access control`.
      > - Finish the setup and relaucnh `VcXsrv` if needed.

3. Allow docker access to VcXsrv:
   1. open powershel terminal and run the following command:
   ```powershell
   xhost +
   ```

#### Linux

1. Make sure you have an X11 server running (most Linux distributions do by default).
2. Allow docker access to X11 server:
   1. Run the following command in a terminal:
   ```bash
   xhost +local:docker
   ```