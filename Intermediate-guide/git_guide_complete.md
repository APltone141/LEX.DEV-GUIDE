# 📚 Panduan Lengkap Git & GitHub - LEX DEV

> **Panduan Praktis untuk Developer Pemula hingga Expert**
> 
> Semua yang perlu Anda ketahui tentang Git & GitHub dalam format yang mudah dipahami.

---

## 📖 Daftar Isi

1. [🔧 Git Dasar - Kontrol Versi Lokal](#-git-dasar---kontrol-versi-lokal)
2. [🌐 GitHub & Kolaborasi Remote](#-github--kolaborasi-remote)
3. [🌿 Strategi Branching](#-strategi-branching)
4. [🔁 Manajemen Commit & History](#-manajemen-commit--history)
5. [👁️ Best Practices Code Review](#️-best-practices-code-review)
6. [🧠 Studi Kasus & Problem Solving](#-studi-kasus--problem-solving)
7. [📌 Tips Penting & Kebiasaan Baik](#-tips-penting--kebiasaan-baik)
8. [🔒 Security & Advanced Topics](#-security--advanced-topics)
9. [🚀 CI/CD Integration](#-cicd-integration)
10. [📱 Mobile & Cross-Platform Development](#-mobile--cross-platform-development)

---

## 🔧 Git Dasar - Kontrol Versi Lokal

### Apa itu Git?

Git adalah sistem untuk melacak perubahan kode Anda. Bayangkan seperti "Save Game" di video game - Anda bisa kembali ke versi sebelumnya kapan saja.

### Konsep Dasar (Mudah Dipahami)

```
📁 Folder Kerja  →  📋 Area Siap  →  📦 Penyimpanan Lokal  →  ☁️ GitHub
   (edit file)      (git add)        (git commit)           (git push)
```

- **Folder Kerja**: Tempat Anda edit file
- **Area Siap**: File yang siap disimpan
- **Penyimpanan Lokal**: History perubahan di komputer
- **GitHub**: Backup online + kolaborasi

### Command Dasar (Copy-Paste Ready)

#### 🚀 Memulai Project

```bash
# Buat project baru
git init my-project
cd my-project

# Clone project yang sudah ada
git clone https://github.com/username/project.git
```

#### 📝 Simpan Perubahan

```bash
# Lihat status file
git status

# Siapkan file untuk disimpan
git add filename.js          # File tertentu
git add .                    # Semua file

# Simpan perubahan dengan pesan
git commit -m "Tambah fitur login"

# Cara cepat (file yang sudah pernah di-add)
git commit -am "Perbaiki bug login"
```

#### 👀 Lihat History

```bash
# Lihat riwayat perubahan
git log --oneline           # Ringkas
git log --graph             # Visual

# Lihat perubahan yang belum disimpan
git diff                    # Perubahan di folder kerja
git diff --staged           # Perubahan di area siap
```

### 🆘 Mengatasi Kesalahan (Untuk Pemula)

#### Undo Terakhir (Simpel)
```bash
# Batalkan commit terakhir, tapi simpan perubahan
git reset --soft HEAD~1

# Kembalikan file yang terhapus
git checkout -- filename.js

# Lihat semua yang pernah dilakukan (untuk recovery)
git reflog
```

---

## 🌐 GitHub & Kolaborasi Remote

### GitHub itu Apa?

GitHub = Git + Social Media untuk programmer. Tempat menyimpan kode online dan kerja bareng tim.

### Fork vs Clone (Bedanya)

| **Fork** | **Clone** |
|----------|-----------|
| Copy project orang lain ke akun Anda | Download project ke komputer |
| Untuk kontribusi ke project orang | Untuk kerja dengan project sendiri |
| Di website GitHub | Di terminal/command line |

### Workflow Kontribusi (Step-by-Step)

#### 1️⃣ Persiapan
```bash
# Fork di GitHub UI dulu, lalu:
git clone https://github.com/USERNAME-ANDA/project.git
cd project

# Hubungkan ke project asli
git remote add upstream https://github.com/pemilik-asli/project.git
```

#### 2️⃣ Mulai Coding
```bash
# Selalu update dulu sebelum mulai
git checkout main
git pull upstream main
git push origin main

# Buat branch baru untuk fitur
git checkout -b fitur-login
```

#### 3️⃣ Selesai Coding
```bash
# Simpan dan upload
git add .
git commit -m "feat: tambah sistem login"
git push origin fitur-login
```

#### 4️⃣ Buat Pull Request
Di GitHub:
1. Klik "Compare & pull request"
2. Isi deskripsi yang jelas
3. Tunggu review dari tim

### Template Pull Request (Salin-Tempel)

```markdown
## Apa yang berubah?
Menambahkan sistem login dengan email dan password

## Jenis perubahan
- [x] Fitur baru
- [ ] Perbaikan bug
- [ ] Update dokumentasi

## Cara test
1. Buka halaman login
2. Masukkan email dan password
3. Pastikan bisa masuk ke dashboard

## Checklist
- [x] Kode sudah di-test
- [x] Tidak ada console.log yang tertinggal
- [x] Mengikuti style guide
```

---

## 🌿 Strategi Branching

### Mengapa Perlu Branch?

Branch = cabang. Seperti copy file, tapi lebih pintar. Anda bisa:
- Eksperimen tanpa merusak kode utama
- Kerja paralel dengan tim
- Mudah kembali jika ada masalah

### GitHub Flow (Recommended - Simpel)

```
main (kode utama)
 ├── fitur-login
 ├── fitur-dashboard  
 └── perbaikan-bug
```

**Aturan Simpel:**
1. `main` = kode yang sudah jadi
2. Buat branch baru untuk setiap fitur
3. Merge ke `main` setelah review
4. Hapus branch setelah merge

### Command Branch

```bash
# Lihat semua branch
git branch -a

# Buat dan pindah ke branch baru
git checkout -b nama-fitur

# Pindah branch
git checkout main

# Hapus branch (setelah merge)
git branch -d nama-fitur

# Hapus branch di GitHub
git push origin --delete nama-fitur
```

### Merge vs Rebase (Kapan Pakai)

```bash
# MERGE - Gabung branch (history lengkap)
git checkout main
git merge fitur-login

# REBASE - Pindah commits (history bersih)
git checkout fitur-login
git rebase main
```

**Kapan pakai:**
- **Merge**: Untuk branch yang dikerjakan bareng
- **Rebase**: Untuk branch pribadi, biar history rapi

### Mengatasi Conflict (Jangan Panik!)

```bash
# Ketika terjadi conflict
git status                  # Lihat file yang conflict

# Edit file, hapus bagian ini:
# <<<<<<< HEAD
# Kode Anda
# =======  
# Kode orang lain
# >>>>>>> branch-name

# Setelah edit
git add nama-file.js
git commit                  # Untuk merge
```

---

## 🔁 Manajemen Commit & History

### Pesan Commit yang Baik

**Format Standar:**
```
jenis: deskripsi singkat

jenis bisa:
- feat: fitur baru
- fix: perbaikan bug  
- docs: update dokumentasi
- style: formatting kode
- refactor: reorganisasi kode
- test: tambah/update test
```

**Contoh Bagus:**
```bash
git commit -m "feat: tambah tombol logout"
git commit -m "fix: perbaiki validasi email"
git commit -m "docs: update panduan instalasi"
```

**Contoh Buruk:**
```bash
git commit -m "update"
git commit -m "fix"
git commit -m "asdf"
```

### Merapikan History (Advanced)

```bash
# Interactive rebase - rapikan 3 commit terakhir
git rebase -i HEAD~3

# Dalam editor yang muncul:
# pick = pakai commit ini
# squash = gabung dengan commit sebelumnya
# reword = ubah pesan commit
# drop = hapus commit
```

### Mengubah Commit Terakhir

```bash
# Ubah pesan commit terakhir
git commit --amend -m "Pesan baru"

# Tambah file ke commit terakhir
git add file-terlupa.js
git commit --amend --no-edit
```

---

## 👁️ Best Practices Code Review

### Tujuan Code Review

1. **Cari Bug**: Tangkep error sebelum ke user
2. **Belajar Bareng**: Share knowledge tim
3. **Jaga Kualitas**: Kode tetap rapi dan bagus
4. **Keamanan**: Pastikan tidak ada security hole

### Checklist Review (Untuk Reviewer)

**✅ Yang Harus Dicek:**
- [ ] Kode jalan tanpa error
- [ ] Logic benar sesuai requirement
- [ ] Tidak ada bug yang obvious
- [ ] Code mudah dibaca dan dipahami
- [ ] Ada test untuk fitur baru
- [ ] Tidak ada hardcoded password/secret
- [ ] Performance tidak bermasalah

### Cara Review yang Baik

**✅ Comment yang Konstruktif:**
```markdown
**Saran:** Bisa pakai `Array.find()` instead of `filter()[0]` untuk performa lebih baik.

**Pertanyaan:** Kapan kondisi ini bisa terjadi? Perlu penjelasan di comment.

**Bagus:** Great use of early return! Kode jadi lebih readable.
```

**❌ Comment yang Tidak Membantu:**
```markdown
"Ini salah"
"Code jelek"
"Ganti semua"
```

### Decision Framework

**APPROVE kalau:**
- Kode works dan tested
- Tidak ada security issue
- Quality acceptable
- Semua concern sudah diaddress

**REQUEST CHANGES kalau:**
- Ada bug yang bisa break production
- Security vulnerability
- Performance issue serius
- Missing critical tests

---

## 🧠 Studi Kasus & Problem Solving

### Case 1: Merge Conflict

**Problem:** Dua orang edit file yang sama.

**Solution:**
```bash
# 1. Pull latest changes
git pull origin main

# 2. Lihat file yang conflict
git status

# 3. Edit file, pilih mana yang mau dipakai
# Hapus marker conflict: <<<<<<<, =======, >>>>>>>

# 4. Add dan commit
git add .
git commit -m "resolve: merge conflict in user.js"
```

### Case 2: Salah Push ke Main

**Problem:** Push langsung ke main tanpa PR.

**Solution (Aman):**
```bash
# 1. Revert commit yang salah
git revert abc1234
git push origin main

# 2. Buat branch yang benar
git checkout -b fitur-yang-benar
git cherry-pick abc1234  # Ambil perubahan yang tadi
# Edit dan improve
git push origin fitur-yang-benar
# Buat PR
```

### Case 3: Lupa Password GitHub

**Solution:**
1. Reset password di GitHub.com
2. Untuk terminal, pakai Personal Access Token:
   - GitHub → Settings → Developer settings → Personal access tokens
   - Generate token baru
   - Pakai token sebagai password

---

## 📌 Tips Penting & Kebiasaan Baik

### 🌅 Rutinitas Harian

**Pagi (sebelum coding):**
```bash
git checkout main
git pull origin main
git checkout your-branch
git rebase main  # Update branch dengan main terbaru
```

**Malam (setelah coding):**
```bash
git add .
git commit -m "WIP: progress fitur dashboard"  # WIP = Work In Progress
git push origin your-branch
```

### 📝 Template .gitignore

```gitignore
# Dependencies
node_modules/
vendor/

# Environment files
.env
.env.local

# Build files
/dist
/build
*.log

# IDE files
.vscode/
.idea/
*.swp

# OS files
.DS_Store
Thumbs.db

# Database
*.sqlite
*.db
```

### 🏷️ Branch Naming Convention

```bash
# Format: jenis/deskripsi-singkat
feature/user-login
bugfix/header-responsive
hotfix/security-patch
docs/api-documentation
```

---

## 🔒 Security & Advanced Topics

### Security Best Practices

#### 🔐 Jangan Commit Secrets

**❌ JANGAN:**
```javascript
const API_KEY = "sk_live_abc123xyz789"; // Jangan hardcode!
const PASSWORD = "admin123";
```

**✅ LAKUKAN:**
```javascript
const API_KEY = process.env.API_KEY;
const PASSWORD = process.env.DB_PASSWORD;
```

#### 🛡️ Signed Commits

```bash
# Setup GPG key untuk sign commits
git config --global user.signingkey YOUR_GPG_KEY
git config --global commit.gpgsign true

# Commit dengan signature
git commit -S -m "feat: tambah fitur authentication"
```

### Advanced Git Features

#### 🏷️ Git Tags (Versioning)

```bash
# Buat tag untuk release
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0

# Lihat semua tags
git tag -l

# Checkout ke tag tertentu
git checkout v1.0.0
```

#### 🔍 Git Bisect (Find Bug)

```bash
# Cari commit yang introduce bug
git bisect start
git bisect bad                    # Current commit has bug
git bisect good v1.0.0           # This version was good

# Git akan checkout middle commit
# Test apakah ada bug, lalu:
git bisect bad    # atau git bisect good
# Repeat until found
```

#### 📊 Git Statistics

```bash
# Statistik kontributor
git shortlog -sn

# File yang paling sering berubah
git log --format=format: --name-only | sort | uniq -c | sort -r

# Aktivitas per hari
git log --pretty=format:"%ad" --date=short | sort | uniq -c
```

---

## 🚀 CI/CD Integration

### GitHub Actions Basic

**.github/workflows/test.yml:**
```yaml
name: Test & Deploy

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'
        
    - name: Install dependencies
      run: npm install
      
    - name: Run tests
      run: npm test
      
    - name: Build project
      run: npm run build
```

### Pre-commit Hooks

**package.json:**
```json
{
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged",
      "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
    }
  },
  "lint-staged": {
    "*.{js,jsx,ts,tsx}": ["eslint --fix", "prettier --write"],
    "*.{css,scss,md}": ["prettier --write"]
  }
}
```

### Automated Testing

**Basic test workflow:**
```bash
# Install testing tools
npm install --save-dev jest husky lint-staged

# Add to package.json scripts:
{
  "scripts": {
    "test": "jest",
    "test:watch": "jest --watch",
    "lint": "eslint src/",
    "lint:fix": "eslint src/ --fix"
  }
}
```

---

## 📱 Mobile & Cross-Platform Development

### React Native Git Workflow

#### 🤖 Android-specific

**.gitignore additions:**
```gitignore
# Android
android/app/build/
android/build/
android/.gradle/
android/gradle/
*.keystore
!debug.keystore

# iOS
ios/Pods/
ios/build/
ios/*.xcworkspace
ios/*.xcuserdata
```

#### 📱 iOS-specific

```bash
# Mengelola iOS dependencies
cd ios && pod install && cd ..

# Commit Podfile.lock
git add ios/Podfile.lock
git commit -m "chore: update iOS dependencies"
```

### Flutter Git Workflow

**pubspec.lock handling:**
```bash
# Selalu commit pubspec.lock
git add pubspec.lock
git commit -m "chore: update flutter dependencies"

# Untuk conflict di pubspec.lock
git checkout --theirs pubspec.lock
flutter pub get
git add pubspec.lock
```

### Cross-Platform Considerations

```bash
# Branching untuk platform-specific features
git checkout -b feature/ios-push-notifications
git checkout -b feature/android-background-sync

# Merge strategy untuk platform features
git checkout develop
git merge feature/ios-push-notifications
git merge feature/android-background-sync
```

---

## 🔧 Git Konfigurasi Lanjutan

### Multi-Account Setup

```bash
# Global config
git config --global user.name "Your Name"
git config --global user.email "personal@email.com"

# Per-repository config
cd work-project
git config user.name "Work Name"
git config user.email "work@company.com"

# SSH key per account
# ~/.ssh/config
Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_personal

Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_work
```

### Git Aliases (Shortcuts)

```bash
# Setup useful aliases
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm commit
git config --global alias.pl pull
git config --global alias.ps push

# Advanced aliases
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
git config --global alias.unstage "reset HEAD --"
git config --global alias.last "log -1 HEAD"
```

### Performance Optimization

```bash
# Enable git rerere (reuse recorded resolution)
git config --global rerere.enabled true

# Speed up git status
git config --global core.preloadindex true
git config --global core.fscache true

# Git maintenance
git maintenance start  # Auto-optimize repository
```

---

## 🎯 Production Deployment Strategies

### Gitflow untuk Production

```bash
# Production release workflow
git checkout -b release/v2.1.0 develop

# Fix release bugs
git commit -m "fix: resolve production compatibility issue"

# Merge to main for production
git checkout main
git merge --no-ff release/v2.1.0
git tag -a v2.1.0 -m "Release version 2.1.0"

# Merge back to develop
git checkout develop
git merge --no-ff release/v2.1.0

# Delete release branch
git branch -d release/v2.1.0
```

### Hotfix Workflow

```bash
# Emergency production fix
git checkout -b hotfix/critical-security-fix main

# Make fix
git commit -m "fix: resolve critical security vulnerability"

# Deploy to production
git checkout main
git merge --no-ff hotfix/critical-security-fix
git tag -a v2.1.1 -m "Hotfix v2.1.1"

# Merge to develop
git checkout develop
git merge --no-ff hotfix/critical-security-fix

# Cleanup
git branch -d hotfix/critical-security-fix
```

### Environment-specific Branches

```bash
# Environment workflow
main          # Production
├── staging   # Staging environment
├── develop   # Development environment
└── feature/* # Feature branches

# Deploy to staging
git checkout staging
git merge develop
git push origin staging

# Deploy to production
git checkout main
git merge staging
git push origin main
```

---

## 🛠️ Troubleshooting & Recovery

### Recovery Scenarios

#### 💀 Complete Repository Corruption

```bash
# Clone fresh copy
git clone https://github.com/user/repo.git repo-backup
cd repo-backup

# Import your local changes
cp -r ../old-repo/src/* ./src/
git add .
git commit -m "recover: restore local changes"
```

#### 🔄 Sync Fork After Long Time

```bash
# Reset fork to match upstream
git remote add upstream https://github.com/original/repo.git
git fetch upstream
git checkout main
git reset --hard upstream/main
git push origin main --force-with-lease
```

#### 🚨 Accidentally Deleted Branch

```bash
# Find the lost branch
git reflog | grep "branch-name"

# Recover the branch
git checkout -b branch-name <commit-hash-from-reflog>
```

### Performance Issues

#### Large Repository Optimization

```bash
# Clean up repository
git gc --aggressive --prune=now

# Remove large files from history
git filter-branch --tree-filter 'rm -f large-file.zip' HEAD

# Modern alternative (git-filter-repo)
pip install git-filter-repo
git filter-repo --path large-file.zip --invert-paths
```

#### Reduce Clone Size

```bash
# Shallow clone (recent history only)
git clone --depth 1 https://github.com/user/repo.git

# Partial clone (without large files)
git clone --filter=blob:limit=50m https://github.com/user/repo.git
```

---

## 📈 Git Analytics & Monitoring

### Repository Health Metrics

```bash
# Code churn analysis
git log --pretty=format:"%h,%an,%ad,%s" --date=short --since="1 month ago" > commits.csv

# File change frequency
git log --name-only --pretty=format: | sort | uniq -c | sort -rn | head -20

# Contributor activity
git log --pretty=format:"%an" --since="3 months ago" | sort | uniq -c | sort -rn
```

### Automated Code Quality

**.github/workflows/code-quality.yml:**
```yaml
name: Code Quality

on: [push, pull_request]

jobs:
  quality:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
      with:
        fetch-depth: 0  # Full history for better analysis
        
    - name: SonarCloud Scan
      uses: SonarSource/sonarcloud-github-action@master
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
        
    - name: Code Coverage
      run: |
        npm test -- --coverage
        bash <(curl -s https://codecov.io/bash)
```

---

## 🎓 Kesimpulan & Next Steps

### Ringkasan Command Penting

```bash
# Daily essentials
git status
git add .
git commit -m "message"
git push origin branch-name
git pull origin main

# Branching
git checkout -b new-feature
git merge feature-branch
git branch -d completed-feature

# Emergency fixes
git stash
git stash pop
git reset --soft HEAD~1
git reflog
```

### Learning Path

1. **Pemula**: Kuasai add, commit, push, pull
2. **Intermediate**: Branching, merging, conflict resolution
3. **Advanced**: Rebasing, hooks, advanced workflows
4. **Expert**: Custom scripts, git internals, team lead

### Recommended Tools

- **GUI**: GitHub Desktop, SourceTree, GitKraken
- **IDE Integration**: VS Code Git, IntelliJ Git
- **CLI Enhancement**: Oh My Zsh git plugin, git aliases
- **Automation**: Husky, lint-staged, GitHub Actions

### Team Adoption Strategy

1. **Week 1**: Basic commands training
2. **Week 2**: Branching workflow setup
3. **Week 3**: Code review process
4. **Week 4**: Advanced features & automation
5. **Ongoing**: Regular retrospectives & improvements

---

## 📚 Referensi & Resources

### Official Documentation
- [Git Documentation](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com)
- [GitHub Flow Guide](https://guides.github.com/introduction/flow/)

### Interactive Learning
- [Learn Git Branching](https://learngitbranching.js.org/)
- [GitHub Skills](https://skills.github.com/)
- [Git Immersion](http://gitimmersion.com/)

### Advanced Topics
- [Pro Git Book](https://git-scm.com/book)
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials)
- [Git Workflows](https://www.atlassian.com/git/tutorials/comparing-workflows)

---

*💡 **Pro Tip**: Bookmark halaman ini dan gunakan sebagai referensi cepat. Git is a journey, not a destination!*

**Happy Coding! 🚀**

---

**© 2024 LEX DEV - Internal Documentation**