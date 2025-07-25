# Elegoo Centaury Carbon – Filament Movement Sensor  
### FR / EN – Capteur de mouvement de filament pour imprimante 3D

---

## 🇫🇷 Description (FR)

🔧 Ce projet est une **amélioration matérielle** pour l’imprimante **Elegoo Centaury Carbon**, permettant de détecter le mouvement du filament.  
Il est basé sur le travail de [Jonathan Rowny](https://github.com/jrowny/cc_sfs), avec comme principale contribution ici la **création d’un PCB personnalisé** pour faciliter l’intégration propre du capteur.

📦 **Capteur requis :**  
👉 Ce projet utilise le **BIGTREETECH Smart Filament Detector V2.0**, un capteur optique à encodeur rotatif.

🔌 **PCB personnalisé :**  
- Fichiers créés avec **KiCad**
- Connexion facile au capteur et à la Centaury
- Ports supplémentaires disponibles pour le **debug ou des améliorations futures**

📁 Tous les fichiers nécessaires sont disponibles dans le dossier `/pcb` :
- `.kicad_pcb`, `.sch`, fichiers Gerber, PDF
- Sérigraphie, dimensions, BOM (Bill of Materials)

---

## 🇬🇧 Description (EN)

🔧 This project is a **hardware upgrade** for the **Elegoo Centaury Carbon** 3D printer that adds **filament motion detection**.  
It is based on the work by [Jonathan Rowny](https://github.com/jrowny/cc_sfs), with the main contribution here being a **custom-designed PCB** to neatly integrate the sensor.

📦 **Required sensor:**  
👉 This project uses the **BIGTREETECH Smart Filament Detector V2.0**, an optical rotary encoder sensor.

🔌 **Custom PCB:**
- Designed with **KiCad**
- Easy connection to the sensor and the Centaury printer
- Additional ports are available for **debugging or future upgrades**

📁 All necessary files are in the `/pcb` folder:
- `.kicad_pcb`, `.sch`, Gerber files, PDFs
- Silkscreen, dimensions, BOM (Bill of Materials)

---

## 🔗 Projet original / Original Project

📚 Basé sur / Based on:  
👉 [Jonathan Rowny – cc_sfs](https://github.com/jrowny/cc_sfs)

---

## 🧰 Matériel requis / Required Hardware

- BIGTREETECH Smart Filament Detector V2.0  
- Résistances, connecteurs, composants SMD ou traversants  
- Câbles dupont ou connecteurs JST selon le montage  
- PCB personnalisé  
- Outils de soudure  
- Imprimante 3D : **Elegoo Centaury Carbon**

---

## ⚙️ Instructions de montage / Assembly Instructions

### 🇫🇷 En français

1. Soudez les composants sur le PCB selon le schéma si vous n'avez pas utilisé un service d’assemblage.  
2. Connectez le capteur BTT V2.0 au PCB.  
3. Branchez le PCB à l'imprimante selon le câblage prévu.  
4. Flashez le firmware proposé dans le projet de [Jonathan Rowny](https://github.com/jrowny/cc_sfs).  
5. Vérifiez la détection du filament via le firmware (compatible Marlin ou Klipper).  
6. Utilisez les **ports restants** pour du debug ou des extensions.

### 🇬🇧 In English

1. Solder the components onto the PCB, unless you're using an assembled PCB service.  
2. Connect the BTT Smart Filament Sensor V2.0 to the PCB.  
3. Connect the PCB to your Elegoo printer using the proper wiring.  
4. Flash the firmware provided in [Jonathan Rowny’s project](https://github.com/jrowny/cc_sfs).  
5. Verify filament movement detection through the firmware (Marlin or Klipper compatible).  
6. Use the **extra ports** for debugging or optional upgrades.

---
## 🔍 BOM interactif  
👉 [Voir le BOM interactif ici](https://sohcahtoaii.github.io/Elegoo-centaury-carbon-Filament-Movement-Sensor/)

## 🖼️ Images / Preview

<img width="1920" height="1032" alt="image" src="https://github.com/user-attachments/assets/71d9bea8-ab6b-4f3b-8761-f1478c0797ff" />

<img width="1920" height="1032" alt="image" src="https://github.com/user-attachments/assets/e0f3ea60-2f8b-4a20-9db9-6902dfea0e4b" />

<img width="1920" height="1032" alt="image" src="https://github.com/user-attachments/assets/9b5a633d-d2a3-4840-aa39-ba731874b6a1" />

---

## ❓ FAQ

**Q : Le capteur fonctionne-t-il avec d'autres imprimantes ?**  
A : Ce design est principalement prévu pour l’Elegoo Centaury Carbon, mais le PCB peut être adapté.

**Q : Peut-on ajouter d'autres fonctions ?**  
A : Oui, des **broches supplémentaires** sont disponibles pour extensions ou debug série.

**Q : Est-ce que je dois modifier le firmware ?**  
A : Non, le capteur est branché sur l’entrée de détection de fin de filament existante. Il fonctionne directement avec la pause automatique.

---

## 📜 Licence / License

**MIT License**  
Libre de modifier, réutiliser et redistribuer ce projet.

---

## 🙏 Remerciements / Credits

- 🔧 Idée originale et base logicielle : [Jonathan Rowny – cc_sfs](https://github.com/jrowny/cc_sfs)  
- 🧩 PCB personnalisé et adaptation Elegoo : *Sohcahtoaii*

---
