# 🛠 System Repair GUI Script

A Python-based **System Repair Utility** with a **Graphical User Interface (GUI)** that automates Windows system file repairs.  
This script executes **SFC (System File Checker) and DISM (Deployment Image Servicing and Management) scans**, logs the results, and displays real-time status updates in a **GUI with a progress bar**.

🔹 **Use Cases & Functions:**
- **Graphical User Interface (GUI) for ease of use** 🖥️  
- **Automatic Admin Privileges** – Ensures the script runs with the required permissions 🔑  
- **Real-time Progress Updates** – Status messages and a progress bar 📊  
- **Runs SFC & DISM with error handling** – Automatically moves to the next step if one fails ✅  
- **Logs all repairs to `repair_log.txt`** – View detailed system repair logs 📄  
- **Auto-Opens Log File** – Monitor logs live in Notepad 📖  

---

## 🚀 Features
✅ **User-friendly GUI** – No need for command-line operations  
✅ **Runs SFC (`sfc /scannow`) to repair system files**  
✅ **Runs DISM (`Dism /online /cleanup-image /restorehealth`) to fix Windows image issues**  
✅ **Automatically handles errors and skips failed steps**  
✅ **Displays real-time status updates with a progress bar**  
✅ **Logs all operations and auto-opens `repair_log.txt`**  

---

## 🖥️ Installation Instructions

### 🔹 **Prerequisites**
Ensure you have **Python 3.x** installed. If not, download it from [python.org](https://www.python.org/downloads/).

### 🔹 **Install Required Modules**
This script relies on **Tkinter** (pre-installed with Python). No additional dependencies are needed. However, you can ensure all required modules exist by running:

```sh
pip install tk
```

---

## 🛠 How to Use

### **1️⃣ Download the Script**
Clone the repository or manually download `repair_gui.py`:

```sh
git clone https://github.com/yourusername/system-repair-gui.git
cd system-repair-gui
```

OR manually save [`repair_gui.py`](repair_gui.py).

### **2️⃣ Run the Script**
Double-click `repair_gui.py`, or run it from the command line:

```sh
python repair_gui.py
```

### **3️⃣ Start the Repair**
- Click **"Start Repair"** to begin.  
- The log file (`repair_log.txt`) will open automatically.  
- Watch the **progress bar** and **status updates**.  
- When finished, click **"Close"**.

---

## 📜 Functionality & Use Cases

This script consists of several key functions, each serving a specific purpose:

### 🔹 `log_message(self, message)`
**📌 Purpose:** Logs status messages to both the GUI and `repair_log.txt`.  
**🛠 Use Case:** Called whenever an action occurs (e.g., running a command, detecting an error).  

---

### 🔹 `open_log_file(self)`
**📌 Purpose:** Automatically opens `repair_log.txt` in Notepad.  
**🛠 Use Case:** Ensures the user can see real-time logs while the repair is running.  

---

### 🔹 `run_command(self, command)`
**📌 Purpose:** Runs a Windows command in an elevated terminal and logs the output.  
**🛠 Use Case:** Used to execute `sfc /scannow` and `Dism /online /cleanup-image /restorehealth`.  
✅ **Handles errors** and proceeds to the next step if a command fails.  

---

### 🔹 `start_repair(self)`
**📌 Purpose:** Main function that initiates system repair, updates GUI, and manages the process.  
**🛠 Use Case:**  
1. Disables the **"Start Repair"** button.  
2. **Opens the log file** for real-time monitoring.  
3. **Runs SFC (`sfc /scannow`)** to check and repair system files.  
4. **Runs DISM (`Dism /restorehealth`)** to fix Windows image issues.  
5. Updates the **progress bar** and **status label**.  
6. If any step fails, it **logs the error but continues the process**.  
7. Enables the **"Close"** button once repairs are complete.  

---

### 🔹 `is_admin()`
**📌 Purpose:** Checks if the script is running with administrator privileges.  
**🛠 Use Case:** Ensures that **SFC and DISM** commands can execute properly.  

---

### 🔹 `restart_as_admin()`
**📌 Purpose:** Relaunches the script with admin privileges if not already elevated.  
**🛠 Use Case:** Prevents permission issues by automatically requesting admin rights.  

---

## 📝 Code Snippet

Here's a preview of the **main function** in `repair_gui.py`:

```python
def start_repair(self):
    """Runs the system repair process with GUI updates."""
    self.start_button.config(state=tk.DISABLED)
    self.progress["value"] = 10
    self.log_message("System Repair Process Started")

    # Open log file in Notepad
    self.open_log_file()

    # Run SFC
    self.progress["value"] = 40
    self.log_message("Running System File Checker (sfc /scannow)...")
    if self.run_command("sfc /scannow") != 0:
        self.log_message("sfc /scannow encountered an error, continuing to DISM...")
    else:
        self.log_message("sfc /scannow completed successfully.")

    # Run DISM
    self.progress["value"] = 70
    self.log_message("Running DISM RestoreHealth...")
    if self.run_command("Dism /online /cleanup-image /restorehealth") != 0:
        self.log_message("DISM encountered an error, but the process will complete.")
    else:
        self.log_message("DISM completed successfully.")

    self.progress["value"] = 100
    self.log_message("System Repair Process Finished")
    self.close_button.config(state=tk.NORMAL)
```

---

## ⚠️ Important Notes
- This script **requires admin privileges** to run system repairs. It will **automatically request elevation** if needed.
- Works on **Windows 10/11** (not compatible with macOS/Linux).
- The process may take **several minutes** depending on system health.

---

## 🤝 Contributing
Feel free to fork this repository and submit pull requests! Suggestions and improvements are always welcome.  

---

## 📜 License
This project is **open-source** and available under the **MIT License**.
