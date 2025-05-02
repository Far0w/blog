

---
title: Create a Blog from Obsidian Markdown
date: 2025-05-02T02:01:58+02:00
draft: false
description: "You wanted to know how to create a blog from an obsidian markdown, here we go!"
tags: [tag1, tag2]
featured_image: "![Image Description](/images/img1.png)"
categories: Todo
comment : false
hidden: false

---
![Image Description](/images/Pasted%20image%2020250502190016.png)



## 📌 Overview

You’ll write posts in **Obsidian**, transform them into a website using **Hugo**, manage the site on **GitHub**, and host it with **Hostinger**, using a **Python script** and optional **PowerShell/Bash script** for automation.

Inspired from: https://blog.networkchuck.com/posts/my-insane-blog-pipeline/

---

## ✅ Prerequisites

1. **Install Obsidian** – [https://obsidian.md/](https://obsidian.md/)
    
2. **Install Git** – [https://git-scm.com/](https://git-scm.com/)
    
3. **Install Go (Golang)** – [https://go.dev/dl/](https://go.dev/dl/)
    
4. **Install Hugo** – [https://gohugo.io/getting-started/installing/](https://gohugo.io/getting-started/installing/)
    
5. **Install Python 3**
    

---

## 📂 Step 1: Prepare Obsidian

- Create a folder `post/` in your vault.
    
- Write each blog post in markdown inside this folder.
    
- Use **YAML front matter** at the top of each note:
    

```markdown
---
title: "My Blog Title"
date: 2024-05-02
tags: ["blog", "obsidian"]
---
```

---

## 🌐 Step 2: Set Up Hugo

1. Open terminal and run:
    

```bash
hugo new site my-blog
cd my-blog
```

2. Initialize Git:
    

```bash
git init
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

3. Add a Hugo theme (example: terminal):
    

```bash
git submodule add https://github.com/panr/hugo-theme-terminal.git themes/terminal
```

4. Update `config.toml` with theme config:
    

```toml
baseURL = "https://example.com/"
languageCode = "en-us"
title = "My Blog"
theme = "terminal"
```

5. Create folder structure:
    

```bash
mkdir -p content/post
mkdir -p static/images
```

---

## 🔁 Step 3: Sync Obsidian Posts and Images

### Windows:

Use `robocopy`:

```powershell
robocopy "C:\path\to\obsidian\post" "C:\path\to\hugo\content\post" /MIR
```

### Mac/Linux:

Use `rsync`:

```bash
rsync -av --delete ~/path/to/obsidian/post/ ~/path/to/hugo/content/post/
```

### Copy images with Python:

Use a script to:

- Parse markdown files.
    
- Copy image files from Obsidian's `attachments` to Hugo’s `static/images`.
    
- Adjust markdown links.
    

---

## 🔧 Step 4: Build and Test Hugo Site

```bash
hugo server -t terminal
```

Open `http://localhost:1313` to preview.

---

## ☁️ Step 5: Push to GitHub

1. Create GitHub repo.
    
2. Add remote:
    

```bash
git remote add origin git@github.com:yourusername/my-blog.git
```

3. Build site:
    

```bash
hugo
```

4. Push full code:
    

```bash
git add .
git commit -m "Initial commit"
git push -u origin master
```

---

## 🌍 Step 6: Create Hosting on Hostinger

1. Add a new website (choose "Empty PHP/HTML site").
    
2. Set custom domain or use temporary domain.
    
3. (If using custom domain via Cloudflare): Add A record pointing to Hostinger IP.
    

---

## 🔗 Step 7: Deploy via GitHub

1. In Hostinger → Git integration:
    
    - Generate SSH key and add it to GitHub.
        
    - Use repo URL: `git@github.com:yourusername/my-blog.git`
        
    - Use branch: `hostinger`
        
2. Push only `public/` folder to `hostinger` branch:
    

```bash
git subtree push --prefix=public origin hostinger
```

---

## 🔁 Step 8: Enable Auto Deployment

1. In Hostinger → Enable Webhook.
    
2. In GitHub → Add Webhook:
    
    - Paste the webhook URL from Hostinger.
        
    - Enable `push` events.
        

---

## 🧠 Step 9: Automate Everything

Create a **PowerShell** or **bash** script to:

- Sync markdown files
    
- Copy images
    
- Rebuild Hugo
    
- Commit and push to GitHub
    
- Push `public/` to `hostinger` branch
    

Example for PowerShell:

```powershell
# Set your paths
$obsidian = "C:\path\to\obsidian\post"
$hugo = "C:\path\to\hugo\content\post"
$imagesScript = "images.py"

# Run sync
robocopy $obsidian $hugo /MIR
python $imagesScript

# Build and push
hugo
git add .
git commit -m "Update"
git push origin master
git subtree push --prefix=public origin hostinger
```

---

## ✅ Summary: Workflow

1. Write post in Obsidian.
    
2. Run automation script.
    
3. Website updates via GitHub and Hostinger.
    

---

Would you like me to generate a ready-to-use PowerShell or Bash script for your setup?