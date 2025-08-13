import qrcode

def generate_qr(data, filename="qrcode.png"):
    # QR Code settings
    qr = qrcode.QRCode(
        version=1,
        error_correction=qrcode.constants.ERROR_CORRECT_H,
        box_size=10,
        border=4,
    )
    qr.add_data(data)
    qr.make(fit=True)

    # Create and save the image
    img = qr.make_image(fill_color="black", back_color="white")
    img.save(filenam)
    print(f"QR Code generated and saved as {filename}")

if __name__ == "__main__":
    text = input("Enter the text or URL to generate QR Code: ")
    generate_qr(text)
import json
import random
import time
from datetime import datetime

# ---------- Configuration ----------
CONFIG_FILE = "config.json"
DATA_FILE = "data.txt"

# ---------- Helper functions ----------
def load_config():
    """Read configuration file or create default one"""
    try:
        with open(CONFIG_FILE, "r", encoding="utf-8") as f:
            return json.load(f)
    except FileNotFoundError:
        default_config = {
            "username": "guest",
            "language": "en",
            "theme": "dark",
            "version": "1.0"
        }
        save_config(default_config)
        return default_config

def save_config(config):
    """Save configuration to file"""
    with open(CONFIG_FILE, "w", encoding="utf-8") as f:
        json.dump(config, f, ensure_ascii=False, indent=4)

# ---------- Sample class ----------
class TaskManager:
    def __init__(self):
        self.tasks = []

    def add_task(self, title):
        task = {
            "id": random.randint(1000, 9999),
            "title": title,
            "done": False,
            "created_at": datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        }
        self.tasks.append(task)
        print(f"✅ Task '{title}' added.")

    def list_tasks(self):
        if not self.tasks:
            print("📭 No tasks found.")
        for task in self.tasks:
            status = "✔️ Done" if task["done"] else "⏳ Pending"
            print(f"{task['id']} - {task['title']} ({status})")

    def mark_done(self, task_id):
        for task in self.tasks:
            if task["id"] == task_id:
                task["done"] = True
                print(f"🎯 Task '{task['title']}' marked as done.")
                return
        print("❌ Task not found.")

# ---------- Simulated API ----------
def fake_api_call():
    print("Sending request to API...")
    time.sleep(1)
    data = {
        "status": "ok",
        "timestamp": datetime.now().isoformat(),
        "data": [random.randint(1, 100) for _ in range(5)]
    }
    return data

# ---------- Save data ----------
def save_data_to_file(data):
    with open(DATA_FILE, "a", encoding="utf-8") as f:
        f.write(json.dumps(data, ensure_ascii=False) + "\n")
    print("💾 Data saved.")

# ---------- Main program ----------
if __name__ == "__main__":
    config = load_config()
    print(f"👋 Hello {config['username']}! Welcome.")

    manager = TaskManager()
    manager.add_task("Write daily report")
    manager.add_task("Review GitHub code")

    print("\n📋 Task list:")
    manager.list_tasks()

    print("\n📡 Fetching data from API...")
    api_data = fake_api_call()
    print("📊 API data:", api_data)

    save_data_to_file(api_data)
