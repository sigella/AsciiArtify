# 📝 AsciiArtify MVP

This is the MVP (Minimum Viable Product) of **AsciiArtify**, a lightweight app for image conversion based on Machine Learning. It allows creating images in **ascii-art** style using ML features — just enough to demonstrate core functionality and gather feedback.

---

## 🚀 Features

✅ Upload images (jpg/png) from local devices 
✅ Convert images to ASCII art 
✅ Save ASCII text locally

🧪 Note: This MVP does **not** include user authentication

---

## 🛠 Infra Stack

- Kubernetes cluster based on K3d
- GitHub repository
- ArgoCD for CI/CD
---

## 🎬 Demo
- [ArgoCD installation](https://drive.google.com/file/d/1qcWaDKGJRagj80kyCpHK32vZ12VBTL3P/view?usp=drive_link) - brief overview of Argo CD installation and basic configuration
- [ArgoCD sync](https://drive.google.com/file/d/1fJEkkpIo6GcvWeuBfFe5a4zjZnoJmmqc/view?usp=drive_link) - demonstrate automatic sync of changes and scaling of the application
- [Application demo](https://drive.google.com/file/d/16ixXWQrbnQOSgbS4R_3I81spaxYujtWc/view?usp=drive_link) - demonstrate the main functionality of the product

## Conclusion
The MVP demonstrates how smooth and simple CI/CD can be.
It shows us that we can easily scale application components and rollout/rollback new features.
On top of that, it can work on any Cloud provides that supports Kubernetes.